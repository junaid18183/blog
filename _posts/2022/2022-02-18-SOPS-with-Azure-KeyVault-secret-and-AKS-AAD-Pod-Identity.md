---
layout: post
title:  "SOPS with Azure KeyVault secret and AKS AAD Pod Identity"
description: "SOPS with Azure KeyVault secret and AKS AAD Pod Identity"
author: juned
categories: [ k8s ]
tags: [k8s]
image: assets/images/k8s.jpg
featured: true
hidden: true
---

# SOPS with Azure KeyVault secret and AKS AAD Pod Identity

We want to achieve Gitops with FLUX in Azure AKS, storing the encrypted secrets in git repo using Mozilla's [SOPS](https://github.com/mozilla/sops).

The obvious problem we have to solve is  enable the flux controller pod to decrypt the secrets encrypted using the Azure key vault , we will use the AAD pod Identity for this.

# Create the KeyVault , key for SOPS and Managed Identity to access the the key

- [ ]  Create the azure key vault and cryptographic key to be used by SOPS
- [ ]  Create a managed identity which flux operator pod will use to decrypt the secrets
- [ ]  Add a policy in managed identity for encrypt / decrypt permission for keyvault secret
    
    ## Create a Azure KeyVault
    
    ```json
    export KEY_VAULT_NAME=bigbang-demo-enbuild
    export RESOURCE_GROUP_NAME=enbuild-demo
    export LOCATION=eastus
    
    az keyvault create --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP_NAME --location $LOCATION
    ```
    
    ### **Create the cryptographic key in KeyVault**
    
    ```json
    export KEY_VAULT_NAME=bigbang-demo-enbuild
    export RESOURCE_GROUP_NAME=enbuild-demo
    export LOCATION=eastus
    
    az keyvault key create --name sops-key --vault-name $KEY_VAULT_NAME --protection software --ops encrypt decrypt
    ```
    
    ## **Create a Managed Identity**
    
    ```json
    export RESOURCE_GROUP_NAME=enbuild-demo
    export LOCATION=eastus
    
    az group create -n $RESOURCE_GROUP_NAME -l  $LOCATION
    
    az identity create -n SopsDecryptorIdentity -g $RESOURCE_GROUP_NAME -l $LOCATION
    ```
    
    ### **Add an access policy for the managed identity created previously**
    
    First Obtain the client Id, object Id, and the resource Id of the identity
    
    ```
    export KEY_VAULT_NAME=bigbang-demo-enbuild
    export RESOURCE_GROUP_NAME=enbuild-demo
    export LOCATION=eastus
    
    CLIENT_ID=$(az identity show -n SopsDecryptorIdentity -g $RESOURCE_GROUP_NAME -o tsv --query "clientId")
    OBJECT_ID=$(az identity show -n SopsDecryptorIdentity -g $RESOURCE_GROUP_NAME -o tsv --query "principalId")
    RESOURCE_ID=$(az identity show -n SopsDecryptorIdentity -g $RESOURCE_GROUP_NAME -o tsv --query "id")
    
    echo $CLIENT_ID
    echo $OBJECT_ID
    echo $RESOURCE_ID
    ```
    
    Now add a policy so that managed identity can use the secret for encrypt as well as decrypt sops operation.
    
    ```json
    az keyvault set-policy --name $KEY_VAULT_NAME --resource-group $RESOURCE_GROUP_NAME --object-id $OBJECT_ID --key-permissions encrypt decrypt
    ```
    
    Get the key id for future use
    
    ```json
    export KEY_VAULT_NAME=bigbang-demo-enbuild
    
    az keyvault key show --name sops-key --vault-name $KEY_VAULT_NAME --query key.kid
    "https://bigbang-demo-enbuild.vault.azure.net/keys/sops-key/3e7781ddc080466d960d16aa8b520836"
    ```
    

# Manually test the SOPS with Azure KeyVault

