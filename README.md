# Installing-Pytorch-with-CUDA-on-a-2013-Macbook-Pro-Retina-15
Installing process based on: https://www.cs.rochester.edu/u/kautz/Installing-Pytorch-Cuda-on-Macbook.html

These instructions have been tested for:

<blockquote>
OS : MacOS High Sierra 10.13.6 (17G14042)<br>
GPU Driver: NVIDIA Web Driver 387.10.10.10.4.140<br>
GPU CUDA Driver Version: 418.105<br>
Xcode Version: 10.1 (10B61)<br>
</blockquote>


**Step 1: Downgrade to High Sierra 10.13.6 (17G14042)**
Check that you are running Mac OS X High Sierra (10.13.6). If you have an older version, upgrade. If you have a newer version you will need to downgrade; Apple banished CUDA with Mojave and later versions of the OS. Downgrading OS X requires <a href="https://www.macworld.co.uk/how-to/mac-software/downgrade-macos-mojave-3581872/">creating a bootable USB memory stick installer and erasing your laptop's hard disk</a>

**Step 2: Downgrade Xcode**
Make developer acc at first, then go to https://developer.apple.com/download/all/ and download Xcode version 9.4. 
Direct link: https://download.developer.apple.com/Developer_Tools/Command_Line_Tools_macOS_10.13_for_Xcode_9.4/Command_Line_Tools_macOS_10.13_for_Xcode_9.4.dmg

**Step 3: Install NVIDIA Drivers**


