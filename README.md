# Downloading and Running Offline NUCAPS Data in SHARPpy
This tutorial explains how to run NUCAPS in SHARPpy in offline mode. The steps here outline how to generate NUCAPS text files from netCDF files that are stored locally.  Anaconda and SHARPpy are assumed to be already installed before trying the steps below.

## Downloading Data for Case Studies

1. Order the NUCAPS Environmental Data Records (EDR) data from [NOAA CLASS](class.noaa.gov), under the [JPSS Sounder Products (JPSS_SND)](https://www.avl.class.noaa.gov/saa/products/search?sub_id=0&datatype_family=JPSS_SND&submit.x=28&submit.y=11) dropdown menu. If you are unfamiliar with CLASS, refer to the [CLASS Tutorial document](https://weather.msfc.nasa.gov/nucaps/resources_training.html) on how to download data.

## Process NUCAPS Data Locally for Case Studies

### Creating SHARPpy-formatted text files from NUCAPS netCDF files

2. Download and save the [sharppy_offline_netcdf_converter.py](https://github.com/NUCAPS/SHARPpy) script to an easily accessible directory. This script will convert the netCDF files to a format that SHARPpy can read.  Switch to *base* Anaconda environment and install the xarray and netcdf4 Python libraries needed by the script.

```bash
conda activate base
conda install -c conda-forge xarray
conda install -c conda-forge netcdf4
```

3. Open *sharppy_offline_netcdf_converter.py* and locate the *satNames* list towards the bottom of the script.  Enter the 3-digit satellite identifier(s) into the list for the EDR files you will be processing.  Save and close the script.

4. After downloading the EDR files, move them to the same directory as *sharppy_offline_netcdf_converter.py*.

5. Run the *sharppy_offline_netcdf_converter.py* script to process all the netCDFs in the current directory. This creates the sounding text and location csv files. These files will be saved in */home/{user}/.sharppy/datasources*.

### Updating SHARPpy to point to the case study files

6. Change your directory to */home/{user}/SHARPpy/datasources* and open *case_study.xml*.  In *case_study.xml*, uncomment the datasource tag(s) you'll be using and change the url to point where the text files reside.

For NOAA-20, the code will look like:

```xml
<datasource name="NUCAPS Case Study NOAA-20" ensemble="false" observed="true">
    <outlet name="STC" url="file:///home/<user>/.sharppy/datasources/j01/{srcid}.txt" format="spc" >
        <time first="0" range="48" delta="1" offset="6" delay="4" cycle="12" archive="24" start="-" end="-"/>
        <points csv="j01_case_study.csv" />
    </outlet>
</datasource>
```

For Suomi-NPP data, the code will look like:

```xml
<datasource name="NUCAPS Case Study Suomi-NPP" ensemble="false" observed="true">
    <outlet name="STC" url="file:///home/<user>/.sharppy/datasources/npp/{srcid}.txt" format="spc" >
        <time first="0" range="48" delta="1" offset="6" delay="4" cycle="12" archive="24" start="-" end="-"/>
        <points csv="npp_case_study.csv" />
    </outlet>
</datasource>
```

For Aqua data, the code will look like:

```xml
<datasource name="NUCAPS Case Study Aqua" ensemble="false" observed="true">
    <outlet name="STC" url="file:///home/<user>/.sharppy/datasources/aq0/{srcid}.txt" format="spc" >
        <time first="0" range="48" delta="1" offset="6" delay="4" cycle="12" archive="24" start="-" end="-"/>
        <points csv="aq0_case_study.csv" />
    </outlet>
</datasource>
```

7. For the XML changes to take effect, you need to reinstall SHARPpy. Switch to the *devel* Anaconda environment and go to the folder that contains your SHARPpy install. For example, in the terminal, type:

```bash
conda activate devel
cd /home/<user>/SHARPpy
python setup.py install
```

8. Lastly, launch the SHARPpy GUI by typing *sharppy* into the terminal:

```bash
sharppy
```
