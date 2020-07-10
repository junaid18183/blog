Portar and CNAB

### Install Portar 
curl https://cdn.porter.sh/latest/install-mac.sh | bash

### Install the required mixins
porter mixin install terraform
porter mixin install aws
porter mixin install kubernetes
porter mixin install helm
porter mixin install az

### Check plugins 
porter plugin list

porter credential generate kubecred --tag getporter/kubernetes:v0.1.0
porter install juned --tag getporter/kubernetes:v0.1.0 -c kubecred


Since the focus is on SAAS, are we 