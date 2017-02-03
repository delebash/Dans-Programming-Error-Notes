Revert master to previous committ
From within project

git reset --hard <old-commit-id>

git push -f <remote-name> <branch-name>

remote-name = your clone url

branch = master another branch that the repository has.
    
    git reset --hard 94a3f694b3211186ca65f0dc51a84ef54fcc68e4
    git push -f https://github.com/delebash/ElectronAureliaPouchSyncfusion.git master


## .gitignore to ingore config files that you want an initial copy on the remote repository but after that no changes should be committed  ##

    1. commit file
    1. add to .gitignore src/config/dreamfactory-config.js
    1. git rm --cached src/config/dreamfactory-config.js
    1. git commit -m "Removed src/config/dreamfactory-config.js"

verify that changes are no longer tracked

https://jlordiales.wordpress.com/2012/12/28/when-git-ignores-your-gitignore/