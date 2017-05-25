# Initial ubuntu 16.04
	sudo apt-get upgrade
	sudo apt-get update
	sudo apt-get install nvidia-375
	sudo apt-get install pip

# Instial ros-Kinetic
	sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list'
	sudo apt-key adv --keyserver hkp://ha.pool.sks-keyservers.net:80 --recv-key 421C365BD9FF1F717815A3895523BAEEB01FA116
	sudo apt-get update
	sudo apt-get install ros-kinetic-desktop-full
	sudo rosdep init
	rosdep update
	echo "source /opt/ros/kinetic/setup.bash" >> ~/.bashrc
	source ~/.bashrc
	source /opt/ros/kinetic/setup.bash
	sudo apt-get install python-rosinstall
# Initial cuda
https://developer.nvidia.com/cuda-downloads

	cd ~/Download
	sudo dpkg -i cuda-repo-ubuntu1604-8-0-local-ga2_8.0.61-1_amd64.deb
	sudo apt-get update
	sudo apt-get install cuda
# Initial cudnn
https://developer.nvidia.com/rdp/cudnn-download

	cd ~/Download
	sudo tar -xvzf cudnn-8.0-linux-x64-v5.1.tgz 
	sudo cp -P cuda/include/cudnn.h /usr/include
	sudo cp -P cuda/lib64/libcudnn* /usr/lib/x86_64-linux-gnu/
	sudo chmod a+r /usr/lib/x86_64-linux-gnu/libcudnn*
# Initial opencv
	cd ~
	git clone https://github.com/daveselinger/opencv.git
	cd opencv
	mkdir build
	sudo apt-get install cmake-gui
	sudo cmake-gui
select opencv and opencv/build->config->generate

	cd build
	sudo cmake ..
	sudo make -j8
	sudo make install
# Initial tensorflow
https://www.tensorflow.org/install/install_sources
	
	cd ~
	sudo apt-get install python-pip python-dev build-essential 
	git clone https://github.com/tensorflow/tensorflow 
	cd tensorflow
Install bazel

	echo "deb [arch=amd64] http://storage.googleapis.com/bazel-apt stable jdk1.8" | sudo tee /etc/apt/sources.list.d/bazel.list
	curl https://bazel.build/bazel-release.pub.gpg | sudo apt-key add -
	sudo apt-get update && sudo apt-get install bazel
	sudo apt-get upgrade bazel
	sudo apt-get install openjdk-8-jdk
	sudo apt-get install pkg-config zip g++ zlib1g-dev unzip
go to https://github.com/bazelbuild/bazel/releases download bazel

	cd ~/Download
	chmod +x bazel-<version>-installer-<os>.sh
	./bazel-<version>-installer-<os>.sh --user
	echo "export PATH=\"$PATH:$HOME/bin"" >> ~/.bashrc
 	sudo apt-get install python-numpy python-dev python-pip python-wheel
	sudo apt-get install libcupti-dev 
Install tensorflow

	cd tensorflow
	./configure
configure

	Please specify the location of python. [Default is /usr/bin/python]: /usr/bin/python2.7
	Please specify optimization flags to use during compilation when bazel option "--config=opt" is specified [Default is -march=native]:
	Do you wish to use jemalloc as the malloc implementation? [Y/n]
	jemalloc enabled
	Do you wish to build TensorFlow with Google Cloud Platform support? [y/N]
	No Google Cloud Platform support will be enabled for TensorFlow
	Do you wish to build TensorFlow with Hadoop File System support? [y/N]
	No Hadoop File System support will be enabled for TensorFlow
	Do you wish to build TensorFlow with the XLA just-in-time compiler (experimental)? [y/N]
	No XLA JIT support will be enabled for TensorFlow
	Found possible Python library paths:
	  /usr/local/lib/python2.7/dist-packages
	  /usr/lib/python2.7/dist-packages
	Please input the desired Python library path to use.  Default is [/usr/local/lib/python2.7/dist-packages]
	Using python library path: /usr/local/lib/python2.7/dist-packages
	Do you wish to build TensorFlow with OpenCL support? [y/N] N
	No OpenCL support will be enabled for TensorFlow
	Do you wish to build TensorFlow with CUDA support? [y/N] Y
	CUDA support will be enabled for TensorFlow
	Please specify which gcc should be used by nvcc as the host compiler. [Default is /usr/bin/gcc]:
	Please specify the Cuda SDK version you want to use, e.g. 7.0. [Leave empty to use system default]: 8.0
	Please specify the location where CUDA 8.0 toolkit is installed. Refer to README.md for more details. [Default is /usr/local/cuda]:
	Please specify the cuDNN version you want to use. [Leave empty to use system default]: 5
	Please specify the location where cuDNN 5 library is installed. Refer to README.md for more details. [Default is /usr/local/cuda]:
	Please specify a list of comma-separated Cuda compute capabilities you want to build with.
	You can find the compute capability of your device at: https://developer.nvidia.com/cuda-gpus.
	Please note that each additional compute capability significantly increases your build time and binary size.
	[Default is: "3.5,5.2"]: 3.0
	Setting up Cuda include
	Setting up Cuda lib
	Setting up Cuda bin
	Setting up Cuda nvvm
	Setting up CUPTI include
	Setting up CUPTI lib64
	Configuration finished
	
Build the pip package

	bazel build --config=opt --config=cuda //tensorflow/tools/pip_package:build_pip_package 
	bazel-bin/tensorflow/tools/pip_package/build_pip_package /tmp/tensorflow_pkg
	sudo pip install /tmp/tensorflow_pkg/tensorflow-1.1.0-py2-none-any.whl
