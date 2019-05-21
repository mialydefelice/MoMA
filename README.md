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
## Wiki
Find more information [here](https://github.com/fjug/MoMA/wiki).
