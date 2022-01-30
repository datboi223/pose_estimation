# 6D Pose-Estimation with Cosypose

In order to use the __[cosypose](https://github.com/datboi223/cosypose)__-approach for 6D-Pose Estimation you get the code first and install it. This directory utilizes the single-view version of cosypose to estimate the translation and rotaton and rotation, relative to the camera that was used to observe the scene.

## Installation
Clone the __[cosypose](https://github.com/datboi223/cosypose)__-repository and follow the instructions below inside the root-folder of that repository
```bash
git clone --recurse-submodules https://github.com/datboi223/cosypose.git
virtualenv -p python3.8 pe_cosypose
pip3 install torch==1.7.1+cu110 torchvision==0.8.2+cu110 torchaudio==0.7.2 -f https://download.pytorch.org/whl/torch_stable.html
pip3 install -r requirements.txt
git lfs pull
```

To finally install cosypose you have to use the following command:
```bash
python setup_venv.py install
python setup_venv.py devel
```

For the program [transforms.py](https://github.com/datboi223/cosypose/blob/master/cosypose/lib3d/transform.py) to work, you also have to insall `eigenpy`. 
For installing eigenpy follow these instructions
```bash
sudo sh -c "echo 'deb [arch=amd64] http://robotpkg.openrobots.org/packages/debian/pub $(lsb_release -cs) robotpkg' >> /etc/apt/sources.list.d/robotpkg.list"
curl http://robotpkg.openrobots.org/packages/debian/robotpkg.key | sudo apt-key add -
sudo apt update
sudo apt install robotpkg-py38-eigenpy # installs eigenpy library in /opt/openrobots/ directory
sudo apt install ros-noetic-eigenpy
```
If you can not run cosypose because of `eigenpy` still not being found, you have to add the directory `/opt/openrobots/lib/` to the `LD_LIBRARY_PATH`
```bash
export LD_LIBRARY_PATH=/opt/openrobots/lib/:$LD_LIBRARY_PATH
```
This usually solves the problem.

## Downloading the Data

To use cosypose you also have to download the required data. For this follow the instructions of the cosypose-repository [here](https://github.com/datboi223/cosypose#downloading-and-preparing-data). Follow the download instructions for the __ycb-Data__ starting with the download of the `urdf`-files. 

Now you can download the `YCB-V` model-weights for single-view pose estimation [here](https://github.com/datboi223/cosypose#pre-trained-models). Follow the instructions there and download the parameters with the following `model_id`-values
- `detector-bop-ycbv-pbr--970850`
- `coarse-bop-ycbv-pbr--724183`
- `refiner-bop-ycbv-pbr--604090`

## TODO: synth+real weights