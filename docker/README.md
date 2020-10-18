# Getting started with Docker

In order to replicate the results smoothly and avoid dependency errors (aka CUDA installation hell) you can use Docker combined with NVIDIA-Docker. Docker will install all the packages in an isolated environment.

Note: You will need an NVIDIA GPU and a Linux OS or WSL2 of Windows Insider Build 20236 or higher to use NVIDIA-Docker.
 
## Installing NVIDIA Docker on Linux 
* [Docker](https://gist.github.com/enric1994/3b5c20ddb2b4033c4498b92a71d909da)
* [Docker-Compose](https://gist.github.com/enric1994/3b5c20ddb2b4033c4498b92a71d909da)
* [nvidia-docker](https://github.com/NVIDIA/nvidia-docker#ubuntu-16041804-debian-jessiestretchbuster)

## Installing NVIDIA Docker on Windows 10 with WSL2
* [WSL2](https://docs.microsoft.com/en-us/windows/wsl/install-win10)
* [Ubuntu-Subsystem](https://docs.microsoft.com/en-us/windows/wsl/install-manual)
* [download-ubuntu-1804-for-wsl](https://aka.ms/wsl-ubuntu-1804)
* [nivida-docker](https://docs.nvidia.com/cuda/wsl-user-guide/index.html)

## Downloading the required files
* Download the `frames` and `masks` folders from [here](https://drive.google.com/drive/folders/13aMItboZBxPnbjlOCbKLg7nxZgBWQt9P) and place them on the `demo` folder.

* Download the files `FlowNet2_checkpoint.pth.tar`, `imagenet_deepfill.pth` and `resnet101_movie.pth` from [here](https://drive.google.com/drive/folders/1Nh6eJsue2IkP_bsN02SRPvWzkIi6cNbE) and place them in `pretrained_models`.

```
├── demo
│   ├── frames
│   └── masks
├── pretrained_models
│   ├── FlowNet2_checkpoint.pth.tar
│   ├── imagenet_deepfill.pth
│   └── resnet101_movie.pth
```


## Start the Docker Container on Linux
1. From the `docker` folder run: `docker-compose up -d` 

2. Access the conatiner: `docker exec -it inpainting bash` 

## Start the Docker Container on Windows WSL2 inside the Ubuntu 18.04 Subsystem
1. From the `docker` folder run: `docker-compose up -d` 

2. Run the container: `sudo docker run --shm-size 4096MB --gpus all -v ~/Deep-Flow-Guided-Video-Inpainting-WSL2:/inpainting -t -d --name my_inpainting inpainting` 

3. Access the container: `sudo docker exec -it my_inpainting bash` 

4. `cd /inpainting`

## Usage
That will open a CLI on the Docker container. Now you can run the demo scripts, for example:

`python3 tools/video_inpaint.py --frame_dir ./demo/frames --MASK_ROOT ./demo/masks --img_size 512 832 --FlowNet2 --DFC --ResNet101 --Propagation`

## Compatibility

* Tested on Ubuntu 18.04 with a GTX 1060 GPU (drivers 410.104). Not working on higher architectures such as sm_75 (Turing), e.g. RTX 2080 Ti.
* Tested on WSL2 of Windows 10 Pro Insider Build 20236 and Ubuntu 18.04 subsytem with GTX 1050 GPU and RTX 2080.
