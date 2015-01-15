#####Version 54 - Jan 2015
* Corrected bug that prevented saving long files (>2Gb) of 16-bit images in Glimpse core/Seq file v 1/Frames per axquisition file.vi 

#####Version 53 - June 2014
* Added/updated copyright text
* Published on GitHub

#####Version 52 – June 2013
* `GPI-Join Sequences.vi`

  1) added code to handle header2 data 

  2) using millisecond ttb values instead of time of first frame values to set relative times of sequences

* Updated project config
* Updated GLIMPSE Sequence Player.vi to display header2 metadata if present
* Glimpse Image Display Controller.vi preset values now saved in global between executions.
* Made sure that info is being converted to correct data type in Write sequence info to MAT file.vi
* Added stage xyz data to header2
* Fixed Load/Save settings VI
* Set up typedef so that we can eventually use I64 file pointers.

#####Version 51 – September 2010 
Revision:  238
* Fixed broken 
* Fixed bug in Join Sequences plug-in where it was saying that the output file had one more frame than it actually had.
* Default file storage directory now is a subfolder with the name of the user (thanks Johnson!).
* Added slim executable installer
* Switched to manually populated project.  Removed defunct build specifications.
* Changed to GPL ver. 3 or higher
* Updated join sequences plugin to be compatible with new file header parameter
* Added end of last cycle time to `Video acquisition state.ctl`
* Bug fix:  Merge sequences now handles timestamps properly.

#####Version 49 – July 2009 
Revision: 126
* Can now read Glimpse format (.seq) movie files produced by Alex’s Matlab routine. (Glimpse set up to read sequence.vi uses the header.mat file if there is no header.glimpse file.)
* New Join Sequences plug in will merge frames from 2 or more sequences in chronological order.
* Video acquisition features are now plug-ins.  They are not in the default glimpse build but can be inserted.
* Miscellaneous organizational stuff:
  * Simplified executable installer build script by removing unneeded components
  * Moved all video acquisition code to plug-ins in \frame grabber
  * Fixed Glimpse.lvproj so builds will work
* Developing particle tracking code but not yet finished
* Changed execution systems to improve UI response: Glimpse Image Display Controller.vi - user interface

#####Version 48 – April 2009
* GLIMPSE Sequence Player now can play just a chosen field of view in movies that were made using the piezo stage to repeatedly image different fields. 
* Bug fix: black/white levels in printing image should now be set properly
* Details:
  * Glimpse Image Display Controller.vi Corrected to properly update last window black/white levels global
  * Modied GLIMPSE Sequence Player.vi to run event-driven.  Frame range.ctt and Glimpse sequence player compute next frame number.vi are new subroutines.
  * Added "error in" input to GLIMPSE Fetch Image.vi
  * Glimpse set up to read sequence.vi: Added "error in" input.

#####Version 47 – March 2009
* Now using LabView 8.6
* Use subversion repository
* Resolved obsolete references to old libraries
* Completely re-worked Glimpse Plugin Handler.vi to make it compatible with the security restrictions in LV 8.  Works in both source and executable builds.  In source builds the plug-in list is assembled dynamically; in exe builds uses list hard coded into Glimpse plugin list plugins.vi
* Changes to build/install scripts:
  1.	Added movie merge plug-in to tree.
  2.	new build targets: LLB, LLB installer
  3.	modified both installers to add labview hardware configuration.ini.default
  4.	The LLB installer does not work; this is a bug in LV 8.6: http://forums.ni.com/ni/board/message?board.id=170&thread.id=355968

#####Version 46 – August 2008
* Now using LabView 8.5.1
* Sequence player now optionally will display the AOI boundaries superimposed on the live video playback.  Hooray!
* Glimpse Image Display Controller.vi New front panel option makes window stay where you leave it on the screen.
* Glimpse Image Display Controller.vi Added black/white level presets to image display controller.
* Change sequence player data file.vi Tried to make UI less annoying by cutting down or the number of clicks needed to select a file.
* Out put of AVI movies from sequences tested and is working.  Intensity scaling seems OK.  
* Re-organized: flatten to 8-bit RGB.vi
* Sequence player:  Print image now works with 16-bit images; prints AOIs too, prints file name and black/white levels.

