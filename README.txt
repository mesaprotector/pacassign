pacassign takes the following options:
	pacassign -h
		Shows this help text.
	pacassign FILEPATH PACKAGE
		Assigns the given file to the given package. It	will be removed
		if that package is uninstalled while no other package owns the
		file.
	pacassign -t FILEPATH PACKAGE
		Assigns the given file to the given package (sticky). It will
		NOT be removed if the package is uninstalled, and the assignment
		will remain.
	pacassign -o FILEPATH
		Lists any package that owns or was assigned the given file. This
		is a superset of `pacman -Qo`. 
	pacassign -l [PACKAGE]
		Lists files manually assigned to the given package, excluding
		sticky assignments. If no package is specified it will list 
		every file manually assigned through pacassign. 
	pacassign -lt [PACKAGE]
		The same as `pacassign -l`, but includes sticky assignments.
	pacassign -ll [PACKAGE]
		The same as `pacassign -lt`, but includes regular file ownership
		as listed by `pacman -Ql`.
