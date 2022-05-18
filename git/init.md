使用github创建repository后的步骤

```
echo "# dltianzheng" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:dltianzheng/dltianzheng.git
git push -u origin main
```

https://git-scm.com/book/zh/v2

git config --global user.name "dltianzheng"

git config --global user.email 18331512890@163.com



```shell
Command line instructions
You can also upload existing files from your computer using the instructions below.


Git global setup
git config --global user.name "Administrator"
git config --global user.email "admin@example.com"

#Create a new repository
git clone git@8112b9d2b726:root/tianzheng-notebook.git
cd tianzheng-notebook
git switch -c main
touch README.md
git add README.md
git commit -m "add README"
git push -u origin main

#Push an existing folder
cd existing_folder
git init --initial-branch=main
git remote add origin git@8112b9d2b726:root/tianzheng-notebook.git
git add .
git commit -m "Initial commit"
git push -u origin main

#Push an existing Git repository
cd existing_repo
git remote rename origin old-origin
git remote add origin git@8112b9d2b726:root/tianzheng-notebook.git
git push -u origin --all
git push -u origin --tags
```