#####Version 45 – August 2007
* Port to LV 8.2.1.  Needs to be tested with acquisition plug ins.
* Pending: add aoi overlay to sequence player/display controller
* Pending: add print screen to aoi controller

#####Version 44 – August 2007
* Added ugly kludge to Acquire sequence of frames.vi to ensure that correct value of “Element 0 of TTB” gets stored in sequence header.  No idea why it isn’t working.

#####Version 43 – June 2006
* Glimpse write video header file.vi:   Starting frame number passed to Write sequence info to MAT file.vi is 0 instead of 1.
* Write sequence info to MAT file.vi now saves image width and height
* Added keyboard shortcut to set aoi menu in sequence player
* Fixed bug in display controller in which black/white levels of current image were updated every time a new image was sent to the controller, regardless of whether or not it was an image for the current window.
* Changed name of Fit Aois to Fit Aois.vi.  
* Fixed Fit Aois.vi so that AOIs do not shrink if they run in to the edge of the frame
* Fit Aois.vi outputs time stamp if no fit when “write record when no fit” is on.

#####Version 42 – January 2006
* Modified AOI to optional rectangle.vi to properly handle empty AOI parameter.  This was needed for compatibility with some plug-in code.
* Cosmetic changes to splash screen.
* Glimpse image display controller.vi:  Corrected to allow windows to initialize out of numerical order (useful for plug-ins).  Added some error handling.
* Changed Glimpse IMAQ startup.vi so that it properly warns the user if an IMAQ board is not present.
* Made MAT file output of glimpse.header information.

#####Version 41 – January 2006
* Included vision71rte.exe and lvruntimeeng.msi in the installer package with a batch file, GLIMPSEpost-install.bat, to execute the installers of the run-time engines and delete them after they’ve completed.
* Exit from Front Panel now working properly.
* The part of Glimpse that saved individual Tiffs (not sequences of Tiffs or stacked Tiffs) had a bug that prevented it from working with 16-bit images.  Fixed.
* In Glimpse Acquire Time Lapse, and Glimpse Acquire to Disk, it used to be that the acquisition directory name that displayed on the screen was the last directory acquired, not the current directory being acquired.  Fixed.
* When reading stacked tiffs, the program now recovers more gracefully if it can’t find a .MAT file containing the time stamps.
* In AOI Stats.vi, the integral of the aoi is now saved into a signed rather than unsigned variable, which should fix a problem encountered with 16-bit images that have negative pixel values.
* Global Plugin Handler included at the Glimpse front panel to run subroutines for additional functionality or hardware-specific processing.
* Changed Get TTB value to correct bug that incorrectly calculated values for interlaced frames.
* Included Movie Merge plugin for use with the Global Plugin Handler.

#####Version 40 – August 2005
* Glimpse display controller now saves settings to a global variable (this change allows plug-ins to react to user changes in display settings). 
* Glimpse display controller now brings the currently adjusted window to the front.  It also has new momentary-action buttons for auto-scale, -size, and -position
* Previous versions of Glimpse saved the time stamps for each frame of a TIFF stack in a separate MAT file, but did not read the time stamps back in when a TIFF stack was read.  This is now rectified.  To read in the time stamps, set Milliseconds per frame equal to zero in Glimpse Sequence Read.vi

#####Version 39 – July 2005
* In sequence player, added capability to simultaneously display multiple views of the same image with different gains/offsets.  
* Updated Image display with gain offset so that all windows display scroll bars even when not autopositioned.
* Fixed help files to remove links to external files.  Note that, depending on security settings, help may not display properly unless glimpse.llb (or .exe) and glimpse.chm are in the same directory under \program files.

#####Version 38 -- October 2004
* Changed program so that sequences with > 32,767 frames would work properly in sequence player.  Went through numerous section of the program to make certain that frame numbers were always stored in a U32.  An exception is the SEQ format file reading and writing, which does not support sequences with more that 65,535 frames owing to a limitation in the format itself.
* Fixed bug in image display gain-offset that sometimes prevented image displays from having scroll bars. 

