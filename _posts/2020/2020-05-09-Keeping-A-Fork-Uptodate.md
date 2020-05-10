---
layout: post
title:  "Keeping a Git Fork Upto date"
description: "Keeping a Git Fork Upto date"
author: juned
categories: [ git ]
tags: [git]
image: assets/images/git.jpg
featured: true
hidden: true
#rating: 4.5
---

### 1. Clone your fork:
    ```
    git clone git@github.com:junaid18183/helm.git --branch master --single-branch
    ```
### 2. Add remote from original repository in your forked repository: 
    ```
    cd helm
    git remote add upstream git@github.com:helm/helm.git
    git fetch upstream
    ```

### 3. Updating your fork from original repo to keep up with their changes:
```
    git pull upstream master
```

### 4. Push your Changes to your Repo Origin
```
git status
git push origin master
git status
```

### 5. Add your changes and commit
```
git commit -am "Fixes repo parsing"
[master 5d9bac4d] Fixes repo parsing
 1 file changed, 14 insertions(+), 1 deletion(-)
```

### 6. Sign off your messages
Few Opensource Repo's like Helm require you to Signoff your messages for enforcing the [DCO](https://developercertificate.org/), so sign the commit, And push the chanegs again to master

```
git commit --amend --signoff
git push --force-with-lease origin master
```

### 8. Set the auto sign off to true in your git config
```
git config --global format.signoff true
```
Once you add this you can 

### 7. Sent a PR to the original repository

Send a PR to the original repository.