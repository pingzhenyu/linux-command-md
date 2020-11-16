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