- [ ]  Manually test the encryption using SOPS CLI
    
    ```json
    ❯ cat sample-secret.yaml
    data:
      myuser: anVuZWQK
      mypassword: VHdpbmUyLURlc3Bpc2UtQnVuaW9uLUFwcmlsLUR1Y2hlc3MtT3B1bGVudGx5
    
    ❯ sops --encrypt --azure-kv https://bigbang-demo-enbuild.vault.azure.net/keys/sops-key/3e7781ddc080466d960d16aa8b520836 sample-secret.yaml > sample-secret-enc.yaml
    
    ❯ cat sample-secret-enc.yaml
    data:
        myuser: ENC[AES256_GCM,data:TMP9XrpIBtQ=,iv:Dk6fVE1nVoqVxVfC1WlGMowM8s+OAURyw+fZcm/klHM=,tag:5UG7uZPEARVIDDhZgzQqqw==,type:str]
        mypassword: ENC[AES256_GCM,data:uFRPawEqEsa36jBWyjK0QRTNpAaIwSwr4KDgUD/ZLs2ukSF+Tt9WD99ke6N4slv8OW5SeMG100qdBuU2,iv:rUlunp/WQBacuMEJmlUDZivz2dLTBOVU3CFAa+Yy+2w=,tag:RUMvS9L7IzRrNK5Wrvlkuw==,type:str]
    sops:
        kms: []
        gcp_kms: []
        azure_kv:
            - vault_url: https://bigbang-demo-enbuild.vault.azure.net
              name: sops-key
              version: 3e7781ddc080466d960d16aa8b520836
              created_at: "2022-02-18T08:51:56Z"
              enc: K9WjRTbWa0O5zXC_z0XqLCUh_LdcmsnWz4hEDCrS_5tKS7Q9MhdngyDT6629_Ade4BKfkF8WUUccGdpdjuZsLN8BmD1dmf1kp6YKPxd4uyCNnAIGSbzrvDEtdSkzZw32pK0u7DhwlVmFmdK1nfis89hFxmWVt3L-j4En6dQt8eyzbKqmT2-KsTXFourrpa0h15quItxYswMmxkFNvo5WiNE9zb6pNQUUyNHrQEuGviqlf5Xk-5oK2Nb7PRr85Y_JzmUGlYPaqhhNvo7isbtXl-DP-GIyreM0CVqc4Uzx3CgDtVqVO7z7LkIReGj69SSjBxUOZMRpwdieude5rKrvig
        hc_vault: []
        age: []
        lastmodified: "2022-02-18T08:52:00Z"
        mac: ENC[AES256_GCM,data:6JsIPK3MMyQDlTEob7W4iemOuOaB4VQC4vkJPlIbYqqef2ex9ICirUGsCEf6bOOnvkjsUCUVEEkyZcUludfKPiDusu+Kvl0kResfJuBopaOAcVw3oMWSVVlFbAmELQGXTTLknHAyFY2ImLmYltonhM8bcbabXZRPv+ZDpxVaG4c=,iv:kN6PqLuX3rnENrPYfrrXLwXliXTIP3bv+MBZWIN3DaI=,tag:WAL/fmNHKjML6yMQnuil3A==,type:str]
        pgp: []
        encrypted_regex: ^(data|stringData)$
        version: 3.7.1
    ```
    
    We can encrypt using config file  so that we don’t have to provide the key vault details in CLI
    
    ```json
    ❯ cat sops.yaml
    ---
    creation_rules:
      - azure_keyvault: 'https://bigbang-demo-enbuild.vault.azure.net/keys/sops-key/3e7781ddc080466d960d16aa8b520836'
        # encrypted_regex: "^(data|stringData)$"
    ```
    
    ```json
    ❯ sops --config sops.yaml -e sample-secret.yaml > sample-secret-enc.yaml
    
    ❯ cat sample-secret-enc.yaml
    data:
        myuser: ENC[AES256_GCM,data:TMP9XrpIBtQ=,iv:Dk6fVE1nVoqVxVfC1WlGMowM8s+OAURyw+fZcm/klHM=,tag:5UG7uZPEARVIDDhZgzQqqw==,type:str]
        mypassword: ENC[AES256_GCM,data:uFRPawEqEsa36jBWyjK0QRTNpAaIwSwr4KDgUD/ZLs2ukSF+Tt9WD99ke6N4slv8OW5SeMG100qdBuU2,iv:rUlunp/WQBacuMEJmlUDZivz2dLTBOVU3CFAa+Yy+2w=,tag:RUMvS9L7IzRrNK5Wrvlkuw==,type:str]
    sops:
        kms: []
        gcp_kms: []
        azure_kv:
            - vault_url: https://bigbang-demo-enbuild.vault.azure.net
              name: sops-key
              version: 3e7781ddc080466d960d16aa8b520836
              created_at: "2022-02-18T08:51:56Z"
              enc: K9WjRTbWa0O5zXC_z0XqLCUh_LdcmsnWz4hEDCrS_5tKS7Q9MhdngyDT6629_Ade4BKfkF8WUUccGdpdjuZsLN8BmD1dmf1kp6YKPxd4uyCNnAIGSbzrvDEtdSkzZw32pK0u7DhwlVmFmdK1nfis89hFxmWVt3L-j4En6dQt8eyzbKqmT2-KsTXFourrpa0h15quItxYswMmxkFNvo5WiNE9zb6pNQUUyNHrQEuGviqlf5Xk-5oK2Nb7PRr85Y_JzmUGlYPaqhhNvo7isbtXl-DP-GIyreM0CVqc4Uzx3CgDtVqVO7z7LkIReGj69SSjBxUOZMRpwdieude5rKrvig
        hc_vault: []
        age: []
        lastmodified: "2022-02-18T08:52:00Z"
        mac: ENC[AES256_GCM,data:6JsIPK3MMyQDlTEob7W4iemOuOaB4VQC4vkJPlIbYqqef2ex9ICirUGsCEf6bOOnvkjsUCUVEEkyZcUludfKPiDusu+Kvl0kResfJuBopaOAcVw3oMWSVVlFbAmELQGXTTLknHAyFY2ImLmYltonhM8bcbabXZRPv+ZDpxVaG4c=,iv:kN6PqLuX3rnENrPYfrrXLwXliXTIP3bv+MBZWIN3DaI=,tag:WAL/fmNHKjML6yMQnuil3A==,type:str]
        pgp: []
        encrypted_regex: ^(data|stringData)$
        version: 3.7.1data:
        myuser: ENC[AES256_GCM,data:TMP9XrpIBtQ=,iv:Dk6fVE1nVoqVxVfC1WlGMowM8s+OAURyw+fZcm/klHM=,tag:5UG7uZPEARVIDDhZgzQqqw==,type:str]
        mypassword: ENC[AES256_GCM,data:uFRPawEqEsa36jBWyjK0QRTNpAaIwSwr4KDgUD/ZLs2ukSF+Tt9WD99ke6N4slv8OW5SeMG100qdBuU2,iv:rUlunp/WQBacuMEJmlUDZivz2dLTBOVU3CFAa+Yy+2w=,tag:RUMvS9L7IzRrNK5Wrvlkuw==,type:str]
    sops:
        kms: []
        gcp_kms: []
        azure_kv:
            - vault_url: https://bigbang-demo-enbuild.vault.azure.net
              name: sops-key
              version: 3e7781ddc080466d960d16aa8b520836
              created_at: "2022-02-18T08:51:56Z"
              enc: K9WjRTbWa0O5zXC_z0XqLCUh_LdcmsnWz4hEDCrS_5tKS7Q9MhdngyDT6629_Ade4BKfkF8WUUccGdpdjuZsLN8BmD1dmf1kp6YKPxd4uyCNnAIGSbzrvDEtdSkzZw32pK0u7DhwlVmFmdK1nfis89hFxmWVt3L-j4En6dQt8eyzbKqmT2-KsTXFourrpa0h15quItxYswMmxkFNvo5WiNE9zb6pNQUUyNHrQEuGviqlf5Xk-5oK2Nb7PRr85Y_JzmUGlYPaqhhNvo7isbtXl-DP-GIyreM0CVqc4Uzx3CgDtVqVO7z7LkIReGj69SSjBxUOZMRpwdieude5rKrvig
        hc_vault: []
        age: []
        lastmodified: "2022-02-18T08:52:00Z"
        mac: ENC[AES256_GCM,data:6JsIPK3MMyQDlTEob7W4iemOuOaB4VQC4vkJPlIbYqqef2ex9ICirUGsCEf6bOOnvkjsUCUVEEkyZcUludfKPiDusu+Kvl0kResfJuBopaOAcVw3oMWSVVlFbAmELQGXTTLknHAyFY2ImLmYltonhM8bcbabXZRPv+ZDpxVaG4c=,iv:kN6PqLuX3rnENrPYfrrXLwXliXTIP3bv+MBZWIN3DaI=,tag:WAL/fmNHKjML6yMQnuil3A==,type:str]
        pgp: []
        encrypted_regex: ^(data|stringData)$
        version: 3.7.1
    ```
    
    ```json
    ❯ sops -d sample-secret-enc.yaml
    data:
        myuser: anVuZWQK
        mypassword: VHdpbmUyLURlc3Bpc2UtQnVuaW9uLUFwcmlsLUR1Y2hlc3MtT3B1bGVudGx5
    ```
    

