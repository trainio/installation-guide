## How to install Linux Ubuntu alongside Windows 10 (+ extras) 

 

# Before the installation: 

# A) UEFI/BIOS 

Set to "UEFI mode only" (no legacy/CSM). 

Disable "secure boot" 

Disable "Intel Rapid Start" (if equipped) 

Disable "fast boot" in UEFI (note this is different than the "fastboot" setting in Windows 8/10). The options in your UEFI/BIOS might say something like Full/Minimal/Automatic for boot mode. Select Full (or thorough, or complete, etc whatever your UEFI vendor has chosen to call it). 

# B) Advanced Power Options (Fastboot) 

Disable fastboot in Windows 8/10 under "advanced power options". Restart computer to ensure that this subsequent boot and the next reboot/shutdown will be in "normal" mode. 

Refer to this video: https://www.youtube.com/watch?v=u5QyjHIYwTQ&t=194s 

MINIMUM BIOS SETUP 

    FAST BOOT OFF 

    SECURE BOOT OFF 

Windows  

Run the command prompt, as admin at type powercfg.exe /hibernate off, and then press Enter. 

 

# Prepare installation on PC 

Download .iso file of Ubuntu desktop 18.4 LTS: https://releases.ubuntu.com/bionic/ 

Download and install Balena Etcher: https://www.balena.io/etcher/ 

Format a USB flash drive in FAT32 

Windows File Explorer > Select Disk > Right click > Format 

Use Etcher to flash the USB stick with the Ubuntu .iso file 

https://youtu.be/u5QyjHIYwTQ?t=112 

 

Create partition (at least 30 GB) 

Open Disk management 

Select your drive 

Right-click > Shrink Volume 

Shrink eg. 80 Gb (remember to leave some empty space for Windows as well) 

 

 

The most common "unmoveable" files are files which are locked during normal computer operation such as virtual memory/pagefile/system restore files as well as a few other files which may be open, but not running "in memory" 

Having come across this myself previously on both server and desktop operating systems - I can say the most likely culprit is the pagefile. 

To fix this: 

    Right-click Computer 

    Select Properties 

    Select Advanced system settings 

    Select the Advanced tab and then the Performance radio button 

    Select the Change box under Virtual memory 

    Un-check Automatically manage paging file size for all drives 

    Select No paging file, and click the Set button 

    Select OK to allow and restart. 

https://www.youtube.com/watch?v=5MkmPLL5tQw 

 

# Ubuntu Installation 

Insert the USB stick (After previous steps the usb is unmounted as default) 

Reboot your PC 

Go to the bios (usually F12 or Del at boot) 

Select “try Ubuntu without installing”  

If Ubuntu crashes: try to add nomodeset to grub file, see instructions here:  

https://www.youtube.com/watch?time_continue=40&v=Tg4fWsFPzSE&feature=emb_title 

 

Launch “install Ubuntu” shortcut on the desktop 

Normal install and select “download updates while installing Ubuntu” 

If you get a message “do you want to unmount …",  click Yes 

Option 1: select “Install Ubuntu alongside Windows Boot Manager”  

Follow the instructions and complete the installation 

 

Shutdown and Restart  

Enter the bios again and choose to boot from your Ubuntu partition 

A menu should prompt and let you choose which environment you want to start 

 

 

 

 

#Install Nvidia drivers: 

Go to Ubuntu > Software & Updates —> additional drivers —> NVIDIA corporation: using NVIDIA drivers … 435 (proprietary, tested) 

 
 

#Install Docker: 

Update+Upgrade Ubuntu (type in Terminal) 

 sudo apt-get update 

 sudo apt-get upgrade 
 

Install Docker(type in Terminal) 

 sudo apt install docker.io 
  

Test run Docker(type in Terminal) 

 sudo systemctl start docker 

 sudo systemctl enable docker 

 sudo systemctl status docker 

 Press CTRL+C to exit 
 

Check Docker version (type in Terminal) 

 docker -v 
 

More information: https://www.hostinger.com/tutorials/install-docker-on-ubuntu/ 
 

 

 
 

#NVIDIA – Docker 

 

 

https://github.com/NVIDIA/nvidia-docker 
 

#Install curl, type (in Terminal): 

sudo apt install curl 

# Add the package repositories  

distribution=$(. /etc/os-release;echo $ID$VERSION_ID)  

curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -  

curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list  

 
sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit  

sudo systemctl restart docker 

 

#Install nvidia-docker 2.0 

Type (in Terminal): 

sudo apt-get install nvidia-docker2  

sudo pkill –SIGHUP dockerd 

Test Nvidia-Docker, type (in Terminal):  

docker run --runtime=nvidia –rm nvidia/cuda nvidia-smi 

 
 

#Check CUDA version  

Type (to Terminal): 

nvidia-smi 

If the drivers were installed correctly you should see info table about your GPU and the version of installed driver + CUDA version (should be 10.1) 

 

#Install Cuda Toolkit (I am not sure if necessary) 

https://developer.nvidia.com/cuda-downloads 

 
 

#Then restart 

#### Test nvidia-smi with the latest official CUDA image 

sudo docker run --gpus all nvidia/cuda:10.0-base nvidia-smi 
 
 

 

#Run ML project 

You can easily run ML project if they provide Docker file: 

For example, try this: https://github.com/junyanz/pytorch-CycleGAN-and-pix2pix/blob/master/docs/docker.md 

Type (in Terminal): 

sudo nvidia-docker run -it -p 8097:8097 taesungp/pytorch-cyclegan-and-pix2pix 

This will download all files and data needed to run the project 

 

#Getting started with Docker 

List all containers in your Docker, type (in Terminal): 

docker image ls -all  

Remove/Delete Docker containers, type (in Terminal): 

docker image rm <name_of_container_file> 
