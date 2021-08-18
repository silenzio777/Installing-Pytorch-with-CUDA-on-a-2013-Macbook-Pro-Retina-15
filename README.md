# Installing-Pytorch-with-CUDA-on-a-2013-Macbook-Pro-Retina-15
Installing process based on: https://www.cs.rochester.edu/u/kautz/Installing-Pytorch-Cuda-on-Macbook.html
<br>Thanks to Henry Kautz!<br>
________________________________________
These instructions have been tested for:

<blockquote>
OS : MacOS High Sierra 10.13.6 (17G14042)<br>
NVIDIA CUDA Toolkit 10.0<br>
GPU CUDA Driver Version: 418.105<br>
GPU Driver: NVIDIA Web Driver 387.10.10.10.4.140<br>
Xcode Version: 9.4<br>
Python 3.7.11<br>
</blockquote>
<br>

<a name="S1"></a>
### Step 1: Downgrade to High Sierra 10.13.6 (17G14042)
Check that you are running Mac OS X High Sierra (10.13.6). If you have an older version, upgrade. If you have a newer version you will need to downgrade; Apple banished CUDA with Mojave and later versions of the OS. Downgrading OS X requires <a href="https://www.macworld.co.uk/how-to/mac-software/downgrade-macos-mojave-3581872/">creating a bootable USB memory stick installer and erasing your laptop's hard disk</a>
<br><br>

<a name="S2"></a>
### Step 2: Downgrade Xcode
Make developer acc at first, then go to https://developer.apple.com/download/all/ and download Xcode version 9.4. 
<a href="https://download.developer.apple.com/Developer_Tools/Command_Line_Tools_macOS_10.13_for_Xcode_9.4/Command_Line_Tools_macOS_10.13_for_Xcode_9.4.dmg">( direct link )</a>
<br><br>
Install Xcode version 9.4.<br>
<br>
Then switch to Xcode version 9.4:
```
sudo xcode-select --switch /Library/Developer/CommandLineTools
```
<br>
You can check current version of Xcode by:

```
clang --version
```
<br>
Should be:
<blockquote>
Apple LLVM version 9.1.0 (clang-902.0.39.2)<br>
Target: x86_64-apple-darwin17.7.0<br>
Thread model: posix<br>
InstalledDir: /Library/Developer/CommandLineTools/usr/bin
</blockquote>
Don't think about 9.4 != 9.1. It's OK 8;
<br><br>

<a name="S3"></a>
### Step 3: Install NVIDIA Drivers
Install the <a href="https://images.nvidia.com/mac/pkg/387/WebDriver-387.10.10.10.40.140.pkg">NVIDIA Quadro and Geforce OS X Driver 387.10.10.10.40.140</a>

Add to your .profile
```
nano ~/.bash_profile
```
<br>
this two lines:<br>

```
export PATH=/Developer/NVIDIA/CUDA-10.0/bin${PATH:+:${PATH}}
export DYLD_LIBRARY_PATH=/usr/local/cuda/lib:$DYLD_LIBRARY_PATH
```
<br><br>
<a name="S4"></a>
### Step 4: Download NVIDIA CUDA Toolkit 10.0 Archive

