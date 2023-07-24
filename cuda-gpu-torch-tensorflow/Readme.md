# Cuda-GPU-Torch-TensorFlow

Install proxychains to skip `filterings`
```
sudo apt-get install tor
sudo apt-get install proxychains
```
Before any commands that connects to internet pass `proxychains` keyword like the following example:  

## Update repositories:
```commandline
sudo proxychains apt-get update
# or 
sudo apt-get update
```


# How to install Nvidia Cuda on ubuntu

```
sudo apt-get update
sudo apt-get upgrade
```

first, remove all GPUs
```
sudo apt-get purge nvidia*
sudo apt-get autoremove
sudo apt-get autoclean
sudo rm -rf /usr/local/cuda*
```

go to the link below:
http://developer.download.nvidia.com/compute/cuda/repos
find the one which is proper for your distribution:
http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub

get the key and add it to the apt sources. so we could use it later.
```
sudo apt-key adv --fetch-keys http://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64/7fa2af80.pub
echo "deb https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2004/x86_64 /" | sudo tee /etc/apt/sources.list.d/cuda.list
```
2204:
```
wget https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64/cuda-archive-keyring.gpg
sudo cp cuda-archive-keyring.gpg /usr/share/keyrings/cuda-archive-keyring.gpg
echo "deb [signed-by=/usr/share/keyrings/cuda-archive-keyring.gpg] https://developer.download.nvidia.com/compute/cuda/repos/ubuntu2204/x86_64 /" | sudo tee /etc/apt/sources.list.d/cuda.list
# The final / determines in which section of the provided link the linux should look for its files
```
Install cuda( we go for cuda 11). It may take a while.
```
sudo apt-get update 
sudo apt-get -o Dpkg::Options::="--force-overwrite" install cuda-11-2 cuda-drivers
```
*NOTE*: the cuda version which is 11-2 in this can be changed to any version your system requires! 11-7 12-1 and so on.
Add the Cuda path to your bashrc so it would be in the PATH for each terminal
```
echo 'export PATH=/usr/local/cuda-11.6/bin${PATH:+:${PATH}}' >> ~/.bashrc
echo 'export LD_LIBRARY_PATH=/usr/local/cuda-11.6/lib64${LD_LIBRARY_PATH:+:${LD_LIBRARY_PATH}}' >> ~/.bashrc
echo 'export CUDA_HOME=/usr/local/cuda-11.6' >> ~/.bashrc
source ~/.bashrc
sudo ldconfig
```

For Windows:
The Windows downloads it for you no need to bother
Even for Ubuntu you can use third-party drivers to install the one that is "tested"

Go to https://developer.nvidia.com/rdp/cudnn-download and download cudnn
Cudnn Librray for Linux(x86_64)

For the older versions of cudnn check the following link:
http://people.cs.uchicago.edu/~kauffman/nvidia/cudnn/


```
tar -xf cudnn-11.0-linux-x64-v7.5.0.56.tgz # it could be different for you
sudo cp -R cuda/include/* /usr/local/cuda-11.0/include
sudo cp -R cuda/lib64/* /usr/local/cuda-11.0/lib64

# or
cd cudnn-linux...
sudo cp -R include/* /usr/local/cuda/include
sudo cp -R lib/* /usr/local/cuda/lib64
```

```
sudo apt-get install libcupti-dev
echo 'export LD_LIBRARY_PATH=/usr/local/cuda/extras/CUPTI/lib64:$LD_LIBRARY_PATH' >> ~/.bashrc
```

Install TensorFlow-2:
```
# GPU
conda create -n tf_gpu python=3.9 tensorflow
pip install tensorflow>=2.7.0 # to upgrade it to the last version
# Note: tensorflow=2.7.0 does not connect to gpu without cudnn libraries in the place.

# CPU
conda create -n tf2_cpu python=3.9
conda activate tf2_cpu
pip install tensorflow # cpu
```

For Windows:
```
Download the cudnn form https://developer.nvidia.com/rdp/cudnn-download 
copy dll files to C:\Windows\System32
```

Install TensorFlow-1:
```
conda install -c anaconda tensorflow-gpu==1.15.0
pip install tensorflow==1.15.0 # cpu
```

Install PyTorch[Turn on VPN]
```
# connect to VPN
conda create -n torch_gpu python=3.9
conda activate torch_gpu
conda install pytorch torchvision torchaudio cudatoolkit -c pytorch # GPU
conda install pytorch torchvision cpuonly -c pytorch # CPU
```

```
NOTE: Python 3.9 users will need to add '-c=conda-forge' for installation
```

torchtext:
```
conda install -c pytorch torchtext
```

torchaudio:
```
conda install -c pytorch torchaudio
```


Usual Installation:

```
pip install pandas numpy scikit-learn opencv-python deep_utils matplotlib
```


Errors

NVIDIA-SMI has failed because it couldn't communicate with the NVIDIA driver
```
Go to boot manager and disable the secure boot after a clean installation of nvidia:)
```
