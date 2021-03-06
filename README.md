# swisssmartfarming

Repo containing code related to the *Swiss Smart Farming* Project (SSF).

## Setup
In order to use the package some setup steps are necessary.

Most of the code is compatible with `python3`. However, some code that needs to run on `Ubuntu 14.04` was written in `python2`, to ensure full-compatibility.

The script `setup.bash` should perform all of the needed setup. This has to be sourced (`source setup.bash`) with one of the following three options:
1. `--all`
2. `--py2`
3. `--py3`

## Dependencies
* `python-pip`
* `virtualenv` (`pip2 install --user virtualenv`)
* `python3-venv`

Many of the geodata operations performed within the project rely on the use of GDAL. GDAL, as well as the Python binding ``pygdal`` have to be installed on the computer. In order for the installation of ``pygdal`` to be successful, its version has to match the GDAL version. Check the installed GDAL version with ``gdal-config --version``. If the GDAL version is e.g. 2.2.3, then ``pygdal==2.2.3.X`` has to be installed, where ``X`` matches one of the available ``pygdal`` versions.

### python2
* rootpath==0.1.1

### python3
* catkin-pkg==0.4.16
* Fiona==1.8.13
* geopandas==0.7.0
* matplotlib==3.1.3
* numpy==1.15.2
* opencv-python==4.2.0.32
* pandas==0.23.4
* Pillow==7.0.0
* pycryptodomex==3.9.7
* pygdal==2.2.3.6
* py3exiv2==0.7.1<sup>1</sup>
* PyYAML==5.1
* rasterio==1.1.2
* roipoly==0.5.2
* rosbag==1.14.5
* rospkg==1.2.4
* rootpath==0.1.1
* scipy==1.1.0
* seaborn==0.10.0
* Shapely==1.7.0
* spectral==0.20

1. ``py3exiv2`` depends on: ``build-essential``, ``python-all-dev``, ``libexiv2-dev``, ``libboost-python-dev`` . Install them using ``apt``.


## Datasets Structure
All the SSF datasets have the structure shown in the following diagram. The root
folder name is the name of the field. The dataset is split into dates at which
the flights were carried out. These are saved directly under the root folder.
Under every date-folder the following can be found:
* ``bagfile.bag``: symbolic link to the dataset source
[bagfile](http://wiki.ros.org/Bags "ROS - Bags")
* ``bagfile.info``: result of the command ``rosbag info <bagfile.bag>`` saved
to a text-file
* ``rtk_data.csv``: file containing the recorded RTK-GPS positions / altitudes
* camera-folders: can be ``nir``, ``rgb``, ``thermal`` or ``vis``. ``thermal``
is shown in brackets since not all flights were performed with a thermal camera.
All camera-folders have the same substructure:
    - ``frames``: folder containing the camera frames extracted from the
    bagfile. The file ``img_tstamps.csv`` also stored here contains the
    timestamp of every frame
    - ``field-name_date-1_nir``: folder with the standard
    [Pix4D folder structure](https://support.pix4d.com/hc/en-us/articles/202558649-Project-Folder-Structure "Pix4D - Project Folder Structure").
    All Pix4D outputs (mosaics, point clouds, DSM, ...) are saved under this
    directory
    - ``field-name_thermal.p4d``: standard Pix4D project file that can be
    imported into Pix4D in order to regenerate / modify some outputs

```
field-name
├── date-1
│   ├── bagfile.bag
│   ├── bagfile.info
│   ├── rtk_data.csv
│   ├── nir
│   │   ├── frames
│   │   │   ├── frame-1.tif
│   │   │   ├── frame-n.tif
│   │   │   └── img_tstamps.csv
│   │   ├── field-name_date-1_nir
│   │   └── field-name_date-1_nir.p4d
│   ├── rgb
│   │   ├── frames
│   │   │   ├── frame-1.jpg
│   │   │   ├── frame-n.jpg
│   │   │   └── img_tstamps.csv
│   │   ├── field-name_date-1_rgb
│   │   └── field-name_date-1_rgb.p4d
│   ├── (thermal)
│   │   ├── frames
│   │   │   ├── frame-1.tif
│   │   │   ├── frame-n.tif
│   │   │   └── img_tstamps.csv
│   │   ├── field-name_date-1_vis
│   │   └── field-name_date-1_vis.p4d
│   └── vis
│       ├── frames
│       │   ├── frame-1.tif
│       │   ├── frame-n.tif
│       │   └── img_tstamps.csv
│       ├── field-name_date-1_vis
│       └── field-name_date-1_vis.p4d
└── date-n
    ├── bagfile.bag
    ├── bagfile.info
    ├── rtk_data.csv
    ├── nir
    │   ├── frames
    │   │   ├── frame-1.tif
    │   │   ├── frame-n.tif
    │   │   └── img_tstamps.csv
    │   ├── field-name_date-n_nir
    │   └── field-name_date-n_nir.p4d
    ├── rgb
    │   ├── frames
    │   │   ├── frame-1.jpg
    │   │   ├── frame-n.jpg
    │   │   └── img_tstamps.csv
    │   ├── field-name_date-n_rgb
    │   └── field-name_date-n_rgb.p4d
    ├── (thermal)
    │   ├── frames
    │   │   ├── frame-1.tif
    │   │   ├── frame-n.tif
    │   │   └── img_tstamps.csv
    │   ├── field-name_date-n_thermal
    │   └── field-name_date-n_thermal.p4d
    └── vis
        ├── frames
        │   ├── frame-1.tif
        │   ├── frame-n.tif
        │   └── img_tstamps.csv
        ├── field-name_date-n_vis
        └── field-name_date-n_vis.p4d
```
