#####Version 30 -- December 2014
* Multi-round autofocus:  Added code to RR autofocus to make multiple attempts at autofocus if
current position is more than a set threshold away from focus point.
* Sync/async autofocus: Added separate top-level VI that opetionally can be used to autofocus periodically regardless of acquisition state.  Also added code so that synchronous autofocus in preview and acquisition
is turned off when aynchronous autofocus is running. (Synchronous will resume when asynchronous is turned off, even in the middle of a run)
* New front panel control in multi-mode acquisition to set number of acquisition files to create.  Preview window now shows total number of frames/total time that can be collected with current settings.
* Created new-hnu branch to hold current version of software for new h nu microscope

#####Version 29 -- July 2014
* Published on GitHub
* Added copyright/license info
* Stripped out defunct code
* Removed Roper camera support (at least for now)
* DLLs aren't redistributable so moved them all to `\Program Files (x86)\Gelles Lab Software`
* new-hnu build file still needs updating

#####Version 28 -- February 2014
* Added capability to periodically autofocus during time lapse waits.  To use, in Autofocus Globals.vi set --AF every N seconds during Wait; 0 = don't-- to a non-zero value.
* Added new top level vi, RR asynchronous autofocus.vi, that allows continuous autofocusing (at a specified repeat rate) asynchronously with acquisition.  As the autofocus laser will be on during acquisition, this typically will require inclusion of an IR blocking filter in the emission pathway.

#####Version 27 -- February-April 2013
* Internal change: set up typedef so that we can eventually us I64 file pointers.
* RR autofocus.vi now gives informative error if you forget to do the calibration.
* ixon camera/ixon get one frame.vi modified to run in any thread in an attempt to increase priority of acquisition process
* Made acquire sequence to disk.vi so that it doesn't close and reopen during acquisitions. r346
* Glimpse Image Display Controller.vi controls to save and restore multiple preset intensities.
* Updates to stage software: fixed longstanding bug where you couldn't change number of fields to scan; made limits for x and y separate; added calibration kludge for USB Mad City stage; eliminated HAL stage specifications globals.vi (info is now in stage globals.vi)
* Starting to set up for orca camera (this not yet finished)
* Acquisition directory now includes additional header info including by frame info: lasers, filter, temperature, flow volume, field, stage xyz values.
* Fixed long-standing bug in Load/Save settings.VI (it actually works now).
* New project for 1024 ixon camera on hnu scope
* Multi-mode acquisition.vi now runs automatically; start/quit buttons
* Properly sets default image size for each microscope at beginning of Multi-mode acquisition.vi (settings in camera defaults globals.vi) 
* More graceful error handling if set image size is too large for camera

#####Version 26 -- December 2012
* Start!.vi refactored into Start!.vi and Start! globals.vi
* Stand alone --shutter all shutters-- program to be invoked by login script to put shutters into known closed state at logon (for safety reasons).
* Now using LabView 2011sp1f2
* Phidgets knob box now working to control stage x, y, z
* Shutters activate.vi closes all shutters when it is run

#####Version 25 -- November 2012
Made changes to retroreflection autofocus routine:
* In Autofocus Globals.vi, new control: Set focus to current z position - If you click this button, program will wait till the next time at which autofocus has been programmed, and will then make the current  retroreflection position the new focal point.
* In Autofocus Globals.vi, new control: Manual focus offset (um) - In future autofocus iterations, focus to a position this far away from the calibrated z position.  This control will automaticallyreset to zero when "set focus point to current z position" is activated.
* Not a change, but note the function of these previously existing controls:  Focus mode can be used to temporarily suspend autofocusing (set to --None--). --AF every Nth cycle, N =-- can be set to autofocus less frequently than every cycle.

#####Version 24 -- April 2011

* Set up for new-h-nu with 1024 ixon camera
* Udated to new versions of Andor SDK, Labview 2010 (32-bit), and Windows7 (64-bit)
* No Griffin knob drivers for Win7, so knobs don--t work
* Updated to new ######Version of Mad City Stage USB driver

