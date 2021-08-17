# Installing-Pytorch-with-CUDA-on-a-2013-Macbook-Pro-Retina-15
Installing process based on: https://www.cs.rochester.edu/u/kautz/Installing-Pytorch-Cuda-on-Macbook.html

These instructions have been tested for:

<br>
<blockquote>
OS : MacOS High Sierra 10.13.6 (17G14042)<br>
GPU Driver: NVIDIA Web Driver 387.10.10.10.4.140<br>
GPU CUDA Driver Version: 418.105<br>
Xcode Version: 10.1 (10B61)<br>
</blockquote>
<br>

**Step 1: Downgrade to High Sierra 10.13.6 (17G14042)<br>**
Check that you are running Mac OS X High Sierra (10.13.6). If you have an older version, upgrade. If you have a newer version you will need to downgrade; Apple banished CUDA with Mojave and later versions of the OS. Downgrading OS X requires <a href="https://www.macworld.co.uk/how-to/mac-software/downgrade-macos-mojave-3581872/">creating a bootable USB memory stick installer and erasing your laptop's hard disk</a>
<br><br>

**Step 2: Downgrade Xcode<br>**
Make developer acc at first, then go to https://developer.apple.com/download/all/ and download Xcode version 9.4. 
Direct link: https://download.developer.apple.com/Developer_Tools/Command_Line_Tools_macOS_10.13_for_Xcode_9.4/Command_Line_Tools_macOS_10.13_for_Xcode_9.4.dmg
<br><br>

**Step 3: Install NVIDIA Drivers**
Install the <a href="https://images.nvidia.com/mac/pkg/387/WebDriver-387.10.10.10.40.140.pkg">NVIDIA Quadro and Geforce OS X Driver 387.10.10.10.40.140</a>

Add to your .profile ( >_nano ~/.bash_profile_ ) two lines:

<blockquote>export PATH=/Developer/NVIDIA/CUDA-10.0/bin${PATH:+:${PATH}}
export DYLD_LIBRARY_PATH=/usr/local/cuda/lib:$DYLD_LIBRARY_PATH
</blockquote>

and **reboot your Mac**
<br><br>

**Step 4: Download NVIDIA CUDA Toolkit 10.0 Archive<br>**

Download installer zip file - <a href="https://developer.nvidia.com/cuda-10.0-download-archive?target_os=MacOSX&target_arch=x86_64&target_version=1013">NVIDIA CUDA Toolkit 10.0 </a>

![DownloadCUDAToolkit_sm](https://user-images.githubusercontent.com/7931919/129792909-49316a74-eb5c-4da2-9821-14faa2295ccf.png)


Install to "/Developer/NVIDIA/CUDA-10.0"


**Step 5: Install NVIDIA cuDNN 7.6.5<br>**
Download installer zip file - <a href="https://developer.nvidia.com/compute/machine-learning/cudnn/secure/7.6.5.32/Production/10.0_20191031/cudnn-10.0-osx-x64-v7.6.5.32.tgz">cudnn-10.0-osx-x64-v7.6.5.32.tgz</a>
Unzip to "/usr/local/cuda/lib"






