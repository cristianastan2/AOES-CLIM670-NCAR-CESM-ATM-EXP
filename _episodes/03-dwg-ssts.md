---
title: "Drought Working Group SSTs"
teaching: 0
exercises: 0 
questions:
- "Setting up the SSTs"
objectives:
keypoints:
---

### The SSTs

The SSTs for each experiment are located on COLA in:
`/glade/scratch/cstan/droughtwg/`

The SST anomalies for the Pacific are located in: `Pacific_SST.nc`

The SST anomalies for the Atlantic are located in: `N_atl_SST.nc`

The climatological SSTs are located in: `monthly_climatology_sst_ice.nc`

Let's read in and make a plot of these data.  Launch Jupyter (or your preferred Python environment):

An example notebook is located here in: `~cstan/clim670/droughtwg/droughwgexps.ipynb'. You should copy it to your home directory or any special subdirectory you use for saving class related files:
~~~
$ cd
$ cp ~cstan/clim670/droughtwg/droughwgexps.ipynb .
~~~
{: .language-bash}

To launch the Jupyter notebook on the NCAR computers

1. Log in to the Production [NCAR JupyterHub](https://jupyterhub.hpc.ucar.edu)
2. Start a [server](https://arc.ucar.edu/knowledge_base/70549913)

This is the NCAR data analysis cluster.  We use the cheyenne supercomputer to run the model.  We use the casper analysis cluster to do data analysis on model output or to do data analysis to prepare data for our model experiments.  

You can now open the Jupyter notebook using the file browser in Jupyter. Slect NPL2023a as kernel.

We will walk through this notebook to look at our data and then to prepare them for use in the CESM.

1. Look at our Drought WG Data
2. Look at the CESM SST Data
3. Make our Drought WG Data look like CESM SST Data
* Full SST fields (anomalies + climatology)
* Same grid
* Same times
* No missing values
* Same units
4. Make a new SST file for CESM to use


3. Replace the right variable with our new SST data.

We can use `ncview` to take a quick look at our data file and confirm that it looks reasonable.

~~~
$ module load ncview
$ ncview /glade/scratch/cstan/input/dwg_pacpos.nc
~~~
{: .language-bash}