#####Version 23 -- February 2011
* Minor changes to incorporate orange laser  and notch filter on hnu

#####Version 19 -- July 2009 (rev. 119)
Use with ver. 49 of Glimpse
* Software added to use new QPD with NI USB6001 interface.   The new hardware seems to eliminate the random pauses in acquisition that we had previously.
* Software added to handle Sutter filter wheel for emission filters in shutters activate.vi and Multi-mode acquisition.vi.  Edit Emission filters.ctl to modify the names of the filters.
* Add "starting" message to Start!.vi
* Moved some hardware dependent files into h-nu directory

#####Version 18 -- May 2009
* New feature: time lapse parameters added to Multi-mode acquisition.vi
* Autofocus Globals.vi default averaging is 1.  Don--t increase this setting; high values tend to cause pauses during acquisition.
* Bug fix:  Time lapse wait for next frame.vi pause now works until 20 ms before end of wait (previously 400 ms); fixed bug where pause was remembered between waits.  
The following changes are to reduce occasional pausing and hang-ups during acquisition:
* To reduce pausing, RR autofocus view-calibrate.vi priority to lowest, standard.  Also rearranged front panel.
* PDQ80.vi normal priority, same as caller for the same reason.  
* Glimpse Image Display Controller.vi - user interface
* PDQ80.vi now sets scan interval to 5 ms and incluses a 5 ms wait to allow UI some compute time.

#####Version 17 -- April 2009
* Using SVN version control
* microscope software.lvproj a project that builds a combined LLB with all software to run h-nu microscope
* reorganized files in directory tree and changed some VI names
* added Start!.vi, to be the replacement for "run experiment.vi".  Works in either source tree or LLB 
* Load-Save settings.vi renamed to GPI-Load-Save settings.vi; now not automatically run; run from Plugins menu of Glimpse.  Default Vis loaded and saved to reflect new names.  Loading saved configuration files that reference the old names will not work.
* Use with glimpse v. 48, LabView 8.6

#####Version 16 -- July 2008
Use with glimpse v. 44
Bug fixes:
* Cured (I hope) bug where autofocus caused program to crash (changed number of scans to zero in call to PDQStartScan in PDQ80.vi; also changed DLL calls to non-reentrant, normal priority)
Laser safety:
* Autofocus laser shutter does not open automatically at startup, you now need to open it manually (RR autofocus view-calibrate.vi)
* Autofocus laser shutter now closes after autofocus even if an error occurs during autofocus (RR autofocus.vi)
Minor ease-of-use issues:
* QPD sensor now averages 25 readings by default (Autofocus Globals.vi)
* Startup temperature now -80 by default (ixon startup.vi)
* Changed scale of XY position graph (RR autofocus view-calibrate.vi)

#####Version 15 -- July 2007

Minor bug fixes/feature adjustments:
* RR autofocus laser is now shuttered during acquisition, even when RR autofocus view-calibrate.vi is running.  Also, camera is shuttered during RR autofocus.  (RR autofocus.vi)
* Several shutter delays shortened. (Ixon multi-mode acquisition.vi and RR autofocus.vi)
* Fixed bug where one additional frame would be collected after pressing --STOP-- in Time lapse wait for next frame.vi
* Window positions adjusted for new display

#####Version 14 -- July 2007

* If wait till next cycle is longer than 5 s, camera shutter now closes during wait.  (Time lapse wait for next frame.vi)
* When scanning n x m fields, you now have a choice of waiting for the cycle time after acquiring every field, as opposed to only waiting after the last field in the set (i.e., the m n th field). (Ixon multi-mode acquisition.vi)
   Bug fixes:
