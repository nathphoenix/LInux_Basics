UBUNTU 22.04

Run nvidia-smi
if failed it means nvidia driver is not installed

so install invidia graphic driver for your os(Linux)

sudo apt update

sudo apt  install cmake

Install cuda toolkit
https://developer.nvidia.com/cuda-11-8-0-download-archive?target_os=Linux&target_arch=x86_64&Distribution=Ubuntu&target_version=22.04&target_type=deb_local

Instruction from the above link below
Base Installer	
Installation Instructions:
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-ubuntu2204.pin
sudo mv cuda-ubuntu2204.pin /etc/apt/preferences.d/cuda-repository-pin-600
wget https://developer.download.nvidia.com/compute/cuda/11.8.0/local_installers/cuda-repo-ubuntu2204-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo dpkg -i cuda-repo-ubuntu2204-11-8-local_11.8.0-520.61.05-1_amd64.deb
sudo cp /var/cuda-repo-ubuntu2204-11-8-local/cuda-*-keyring.gpg /usr/share/keyrings/
sudo apt-get update
sudo apt-get -y install cuda

see how to download cuDNN here for linux
https://stackoverflow.com/questions/76139931/azure-vm-loaded-runtime-cudnn-library-8-2-4-but-source-was-compiled-with-8-6-0

export URL="PASTE-LINK-HERE"
 URL="https://developer.download.nvidia.com/compute/cudnn/secure/8.9.7/local_installers/11.x/cudnn-linux-x86_64-8.9.7.29_cuda11-archive.tar.xz?kqONwxWuKPGshVARa6ZU5xmqfAghwLq9BnY5u0Y8C3pm60ku8bje-knxkqhAH1IiuTNSzOl4e0UzdUJJSoJmRfmStegHT73DxRWFwBBV1V7h5X_cDs6jLxZXdvvxJacYMoe0T9YF2KNXUpGuNzuNNkFPS8utm9ULEPtuKRdpDquMPV8LOFEH9r8mot5Ft_AVyLRM1zcJnuCLdSe-8edStW8=&t=eyJscyI6InJlZiIsImxzZCI6IlJFRi1tZWRpdW0uY29tL2dlZWtjdWx0dXJlL2luc3RhbGwtY3VkYS1hbmQtY3Vkbm4tb24td2luZG93cy1saW51eC01MmQxNTAxYTg4MDUifQ=="


# ==== DOWNLOAD CUDDN ==== 
curl $URL -o ./cudnn-linux-x86_64-8.6.0.163_cuda11-archive.tar.xz (This is the format)
i.e curl $URL -o ./cudnn-linux-x86_64-8.9.7.29_cuda11-archive.tar.xz

Extract the zip cuDNN file
sudo tar -xvf ./cudnn-linux-x86_64-8.6.0.163_cuda11-archive.tar.xz
i.e  sudo tar -xvf ./cudnn-linux-x86_64-8.9.7.29_cuda11-archive.tar.xz

# ==== INSTALL CUDDN ==== 
sudo cp ./cudnn-*-archive/include/cudnn*.h /usr/local/cuda/include 
i.e sudo cp ./cudnn-linux-x86_64-8.9.7.29_cuda11-archive/include/cudnn*.h /usr/local/cuda/include

sudo cp -P ./cudnn-*-archive/lib/libcudnn* /usr/local/cuda/lib64 
i.e  sudo cp -P ./cudnn-linux-x86_64-8.9.7.29_cuda11-archive/lib/libcudnn* /usr/local/cuda/lib64

sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
# ==== CONFIGURE DYNAMIC RUNTIME BINDINGS ==== 
sudo ldconfig

sudo apt install python3-pip

install pytorch and cuda from pytorch site
pip install torch==2.3.0 torchvision==0.18.0 torchaudio==2.3.0 --index-url https://download.pytorch.org/whl/cu118

pip install tensorflow==2.12.0