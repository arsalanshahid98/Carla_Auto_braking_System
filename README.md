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

Check if all the perquisites are correctly installed and working as they are supposed to be:
1.	Open cmd.exe or powershell prompt through anaconda and type `python --version` , it should print your python version.</br>
2.	Open your jupyter lab and check your pytorch: 
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
3.	Check your Carla installation via jupyter, first start your CarlaUnreal.exe (or any version equivalent), once you are in spectator mode and can move around as a spectator, The above code should connect to carla simulator and atleast move or change the camera location which indicates successful connection, type the following in jupyter and run: 
```python
Import carla
Import random

#connect to simulator
client = carla.Client('localhost', 2000) # carla server starts on port: 2000
world = client.get_world()

#get location of the client (I use this to confirm the connection with the sim)
spectator = world.get_spectator()
transform = spectator.get_transform()
spectator.set_transform(carla.Transform())
```
4.	Verify the remaining following imports if you don’t have these make sure they are installed before going forward: 
```python
import carla # already verified
import numpy as np
import cv2
import threading
import queue
import pygame
import time
from ultralytics import YOLO
```
### Running the abs Script
1.	Make sure the model files road_marking_detector.pt and vehicle_detector(y11).pt are in the same directory as abs.ipynb. If not then change the paths in the following variables to the model files: 
```python
# Load YOLO models
vehicle_model = YOLO("vehicle_detector(y11).pt")
road_model = YOLO("road_marking_detector.pt")
```
2.	Start Carla using CarlaUnreal.exe OR use the following command in cmd/powershell if your system can’t handle a heavy load `CarlaUnreal.exe -quality-level=Low -ResX=800 -ResY=600 -Windowed -NoVSyn -benchmark -fixed-time-step=0.05` you can check out Carla’s documentation for more custom commands.
3.	Once Carla is started and you can move freely around as spectator, execute the abs.ipynb script, two windows will popup, a pygame window and an inference window.
4.	Pygame window is for controlling the vehicle, the following are the key bindings for vehicle controles: 
```
W: Move forward
S: Brake
A:  Turn left
D: Turn right
R: Toggle Reverse Gear
```
5.	You can drive around in the vehicle and test around, the ABS currently works for vehicles and Crosswalks.
The

