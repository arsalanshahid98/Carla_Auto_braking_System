# Carla Auto Braking System
## Requirements and Setup before starting
### The following are the requirements and software I had or downloaded:
Note: Anaconda environment is recommended for this setup, all the requirements are installed in the anaconda environment.</br>
[Python]( https://www.python.org/) version: 3.11.11 (Carla 0.10.0 works with latest python version)</br>
[Carla]( https://github.com/carla-simulator/carla/releases) version: 0.10.0</br>
[Pytorch]( https://pytorch.org/get-started/locally/) 2.6.0+cu126 for Cuda 12.6 (my own Cuda version is 12.8 but pytorch for cuda 12.6 works just fine) </br>
[Anaconda](https://www.anaconda.com/) (any working version) </br>
[Ultralytics](https://docs.ultralytics.com/quickstart/#conda-docker-image) (any working version) </br>
Yolo version: 8 was trained on road markings, pretrained version 11 was used for vehicle detection. </br>

### Downloading and getting Carla ready for use
Download premade Carla zip file from their official [Blog]( https://carla.org/2024/12/19/release-0.10.0/) or their [GitHub page](https://github.com/carla-simulator/carla/releases) this zip file contains CarlaUnreal.exe executable file or any version equivalent exe file where you can directly enter the simulator in spectator mode.
To connect your Jupyter notebook with Carla, OR to connect Carla with python via anything you will need Carla’s package for python here is how you will install: 
1.	Find Carla’s wheel file, mine was located in the following directory: carla\PythonAPI\carla\dist
2.	you will find 4 to 5 wheel files for different python versions.
3.	Open this directory with wheel files in terminal/CMD/powershell OR navigate through it using cd commands.
4.	Since I’m using python 3.11.11, I installed wheel file carla-0.10.0-cp311-cp311-win_amd64.whl.
5.	Following is how you install the wheel file: `pip install <wheel-file-name>.whl`  in my case it was `pip install carla-0.10.0-cp311-cp311-win_amd64.whl` .
6.	You can `pip list` and check the site packages and verify that Carla is there.
</br>Check if all the perquisites are correctly installed and working as they are supposed to be:</br>
Open cmd.exe or powershell prompt through anaconda and type `python --version` , it should print your python version.</br>
Open your jupyter lab and check your pytorch: 
```python
#Import pytorch
import torch
#Check pytorch version
print(torch.__version__)
#This will print whether CUDA is available and, if so, the number of GPUs and the name of the first GPU
#basically this is to verify if pytorch can use your gpu
print(f"CUDA Available: {torch.cuda.is_available()}")
if torch.cuda.is_available():
    print(f"Number of GPUs available: {torch.cuda.device_count()}")
    print(f"GPU Name: {torch.cuda.get_device_name(0)}")
```

