# Simlified instruction
This branch is for processing reg-1.bag dataset.

## Step 1 (prepare data)
Download the dataset `reg-1.bag` by clicking [link](https://cloud.cylab.be/public.php/dav/files/7PgyjbM2CBcakN5/reg-1.bag) (it is part of [Bunker DVI Dataset](https://charleshamesse.github.io/bunker-dvi-dataset)) and convert with [tool](https://github.com/MapsHD/livox_bag_aggregate) to 'reg-1.bag-pc.bag'.

File 'reg-1.bag-pc.bag' is an input for further calculations.
It should be located in '~/hdmapping-benchmark/data'.


## Step 2 (prepare docker)
```shell
mkdir -p ~/hdmapping-benchmark
cd ~/hdmapping-benchmark
git clone https://github.com/MapsHD/benchmark-LeGO-LOAM-to-HDMapping.git --recursive
cd benchmark-LeGO-LOAM-to-HDMapping
git checkout Bunker-DVI-Dataset-reg-1
docker build -t lego-loam_noetic .
```

## Step 3 (run docker, file 'reg-1.bag-pc.bag' should be in '~/hdmapping-benchmark/data')
```shell
cd ~/hdmapping-benchmark/benchmark-LeGO-LOAM-to-HDMapping
chmod +x docker_session_run-ros1-lego-loam.sh 
cd ~/hdmapping-benchmark/data
~/hdmapping-benchmark/benchmark-LeGO-LOAM-to-HDMapping/docker_session_run-ros1-lego-loam.sh reg-1.bag-pc.bag .
```

## Step 4 (Open and visualize data)
Expected data should appear in ~/hdmapping-benchmark/data/output_hdmapping-lego-loam
Use tool [multi_view_tls_registration_step_2](https://github.com/MapsHD/HDMapping) to open session.json from ~/hdmapping-benchmark/data/output_hdmapping-lego-loam.

You should see following data
--
lio_initial_poses.reg
poses.reg
scan_lio_0.laz
scan_lio_1.laz
scan_lio_2.laz
scan_lio_3.laz
scan_lio_4.laz
scan_lio_5.laz
scan_lio_6.laz
scan_lio_7.laz
scan_lio_8.laz
scan_lio_9.laz
session.json
trajectory_lio_0.csv
trajectory_lio_1.csv
trajectory_lio_2.csv
trajectory_lio_3.csv
trajectory_lio_4.csv
trajectory_lio_5.csv
trajectory_lio_6.csv
trajectory_lio_7.csv
trajectory_lio_8.csv
trajectory_lio_9.csv
--

# LeGO-LOAM-converter


## Example Dataset: 

Download the dataset `reg-1.bag` by clicking [here](https://cloud.cylab.be/public.php/dav/files/7PgyjbM2CBcakN5/reg-1.bag) from [Bunker DVI Dataset](https://charleshamesse.github.io/bunker-dvi-dataset).

## Intended use 

This small toolset allows to integrate SLAM solution provided by [LeGO-LOAM](https://github.com/RobustFieldAutonomyLab/LeGO-LOAM) with [HDMapping](https://github.com/MapsHD/HDMapping).
This repository contains ROS 1 workspace that :
  - submodule to tested revision of LeGO-LOAM
  - a converter that listens to topics advertised from odometry node and save data in format compatible with HDMapping.

## Dependencies

```shell
sudo apt update
sudo apt install -y docker.io
sudo usermod -aG docker $USER
```

## Convert ros1 CustomMsg to PointCloud2

For usage instructions, click [here](https://github.com/MapsHD/livox_bag_aggregate).

## Workspace

```shell
mkdir -p ros_ws/src/
cd ros_ws/src/
git clone https://github.com/MapsHD/benchmark-LeGO-LOAM-to-HDMapping.git --recursive
```

## Docker build
```shell
cd ros_ws/src/benchmark-LeGO-LOAM-to-HDMapping
docker build -t lego-loam_noetic .
```

## Docker run
```shell
cd ros_ws/src/benchmark-LeGO-LOAM-to-HDMapping
chmod +x docker_session_run-ros1-lego-loam.sh 
./docker_session_run-ros1-lego-loam.sh <input_bag> <output_folder>

# For usage instructions or options, you can run:
./docker_session_run-ros1-lego-loam.sh --help
```