* Stage scanning didn--t work properly except when number of fields was 3 x 3.  Duh.  (stage step to next field.vi)
* Time lapse wait for next frame.vi sometimes got stuck so that you needed to press --Go-- to get it to start again.
* Sometimes when you pressed stop, acquisition didn--t stop immediately but only after the next frame.  (ixon acquire sequence to disk.vi)

#####Version 13 -- June 2007

* Re-wrote knob driver xy.vi and knob driver z.vi to eliminate the annoying slow response caused by slow processing of multiple stage move commends in rapid succession.
* Added the new top level routine Load-Save settings.vi to save and restore experiment parameters.

#####Version 12 -- June 2007

* Added the capability to automatically or manually focus using the quadrant photodiode/IR laser setup.  This involved minor changes to gpi-h-nu-ixon.vi plus the addition of new routines RR autofocus view-calibrate.vi (a top-level routine),  RR autofocus calibrate.vi, and RR autofocus.vi. Also made extensive changes to Autofocus Globals.vi, which serves as the settings page for both image analysis and retroreflection autofocus methods.  The quadrant photodiode is run throught the new PDQ80.vi, which calls the home-made dll Pds80qs1.dll.  See earlier note about drivers etc. for this device.
* Bug fix:  Calculate field raster.vi now handles field arrays that are only one row or one column wide.

#####Version 11 -- May 2007

* Added capabilities to gpi-h-nu-ixon.vi so that you can acquire from multiple fields of view in the sample during the acquisition run.  The program goes thru a complete cycle of the wavelength program at one field, then steps the piezo stage to the next field and repeats.  A user-specified number of fields are scanned (in a rectangular array).  When you run gpi-h-nu-ixon.vi, if the --Scan fields-- box was checked on the front panel a new panel stage step to next field.vi will pop up to allow you to specify the x and y dimensions of the field array.  Note that data from all fields is combined in a single output file (there are separate files for each laser wavelength as usual).  To analyze data for each field separately, the analysis program will have to pull out every Nth frame--.
* Time lapse wait for next frame.vi now has a --Pause-- button to temporarily pause acquisition and a --Go now-- button to skip the wait.
* Added note about context help to front panel
* Added index display to Acquisition Protocol control so that protocols of >3 steps are possible.  Duh.
* Made a typedef for move stage command.  Added options to re-center stage in xy or z and to do movements to an absolute position instead of moving relative to current position.  Modified Stage Controller.vi accordingly.
* Added globals for max stage movement in xy and z to Stage globals.vi

#####Version 10 -- Mar 2007

* Add shutters activate.vi
* Added GaAs laser (laser type.ctt, shutter operate.vi, ixon multimode acquisition.vi)  
* Shutter operate.vi updates global variable with shutter status; same for camera shutter operate.vi (hardware status globals.vi)
* Made shutter -- > port translation vi (shutter port lookup.vi) 
* Uses Glimpse 47/LV 7.1.1

#####Version 9
I don't think there is one, but leaving space just in case

#####Version 8 -- Mar 2006

* Corrected counting error that previously put number of frames acquired minus one in glimpse header file.

#####Version 6 -- Jan 2006

* "vollath_calculation_focus_algorithm_serge_doug.vi" updated to handle negative pixel values in 16-bit images
* In Ixon multi-mode acquisition.vi, Added an extra 20 ms delay to allow time for shutters to close after each channel is acquired.
* Ixon multi-mode acquisition.vi: now collects N cycles, not N+1 cycles
* iXon Autofocus.vi:  Autofocus shutters now close before, not after, final stage movement to allow time for shutters to close.  Additional multi-step delay parameter added to autofocus globals to allow additional waiting after first and last stage movements, which are bigger than the intermediate movements.

#####Version 5 -- Jan 2005

* Added autofocusing to iXon multi-mode acquisition
* Updated help file

#####Version 4 -- Jan 2005

* Added z-stack acquisition top-level VI

######Version 3 -- Dec. 2005

* Modified ixon startup.vi so that it actually turns off the camera when your--re done.  Duh.

#####Version 1 - Aug. 2005



