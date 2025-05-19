---
id: 6lbge1wk1m9u2ycht7ixbh0
title: ssh
desc: ''
updated: 1743221088204
created: 1741332630767
---


Creating ssh 2 files

```bush
ssh-keygen -t rsa -b 4096 -C "your-email@example.com"
```

- upload public key to aws codecommit 
- take ID from aws and add to .ssh/config
- you can add more ssh key to this config file by named with **Host codecommit-dev**

Remark - I got a error with this named Host.so i changed line 2 from 
- ~~HostName git-codecommit.*.amazonaws.com~~ to
- **HostName git-codecommit.ap-southeast-1.com**


this is a sample of .ssh/config file.
```bush
Host git-codecommit.*.amazonaws.com
  User APKAVVX3LCQUQEBLTJ6W
  IdentityFile ~/.ssh/id_rsa
  
Host codecommit-dev
  HostName git-codecommit.ap-southeast-1.amazonaws.com
  User APKA3FRRJFYP77QOZIVX
  IdentityFile ~/.ssh/idrsa_dev
```

checking ssh-service status

```bush
Get-Service ssh-agent
```

### if stopped ssh need to run from admin powershell
```bush
Set-Service -Name ssh-agent -StartupType Automatic
Start-Service ssh-agent
```

### ssh need to add 
```bush
ssh-add C:\Users\htetoo.lwin\.ssh\idrsa_dev
# check 
ssh-add -L
```
### Calling host variable

you can see only using **codecommit-dev** in **ssh://codecommit-dev/v1/repos/git-test**

In config of .ssh/config
```bash
Host codecommit-dev
  HostName git-codecommit.ap-southeast-1.amazonaws.com
  User APKA3FRRJFYP77QOZIVX
  IdentityFile ~/.ssh/idrsa_dev
```
so codecommit-dev = git-codecommit.ap-southeast-1.amazonaws.com

- so you can call git clone like this
```bash
git clone ssh://codecommit-dev/v1/repos/kbz-analytics-glue
```

-------------------------------------

ssh can use by share 

so I use only one ssh key to aws prod and dev

----------------- End 