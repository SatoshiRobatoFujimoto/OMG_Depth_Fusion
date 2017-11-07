# Optimal Mixture of Gaussians for Depth Fusion
Implementation of the filter proposed in:

**Paper:** Probabilistic RGB-D Odometry based on Points, Lines and Planes Under Depth Uncertainty, P. Proença and Y. Gao
[arxiv](https://arxiv.org/abs/1706.04034)

The OMG filter is aimed at denoising and hole-filling the depth maps given by a depth sensor, but also (more importantly) capturing the depth uncertainty though spatio-temporal observations, which proved to be useful as an input to a probabilistic visual odometry system.

The code runs the OMG on RGB-D dataset sequences (e.g. ICL_NUIM and TUM). Some examples are included in this repository.
This release does not include the VO system, thus instead of using the VO frame-to-frame pose, we rely on the groundtruth pose to transform the old measurements (the registered point cloud) to the current frame.

## Dependencies

* Opencv
* Eigen3

## Ubuntu Instructions
Tested with Ubuntu 14.04

To compile, inside the directory ``./OMG`` type:
```
mkdir build
cd build
cmake ../
make
```
To run the executable type:
```./test_OMG 4 9 TUM_RGBD sitting_static_short```
or
```./test_OMG 4 9 ICL_NUIM living_room_traj0_frei_png_short```

## Windows Instructions

Tested configuration: Windows 8.1 with Visual Studio 10 & 12

This version includes already a VC11 project
Just make the necessary changes to link the project with OpenCV and Eigen

## Usage

General Format
```./test_OMG <max_nr_frames> <consistency_threshold> <dataset_directory> <sequence_name>```

* ***max_nr_frames:*** is the window size - 1, i.e., the maximum number of previous frames used for fusion
* ***consistency threshold:*** is used to avoid fusing inconsistent measurements, if the squared distance between a new measurement and the current estimate is more than current uncertainty times this threshold than the new measurement is ignored. Setting this higher may produce better quality but will capture less the temporal uncertainty
