These are some suggested steps to take to get your microscope setup working with Glimpse and the microscope plug-ins.  This is going to entail making a modified version of the software for your microscope. 

* The development of Glimpse was supported in part by US government grants.  To make certain that taxpayers get the most science for the money that they spent, the software is licensed under the [GPL version 3](http://www.gnu.org/licenses/gpl.txt), which allows you to modify and redistribute the software for free subject to certain conditions.  [Please familiarize yourself](http://www.gnu.org/licenses/quick-guide-gplv3.html) with your obligations under the GPL if you modify or redistribute Glimpse.

* Start by installing the [required software](https://github.com/gelles-brandeis/Glimpse/wiki/Glimpse-core#software-requirements) from NI, and Matlab.

* Create an account on Github.  Install Github for Windows.

* [Clone the Glimpse repository](github-windows://openRepo/https://github.com/gelles-brandeis/Glimpse).  This makes a local copy for you to work with.

* Make your own *separate* Github repository to hold versions of any of the Glimpse files that you modify and any new files that you create.  You should include only modified/new files here, not unmodified copies of files from the Glimpse repository (this will help minimize the work if you ever want to update your configuration with VIs from a newer version of Glimpse).

* In your repository, create a project file for your microscope (your can start by making a modified version of `microscope plugins\h-nu-ixon1024 microscope software.lvproj`) and a subdirectory with microscope-specific VIs (for example, make modified versions of the ones in `h-nu-ixon`. 

* The project file will point to files in both repositories.  In some cases, a file with the same name will appear in both places.  Use the LabView Project Explorer conflict resolution feature to insure that the right version of any conflicting files is loaded.

* Use `Start!.vi` to run the software.  Debug and modify as needed, always saving changed files in your own local repository.

* Once the software works, use the build feature of the project to produce an LLB with the production version of the software.  Place into a subdirectory under Program Files (x86).  Make this read-only so that non-administrator users don't inadvertently modify it.

* Share your work with other labs by committing the changes in your repository and syncing to Github.  Before you do this add an appropriate copyright/license text to the block diagram of each original VI you created.   For modified versions of Glimpse VIs, simply add your copyright text to the notice that is already there. See See http://www.gnu.org/licenses/gpl-howto.html  

* If you let me know about your repository I will post a link on this wiki page to bring it to the attention of other labs who might want to make use of your work. 