#####Version 37 -- September 2004
* Now works with LabView 7.1.  Note that IMAQ 3.0 is required.
* In Glimpse window Average.vi:
  * Corrected bug that prevented 16-bit images with negative pixel values from averaging properly
  * Made "Stop" button functional even after avaraging has begun
  * Added option to use a jumping window instead of a sliding one.
* Modified acquire to disk to better facilitate plug-ins that stop and restart aqcuisition.  Also made some minor changes along the same lines to Acquire Time Lapse.  Added documentation for both.
* Version 37 was never formally released; video acquisition has not been extensively tested with this version except for plug-ins.

#####Version 36 -- August 2004
* There is now a help file, and many menus have context help.  Please tell Jeff what additional help needs to be added.
  * To see the context help window, press Ctrl-H OR click the yellow question mark toolbar button OR select Help>>Show Context Help.  The context help window shows help for whatever is under the cursor.  To show the context help for the whole menu, position the cursor on the menu icon in the upper right corner.
  * To view the help file, select Help>>Help for this VI OR click Click here for more help in the context help menu.
* 16-bit images are now truly 16 bit, not 15 bit as before.  LabView uses an intensity range of -32768  to +32767, not 0 to 65536.  External stacked TIFF files now properly convert to/from 0 to 65536 upon input/output.  It is no longer necessary to subtract 32,768 from each pixel after reading Labview-produced TIFFs into Matlab.
* Changes to tracking by image fitting routines:
  * Now handles multiple functions
  * Now allows each parameter to be held constant or varied at the user's option.  
  * Now shows which params do not require initial values.
  * Fixed bug where you could not change the starting and ending frame numbers in the fit window; now you can.
  * Added a checkbox that Controls the output of the program for AOIs in which the fit fails or one or more of the parameters is out of range. If the box is not checked, there is no output from such AOIs. If the box is checked the program outputs the integral of the AOI only. The other parameters are output as zero, except for the MSE which is output as -1 (to identify the record as a "no fit").  This will allow plotting the baseline intensity of the AOI after a molecule has photobleached.
  * The "Cancel" button in Fit One AOI now actually does cancel.  Duh.  It takes a while, because it finishes all AOIs in the current frame.
  * The fit routines now use analytical derivatives instead of estimating them.  This is an internal matter that should not significantly affect the results.
* Fixed problem with saving multiple aois into stacked tiffs.
* Can now save sequence into avi format.  Warning: the AVIs are uncompressed (and therefore large) and only have 8 bits of resolution.
* Sequence player
  * added controls to disable autmatic sizing and repositioning of image window, if the user so desires
  * in the Select AOIs window, and in the Tracking Results window, auto resizing is disabled after the first frame, so you may have to resize the window manually.
  * added adjustable scaling for the black/white level control
