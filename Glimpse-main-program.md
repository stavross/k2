The Glimpse Main Program is the GUI for viewing and working with video data.  
It has no microscope-dependent parts and thus can be run on pretty much any computer.

Software requirements:
* Matlab
* The directory that the software is run from must have a text file 
"LabView hardware configuration.ini" that contains a pointer to the data 
storage directory, e.g.,

[RAID drive]
Root path=d:\glimpse


The glimpse main program is in the *Glimpse core* directory tree.

The project file is *Glimpse.lvproj*.
