Revert master to previous committ
From within project

git reset --hard <old-commit-id>

git push -f <remote-name> <branch-name>

remote-name = your clone url

branch = master another branch that the repository has.
    
    git reset --hard 94a3f694b3211186ca65f0dc51a84ef54fcc68e4
    git push -f https://github.com/delebash/ElectronAureliaPouchSyncfusion.git master