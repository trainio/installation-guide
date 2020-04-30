# installation-guide

Install Docker: 

https://www.hostinger.com/tutorials/install-docker-on-ubuntu/ 
 

sudo apt-get update 

sudo apt-get upgrade 
 

sudo apt install docker.io 
  

sudo systemctl start docker 

sudo systemctl enable docker 
 

sudo systemctl status docker 
 

docker -v 
 

 
 

NVIDIA - Docker 

https://github.com/NVIDIA/nvidia-docker 
 

# Add the package repositories  

distribution=$(. /etc/os-release;echo $ID$VERSION_ID)  

curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add -  

curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list  

 
sudo apt-get update && sudo apt-get install -y nvidia-container-toolkit  

sudo systemctl restart docker 
 

 
 

# Install Cuda Toolkit (You don't need it, but nice to have) 

 https://docs.nvidia.com/cuda/cuda-installation-guide-linux/index.html#pre-installation-actions

https://developer.nvidia.com/cuda-downloads 

 
 

Then restart 

 
 

#### Test nvidia-smi with the latest official CUDA image 

docker run --gpus all nvidia/cuda:10.0-base nvidia-smi 
 

You might need sudo rights  
