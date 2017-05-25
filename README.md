# Initial ubuntu 16.04
	sudo apt-get upgrade
	sudo apt-get update
	sudo apt-get install nvidia-375

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
#select opencv and opencv/build
#config
#generate

	cd build
	sudo cmake ..
	sudo make -j8
	sudo make install
# Initial tensorflow