# Test the secret decryption from AKS POD manually

- [ ]  Deploy the AKS or modify existing AKS to enable the pod identity
    
    ```json
    ❯ az aks create -g enbuild-demo --node-count 1 -n james-test -k 1.21.7 --enable-managed-identity --enable-pod-identity --enable-pod-identity-with-kubenet
    ```
    
    If you are have existing cluster, modify it 
    
    ```json
    ❯ az aks update -n james-test -g enbuild-demo --enable-managed-identity --enable-pod-identity --enable-pod-identity-with-kubenet
    ```
    
    - [ ]  Add the pod-identity to the AKS cluster  in default namespace
    
    ```json
    ❯ az aks pod-identity add --resource-group enbuild-demo --cluster-name james-test --name sops --namespace default  --identity-resource-id /subscriptions/a36fedae-d136-4bf9-8249-d24d8cbf5f66/resourceGroups/enbuild-demo/providers/Microsoft.ManagedIdentity/userAssignedIdentities/SopsDecryptorIdentity
    ```
    
    - [ ]  Verify the *azureidentity* is deployed in default namespace
        
        ```json
        ❯ kubectl get azureidentity
        NAME   AGE
        sops   119m
        ```
        
    - [ ]  Create a sample Deployment using sops image and verify the decrypt is working fine.
        
        Make a note in below deployment, 
        
        - the namespace is ***default*** , as the azureidentity is added in default namespace.
        - the sample encrypted file is mounted as config-map
        - the deployment label ***aadpodidbinding*** is present and set to ***sops.***  Since the ***azureidentity***  we created is with the name sops.
        - For SOPS cli to work with AAD pod identity we need to set the ENV variable ***AZURE_AUTH_METHOD*** and set it to ***msi***
            
            below is the sample deployment file.
            
            ```json
            ---
            apiVersion: v1
            data:
              sample-secret-enc.yaml: |
                data:
                    myuser: ENC[AES256_GCM,data:9SK3Aykc8uo=,iv:HEhUfPpx/uyZBNbySYK5jcfr4o0N7GpvVF2GaryP8Qo=,tag:8qXx/YtoeH7BmH5xJ4IV2w==,type:str]
                    mypassword: ENC[AES256_GCM,data:rlYjZ/EgyPwVsaWUfCMCoslxd5BAWmUoYwjMJR1zaOnUXI2MdzzsqalRabJ7ti7A+BxtogZOoo8dBLkn,iv:2Z/kliSZ33M5vd5mXEst5INRZRYzDOW7PJ8PBFg5+hE=,tag:+/hItGzZraY3tXdINqXMHw==,type:str]
                sops:
                    kms: []
                    gcp_kms: []
                    azure_kv:
                        - vault_url: https://bigbang-demo-enbuild.vault.azure.net
                          name: sops-key
                          version: 3e7781ddc080466d960d16aa8b520836
                          created_at: "2022-02-18T07:20:12Z"
                          enc: RAlWdd6R9sC5Q7bT22bP4L5VZon79pIcLleARSzNo-wPduFjqlRiFuuUDDbzyzpgj9VxDwHk_KOVAySB3FiOMGKC7SZ0Jgs5pp3NQCSUc86520JOugBfo0Njqp2wCmgfrwiwrBMJUwiK02fkFp1E0Ewc-rNb9DRCdttK1CueR9X70v01w1VDOa4dXJmCz86uByzG-_hW5I7dgDdRh92AztSiCb_f5-HcrKwdc2KJ-rJYIUSIM1bymy_V2w2cvQcejDpvfHbr1Amer9HiKnlqcarOME5L2a2C3HGQRziqb5AI942Vauu4I0cJFQzUmsTQ98sDCO6kYfxN16H8KqNrsA
                    hc_vault: []
                    age: []
                    lastmodified: "2022-02-18T07:20:14Z"
                    mac: ENC[AES256_GCM,data:grsvcgSO/WzA1QjlUrWjI2oiDVAYX/Na5ffvxK9DBwXN4DgFxJEWHqPOlOfDWn5BvMKr2Ey9I69x6/chnvsALtdBhDArY5DpJM5HOaTLfuT0CMf1DwvJ8kXanV10B/WRV/YqU6AACbrgJGT15+fDBLO7RbtDolotbEZ+9hjaXtI=,iv:1fC1er/obnmkr2TDUJEv4Ex33f3TuRbgHN0R3Agg3KM=,tag:YKjLsQ/J0k2OfICiLbZSkA==,type:str]
                    pgp: []
                    encrypted_regex: ^(data|stringData)$
                    version: 3.7.1
            kind: ConfigMap
            metadata:
              name: test-secret
              namespace: default
            ---
            apiVersion: apps/v1
            kind: Deployment
            metadata:
              name: sops-demo
              namespace: default
              labels:
                app: sops-demo
            spec:
              replicas: 1
              selector:
                matchLabels:
                  app: sops-demo
              template:
                metadata:
                  labels:
                    app: sops-demo
                    aadpodidbinding: sops
                spec:
                  volumes:
                    # You set volumes at the Pod level, then mount them into containers inside that Pod
                    - name: test-secret
                      configMap:
                        # Provide the name of the ConfigMap you want to mount.
                        name: test-secret
                        # An array of keys from the ConfigMap to create as files
                        items:
                        - key: "sample-secret-enc.yaml"
                          path: "sample-secret-enc.yaml"
                  containers:
                    - name: sops-demo
                      image: mozilla/sops:latest
                      command: ["sops", "-d","/tmp/sample-secret-enc.yaml"]
                      # command: ["sleep","3600"]
                      env:
                        - name: KEYVAULT_NAME
                          value: bigbang-demo-enbuild
                        - name: SECRET_NAME
                          value: Password
                        - name: AZURE_AUTH_METHOD
                          value: msi
                      volumeMounts:
                      - mountPath: /tmp/sample-secret-enc.yaml
                        name: test-secret
                        subPath: sample-secret-enc.yaml
            ```
            
            ```json
            ❯ kubectl apply -f deployment.yaml
            configmap/test-secret unchanged
            deployment.apps/sops-demo unchanged
            
            ❯ kubectl get po
            NAME                        READY   STATUS      RESTARTS   AGE
            sops-demo-7b76486b7-2f9td   0/1     Completed   3          53s
            
            ❯ kubectl logs -f sops-demo-7b76486b7-2f9td
            data:
                myuser: anVuZWQK
                mypassword: VHdpbmUyLURlc3Bpc2UtQnVuaW9uLUFwcmlsLUR1Y2hlc3MtT3B1bGVudGx5
            ```
            

