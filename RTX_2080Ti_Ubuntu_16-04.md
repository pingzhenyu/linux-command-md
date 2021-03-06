# Install CUDA enabled TensorFlow GPU for NVidia RTX 2080 Ti

For many reasons, it is better to use Ubuntu 16.04 LTS (most probably 18.04 would also work).

It is essential to have precise versions of drivers, CUDA, cuDNN, and Tensorflow otherwise, it will not work correctly.

Tensorflow GPU 1.14.0
NVidia driver 410.57
CUDA toolkit 10.0 (V10.0.130)
cuDNN 7.6.2.24 for CUDA 10.0

First download
- [NVidia driver](https://www.nvidia.com/download/driverResults.aspx/138279/en-us)
- [CUDA 10.0](https://developer.nvidia.com/cuda-10.0-download-archive?target_os=Linux) - Linux > x86_64 - Ubuntu - 16.04 - runfile (local)
- [cuDNN library](https://developer.nvidia.com/rdp/cudnn-download) - download runtime library, developer library and code samples (optional)

Create `blacklist-nouveau.conf` in CUDA toolkit folder:
```
blacklist nouveau
options nouveau modeset=0
```


## Prepare for installation

If you have any drivers on your computer, or having some older or newer version of CUDA, cuDNN or TensorFlow uninstall it first.

Start with Python2 and Python3 libraries:

```sh
pip uninstall tensorflow tensorflow-gpu
pip3 uninstall tensorflow tensorflow-gpu
```

Then uninstall if possible Nvidia from the computer, purge and reboot:

```sh
sudo nvidia-uninstall
sudo apt purge nvidia*
sudo apt autoremove
reboot
```

## Install NVidia driver

Next time the computer boot without drivers in poor resolution. Install the correct driver first. 

```sh
sudo chmod +x NVIDIA-Linux-x86_64-410.57.run
sudo ./NVIDIA-Linux-x86_64-410.57.run --no-x-check
```

In the beginning, you will be informed that something went wrong, choose to continue. After the driver installs, press no to update X server and reboot (maybe it is not necessary).

After login, you can test the driver with `nvidia-smi` to check the version of the driver, that is `410.57`.

## Install CUDA toolkit

Copy the `blacklist-nouveau.conf` into your home folder.

Enter a TTY with <kbd>CTRL</kbd>+<kbd>ALT</kbd>+<kbd>F1</kbd>, where:

```sh
sudo service lightdm stop
sudo -i
cd /home/michal
sudo cp ~/blacklist-nouveau.conf /etc/modprobe.d
sudo update-initramfs -u
exit
sudo chmod +x cuda_10.0.130_410.48_linux.run
sudo sh cuda_10.0.130_410.48_linux.run
reboot
```

When rebooted you need to add you CUDA into you paths in `.bashrc` with these entries:

```
# CUDA and CUDNN paths
export PATH=$PATH:/usr/local/cuda-10.0/bin
export CUDADIR=/usr/local/cuda-10.0
export LD_LIBRARY_PATH=$LD_LIBRARY_PATH:/usr/local/cuda-10.0/lib64
```

After sourcing `source ~/.bashrc` or opening new terminal you can verify the installation with `nvcc --version` which should give a version 10.0.

## Install cuDNN library

Install all three deb packages.

```sh
sudo dpkg -i libcudnn7_7.6.2.24-1+cuda10.0_amd64.deb
sudo dpkg -i libcudnn7-dev_7.6.2.24-1+cuda10.0_amd64.deb
sudo dpkg -i libcudnn7-doc_7.6.2.24-1+cuda10.0_amd64.deb
reboot
```

## Install Tensorflow for GPU

In the end, you just now install a specific version of Tensorflow, and you are ready to go:

```sh
pip3 install --user tensorflow-gpu==1.14.0
```

Of course, you can do the same for Python2; this specific version of Tensorflow should be compatible with Python 2.7 and Python 3.3 - 3.7.

To verify the installation, go for the terminal and open Python console. Then import TensorFlow and try GPU detection test.

```python
import tensorflow as tf
tf.test.test.is_gpu_available()
```

You should get `True` if everything went OK. Otherwise, you start with uninstalling all things and follow the tutorial from the beginning.

## Troubleshooting 

### Login loop
If you stuck in the login loop after updating your computer, all you need to do is to reinstall the driver.

### Adjust DPI for 4K display

```sh
sudo apt-get install dconf-editor
sudo xhost +SI:localuser:lightdm
sudo su lightdm -s /bin/bash
dconf-editor
```

Navigateto `com` - `canonical` - `unity-greeter` and change the `xft-dpi`.

132 is good for ful HD
184 is good for 4K

For more info how to compute DPI see [this](https://metebalci.com/blog/using-ubuntu-16-on-hidpi-and-4k-displays/)



# Installing cuDNN On Linux
## 2.1. Prerequisites
Ensure you meet the following requirements before you install cuDNN.
For the latest compatibility software versions of the OS, CUDA, the CUDA driver, and the NVIDIA hardware, see the cuDNN Support Matrix.

### 2.1.1. Installing NVIDIA Graphics Drivers
About this task
Install up-to-date NVIDIA graphics drivers on your Linux system.

Procedure
Go to: NVIDIA download drivers
Select the GPU and OS version from the drop-down menus.
Download and install the NVIDIA graphics driver as indicated on that web page. For more information, select the ADDITIONAL INFORMATION tab for step-by-step instructions for installing a driver.
Restart your system to ensure the graphics driver takes effect.
### 2.1.2. Installing The CUDA Toolkit For Linux
About this task
Refer to the following instructions for installing CUDA on Linux, including the CUDA driver and toolkit: NVIDIA CUDA Installation Guide for Linux.

## 2.2. Downloading cuDNN For Linux
Before you begin
In order to download cuDNN, ensure you are registered for the NVIDIA Developer Program.

Procedure
Go to: NVIDIA cuDNN home page.
Click Download.
Complete the short survey and click Submit.
Accept the Terms and Conditions. A list of available download versions of cuDNN displays.
Select the cuDNN version you want to install. A list of available resources displays.

## 2.3. Installing cuDNN On Linux
About this task
The following steps describe how to build a cuDNN dependent program. Choose the installation method that meets your environment needs. For example, the tar file installation applies to all Linux platforms, and the Debian installation package applies to Ubuntu 16.04 and 18.04.

In the following sections:
your CUDA directory path is referred to as /usr/local/cuda/
your cuDNN download path is referred to as <cudnnpath>

### 2.3.1. Installing From A Tar File
Before issuing the following commands, you'll need to replace x.x and v8.x.x.x with your specific CUDA version and cuDNN version and package date.
Procedure
Navigate to your <cudnnpath> directory containing the cuDNN Tar file.
Unzip the cuDNN package.
```sh
$ tar -xzvf cudnn-x.x-linux-x64-v8.x.x.x.tgz
```
  
Copy the following files into the CUDA Toolkit directory, and change the file permissions.
```sh
$ sudo cp cuda/include/cudnn*.h /usr/local/cuda/include
$ sudo cp cuda/lib64/libcudnn* /usr/local/cuda/lib64
$ sudo chmod a+r /usr/local/cuda/include/cudnn*.h /usr/local/cuda/lib64/libcudnn*
```
### 2.3.2. Installing From A Debian File
Before issuing the following commands, you'll need to replace x.x and 8.x.x.x with your specific CUDA version and cuDNN version and package date.
About this task
Procedure
Navigate to your <cudnnpath> directory containing the cuDNN Debian file.
Install the runtime library, for example:
```sh
sudo dpkg -i libcudnn8_x.x.x-1+cudax.x_amd64.deb
Install the developer library, for example:
sudo dpkg -i libcudnn8-dev_8.x.x.x-1+cudax.x_amd64.deb
Install the code samples and the cuDNN library documentation, for example:
sudo dpkg -i libcudnn8-samples_8.x.x.x-1+cudax.x_amd64.deb
```

### 2.3.3. Installing From An RPM File
About this task
Procedure
Download the rpm package libcudnn*.rpm to the local path.
Install the rpm package from the local path. This will install the cuDNN libraries.
```sh
rpm -ivh libcudnn8-*.x86_64.rpm
rpm -ivh libcudnn8-devel-*.x86_64.rpm
rpm -ivh libcudnn8-samples-*.x86_64.rpm
```

## 2.4. Verifying The cuDNN Install On Linux
About this task
To verify that cuDNN is installed and is running properly, compile the mnistCUDNN sample located in the /usr/src/cudnn_samples_v8 directory in the Debian file.

Procedure
```sh
Copy the cuDNN sample to a writable path.
$cp -r /usr/src/cudnn_samples_v8/ $HOME
Go to the writable path.
$ cd  $HOME/cudnn_samples_v8/mnistCUDNN
Compile the mnistCUDNN sample.
$make clean && make
Run the mnistCUDNN sample.
$ ./mnistCUDNN
```
If cuDNN is properly installed and running on your Linux system, you will see a message similar to the following:
Test passed!

## 2.5. Upgrading From v7 To v8
Since version 8 can coexist with previous versions of cuDNN, if the user has an older version of cuDNN such as v6 or v7, installing version 8 will not automatically delete an older revision. Therefore, if the user wants the latest version, install cuDNN version 8 by following the installation steps.
```sh
About this task
To upgrade from v7 to v8 for RHEL, run:
sudo rpm --upgrade *.rpm
To upgrade from v7 to v8 for Ubuntu, run:
sudo dpkg -i libcudnn*.deb
```

To switch between v7 and v8 installations, issue sudo update-alternatives --config libcudnn and choose the appropriate cuDNN version.

## 2.6. Troubleshooting
About this task
Join the NVIDIA Developer Forum to post questions and follow discussions.

