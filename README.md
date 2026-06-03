To set up a new project, create the project repo and select this repository as the template by navigating to "Settings." More information [here](https://docs.github.com/en/repositories/creating-and-managing-repositories/creating-a-template-repository). 

To finish setup, you need to do the following:

1. Add the project to Overleaf and set up the syncing between Overleaf and the project folder. Edit `research/bin/backup_overleaf.sh` to add code pointing to the Overleaf and project directory:
```
sync_project <Overleaf Project Name> "/home/jgs/Dropbox/Apps/Overleaf/<Overleaf Project Name>" "/home/jgs/Dropbox/research/projects/active/<path to paper directory in project folder>" 
```
2. Set up permissions to allow RA work (if needed). You can make it so that anyone can do anything, or you could use groups to control this. 
```
sudo setfacl -d -m -R u::rwx,g::rwx,o::rwx /home/jgs/Dropbox/research/projects/active/<proj_dir>
```
I haven't verified that this works:
```
# 1. Change the group ownership of the directory and all existing contents
sudo chgrp -R yourgroup /path/to/target_dir

# 2. Set the setgid bit on all existing and future subdirectories
sudo find /path/to/target_dir -type d -exec chmod g+s {} +
```
3. Allow RA access to the folder on the server
```
# Link the directory to the RA home folder
sudo ln -s /home/jgs/Dropbox/research/projects/active/<proj_dir> <RA dir>
# Make sure permissions are set so the RA has access (probably taken care of by step 2)
```
