The Glimpse core is the GUI for viewing and working with video data.  It has no microscope-dependent parts and thus can be run on pretty much any computer.

##### Software requirements
* Matlab
* LabView Development System
* NI Vision
* `LabView hardware configuration.ini`: The directory that contains the software (`Glimpse.exe` or `Glimpse.llb`) needs this text file, which should point to the default data storage directory by containing: 

```
[RAID drive]
Root path=d:\glimpse
```

##### Building
The glimpse core program is contained in the `glimpse core` directory tree.  The project file `glimpse core\glimpse.lvproj` will build a .llb or .exe version of the program, or installers for the latter. For those with access, the Gelles lab file server has pre-built versions of the installer(s) at `lab\glimpse installers`.
