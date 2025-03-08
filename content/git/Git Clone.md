
```
git clone --single-branch --branch <branch_name> url [folder]
```

After that, if we want to fetch more branch, run this command and check the result

```
git config remote.origin.fetch "+refs/heads/*:refs/remotes/origin/*"

git remote set-branches --add origin [remote-branch]
git remote set-branches --add origin "release-1.*"


git fetch origin
```