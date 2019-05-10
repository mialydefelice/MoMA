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


## Installation for use with command line

1. Download Gurobi binary in [Gurobi Download Center](http://www.gurobi.com/downloads/download-center) 
* Get the right license for you from [Gurobi](http://www.gurobi.com)
* Add the following to your .bashrc file so the path to your gurobi version is set, and the license is accessible.
`export GUROBI_HOME="/opt/gurobi{version}/mac64"
export PATH="${PATH}:${GUROBI_HOME}/bin"
export LD_LIBRARY_PATH="${LD_LIBRARY_PATH}:${GUROBI_HOME}/lib"
export GRB_LICENSE_FILE=/your/path/to/your/gurobi/license/gurobi.lic`

3. Install & run MoMA
## Wiki
Find more information [here](https://github.com/fjug/MoMA/wiki).
