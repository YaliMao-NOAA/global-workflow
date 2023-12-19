GFS V16.3.12 RELEASE NOTES

-------
PRELUDE
-------

Enable the monitoring of NOAA-21 and GOES-18 radiances in the GFS. A new version of CRTM with new coefficient files is required and included in this change.

IMPLEMENTATION INSTRUCTIONS
---------------------------

The NOAA VLab and the NOAA-EMC and NCAR organization spaces on GitHub .com are used to manage the GFS code.  The SPA(s) handling the GFS implementation need to have permissions to clone VLab Gerrit repositories and private NCAR UPP_GTG repository. All NOAA-EMC organization repositories are publicly readable and do not require access permissions.  Please proceed with the following steps to install the package on WCOSS2:

```bash
cd $PACKAGEROOT
mkdir gfs.v16.3.12
cd gfs.v16.3.12
git clone -b EMC-v16.3.12 https://github.com/NOAA-EMC/global-workflow.git .
cd sorc
./checkout.sh -o
```

The checkout script extracts the following GFS components:

| Component | Tag         | POC               |
| --------- | ----------- | ----------------- |
| MODEL     | GFS.v16.3.1   | Jun.Wang@noaa.gov |
| GLDAS     | gldas_gfsv16_release.v.2.1.0 | Helin.Wei@noaa.gov |
| GSI       | gfsda.v16.3.12 | Andrew.Collard@noaa.gov |
| UFS_UTILS | ops-gfsv16.3.0 | George.Gayno@noaa.gov |
| POST      | upp_v8.3.0 | Wen.Meng@noaa.gov |
| WAFS      | gfs_wafs.v6.3.1 | Yali.Mao@noaa.gov |

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
* `versions/run.ver` - change `version=v16.3.12` and `gfs_ver=v16.3.12`

SORC CHANGES
------------

* No changes from GFS v16.3.11

JOBS CHANGES
------------

* No changes from GFS v16.3.11

PARM/CONFIG CHANGES
-------------------

* No changes from GFS v16.3.11

SCRIPT CHANGES
--------------

* No changes from GFS v16.3.11

FIX CHANGES
-----------

* Changes to `fix/fix_gsi/global_satinfo.txt` and `fix/fix_gsi/global_convinfo.txt`

MODULE CHANGES
--------------

* No changes from GFS v16.3.11

CHANGES TO FILE SIZES
---------------------

* No changes from GFS v16.3.11

ENVIRONMENT AND RESOURCE CHANGES
--------------------------------

* No changes from GFS v16.3.11

PRE-IMPLEMENTATION TESTING REQUIREMENTS
---------------------------------------

* Which production jobs should be tested as part of this implementation?
  * GSI
* Does this change require a 30-day evaluation?
  * No

DISSEMINATION INFORMATION
-------------------------

* No changes from GFS v16.3.11

HPSS ARCHIVE
------------

* No changes from GFS v16.3.11

JOB DEPENDENCIES AND FLOW DIAGRAM
---------------------------------

* No changes from GFS v16.3.11

DOCUMENTATION
-------------

* No changes from GFS v16.3.11

PREPARED BY
-----------
Kate.Friedman@noaa.gov
Andrew.Collard@noaa.gov