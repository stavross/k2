The microscope plug-ins consist of LabView VIs and controls that are part of the Glimpse software and run alongside the Glimpse core.  The plugins are used in controlling a microscope setup (cameras, shutters, filterwheels,...) and acquiring and saving images.

### Hardware and supporting software
The microscope plugin require the commercial software packages listed on the [Glimpse core](https://github.com/gelles-brandeis/Glimpse/wiki/Glimpse-core) page.  We currently run 64-bit Windows7 machines for our microscopes, but use the *32-bit* version of LabView to avoid potential driver problems.  I'm not certain this precaution is necessary.

Other software (e.g., drivers and the hardware manufacturer's LabView support library) may be required to use the plug-in with particular microscope hardware.  Below is information about different hardware setups we have used with microscope plugins and some pointers on getting it working with the software.

###Some notes on specific hardware

####Camera -- Andor iXon (PCI)

#####Additional software required 
Andor SDK Software Development Kit (Must be installed in c:\program files\andor ixon?).  Program must be able to access atm32cd.dll, so this should be placed in the C:\Program Files (x86)\National Instruments\LabVIEW xxxxx directory.

#####Configuration of software
Include `ixon camera` and either `ixon512` or `ixon1024` directories in project. There are also some microscope-specific VIs needed.  See `h-nu ixon` directory for examples.

#####Cable

Mfr. Supplied.

####Camera – Hamamatsu Orca CMOS

Tested with model number C11440-22CU.
#####Additional software required 
Hamamatsu Video Capture Library for LabView (should get installed in Labview user.lib).
#####Configuration of software

Include `orca camera` directory and appropriate microscope directory (e.g., `hnu-orca`) in project. 

#####Cable
Mfr. Supplied.

####Filter wheel - Sutter Instruments Lambda 10-3 (RS-232)

#####Additional software required

* Su10x.llb from NI instrument driver library.  Install in instr.lib directory (use Tools>Instruemntation>Find Instrument Drivers from within labview)

* NI-VISA

#####Configuration of software

* Use NI-MAX to set the com port to 9600,N,1 and the COM port name to FILTERWHEEL

* Set the names of the different filters in emission filters.ctl (located in the directory for the particular microscope).

* Set delay time in `filter wheel settings globals.vi`

* Include `filter wheel` in project.

#####Cable

Mfr.-supplied DB-9/DB-9 cable.  

#####Notes

This device also has a USB interface, but I wasn’t able to figure out how to get it to work with Labview.  Instead we use the NI four serial ports <-> USB box.

####Knobs -- Griffin Powermate knobs (USB) DEFUNCT

Two knobs to control stage x-y-z

#####Additional software required 

NI-USB Powermate driver (This is a driver built by JG that has to be installed on the system before a Powermate is plugged in for the first time.  Do not install the Griffin-provided drivers.)

######Configuration of software
Use NI-MAX to associate the names “knob1” and “knob2” with the devices

#####Notes
Does not work in Win7 because of [this problem](http://digital.ni.com/public.nsf/allkb/E811055409D5B8778625782900701DFB?OpenDocument) or maybe it’s [this problem](http://forums.ni.com/t5/LabVIEW/Write-on-a-hid-with-labview-using-the-library-hid-dll/m-p/570119).  Frustratingly, [this approach](http://digital.ni.com/public.nsf/allkb/CA411647F224787B86256DD000669EFE) doesn’t work either because only the direction of rotation is accessible, not the amount rotated.  *Abandoned*.

####Knobs – Phidgets knob box (USB)
Three knobs to control stage x-y-z.  We used three [Phidgets 1052 encoder/pushbuttons](http://www.phidgets.com/products.php?category=7&product_id=1052) mounted in a project box with a mini USB hub.  Cheap and works like a charm.

#####Additional software required 
[Phidgets Windows driver and Phidgets Labview library](http://www.phidgets.com/docs/Language_-_LabVIEW) installed into the Labview user.lib directory (be sure to match the 32/64 bit version of the library with the 32/64 bit version of labview when a Win 64 OS is used).  The library directory should be named `<userlib>\Phidgets libarary`.

#####Configuration of software
* Include `phidgets knobs` in project.

*Set the serial numbers of the three knobs as default in `<microscope name>\knob globals.vi`.

####Shutter controller - NI-DIO-96 card (PCI)
On h-nu, the shutters are connected to a NI PCI-DIO-96 board which is also used to run the stage.  The actual shutter controllers are commercial Uniblitz boxes or home-built ones that take a TTL input from the DIO lines.

#####Additional software required
NI-DAQmx

#####Configuration of software
* Include `h-nu shutters` in project.

* Edit laser `type.ctt` to specify names of lasers. If you want to change the number of lasers, you also have to edit `shutters activate.vi`.

* Modfy `shutter port lookup.vi` to specify device name and port number of DIO card for each laser.

#####Cable
This table gives the h-nu wiring:
Breakout box output	Pin number on 2nd ribbon cable	Port number on PCI-DIO-96	Line number on PCI-DIO-96	Shutter controller	Shutter
1	23	7	4	--	Camera
2	24	10	4		Orange Laser (594 nm)
3	31	7	0		IR laser (785 nm)
4	32	10	0	4	blue laser (488 nm)
5	15	8	0	5	green (532 nm)
6	16	11	0	6	Red (633)
Shutter controller - NI USB6008 (USB)
On new-h-nu, the shutters are connected to an NI USB6008. The actual shutter controllers are home-built ones that take a TTL input from the DIO lines.
Additional software required
NI-DAQmx
Configuration of software
Edit laser type.ctt to specify names of lasers.  If you want to change the number of lasers, you also have to edit shutters activate.vi.
Modfy shutter port lookup.vi to specify device name and port number of DIO card for each laser.
Cable
Standard USB A/B
Quadrant photodiode – NI USB6008 (USB)
Additional software required
NI-DAQmx
Configuration of software
See front panel of qpd config globals.vi
Cable
Custom shielded cable – see diagram.
Notes
We used a Pacific Silicon Sensors QP50-6-18u-SD2 in a custom enclosure with a generic +/- 12V power supply.  On another microscope we used the ThorLabs PDQ80A by throwing away their USB interface (feh!) and connecting the sensor to the NI USB6000.  This approach is more expensive but comes in an enclosure. See additional documentation.
Quadrant photodiode – ThorLabs PDS80QS1 (USB)
Defunct – This setup used the ThorLabs-provided  USB interface.  It never worked very well, probably because I had to kludge a driver that would work with Labview because Thorlabs doesn’t provide a Labview driver. Grrr.
Additional software required 
Pds80qs1.dll (written by JG; must be in same directory as plug-in) and Thorlabs driver (install before plugging in detector).  As currently compiled, the dll requires that the MS visual C++ express compiler and the appropriate Windows SDK be installed on the target machine (i.e. the machine on which the dll is to be executed.  I’m assuming this requirement would go away if the dll were recompiled with the non-express version of the compiler, but I haven’t tried this.
Configuration of software
Cable
Notes
Piezo stage -- Mad City Labs, NI-DIO-96 (PCI)
Additional software required 
NI-DAQmx
Configuration of software
Edit device name/port number in Nano-drive set using NI.vi
Cable
Supplied by mfr.
Notes 
Piezo stage -- Mad City Labs Nanodrive (USB)
Additional software required 
Mad City Labs driver and DLLs Madlib.dll and wdapi1010.dll (installed in C:\Program Files (x86)\Gelles Lab Software)
Configuration of software
None.
Notes 

Valve – Hamilton MVP (RS-232)
Additional software required 
Configuration of software
Notes 
Cable and software protocol described in mfr’s manual.

Additional software required 
Configuration of software
Cable
Notes 


