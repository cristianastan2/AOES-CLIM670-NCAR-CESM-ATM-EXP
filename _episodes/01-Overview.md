---
title: "Experiment with the Atmosphere"
questions:
- "How do I setup and run an experiment with prescribed ocean forcing?"
- "How is the ocean forcing defined?"
objectives:
keypoints:
- ""
---

In this lesson, we will learn about setting up experiments using the atmosphere with the ocean in data mode with prescribed SST forcing.  

We will start with a basic case of running an atmosphere-forced experiment.  We will then consider a specific scientific question and setup experiments using the atmosphere-forced experiment to answer this question, following the *Drought Working Group Experiments*.  

### Running the Atmosphere

Anytime we want to setup a new expeiment, we will create a newcase using the `create_newcase` script.  The script requires us to provide several things when we run it.  Let's figure out the correct options for setting up a case with the atmosphere in forced mode.

`--case ~/case/casename`
We can name our case whatever we want

`--res f19_g17` 
We are using this resolution, but we will need to check if it is available for what we want to do

`--compset COMPSET`
We will need to determine the right compset for this experiment.

`--project UGMU0032`
This is our project code.  It does not change.

### What `compset` do we use?

There are two ways to determine which compset to use.  
1. There is a tool:

~~~
$ CIMEROOT/scripts/query_config --compsets
~~~
{: .language-bash}

We can see from this that the compsets with `cam`, the atmosphere model, active all start with `F`, but it gives us the complicated long name and doesn't provide us with all the information we need.  Let's take a look at the [ website](http://www.cesm.ucar.edu/models/cesm2/config/compsets.html) for more information. 

Notice that the website indicates which version of CESM you are using in the upper right corner.  Our version is `CESM 2.1.1`.  Let's scroll until we find the `F` compsets. 

There are several options here, but the most basic option is `FHIST`.  This is an atmosphere forced run with prescribed ocean and ice using historical GHG forcing.

Remember that the compset determines which grids are `scientifically validated`, meaning which ones have been tested. 

> ### Is our resolution grid `scientifically validated` for any of the `F` compsets?
>
> Take a look at the webpage and view the scientifically validated grid for 
> the F-composets. See if our grid is listed.
>
>
{: .challenge}  

> ### Create your case
>
> Create a new case using the `FHIST` compset with our grid and project code
> Call the case whatever you wish.
>
> ~~~
> $ ./create_newcase --case ~/cases/testatmF --res f19_g17 --compset FHIST --project UGMU0032
> ~~~
> {: .language-bash}
> 
> 
> You will get an error.  Read the error.  
>
> What does it mean? 
> What do you need to do to setup your case with this compset and grid resolution?
>
>> ### Solution
>>
>> `create_newcase` is letting us know that our grid is not scientifically validated for this
>> compset.  It tells us we can use the `--run_unsupported` option to use this grid and compset 
>> anyway.
>>
>> ~~~
>> $ ./create_newcase --case ~/cases/testatmF --res f19_g17 --compset FHIST --project UGMU0032 --run-unsupported
>> ~~~
>> {: .language-bash}
>>
> {: .solution}
>
>
> Complete the setup, build the case and run it for 1-month as a test
>
>> # Solution 
>> 
>> ~~~
>> $ ./case.setup
>> $ qcmd -- case.build
>> $ ./xmlchange STOP_OPTION=nmonths
>> $ ./xmlchange STOP_N=1
>> ~~~
>> {: .language-bash}
>>
>
{: .challenge}  

### How is the ocean prescribed in this run?

The file specifying the SST and Ice data is located in `SSTCE_DATA_FILENAME`. We can use `xmlquery` to see what this is set to.

~~~
$ ./xmlquery SSTICE_DATA_FILENAME
~~~
{: .language-bash}

~~~
	SSTICE_DATA_FILENAME: /glade/p/cesmdata/cseg/inputdata/atm/cam/sst/sst_HadOIBl_bc_1x1_1850_2017_c180507.nc
~~~
{: .output}

Let's look at the description of this variable in `env_run.xml`:
`SSTICE_DATA_FILENAME`
: Prescribed SST and ice coverage data file name.
    Sets SST and ice coverage data file name.
    This is only used when DOCN_MODE=prescribed.

Based on the filename, this appears to be SST and Ice data on a 1x1 degree grid from 1850-2017. We can do `ncdump -h` on the file to get more information.
~~~
$ ncdump -h /glade/p/cesmdata/cseg/inputdata/atm/cam/sst/sst_HadOIBl_bc_1x1_1850_2017_c180507.nc
~~~
{: .language-bash}

The data contains several variables:  `ice_cov`, `SST_cpl`, etc.
The global attributes tell us how this data was made and even give us a reference for it.  We can look this up in more detail if we want.  For now, let's take a look at the data using `ncview`.

~~~
$ module load ncview
$ ncview /glade/p/cesmdata/cseg/inputdata/atm/cam/sst/sst_HadOIBl_bc_1x1_1850_2017_c180507.nc
~~~
{: .language-bash}

We now know how to create a case with ocean prescribed.

We know how to set the file that prescribes the ocean.

We have an example file that prescribes the ocean.

{% include links.md %}