# Deploy the FLUX and test it GitOps end to end

Since we are going to use AAD Pod Identity , we have to first create the pod-identity in flux-system namespace. 

The identity-resource-id is the resource id of the key-vault created before.

```json
❯ kubectl create ns flux-system

❯ az aks pod-identity add --resource-group enbuild-demo --cluster-name james-test --name sops --namespace flux-system  --identity-resource-id /subscriptions/a36fedae-d136-4bf9-8249-d24d8cbf5f66/resourceGroups/enbuild-demo/providers/Microsoft.ManagedIdentity/userAssignedIdentities/SopsDecryptorIdentity
```

Now deploy the flux. 

```json
export GITHUB_USER=junaid18183
export GITHUB_REPO=aad-pod-identity-aks-flux-sops-demo
export CLUSTER_NAME=aks
export GITHUB_TOKEN=DUMMYTOKEN

❯ flux bootstrap github --owner=$GITHUB_USER --repository=$GITHUB_REPO --branch=main --path=./clusters/$CLUSTER_NAME
```

once the flux is deployed we need to patch the `kustomize-controller` deployment and add the aadpodidbinding label and AZURE_AUTH_METHOD env variable. 

You can use the below ***kustomization*** patch to achieve that, 

```json
❯ cat sops-kustomize-patch.yaml
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: kustomize-controller
  namespace: flux-system
spec:
  template:
    metadata:
      labels:
        aadpodidbinding: sops  # match the AzureIdentityBinding selector
    spec:
      containers:
      - name: manager
        env:
        - name: AZURE_AUTH_METHOD
          value: msi
```

With this changes in place you can add any encrypted secrets to your gitops and flux will automatically encrypt it.

```json
❯ cat kustomization.yaml
apiVersion: kustomize.config.k8s.io/v1beta1
kind: Kustomization
resources:
- gotk-components.yaml
- gotk-sync.yaml
patchesStrategicMerge:
  - sops-kustomize-patch.yaml
```