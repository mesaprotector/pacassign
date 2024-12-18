# pacassign
Assign files on your system to software packages to uninstall more cleanly

Arch's package manager, pacman, is pretty good at cleaning up when you uninstall a package. However, stuff can still remain in places like /var/log and $HOME, and six months later you're left wondering if it's safe to remove that "~/.config/QtProject.conf" file that you can't recall ever using. 

For the install micromanagers out there (like me), this little utility provides a solution. It doesn't do anything fancy like modify the pacman database; instead you can manually ASSIGN files to any package you have installed, which will be kept track of in its own separate database, and optionally will be removed when that package is, using a pacman hook. 

This script is especially meant to be used with the handy lostfiles utility, which finds all unowned files on your system outside of $HOME; you can assign most false positives and filter them out.

Options supported:
- query which files are owned by/assigned to a given package (`pacassign -l`, analogous to `pacman -Ql`)
- query which packages own/are assigned a given file (`pacassign -o`, analogous to `pacman -Qo`)
- assign a file to a package, to be removed when that package is (just `pacassign`)
- sticky-assign a file to a package; it won't be removed with the package, but will still show up in queries (`pacassign -t`)
- undo a previous assignment (`pacassign -r`)

See helpfile for more detailed information.

To protect against disasters (such as assigning your ~ to a single package), pacassign will sticky-assign all parent directories of any assigned file, so that they won't get removed; this can be manually overridden.

The script mostly works, but bugs almost certainly still exist; help welcome. 

# Configuration

There are only two configuration options; both are set by environment variable.

The first one is PACASSIGN_USER. If set to "root", only root can run pacassign, and the pacman hook will run as root. If set to your regular user, you will be able to run pacassign without root, but pacassign will not be able to clean up files that you do not have permission to delete. 

The second one is PACASSIGN_ENFORCE. If set to "yes" (VERY MUCH NOT RECOMMENDED UNTIL THIS SCRIPT HAS BEEN MORE THOROUGHLY TESTED!) then the pacman hook will delete files assigned to a package on its removal, provided they aren't owned by anything else. Otherwise, the pacman hook will just print the list of files it *would* have deleted.
