---
title: "Run the model with DWG SSTs"
teaching: 0
exercises: 0 
questions:
- "How do I run the model wih these SSTs?"
objectives:
keypoints:
---

###  Model Configuration

We now need to change the model configuration to run with our new file. We will change some things and confirm a few other configuration parameters
~~~
$ ./xmlchange SSTICE_DATA_FILENAME=/glade/scratch/cstan/input/dwg_pacpos.nc
~~~
{: .language-bash}

Check these other variables and confirm we know what they do and how they should be set.
~~~
$ ./xmlquery SSTICE_YEAR_START
$ ./xmlquery SSTICE_YEAR_END
$ ./xmlquery SSTICE_YEAR_ALIGN
~~~
{: .language-bash}

We will run 1-month as a test.
~~~
$ ./xmlchange STOP_N=1
$ ./xmlchange STOP_OPTION=nmonths
$ ./case.submit
~~~
{: .language-bash}

> ## Do the SSTs ouput by the model look like your SSTs?  
>
> Once your test run is able to run successfully, you will want to cofirm that it is working as expected. 
>
> Since yours will have to wait in the queue, we can look at my data to confirm that it ran properly. 
> There is no ocean model output since the ocean is not run. 
>
> My data are located in: '/glade/scratch/cstan/archive/testatmF/atm/hist/`
>
> The variable `TS` in the atm history files is SST over the ocean.
>  How can you convince youself that the data is consistent enough to believe that the SST data provided
>  is being used by the model?
>
> A sample program to get you started is located in: `~cstan/clim670/CheckSSTData.ipynb`
>
{: .challenge}


Once we have convinced ourselves that this works properly, how would we continue the run for a full year so we can test that?

Once a full year works and we have tested it properly, how would we run for 10-years?
