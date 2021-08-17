# Installing-Pytorch-with-CUDA-on-a-2013-Macbook-Pro-Retina-15
Installing process based on: https://www.cs.rochester.edu/u/kautz/Installing-Pytorch-Cuda-on-Macbook.html

These instructions have been tested for:

<blockquote>
OS : MacOS High Sierra 10.13.6 (17G14042)<br>
GPU Driver: NVIDIA Web Driver 387.10.10.10.4.140<br>
GPU CUDA Driver Version: 418.105<br>
Xcode Version: 10.1 (10B61)<br>
Python 3.7.11<br>
</blockquote>
<br>

**Step 1: Downgrade to High Sierra 10.13.6 (17G14042)<br>**
Check that you are running Mac OS X High Sierra (10.13.6). If you have an older version, upgrade. If you have a newer version you will need to downgrade; Apple banished CUDA with Mojave and later versions of the OS. Downgrading OS X requires <a href="https://www.macworld.co.uk/how-to/mac-software/downgrade-macos-mojave-3581872/">creating a bootable USB memory stick installer and erasing your laptop's hard disk</a>
<br><br>

**Step 2: Downgrade Xcode<br>**
Make developer acc at first, then go to https://developer.apple.com/download/all/ and download Xcode version 9.4. 
<a href="https://download.developer.apple.com/Developer_Tools/Command_Line_Tools_macOS_10.13_for_Xcode_9.4/Command_Line_Tools_macOS_10.13_for_Xcode_9.4.dmg">( direct link )</a>
<br><br>
Install Xcode version 9.4.<br>
<br>

Then switch to Xcode version 9.4:<br>
>sudo xcode-select --switch /Library/Developer/CommandLineTools
<br>

(Switch Xcode back to the version 10.0.0:<br>
>sudo xcode-select --switch /Applications/Xcode.app/Contents/Developer
<br>

You can check current version of Xcode by:<br>
>clang --version

<br>
Should be:<br>

>
>Apple LLVM version 9.1.0 (clang-902.0.39.2)<br>
>Target: x86_64-apple-darwin17.7.0<br>
>Thread model: posix<br>
>InstalledDir: /Library/Developer/CommandLineTools/usr/bin
>
Don't think about 9.4 == 9.1. ( It's OK 8; )
<br><br>

**Step 3: Install NVIDIA Drivers**
Install the <a href="https://images.nvidia.com/mac/pkg/387/WebDriver-387.10.10.10.40.140.pkg">NVIDIA Quadro and Geforce OS X Driver 387.10.10.10.40.140</a>

Add to your .profile<br>
>nano ~/.bash_profile
<br>

this two lines:<br>

<blockquote>export PATH=/Developer/NVIDIA/CUDA-10.0/bin${PATH:+:${PATH}}
export DYLD_LIBRARY_PATH=/usr/local/cuda/lib:$DYLD_LIBRARY_PATH
</blockquote>

and **reboot your Mac**
<br><br>

**Step 4: Download NVIDIA CUDA Toolkit 10.0 Archive<br>**

Download installer <a href="https://developer.nvidia.com/cuda-10.0-download-archive?target_os=MacOSX&target_arch=x86_64&target_version=1013">NVIDIA CUDA Toolkit 10.0 </a>(1,8 GB)<br>

![DownloadCUDAToolkit_sm](https://user-images.githubusercontent.com/7931919/129793652-02818cad-e510-4b40-9bf4-536121342d58.png)

Install to "/Developer/NVIDIA/CUDA-10.0"
<br><br>

**Step 5: Install NVIDIA cuDNN 7.6.5<br>**
Download installer zip file - <a href="https://developer.nvidia.com/compute/machine-learning/cudnn/secure/7.6.5.32/Production/10.0_20191031/cudnn-10.0-osx-x64-v7.6.5.32.tgz">cudnn-10.0-osx-x64-v7.6.5.32.tgz</a> (654,8 MB)<br>
Unzip to "/usr/local/cuda/lib"<br>
<br>
There are two directories with files:<br>

>/include<br>
>cudnn.h<br>

and<br>

>/lib<br>
>libcudnn.7.dylib<br>
>libcudnn.dylib<br>
>libcudnn_static.a<br>
<br>

Then make a alias (symlink) of "libcuda.dylib" as name "libcuda.so.1"<br>

>cd /usr/local/cuda/lib/<br>
>ln -s libcuda.dylib libcuda.so.1<br>
<br>

**Step 6: Install Conda<br>**
Install <a href="https://www.anaconda.com/distribution/">Anaconda</a>. Create an environment named ptc that includes pip, activate it, and install libraries:

>conda create --name ptc python=3.7<br>
>conda activate ptc<br>
>conda install numpy ninja pyyaml mkl mkl-include setuptools cmake cffi typing_extensions future six requests dataclasses intel-openmp<br>
>conda install torchvision<br>
>conda install pkg-config libuv<br>
<br>


**Step 7: Build Pytorch<br>**



