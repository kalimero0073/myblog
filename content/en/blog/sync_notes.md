+++
title = "How I automated the synchronization of my KeepNote files"
subtitle = "Tools: Win10, Git with Github, PowerShell"
tags = ['git', 'automation', 'keepnote']
date = 2021-03-31
draft = false

# For description meta tag
description = "Automated sync of keepNote files using GitHub"

# Comment next line and the default banner wil be used.
banner = 'img/automation.jpg'

+++

## Steps :

- Go into the folder where you keep your files: e.g. /docu and initialize a git repository using "git init" via e.g. Git Bash terminal.

```
$ cd /<folder>/docu
$ git init
```

- Then create a repository on Github (https://docs.github.com/en/github/getting-started-with-github/create-a-repo) and connect your local folder with the remote repository using "git remote add origin https://github.com/<your_username>/<your_repo>.git".

$ git remote add origin https://github.com/<your_username>/<your_repo>.git

- Add and upload your file to the remote repository using "git add .", "git commit -m "initial commit"" and "git push origin master"

```
$ git add .
$ git commit -m "initial commit"
$ git push origin master
```
- Create a powershell file "keepnotescript-office-push.ps1" in your repository (you can place it actually anywhere, but I prefer it placed within the repository as no sensitive data is included) and write a script that commits and pushes changes. Attention: this script applies only to the computer you are working on, except you keep the same directory structure on both. Here is the script content:

cd \<some_folder>\<some_folder>\docu 
git add .
git commit -am "made changes"
git push origin master

- Create a powershell file "keepnotescript-office-pull.ps1" in your repository (you can place it actually anywhere, but I prefer it placed within the repository as no sensitive data is included) and write a script that pulls changes. Attention: this script applies only to the computer you are working on, except you keep the same directory structure on both. Here is the script content:

cd \<some_folder>\<some_folder>\docu 
git pull origin master

- Add the powershell files to the Win10 logoff. I followed the instructions on https://lifehacker.com/use-group-policy-editor-to-run-scripts-when-shutting-do-980849001. I added the "keepnotescript-office-pull.ps1" to the User Configuration > Windows Settings > Scripts (Lognon/Logoff) > Logon and the "keepnotescript-office-push.ps1" to the User Configuration > Windows Settings > Scripts (Lognon/Logoff) > Logoff. So every time when I logon to my computer the lates changes are pulled from Github, whereas when I logoff it pushed any changes to the Github repository. 

If you run into issues (e.g. mmc.exe has been blocked) google solutions - in most of the cases you will find a satisfying answer (e.g. https://www.wintips.org/fix-mmc-exe-this-app-has-been-blocked-for-your-protection/). I disabled the UAC in Win10, added the files and then reactived it again as it is a security feature which should be activated.

