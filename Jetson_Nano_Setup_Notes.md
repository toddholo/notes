NVIDIA SDK Manager  

MAJOR NOTE: the SDK Manager is for a desktop machine - NOT the Jetson Nano

https://developer.nvidia.com/EMBEDDED/downloads  
https://developer.nvidia.com/nvidia-sdk-manager 
https://docs.nvidia.com/sdk-manager/download-run-sdkm/index.html  

From a terminal window, install the Debian package with the command: 
```
sudo apt install ./sdkmanager_[version]-[build#]_amd64.deb
```
Launch  

```
sdkmanager
```



A very Manual way to set up the JN  
Source:  
https://www.pyimagesearch.com/2020/03/25/how-to-configure-your-nvidia-jetson-nano-for-computer-vision-and-deep-learning/

JetPack 4.4

Set up SSH for headless  

Get JN NAME  

~~~
 whoami
~~~
  
Get IPADDRESS from Router or from JN terminal type  

```
ifconfig
```

Login from another computer

```
ssh NAME@IPADDRESS
```

Do your business  

Set the JN to use maximum power  

```
sudo nvpmodel -m 0
sudo jetson_clocks
```

Remove Libre Office  

```
sudo apt-get purge libreoffice*
sudo apt-get clean
```

Don't do this  
Update System  

```
sudo apt-get update && sudo apt-get upgrade
```

Install dev tools  

```
sudo apt-get install git cmake
sudo apt-get install libatlas-base-dev gfortran
sudo apt-get install libhdf5-serial-dev hdf5-tools
sudo apt-get install python3-dev
sudo apt-get install nano locate
```

SciPy prerequisites & system level Cython Library  

```
sudo apt-get install libfreetype6-dev python3-setuptools
sudo apt-get install protobuf-compiler libprotobuf-dev openssl
sudo apt-get install libssl-dev libcurl4-openssl-dev
sudo apt-get install cython3
```
Add XML tools for wotking with TF object detection  

```
sudo apt-get install libxml2-dev libxslt1-dev
```

Update CMake for compliling openCV  

```
wget http://www.cmake.org/files/v3.13/cmake-3.13.0.tar.gz
tar xpvf cmake-3.13.0.tar.gz cmake-3.13.0/
```

Compile CMake  

```
cd cmake-3.13.0/
./bootstrap --system-curl
make -j4
```

update the bash profile  

```
echo 'export PATH=/home/nvidia/cmake-3.13.0/bin/:$PATH' >> ~/.bashrc
source ~/.bashrc
```

Install OpenCV and dependancies  

```
sudo apt-get install build-essential pkg-config
sudo apt-get install libtbb2 libtbb-dev
```

Codecs and image libraries  

```
sudo apt-get install libavcodec-dev libavformat-dev libswscale-dev
sudo apt-get install libxvidcore-dev libavresample-dev
sudo apt-get install libtiff-dev libjpeg-dev libpng-dev
```

GUI libraries  

```
sudo apt-get install python-tk libgtk-3-dev
sudo apt-get install libcanberra-gtk-module libcanberra-gtk3-module
```

Video4Linux  

```
sudo apt-get install libv4l-dev libdc1394-22-dev
```

Install pip  

```
wget https://bootstrap.pypa.io/get-pip.py
sudo python3 get-pip.py
rm get-pip.py
```

If this error appears  
```
WARNING: The directory '/home/$USERNAME/.cache/pip' or its parent directory is not owned or is not writable by the current user. The cache has been disabled. Check the permissions and owner of that directory. If executing pip with sudo, you may want sudo's -H flag.
```
try  

```
sudo chown -R $USERNAME /home/$USERNAME/.cache/pip
```

sudo chown -R todd /Users/todd/Library/Caches/pip  

Setup Virtual Env   

```
sudo pip install virtualenv virtualenvwrapper
```

Add virtualenvwrapper information to ~/.bash  

```
nano ~/.bashrc
```

add the following to the end of the document  

```
# virtualenv and virtualenvwrapper
export WORKON_HOME=$HOME/.virtualenvs
export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python3
source /usr/local/bin/virtualenvwrapper.sh
export PATH=/home/nvidia/cmake-3.13.0/bin/:$PATH
```

save and exit  

load the bash profile  

```
source ~/.bashrc
```

Create Virtual Environments  
Some Helpful Commands  

Create a Python virtual environment  
```
mkvirtualenv $ENVNAME -p python3
```

List virtual environments installed on your system  
```
lsvirtualenv
```

Remove a virtual environment  
```
rmvirtualenv $ENVNAME
```

Activate a Python virtual environment  
```
workon $ENVNAME
```

Exits the virtual environment taking you back to your system environment  
```
deactivate
```

Create an env  

```
mkvirtualenv py3cv4 -p python3
```

Install the Protobuf Compiler  

```
wget https://raw.githubusercontent.com/jkjung-avt/jetson_nano/master/install_protobuf-3.6.1.sh
sudo chmod +x install_protobuf-3.6.1.sh
./install_protobuf-3.6.1.sh
```

This may take a long time - get a coffee or tea.todd

install protobuf in your Virtual ENV

```
workon py3cv4 # if you aren't inside the environment
cd ~
cp -r ~/src/protobuf-3.6.1/python/ .
cd python
python setup.py install --cpp_implementation
```

Install TensorFlow, Keras, NumPy, and SciPy


