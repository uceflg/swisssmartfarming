# swisssmartfarming

Repo containing all the code related to the *Swiss Smart Farming* Project (SSF).
The code is here

## Install
Depends on:
* python3-venv

## Dependencies
Many of the geodata operations performed within the project rely on the use of GDAL. GDAL, as well as the Python binding ``pygdal`` have to be installed on the computer. In order for the installation of ``pygdal`` to be successful, its version has to match the GDAL version. Check the installed GDAL version with ``gdal-config --version``. If the GDAL version is e.g. 3.0.2, then ``pygdal==3.0.2.X`` has to be installed, where ``X`` matches one of the available ``pygdal`` versions.

python3
* catkin-pkg==0.4.16
* cv-bridge==1.13.0
* geopandas==0.7.0
* matplotlib==3.1.3
* numpy==1.15.2
* Pillow==7.0.0
* pycryptodomex==3.9.7
* pygdal==2.2.3.6
* py3exiv2==0.7.1<sup>1</sup>
* rasterio==1.1.2
* rosbag==1.14.3
* rospkg==1.2.4
* rootpath==0.1.1
* scipy==1.1.0
* seaborn==0.10.0
* yaml

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
