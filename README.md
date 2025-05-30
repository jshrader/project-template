To set up a new project, create the project repo and select this repository as the template by navigating to "Settings." More information [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository). 

To finish setup, you need to add the project to Overleaf and set up the syncing between Overleaf and the project folder. To do this, edit `research/bin/backup_overleaf.sh` to add code pointing to the Overleaf and project directory:
```
echo "<project name>"                                                                   
rsync -avu --delete --exclude-from='/home/jgs/Dropbox/research/bin/backup_overleaf_exclude.txt' \
  "/home/jgs/Dropbox/Apps/Overleaf/<project name>/" \
  "/home/jgs/Dropbox/research/projects/active/<proj_dir>/output/paper/overleaf_bu/"                                                               
(cd /home/jgs/Dropbox/research/projects/active/<proj_dir>/output/paper/overleaf_bu/overleaf_bu/ &&                
     git add .                                                                                           
 git commit -m "Overleaf backup $(timestamp)" -m "$period autosync of Overleaf files."                   
 git push                                                                                                
)                                                                                                        
```
