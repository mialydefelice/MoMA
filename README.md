# MoMA
The **Mo**ther **M**achine **A**nalyzer.

## Abstract
The Mother Machine is a microfluidic device designed to study e.g. bacteria. 
It allows the observation of growth and division of the progeny of single “mother” cells over many generations using time lapse microscopy.
Individual cells need to be tracked over time. 
Tracking consist of two equally important tasks: 
*(i)* cells need to be segmented in each frame, and 
*(ii)* all segments of the same cell need to be linked between frames. 
Tracking large numbers of cells under different environmental conditions will allow biologists to better understand the stochastic 
dynamics of gene expression within living cells. 
Respective high throughput studies of cells in the Mother Machine would be greatly facilitated if the tracking task would be automated.

The tracking model we use is built on the basis of a large set of cell segmentation hypotheses for each video frame. 
Possible tracking *assignments* between segments across time, including cell identity mapping, cell division, and cell exit events 
are enumerated. Each such assignment is represented as a binary decision variable with unary costs based on image and object features 
of the involved segments. We find a cost-minimal and consistent solution (maximum a posteriori) by solving an integer linear program 
using [Gurobi](http://www.gurobi.com).

MoMA offers six innovative ways for semi-automatic curation of automatically found tracking solutions. 
We show how all proposed interactions can be elegantly incorporated into the assignment tracking model mentioned above.
After interactively pointing at a single mistake, multiple segmentation and tracking errors are fixed automatically in one single
reevaluation of the model.


## Application
To get started, read our
* [Installation guide](https://github.com/fjug/MoMA/wiki/Installation%20guide)
* [Quick user guide](https://github.com/fjug/MoMA/wiki/Quick%20user%20guide)

and download
* [Example datasets](https://github.com/fjug/MoMA/wiki/MoMA%20Datasets)
* [Tutorial movies](https://github.com/fjug/MoMA/wiki/MoMA%20Movies)


## Installation for use with command line on MacOSX

1. Download Gurobi binary in [Gurobi Download Center](http://www.gurobi.com/downloads/download-center) 
* Get the right license for you from [Gurobi](http://www.gurobi.com)
* Add the following to your .bashrc file so the path to your gurobi version is set, and the license is accessible.

`export GUROBI_HOME="/opt/gurobi{version}/mac64"`

`export PATH="${PATH}:${GUROBI_HOME}/bin"`

`export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${GUROBI_HOME}/lib"`

`export GRB_LICENSE_FILE=/your/path/to/your/gurobi/license/gurobi.lic`

* Run your .bashrc file by typing `source ~/.bashrc` in your command line.

2. [Download latest version of FIJI](http://fiji.sc).

* Create a link named `fiji`, pointing to the ImageJ executable (e.g. `ImageJ-macosx`)

3. Make sure you have Java8 installed. Don't check using system preferences rather in command line type:

`java -version`. 

If not download Java8, or OpenJDK.

* To download OpenJDK type the following into your command line: `brew cask install adoptopenjdk`.

* Else, visit [Oracle](https://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) to download Java8

4. Create a local file (`run_scripts_local`) to hold all necessary files to run scripts.

 * Since the .jar files (downloaded at a later step) are so large, they cannot be stored within the github repository. We will have to store all the files necessary to run this program in a different file.
 
 * Copy the contents of `run_scripts` into `run_scripts_local`.

5. Download necessary Jar files:

* From [http://sites.imagej.net/MoMA/plugins/](http://sites.imagej.net/MoMA/plugins/) download MMPreprocess_-1.2.jar-20170612121927 and MotherMachine_-0.10.9.jar-20170501231000

* IMPORTANT: Do not download the latest versions of these files, if you do it will throw an error when you try to run them.

* Add these files to `run_scripts_local`

6. If you are on MacOSX make sure you have XQuartz installed and that `Xvfb` is included in this download.
* I have included an updated version of `xvfb-run` that is compatible with mac, this file should already be within `run_scripts_local` named `xvfb-run_updated`. 
* If you are running Linux you may not be able to use this updated version. In this case the version you will need is already in the `run_scripts` folder, named `xvfb-run`

7. Make files executible,run the following from the `run_scripts_local folder`.

`chmod u+x moma_pre_cli`

8. Create symbolic links:

* Create link to Fiji:

`ln -s /path/to/ImageJ-macosx /path/to/run_scripts_local/fiji`

* Create link to `xvfb-run_updated` or `xvfb-run`.

Make sure to point to the normal or updated version depending on the system you are using.

`ln -s /path/to/run_scripts_local/xvfb-run_update.txt /path/to/run_scripts_local/xvfb-run`


## Installation for use with FIJI.

MoMA is available for download in two different ways:
* For **new users** it is **recommended** to try out the **Fiji plugins** which will guide you through the analysis process.
* Advanced users may want to try the command line tools to facilitate automated pre-processing of many data sets, e.g. by exploiting high performance computing capabilities. Advanced users may also profit from direct access to MoMAs [open source code](Developing-MoMA).

# Installation of Fiji and the MoMA plugin
The first step is to download and install Fiji from http://fiji.sc/Downloads.
Afterwards, run Fiji and click its _Help > Update..._ menu entry.

In the _ImageJ updater_ dialog that appears click on the _Manage Update Sites_ button:

<div align="center"><img src="https://github.com/fjug/MoMA/wiki/images/updatesites1.png" width="500"></div>

The _Manage update sites_ dialog will open. Click the _Add update site_ button and enter "MoMA" in the _name_ column on the left and "http://sites.imagej.net/MoMA/" in the _URL_ column on the right. Click the _Close_ button afterwards.

<div align="center"><img src="https://github.com/fjug/MoMA/wiki/images/updatesites2.png" width="500"></div>

Close the _ImageJ Updater_ window by clicking the _Apply changes_ button:

<div align="center"><img src="https://github.com/fjug/MoMA/wiki/images/updatesites4.png" width="500"></div>

After restarting Fiji, a menu entry _Plugins > MoMA_ should appear. If not, please [contact us](mailto:jug@mpi-cbg.de)!

## Running MoMA for the first time
Check the installation by clicking the menu _Plugins > MoMA > MoMA application_;

When you run MoMA for the first time, it will ask you to get a license for the [Gurobi Solver engine](http://www.gurobi.com/) it utilises for optimisation. Visit http://www.gurobi.com/downloads/licenses/license-center to acquire this license. Most academic users may want to click “Obtain a free university license”. Afterwards, copy and paste ```grbgetkey xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx``` in the **Getting Gurobi License File** dialog.
<div align="center"><img src="https://github.com/fjug/MoMA/wiki/images/Getting_Gurobi_License_File_and_Desktop2.png" width="400"></div>
After clicking ok, a console window may appear showing the installation progress. Finally, after installation succeeded, a window titled _MoMA configuration_ will appear. You may download an [example data set](MoMA-Datasets) and follow the instructions in our [Quick user guide](Quick-user-guide) to learn how MoMA can be used.

# Installation of command line tools for MoMA
The following procedures are not neccessary for running MoMA inside Fiji. These steps are only recommended to be performed by advanced users requiring command line functionality.

To run MoMAs command line tools, you need either Java 8 Development Kit or Runtime Environment installed on your computer. Download and install it from here:
* [Download Java 8 JDK](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html) (Development Kit)
* [Download Java 8 JRE](http://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html) (Runtime Environment)

* Download the most recent version of MotherMachine_.jar and MMPreprocess_.jar from here:
http://sites.imagej.net/MoMA/plugins/

Detailed information on how to apply the preprocessing steps from the command line can be found here:
* [Preprocessing From The Command Line](Preprocessing-From-The-Command-Line)


## Wiki
Find more information on how to run the pipline visit [here](https://github.com/fjug/MoMA/wiki).
