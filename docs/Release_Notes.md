GFS V16.3.21 RELEASE NOTES

-------
PRELUDE
-------
Update GCIP script and parm file for NESDIS GMGSI product updates:
* Update GCIP script to work with the new filenames of Global Mosaic of Geostationary Satellite Imagery (GMGSI) products.
* Update GCIP parm file because one sensor number is new to the current GCIP configuration, and the locations of multiple senors are changed.

IMPLEMENTATION INSTRUCTIONS
---------------------------

The NOAA VLab and the NOAA-EMC and NCAR organization spaces on GitHub are used to manage the GFS code.  The SPA(s) handling the GFS implementation need to have permissions to clone VLab Gerrit repositories and the private NCAR UPP_GTG repository.  All NOAA-EMC organization repositories are publicly readable and do not require access permissions.  Please proceed with the following steps to install the package on WCOSS2:

```bash
cd $PACKAGEROOT
mkdir gfs.v16.3.21
cd gfs.v16.3.21
git clone -b EMC-v16.3.21 https://github.com/NOAA-EMC/global-workflow.git .
cd sorc
./checkout.sh -o
```

The checkout script extracts the following GFS components:

| Component | Tag         | POC               |
| --------- | ----------- | ----------------- |
| MODEL     | GFS.v16.3.1   | Jun.Wang@noaa.gov |
| GLDAS     | gldas_gfsv16_release.v.2.1.0 | Helin.Wei@noaa.gov |
| GSI       | gfsda.v16.3.20 | Andrew.Collard@noaa.gov |
| UFS_UTILS | ops-gfsv16.3.20 | George.Gayno@noaa.gov |
| POST      | upp_v8.3.0 | Wen.Meng@noaa.gov |
| WAFS      | gfs_wafs.v6.3.4 | Yali.Mao@noaa.gov |

To build all the GFS components, execute:
```bash
./build_all.sh
```
The `build_all.sh` script compiles all GFS components. Runtime output from the build for each package is written to log files in directory logs. To build an individual program, for instance, gsi, use `build_gsi.sh`.

Next, link the executables, fix files, parm files, etc in their final respective locations by executing:
```bash
./link_fv3gfs.sh nco wcoss2
```

Lastly, link the ecf scripts by moving back up to the ecf folder and executing:
```bash
cd ../ecf
./setup_ecf_links.sh
```
VERSION FILE CHANGES
--------------------

* `versions/run.ver` - change `version=v16.3.21`, `gfs_ver=v16.3.21`

SORC CHANGES
------------

* New UFS_UTILS tag - `emcsfc_snow2mdl` program and associated scripts are updated to process global AFWA snow data
* New GSI tag - `src/gsi/read_prepbufr.f90` code update for new saildrone subtype

JOBS CHANGES
------------

* `jobs/JGLOBAL_ATMOS_EMCSFC_SFC_PREP` - new AFWA filename

PARM/CONFIG CHANGES
-------------------

* No changes from GFS v16.3.20

SCRIPT CHANGES
--------------

* No changes from GFS v16.3.20

FIX CHANGES
-----------

* GSI `global_convinfo.txt` fix update for saildrone

MODULE CHANGES
--------------

* No changes from GFS v16.3.20

CHANGES TO FILE AND FILE SIZES
------------------------------

No longer ingest:
* `${RUN}.${cycle}.NPR.SNWN.SP.S1200.MESH16.grb` (`AFWA_NH_FILE`)
* `${RUN}.${cycle}.NPR.SNWS.SP.S1200.MESH16.grb` (`AFWA_SH_FILE`)

Now ingest:
* `${RUN}.${cycle}.snow.usaf.grib2` (`AFWA_GLOBAL_FILE`)

ENVIRONMENT AND RESOURCE CHANGES
--------------------------------

* No changes from GFS v16.3.20

PRE-IMPLEMENTATION TESTING REQUIREMENTS
---------------------------------------

* Which production jobs should be tested as part of this implementation?
  * WAFS gcip job
* Does this change require a 30-day evaluation?
  * No

DISSEMINATION INFORMATION
-------------------------

* No changes from GFS v16.3.20

HPSS ARCHIVE
------------

* No changes from GFS v16.3.20

JOB DEPENDENCIES AND FLOW DIAGRAM
---------------------------------

* No changes from GFS v16.3.20

DOCUMENTATION
-------------

* No changes from GFS v16.3.20

PREPARED BY
-----------
Kate.Friedman@noaa.gov
George.Gayno@noaa.gov
Andrew.Collard@noaa.gov
