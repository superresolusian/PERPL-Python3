# PERPL (Pattern Extraction from Relative Positions of Localisations) 

This project provides functions for finding relative positions between points in 3D space and plotting as distance histograms for single molecule localisation data e.g. direct stochastic optical reconstruction microscopy (dSTORM) or photoactivated light microscopy (PALM). It also provides functions for fitting in silico model relative position distributions to those obtained from experimental localisations and allows the user to select the most likely structural model to describe the experimental data.

The software uses a file containing localisation data, analyses the distribution of relative positions between them within a certain maximum distance ('filter distance') and outputs and saves these relative positions. The filter distance is applied in 3D (or in 2D, as required). The software compares these outputs to relative position distributions obtained from synthetic localisation data models based on hypotheses of structural features. It outputs model fits and relative likelihoods for these models.

This algorithm was developed by **Alistair Curd** of the University of Leeds on 30 July 2018.

Copyright 2018 Peckham Lab

It was ported from Python 2 to Python 3 and made more user friendly by **Joanna Leng** at the University of Leeds who is funded by EPSRC as a Research Software Engineering Fellow (EP/R025819/1).

**History before 2022-12-20:** On 2022-12-20 this project was migrated from Bitbucket ([https://bitbucket.org/apcurd/perpl-python3/](https://bitbucket.org/apcurd/perpl-python3/)). We were unable to port the whole history because it included files that were too large for Github. The current repository ([https://github.com/AlistairCurd/PERPL-Python3](https://github.com/AlistairCurd/PERPL-Python3)) holds development of the master branch from that point.

Licensed under the Apache License, Version 2.0 (the "License"); you may not use this file except in compliance with the License. You may obtain a copy of the License at http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software distributed under the License is distributed on an "AS IS" BASIS, WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied. See the License for the specific language governing permissions and limitations under the License.


## DEVELOPED WITH: 
The latest version was developed using Python 3.11.4 and Anaconda, Inc. on a Windows 10 system. Previous version hav also been developed on a Centos system and exectuted a limited number of times on an Apple Mac.


## QUICK START: 
Immediately below are a set of instructions that allow you to execute the PERPL analysis software quickly. There are no explanations of the steps here. Please look at the rest of the README file if you have any problems.

This software uses Anaconda with Python 3 so you will need to install and open an Anaconda shell. Installing the Miniconda version of Anaconda will be quicker and use less storage on your machine. Once the shell is open, type the following the FIRST time you run the PERPL software (it is not required for later runs):

`conda env create -f environment.yml`

Next, activate the PERPL Anaconda environment using the following command:

`conda activate PERPL`

Execute the *relative_positions.py* Python script that analyses suitably processed experimental data. This should be localisation data that has been processed into *X* and *Y* (2D) or *X*, *Y* and *Z* (3D) coordinates stored in a text or .csv file. You will be asked to provide input, such as the input data filename, to the script as it executes. Example data files can be found as described in the **DATA** section. A relatively small data file useful for testing the software is *Nup107_3D_10000_from_36297_locs.csv*, choose 3D analysis and a filter distance of 200nm. We plan to upload the data to Zenodo and include instructions here on how to access them.

`python relative_positions.py`

Execute the *rot_2d_symm_fit.py* Python script. This will read in output data from the *relative_positions.py* script and compare it to a model of localisations with 2D rotational symmetry. Again you will be asked to provide input, which should be a list of relative positions, not a list of localisations. A good test file for this script is *Nup107_SNAP_3D_GRROUPED_10nmZprec_PERPL-relpos_200.0filter.csv*, which itself was generated by running *relative_positions.py* on *Nup107_SNAP_3D_GRROUPED_10nmZprec.txt*.

`python rot_2d_symm_fit.py`

**NB** These scripts use meaningful filenames and directories to store the results. This sometimes creats long paths which Windows in particular finds difficult to handle. If this happens use the *-s* flag at the ends of these commands to switch to a shorter naming convention.


## ENVIRONMENT:
Install Anaconda or Miniconda from anaconda.org. Use the Anaconda/Miniconda Windows Prompt or Terminal/command line.

The conda environment, with all the necessary modules, can be set up using the *environment.yml* file. 

To see what conda environments you have, run the command

`conda env list`

To create a new Anaconda environment for PERPL, run the command

`conda env create -f environment.yml`

To start using the environment, run the command

`conda activate PERPL`

To stop using that enviroment:

`conda deactivate`

To remove the environment, if you no longer want to use PERPL:

`conda remove --name PERPL --all` 


## USAGE:
There are two **Python scripts** that can be executed from the command line from a shell with Python 3 available, these are *relative_positions.py* and *rot_2d_symm_fit.py*.

Each of these can be run from the command line in two ways:

1. They can be executed and all the necessary parameters for the code to execute successfully can be provided as flags/arguments at the command line. 
2. They can be executed from the command line where no flags/arguments are provided. In this case the user is asked to provide the necessary information as the script executes via a file browser for the input file and via the command line for all other information.

In both these cases the user can choose to execute the code in verbose mode and monitor its progress via output printed to the command line (standard output).

Each time these scripts run, a HTML report is created in the directory where the input data is stored. The paths and filenames provide information on when the script executed and the parameters selected, as well as being documented in the report. The image files used in the report are saved to the directory with the report. You can view the report in a web browser on the machine where it was created by double clicking on the HTML file in the directory. If you wish to share the file, you can print it (or save it as a pdf if correctly configured) via your web browser. If you wish to share the HTML report as HTML, remember to share the image files with the HTML file.

There are also **Jupyter notebooks** for fitting models to the data and producing plots and numerical results. These may be run interactively, and modified, e.g. for path to the input data and choice of model to fit to the input data. These may be found and run in a web browser by typing `jupyter notebook` in the command prompt.

### relative_positions.py

To execute interactively, provide no flags (arguments) and type:

`python relative_positions.py`

To execute silently with default values, all you need is to include a data file; type:

`python relative_positions.py  -i data_file.csv`

To execute silently with your own values you also need to include a data file; type for example:

`python relative_positions.py  -i data_file.csv -d 2 -f 200 -z 12 -s`

To get information on the flags and usage, type:

`python relative_positions.py  -h`

This script can take several minutes to run, depending on the size (number of localisations) and density of the input data.

### rot_2d_symm_fit.py
This script is executed to compare a model with rotational 2D symmetry with experimental fluorescence localisation microscopy data. The script reads in output data generated by relative_positions.py and compares it to a model that it generates.

To execute interactively, provide no flags (arguments) and type:

`python rot_2d_symm_fit.py`

To execute silently with default values, all you need is to include a data file; type:

`python rot_2d_symm_fit.py  -i data_file_output_from_relative_positions.csv`

To execute silently with your own values, you need to include a data file and filter distance (the filter distance only has an effect if it is less than that used in generating the input data when executing relative_positions.py); type for example:

`python rot_2d_symm_fit.py  -i data_file_output_from_relative_positions.csv -f 100`

To get information on the flags and usage, type:

`python rot_2d_symm_fit.py  -h`

Examples of usage are in the bash script *command_line_demo.sh*. This is a Linux script and will not run on Windows in an Anaconda shell. If you transfer this script to a Linux system you may need to run the `dos2unix` command on it to make it work, as well as `chmod u+x command_line_demo.sh`. If you create the **data-perpl** directory as described in the **DATA** section then the script should pick up the data without you having to change the path in the script.


### Jupyter notebooks (.ipynb)

To start the Jupyter notebook environment, go to an Anaconda shell that is running the PERPL environment and type:

`jupyter notebook`

Select **Python 3** for the **kernel**, if necessary. 

The notebook environment will open in your web browser. Select a notebook (*.ipynb* file). Use the control panel at the top of the notebook page to run each block of code or the entire notebook. The individual blocks of code are in a box that is called a cell. When a cell has completed its execution, the tag by it goes from **In []:** to for example **In [10]:** for the 10th cell in the notebook. While the cell is executing, it will read as **In [\*]:**, so if the computation takes some time you must wait until this changes before running the next cell. This panel allows you to add, document and interact with the code in the notebook in a variety of ways.

**NB** Each notebook requires you to load data into it (see **DATA** section).


## DOXYGEN DOCUMENTATION
Doxygen documentation for this project can be created. Python doxygen is part of the PERPL environment so you do not need to install doxygen.

Run the command in the top directory of the source code:

`doxygen`

After this has run a doc/html directory will appear. Open the index.html file in this directory.

The doxygen documentation for this project lists gives the API (Application Programmers Interface) for all the modules and scripts in this project making it useful to developers who wish to further develop this software.

## DATA

Test data for this software, or examples with which the software can be used, can be found at [https://bitbucket.org/apcurd/perpl_test_data](https://bitbucket.org/apcurd/perpl_test_data).
These files are:

* *ACTN2-Affimer_PERPL-relpos_200.0filter_len2440488.pkl*
* *ACTN2-Affimer_locs_maxprec5.pkl*
* *ACTN2-mEos2_PERPL-relpos_200.0filter_6FOVs_aligned_len1229656.pkl*
* *DNA-origami_DNA-PAINT_locs_xyz.csv*
* *DNA-origami_DNA-PAINT_locs_xyz_PERPL-relpos_250.0filter.csv*
* *Nup107_3D_10000_from_36297_locs.csv* **(useful for quick first test of *relative_positions.py*)**
* *Nup107_SNAP_3D_GRROUPED.txt*
* *Nup107_SNAP_3D_GRROUPED_10nmZprec.txt*
* *Nup107_SNAP_3D_GRROUPED_10nmZprec_PERPL-relpos_200.0filter.csv* **(useful for test of *rot_2d_sym_fit.py*)**
    * This file was itself generated by running *relative_positions.py* on *Nup107_SNAP_3D_GRROUPED_10nmZprec.txt* with a 200-nm filter distance.
* *mEos3-LASP2_PERPL-relpos_200.0filter_5FOVs_aligned_len533140.pkl*
* *mEos3-MYPN_NNS_aligned_5_FOVs_len1445698.pkl*

The shell script *command_line_demo.sh* and the Jupyter notebooks will find these files and load the required data from relative paths. This will work if the data is placed in a directory called *data-perpl*, which is within the same parent directory (*perpl-home*, or a name of your choice) as the PERPL software directory (*perpl-python3*). A schematic of this directory structure is given below. 

- *perpl-home*
	* *data-perpl*
    * *perpl-python3*

You can also download the data into any directory on your system and edit the file name and path in the relevant script/notebook, if you prefer.

## FILES INCLUDED: 

* *README.md*: This file, which contains information about the software in this project.
* *command_line_demo.sh*: A bash script that executes the Python scripts relative_positions.py and rot_2d_symm_fit.py with various command line options.
* *Doxyfile*: Configuration file for the automated documentation system doxygen.
* *environment_perpl.yaml*: Anaconda configuration file that creates the environment used to develop this software.
* *license.md*: Software licensing file.
* *.gitignore*: Hidden configuration file for git, a distributed version-control system.
* *.gitattributes*: Hidden configuration file for git, a distributed version-control system.

### Python Code

* *relative_positions.py*:  A Python script that calculates the relative positions between points detected during fluorescence localisation microscopy.
* *rot_2d_symm_fit.py*:     A Python script that fits rotational symmetry models to relative positions among localisation microscopy data. The models are generated from synthetic localisation data.
* *background_models.py*:   A Python module that creates models of relative position data resulting from background in fluorescence localisation microscopy data.
* *centriole_analysis.py*: A Python module that fits centriole model data to relative positions among localisation microscopy data. The models are generated from synthetic localisation data.
* *dna_paint_data_fitting.py*: A Python module that fits model data to relative positions among localisation microscopy data from DNA-PAINT imaging of a DNA-origami structure. The models are generated from synthetic localisation data, e.g. in *polyhedramodelling.py*.
* *linearrepeatmodels.py*: A Python module containing candidate models for relative position distributions in a 1D arrangement of localisations of a target molecule.
* *modelling_general.py*: A Python module with functions generally useful for analysing relative positions, and generating and fitting models of fluorescence localisation microscopy data.
* *modelstats.py*: A Python module with statistical functions useful for analysing models against experimental data.
* *plotting.py*: A Python module with functions to create plots of data and analysis results.
* *polyhedramodelling.py* A Python module containing candidate models for relative position distributions in simple polyhedral arrangements of localisations of a target protein.
* *reports.py*: A Python module with functions to produce html reports for the python scripts relative_positions.py and rot_2d_symm_fit.py.
* *two_layer_fitting.py*: A Python module which fits a two-layer model of locallisation distribution to experimental data.
* *utils.py*: A Python module with useful functions.
* *zdisk_modelling.py*: A Python module which fits models of relative positions in Z-disc data to relative positions among localisation microscopy data.
* *zdisk_plots.py* A Python module containing function for plotting relative position data and fitted models for Z-disc protein localisation data.

* *test_relative_positions.py*: test file for the relative_positions.py module.
* *test_linearrepeatmodels.py*: test file for the linearrepeatmodels.py module.

### Jupyter notebooks

* *make_ACTN2_Affimer_PERPL_plots.ipynb*: A Jupyter notebook for generating plots and model fits to Z-disc protein relative position data.
* *make_ACTN2_Affimer_reconstructions.ipynb*: A Jupyter notebook for generating XY projections of the distribution of single molecule localisations in a FOV.
* *make_ACTN2_mEos_PERPL_plots.ipynb*: A Jupyter notebook for generating plots and model fits to Z-disc protein relative position data.
* *make_DNA_origami_PERPL_plots.ipynb*: A Jupyter notebook for generating plots and model fits to relative position data among DNA-origami localisation data.
* *make_Nup107_reconstructions.ipynb*: A Jupyter notebook for generating XY projections of the distribution of single molecule localisations in a FOV.
* *make_Nup107_Z_PERPL_plots.ipynb*: A Jupyter notebook for generating plots and model fits to relative position data among nuclear pore protein localisation data (along the Z-axis).
* *make_mEos_LASP2_PERPL_plots.ipynb*: A Jupyter notebook for generating plots and model fits to Z-disc protein relative position data.

### Unittests

There are unit tests in the tests directory. These will be of interest to a software engineer who wishes to extend this project. They can be run from a Python 3 shell with the command.

`python -m unittest discover -s tests`