* Both AVI and stacked TIFF output now produce a separate documentation file (in Matlab's MAT format).  The only contents of the file will be a structure named 'vid'.   Read the file using the Matlab 'load' command:
```
>> load 16.01.mat
>> vid

vid = 

      moviefile: '\\Jg_i\c-drive\LabView development\Glimpse\junk4\16.01.tif'
       username: 'gelles'
    description: 'GLIMPSE v. 36 (8/04)'
        nframes: 5
          time1: 3.1555e+009
            ttb: [300 334 367 400 434]
          depth: 0
```
Notes on the elements of the structure:

nframes -- number of frames in the movie

time1 -- time of acquisition of the first frame in seconds from Jan 1, 1904

ttb -- timestamps of  frames in milliseconds

depth -- 0 <-> 8-bit; 1 <-> 16-bit

Internal features:

* Image display gain-offset handles both image display in an indicator and in a separate window.  This is intended to replace Image indicator gain-offset.vi


#####Version 35 -- February 2004
-- Average Frames now averages into a 32-bit integer array instead of a 16-bit image; this now allows averaging 16-bit images without fear of overflow.
-- Corrected bug in setting gain and offset in GLIMPSE Acquire Time Lapse.vi.  The bug did not affect operation of glimpse but did prevent gain and offset being set properly in plug-ins that stop and restart acquisition.

#####Version 34 -- January 2004
-- Eliminated GetPrintersList.vi; now using vi.llb function Query Available Printers.vi
-- Added "autoscale intensities" button to sequence player.
-- Changes nearly every major vi in program to pass header information thru parameters rather than thru globals.  Also added code to make unique image buffer names in the acquisition routines.  Taken together, these changes make it possible to have multiple instances of the acquisition routines (for example, to do alternating acquisitions from two different video channels).
-- Reorganized acquisition vis to make them better accesible to external calls, to allow users to write their own acquitision routine "plug-ins".  A limitation of this approach is that it requires the source of the Glimpse application and the full development #####Version of LabView (does not work with an executable #####Version of Glimpse).
-- When called from a plug-in, the revised acquisition routines can collect a specified number of frames and then stop, saving the state of the acquisition so that it can be resumed later.  This means that a plug-in can stop and re-start acquistion to the same file, allowing interruptions for autofocusing, shuttering, etc.
-- Added a button for context help and documentation for many of the operating controls.  Some of the controls are not yet documented, or are documented incorrectly.
-- Re-wrote video buffer allocation VIs.  They now time out, so they don't have to pop up, eliminating some needless clutter to the UI.
-- Inserted a work-around (in Acquisition buffer init phase 2.vi) for the bug in NI-IMAQ (the bug is in IMAQ RectToCoord.vi, which is called by IMAQ Configure List.vi) that prevents it from setting acquisition regions properly.
-- Added a "Number of iterations" control to the tracking by curvefitting panel.  Reducing this number should reduce the time wasted on fitting bad images that do not converge.
-- Time stamps in Acquire Time Lapse now use the middle of the acquisition of each frame, not the beginning.
-- Added code to acquire 10-bit images from the PCI-1409 boards, but this has not been tested and probably doesn't work yet.
-- Added the capability to read and write video sequences as Matlab-style stacked Tiffs.  These routines use Matlab and so will not run unless Matlab is installed.




#####Version 33 -- December 2003
-- Migrate to Labview 7

#####Version 32 -- July 2003
-- Added "update graphics" checkbox to fitting window.  Unchecking this should greatly improve speed on long runs.

#####Version 31 -- June 2003
-- "Acquiring larger than 8-bit images" error message no longer erroneously appears when acquiring 8-bit images.  Duh.
-- Added AOI --> OR conversion to Extract 16-bit array from Image.vi.  The effect of this is to correct a bug where fits were to aois 1 pixel larger than specified.
-- Modified Fit AOIs to handle multple analysis procedures
-- Modified Fit One AOI to take parameters as an array, not as a cluster, to allow for variable numbers of parameters
-- Added AOI Stats analysis procedure to calculate aoi centroids, integrals, mins and maxs.
-- Improvements to html tracking report.  Now links to .csv file.

#####Version 30 -- May 2003
-- .csv is now default file type in tracking by curve fitting aois routine.
-- in autofocus, "delta focus steps" displayed was previously too large by one
-- autofocus now does not change focus or move aoi if aoi contrast too low or if aois contain any pixels equal to zero or maximum
-- 16 bit images work in field modes
-- Can save sequences of 16 bit images to multiple tiff files (but not to .seq files) and single images to tiff files (but not to .img files).
-- Print images now uses same code as print aois.
-- Average frames now works with 16 bit images.  Images are summed into a 16 bit buffer, so they will overflow if they are too bright or if too many frames are averaged.  Ask Jeff to fix this if it becomes a problem.
-- Added more informative error message if you try to acquire video > 8 bits.
-- Increased ring size to 100 in an effort to prevent buffer overrun errors.  However, this change may cause a slight delay between clicing the button and the commencement of acquisition.
-- Live video should now start with the correct gain and offset instead of waiting until the first time gain and offset are changed.

#####Version 29 -- May 2003
-- Fixed the bug in assigning time values during acquisition of averaged frames.  Really.
-- Fixed bugs in autofocus relating to image orientation and inappropriate disengagement of clutch.

#####Version 28 -- April-May 2003
--added code to turn off vcr acquisition option if no vcr is present
--acquisition is now stopped and restarted every time gain and offset are changed; this cures the bug where the gain and offset would not work with the 1409 board (in the new computer)
--add autofocus to time lapse acquire, but it needs tweaking to work better.
--Read TIFF, AOI routines, and Player now work with 16 bit images.  Warning: no other parts of the program work with 16-bit images.  16 bit images work in frame mode only.
--Display gain and offset now settable in Player.  Settings carry through to AOI and fitting sub-vis.
--Added 2D Gaussian curve fitting to Player.
--Added button to AOIs menu that prints the image with superimposed aois.
--Read sequence from disk now has option to set time interval between frames for input from multiple tiff files.  This may (?) cure the bug in which time lapse sequences were some times reset to 33 ms fame intervals.
--In subtract background, tiff is now properly used as the default file type for the background image.  The abort button now abouts without asking for the file name.

#####Version 27 -- March 2003
--Fixed progress bar limits in Make whole seq.vi
--fixed glimpse acquire time lapse to zero ttb array before acquiring.  Also made various changes to routines that call

#####Version 26 -- February 24, 2003
--Fixed a spectacular bug in Glimpse FEtch Image.vi in which Fields, even 1st was being handled completely incorrectly.
--Fixed incorrect reuse of image buffer in Glimpse average fields.
--640 x 480 now default in Initialize
--Added VCR batch queue vi.
--Extensive mods to error handling and UI in VCR routines.
--For many windows, closes the parent window while the child window is open to eliminate confusion about which window is active.
--Exit button in launcher now exits Labview
--Added about glimpse

#####Version 25 -- February 2003

-- Fixed oversight where player did not close old acquisition files when new files were opened internal to the vis. This prevented files from being deleted.
-- Fixed problem with player exit button sometimes not working.
-- Shortened save by tag to be within char. limit
-- Modified open acquisition file for write.vi to gracefully handle blank file name selections.
-- Added skip frame test.vi for testing acquisition hardware.

#####Version  24 -- January 2003
-- Modified to solve problem that labview stream files have to be smaller than 2^31-1 bytes to allow indexing.  This entailed changes to:
----init
----acquire to disk
----player
----save seq
----test seq
----seq read
----acquire time lapse
----subtract background
----filter
----batch acquire
-- subtract background and filter now properly handle fields modes.  they are now non-destructive, storing results into a new acquisition file.
-- Read Seq:
----extensively modified to rationalize and (hopefully) to fix intermittent bugs
----added code to read TTB
----now displays file name and header info during read
-- Save img now saves in tiff format as well; saves whole frames as well as aois
--add version string to globals; display in splash screen and write this to seq files
--improved error handling throughout.  some routines now use customized error handler to responde properly to user error codes (>5000).
--split fetch frame and fetch ttb value to improve seq save speed.
--removed gallery button since that feature is not going to get implemented anytime soon.

#####Version 23 -- September 2002
-- Derived directly from v. 21, but incorporated new "Get environment variable.vi" from v.22.
-- Record sequence to disk:
---- Improved error handling for file open etc.
---- New code for opening new or overwriting old files
---- improved code for detecting skipped frames
---- use new file for autostart
---- save offsets table to disk
---- return file name
-- Sequence player:
---- file handling in play
---- added select file button
---- added file indicator
---- revamped field/frame code; works ok with new setup
-- Save sequence: both seq and tiff changed to get from disk and to be compatible with frames/fields
-- changes to launcher

#####Version 22 -- April 2002
-- Last (?) non-disk-acquire version.
-- Fixed some kind of problem with getting environment variable (username?).  Can't remember exactly what.

#####Version 21 -- 
-- Testing acquire to disk performance.  Never used in production.
#####Version 20 -- March 2002
-- Added batch digitize vi to automatically acquire a single sequence using VCR
-- Making production version as .exe instead of .llb
#####Version 19 -- March 2002
-- Fixed problem with stop button in sequence player sometimes not working properly.
-- "Fire up" and "initialize" windows position themselves in LR corner of screen.
#####Version 18 -- Feb. 2002
-- Fixed abort button in "fire up ring acquisition" VI.  Also put 50 ms delay inside loop in that vi to prevent system stalling on startup.  Also removed error handlers in various other routines so system will not get hung up if there is no video in.
-- Updated to use NI-IMAQ 2.5
#####Version 17 -- Sept. 2001
-- Added timestamp and mode display to sequence player
-- Changes window positions in sequence player
-- Rewrote display/save averaged fields code (in fetch image vi) so that it does in fact actually do that.
-- Cosmetic changes to window average vi.

#####Version 16 -- June 2001
-- Added vi to do temporal filtering on sequence in RAM. 

#####Version 14 -- July 2000
-- Corrected bug that mis-sized fixed size aois by 1 or 2 pixels.
-- Made save seq save correct size aois instead of correct size - 1

#####Version 13 -- Apr. 2000
-- Option to save/display fields as well as frames
-- Sequence player positions tool palette and deletes it when vi is closed

#####Version 12 -- Sept. 1999
-- Save sequence of tiff files fixed up, now handles aois.
-- Initialization window now shows live video and you can specify the acquisition window using the mouse
-- Tools window now is positioned properly relative to live video windows

#####Version 11 -- Sept. 1999 (never released)
-- Skipping frames during acquisition now works properly
-- Removed some unused sub-vis from library
-- Much better refresh rate in live video vi

#####Version 10 -- Sept. 1999
-- Redesigned acquisition to start and stop a small ring acquisition as needed.  
-- Annoying waits to reset acquisition are gone. Initialization is much faster.
-- You no longer need to specify "frame averaging" or "continuous" at time of initialization.
-- The program has greatly reduced overhead for frame averaging, meaning that less data is lost.  The main reason for this is that you know have the option of not displaying frames as they are acquired, which can save considerable time.  Overhead is particularly low (almost zero) on JG_Z, which has a faster processor that JG_I.
-- If you run out of memory, program should tell you ("buffer overrun") instead of crashing.  If you have an overrun close Glimpse to free up memory, then set it to acquire fewer frames. You can check memory available while the program is running:  Run Task Manager (CTL-ALT-DEL, then T) and look at Available Physical Memory under the Performance tab. If it gets <~7000 K, you are running out.  Don't run other programs while doing acquisition.
-- Removed bug in set gain and offset.  Note that you can use the digital control to set offset > 10 if desired.
-- Changed shortcut keys in player.
-- Known bugs: sometimes you have to click the "stop" button several times to stop acquiring averaged frames.

#####Version 9 -- Sept. 1999
-- Set up to test splitting IMAQ start and stop routines.  This didn't work for stopping and restarting acquisition.  Never released.

#####Version 8a -- Sept. 1999
-- Updated to work with LV 5.1 and NI-IMAQ 2.2.  Required changing all IMAQ refnos to new format.

#####Version 7 and 8
-- porting intermediates; never functional

#####Version 6
-- Background subtract
-- Slight mod of get env. variable; seems to work better

#####Version 5 -- May 1999
- Incorporated JYs correted code for writing sequence files.  Previous versions occasionally corrupted the last pixel on a line due to a problem with the implementation of the compression algorithm.
- Read Seq added.  Known limitations: 1) uses memory in a very inefficient manner.  may run out of ram or run very slowly when large sequences are read.  2) does not read the time table, so if you resave a sequence loaded from the disk, the time information will be lost.  3) On one occasion, I had a seq file which simply could not be read in.  Let me know if this happens to you.

#####Version 4 -- May 1999 (Never Released)
- Add save sequence of tiff files (Wei)
- Modify save img (JG)
	=make more self-explanatory
	=close window if save is cancelled by user.
	=make frame number selection work properly.
- Add histogram to live video (JG)
- Added print image button in player
- Changed tool palette in aoi player and live video so that the cursor can be used to investigate pixel intensities.

