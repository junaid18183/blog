---
layout: post
title:  "Signing images and creating  SBOM using cosign in CI Pipeline"
description: "Signing images and creating  SBOM using cosign in CI Pipeline "
author: juned
categories: [ k8s ]
tags: [k8s]
image: assets/images/k8s.jpg
featured: true
hidden: true
---
# Signing images and creating  SBOM using cosign - Part2

In [part 1](https://www.ijuned.com/Signing-images-and-creating-SBOM-using-cosign/)  we manually created container image, signed it and also attached the SBOM of the image to registry. 

We will perform same actions using CI pipeline using github actions achieving the Hermetic builds for the [SLSA](https://slsa.dev/spec/v0.1/levels). 

I have created the sample repository https://github.com/junaid18183/sampleapp so that we can see the CI in action. 

The gist of the pipeline is this [workflow](https://github.com/junaid18183/sampleapp/blob/main/.github/workflows/docker-publish.yml) file,  lets check in detail what each step is doing,

First three  steps are pretty obvious, we are 

- getting the code via checkout action
- Logging into the Github Container Registry ( the GHCR_ACCESS_TOKEN is the secret created in the repo containing my Personal Access Token )
- Building and Pushing the image to our registry.

- Next we are creating the SBOM using the [anchore/sbom-action](https://github.com/anchore/sbom-action)  we are also creating artefact  named `sbom.spdx` so that any following job can consume it  and its also available in github workflow run outputs.
- Next step we download the cosign using the official [sigstore/cosign-installer](https://github.com/sigstore/cosign-installer) action.
- And finally we are signing the image and attaching the SBOM to the image.

Few important points to note though, 

We are pushing the image as github commit sha not a particular tag, Since the commit sha is immutable so that we are 100% sure on the verification part that the image in question is same. 

```bash
rancher-desktop sampleapp main ❯ COSIGN_EXPERIMENTAL=true cosign verify ghcr.io/junaid18183/sampleapp:67bb91efb62bfae268bcd0a243a10d48fde80559 | jq "."

Verification for ghcr.io/junaid18183/sampleapp:67bb91efb62bfae268bcd0a243a10d48fde80559 --
The following checks were performed on each of these signatures:
  - The cosign claims were validated
  - Existence of the claims in the transparency log was verified offline
  - Any certificates were verified against the Fulcio roots.
[
  {
    "critical": {
      "identity": {
        "docker-reference": "ghcr.io/junaid18183/sampleapp"
      },
      "image": {
        "docker-manifest-digest": "sha256:3408cd56925524ab26302d4c488c5e8fbce357d7dfa1bb03994780b47697f49b"
      },
      "type": "cosign container image signature"
    },
    "optional": {
      "Bundle": {
        "SignedEntryTimestamp": "MEQCIBrzgx7XaYGkDzkpvxJS+locgn1SaTGBd0gDzLWVwoqRAiAxzhQ0nhSk75I7O9h2FWj0JFXDzwo/K/8nNPWal83scg==",
        "Payload": {
          "body": "eyJhcGlWZXJzaW9uIjoiMC4wLjEiLCJraW5kIjoiaGFzaGVkcmVrb3JkIiwic3BlYyI6eyJkYXRhIjp7Imhhc2giOnsiYWxnb3JpdGhtIjoic2hhMjU2IiwidmFsdWUiOiJiZjFkYWI1MzRjOTU0YWU4ZWJkNTJmNzU5NzIxNDdkNWRmM2QyMWQ4MjZlZGY2NTgzMzVkMzAzODU3YjFlN2E4In19LCJzaWduYXR1cmUiOnsiY29udGVudCI6Ik1FUUNJRUlIdVhTM0g1S0ZPWGZlL1EyTzlabXprL2o5dStvVllaaHpFc2VmQy81a0FpQlZScVl1NTU3NlRNNDdaTXdzYy9KMHQ5WXdXZGRVVU1wckQzMWpTbWg4a2c9PSIsInB1YmxpY0tleSI6eyJjb250ZW50IjoiTFMwdExTMUNSVWRKVGlCRFJWSlVTVVpKUTBGVVJTMHRMUzB0Q2sxSlNVTjVWRU5EUVdzclowRjNTVUpCWjBsVlFVcExOQ3MyUmpOMFIzZERkVGhDWTJOeU1XTjBOR3cxVDBrMGQwTm5XVWxMYjFwSmVtb3dSVUYzVFhjS1MycEZWazFDVFVkQk1WVkZRMmhOVFdNeWJHNWpNMUoyWTIxVmRWcEhWakpOVWtWM1JIZFpSRlpSVVVSRmQyaDZZVmRrZW1SSE9YbGFWRUZsUm5jd2VRcE5ha0Y0VFVSUmVFMXFRWGxOVkdoaFJuY3dlVTFxUVhoTlJGRjRUV3BGZVUxVVpHRk5RazE0UlZSQlVFSm5UbFpDUVc5VVEwaE9jRm96VGpCaU0wcHNDazFHYTNkRmQxbElTMjlhU1hwcU1FTkJVVmxKUzI5YVNYcHFNRVJCVVdORVVXZEJSVE5VTmpKa1pGTkplRUpZVkZOMGVVTkVZV2d3Um1ScEszaG1ZV1VLY0dWdkwySXhZV0paVTB0VmMxbHFZVTEwTVhGT01sbExNamxQWVd0WWFFUnZjalUxVG14QlpFRnVUVXBVWTB0UE9HNDNkVkJ2UmxZdlMwOURRVmRuZHdwblowWnJUVUUwUjBFeFZXUkVkMFZDTDNkUlJVRjNTVWhuUkVGVVFtZE9Wa2hUVlVWRVJFRkxRbWRuY2tKblJVWkNVV05FUVhwQlRVSm5UbFpJVWsxQ0NrRm1PRVZCYWtGQlRVSXdSMEV4VldSRVoxRlhRa0pUTUVSRlFXazJhRGwwZWxCWWNFVXJibkZEU1RWMVJtbDROazVVUVdaQ1owNVdTRk5OUlVkRVFWY0taMEpTV1hkQ05XWnJWVmRzV25Gc05ucEtRMmhyZVV4UlMzTllSaXRxUW05Q1owNVdTRkpGUlZsVVFtWm9iREZ2WkVoU2QyTjZiM1pNTW1Sd1pFZG9NUXBaYVRWcVlqSXdkbUZ1Vm5WWlYyeHJUVlJuZUU5RVRYWmpNa1owWTBkNGJGbFlRbmRNZVRWdVlWaFNiMlJYU1haa01qbDVZVEphYzJJelpIcE1NbEoyQ2xreWRHeGphVEYzWkZkS2MyRllUbTlNYm14MFlrVkNlVnBYV25wTU1taHNXVmRTZWt3eU1XaGhWelIzVDFGWlMwdDNXVUpDUVVkRWRucEJRa0ZSVVhJS1lVaFNNR05JVFRaTWVUa3dZakowYkdKcE5XaFpNMUp3WWpJMWVreHRaSEJrUjJneFdXNVdlbHBZU21waU1qVXdXbGMxTUV4dFRuWmlWRUZUUW1kdmNncENaMFZGUVZsUEwwMUJSVU5DUVZKM1pGaE9iMDFFV1VkRGFYTkhRVkZSUW1jM09IZEJVVTFGUzBSWk0xbHRTVFZOVjFadFdXcFplVmx0V21oYVZFa3lDazlIU21wYVJFSm9UV3BSZWxsVVJYZGFSRkUwV20xU2JFOUVRVEZPVkd0M1EyZFpTVXR2V2tsNmFqQkZRWGROUkdGQlFYZGFVVWwzV0ZJM09XRkJRbWNLUlM5R1prOXpNa0ZsUVVkUGRubDJVREVyUnpKUmRrOWtXbE5HUVZoUmJEazRVVWxUV0d4UUx6VmFXR1ZFZW1OMlVtRTVRekJaZEM5QmFrVkJlVm96TmdwNE1VRldMMEZEYjFCVlNYQjBiMFkzWW1NM2NsaElabWszZFdaVU5WRXljRGt3UW0xc1VIUnpPRXR3ZWxWTGVXaEpOV0pQYW05b01rWnBhMFlLTFMwdExTMUZUa1FnUTBWU1ZFbEdTVU5CVkVVdExTMHRMUW89In19fX0=",
          "integratedTime": 1641297739,
          "logIndex": 1023447,
          "logID": "c0d23d6ad406973f9559f3ba2d1ca01f84147d8ffc5b8445c224f98b9591801d"
        }
      },
      "Issuer": "https://token.actions.githubusercontent.com",
      "Subject": "https://github.com/junaid18183/sampleapp/.github/workflows/docker-publish.yml@refs/heads/main"
    }
  }
]
```

And next important item to note is , 

Since we are using **keyless mode of the cosign signing** we have to get the  Github Actions OIDC tokens. This is done by adding the `id-token` [permission](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#permissions-for-the-github_token) to our [job](https://github.com/junaid18183/sampleapp/blob/main/.github/workflows/docker-publish.yml#L9) 

## Reference

- [https://chainguard.dev/posts/2021-12-01-zero-friction-keyless-signing](https://chainguard.dev/posts/2021-12-01-zero-friction-keyless-signing)
- [https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect#updating-your-actions-for-oidc](https://docs.github.com/en/actions/deployment/security-hardening-your-deployments/about-security-hardening-with-openid-connect#updating-your-actions-for-oidc)