Download installer <a href="https://developer.nvidia.com/cuda-10.0-download-archive?target_os=MacOSX&target_arch=x86_64&target_version=1013">NVIDIA CUDA Toolkit 10.0 </a>(1,8 GB)<br>
<br>
![DownloadCUDAToolkit_sm](https://user-images.githubusercontent.com/7931919/129793652-02818cad-e510-4b40-9bf4-536121342d58.png)<br>
<br>
It will be installed to "/Developer/NVIDIA/CUDA-10.0"
<br><br>
**reboot your Mac**<br>
<br>
<a name="S5"></a>
### Step 5: Install NVIDIA cuDNN 7.6.5
<a href="https://developer.nvidia.com/login">Joint to NVIDIA Developer Program.</a><br>
And download installer zip file - <a href="https://developer.nvidia.com/compute/machine-learning/cudnn/secure/7.6.5.32/Production/10.0_20191031/cudnn-10.0-osx-x64-v7.6.5.32.tgz">cudnn-10.0-osx-x64-v7.6.5.32.tgz</a> (654,8 MB)<br>
<br>
Then Unzip it to "/usr/local/cuda/"<br>
<br>
There will be two directories with files:<br>

>/include<br>
>cudnn.h<br>

and<br>

>/lib<br>
>libcudnn.7.dylib<br>
>libcudnn.dylib<br>
>libcudnn_static.a<br>
<br>

Copy file "libcuda.dylib" from "/Developer/NVIDIA/CUDA-10.0/lib" to "/usr/local/cuda/lib"<br>
And then make a alias (symlink) of "libcuda.dylib" as name "libcuda.so.1"<br>

```
sudo cp /Developer/NVIDIA/CUDA-10.0/lib/libcuda.dylib /usr/local/cuda/lib
cd /usr/local/cuda/lib/
ln -s libcuda.dylib libcuda.so.1
```
<br><br>

<a name="S6"></a>
### Step 6: Install Conda
Install <a href="https://www.anaconda.com/distribution/">Anaconda</a>. Create an environment named "ptc" that includes pip, activate it, and install libraries:

```
conda create --name ptc python=3.7
conda activate ptc
conda install numpy ninja pyyaml mkl mkl-include setuptools cmake cffi typing_extensions future six requests dataclasses intel-openmp
conda install torchvision
conda install pkg-config libuv
```
<br><br>

<a name="S7"></a>
### Step 7: Build Pytorch
Download Pytorch install:<br>
```
conda activate ptc
git clone --recursive https://github.com/pytorch/pytorch
```
<br>
Finally you build:<br>

```
cd pytorch
export CMAKE_PREFIX_PATH=${CONDA_PREFIX:-"$(dirname $(which conda))/../"}
MACOSX_DEPLOYMENT_TARGET=10.9 CC=clang CXX=clang++ python setup.py install
```

<br>
it will take some time... about hour 8).
<br><br>
It will be installed to:

```
/Users/<-USERNAME->/opt/anaconda3/envs/ptc/lib/python3.7/site-packages/torch"
```

And:

```
/Users/<-USERNAME->/opt/anaconda3/envs/ptc/lib/python3.7/site-packages/torch-1.10.0a0+git30214ae-py3.7.egg-info
```

(or similar)
<br>

After success build reboot your Mac<br>
<br><br>

<a name="S8"></a>
### Step 8: Upgrade torchvision and torchsummary

```
conda activate ptc
pip install torchvision==0.10.0 --no-deps
pip install --upgrade Pillow
pip install pandas
pip install torchsummary==1.5.1 --no-deps
```

Use "--no-deps" option because if you just run "pip install torchvision" it will be replace you Torch installation by CPU version of Torch.

<br><br>
<a name="S9"></a>
### Step 9: Test Pytorch
Test that pytorch with CUDA is working:<br>

```
conda activate ptc
python
>>import torch
>>torch.cuda.is_available()
```

You should see onу word "true"<br>
<br>

```
python
from torch import cuda
print('__CUDNN VERSION:', torch.backends.cudnn.version())
print('__Number CUDA Devices:', torch.cuda.device_count())
print('__CUDA Device Name:',torch.cuda.get_device_name(0))
print('__CUDA Device Total Memory [GB]:',torch.cuda.get_device_properties(0).total_memory/1e9)
```

You should see:<br>
```
__CUDNN VERSION: 7605
__Number CUDA Devices: 1
__CUDA Device Name: GeForce GT 750M
__CUDA Device Total Memory [GB]: 2.147024896
```
![CUDATest](https://user-images.githubusercontent.com/7931919/129861051-8cee6d45-e16a-44ac-accd-264617774871.png)
<br>
By my test (fine-tunning Resnet18) this install CUDA provides about a 1.8X speedup over the CPU for Pytorch on Macbook Pro 2019 with ATI graphics.
Yes, in this case Macbook Pro 2013 with NVidia faster then Macbook Pro 2019 with ATI.<br>
<br><br>
<a name="S10"></a>
### Step 10: Some hack

You can easily save this installation just zipping two those dir:<br>

```
/Users/<-USERNAME->/opt/anaconda3/envs/ptc/lib/python3.7/site-packages/torch
```
and
<br>
```
/Users/<-USERNAME->/opt/anaconda3/envs/ptc/lib/python3.7/site-packages/torch-1.10.0a0+git30214ae-py3.7.egg-info
```
(or similar)<br>

And unzip it, and replace, if some pip or conda installer kill your installation to cpu version of Pytorch.<br>

____________________________________________
Option: switch Xcode back to the version 10.0.0:<br>
  
```
  sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
```

<br>
Good luck!<br>
2021.08.17<br>
silenzio<br>
<br>

