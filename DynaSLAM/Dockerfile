FROM tensorflow/tensorflow:latest-gpu-py3
MAINTAINER Kenan Deng <kenand@andrew.cmu.edu>

ENV OPENCV_VERSION=2.4.11
ENV EIGEN_VERSION=3.3.7
ENV EIGEN_URL=http://bitbucket.org/eigen/eigen/get/${EIGEN_VERSION}.tar.bz2
ENV DEBIAN_FRONTEND=noninteractive
ENV DOWNLOAD_PATH=/Download

#Essentail files
RUN apt-get update && \
	apt-get install -y build-essential && \
	apt-get install -y cmake && \
	apt-get install -y curl && \
	apt-get install -y gcc && \
	apt-get install -y git && \
	apt-get install -y libglew-dev


#OpenCV dependency
RUN apt-get install -y qt5-default libvtk6-dev && \
	apt-get install -y unzip wget && \
	apt-get install -y zlib1g-dev libpng12-dev libjpeg-dev libwebp-dev libpng-dev libtiff5-dev libjasper-dev libopenexr-dev libgdal-dev && \
	apt-get install -y libdc1394-22-dev libavcodec-dev libavformat-dev libswscale-dev libtheora-dev libvorbis-dev libxvidcore-dev libx264-dev yasm libopencore-amrnb-dev libopencore-amrwb-dev libv4l-dev libxine2-dev && \
	apt-get install -y libtbb-dev libeigen3-dev && \
	apt-get install -y python-dev python-tk python-numpy python3-dev python3-tk python3-numpy


#OpenCV
RUN mkdir ${DOWNLOAD_PATH} 
RUN cd ${DOWNLOAD_PATH} && \
	wget https://github.com/opencv/opencv/archive/${OPENCV_VERSION}.zip && \
	unzip ${OPENCV_VERSION}.zip && \
	rm ${OPENCV_VERSION}.zip && \
	mv opencv-${OPENCV_VERSION} OpenCV && \
	cd OpenCV && \
	mkdir build && \
	cd build && \
	cmake -DCMAKE_CXX_COMPILER=/usr/bin/g++ CMAKE_C_COMPILER=/usr/bin/gcc -DCMAKE_BUILD_TYPE=RELEASE -DCMAKE_INSTALL_PREFIX=/usr/local -DWITH_CUDA=OFF -DWITH_TBB=ON -DBUILD_NEW_PYTHON_SUPPORT=ON -DWITH_V4L=ON -DINSTALL_C_EXAMPLES=ON -DINSTALL_PYTHON_EXAMPLES=ON -DBUILD_EXAMPLES=ON -DWITH_QT=ON -DWITH_OPENGL=ON -DBUILD_FAT_JAVA_LIB=ON -DINSTALL_TO_MANGLED_PATHS=ON -DINSTALL_CREATE_DISTRIB=ON -DINSTALL_TESTS=ON -DENABLE_FAST_MATH=ON -DWITH_IMAGEIO=ON -DBUILD_SHARED_LIBS=OFF -DWITH_GSTREAMER=ON -DBUILD_TIFF=ON .. && \
	make -j4 && \ 
	make install && \
	ldconfig

#Eigen
RUN cd ${DOWNLOAD_PATH} && \
	wget http://bitbucket.org/eigen/eigen/get/${EIGEN_VERSION}.tar.bz2 && \
	mkdir eigen && \
	tar -xvjf ${EIGEN_VERSION}.tar.bz2 --strip-components=1 -C ./eigen &&\
	cd eigen && \
	mkdir build && \
	cd build && \
	cmake .. &&\
	make install

#Pangolin
RUN cd ${DOWNLOAD_PATH} && \
	git clone https://github.com/stevenlovegrove/Pangolin.git &&\
	cd Pangolin &&\
	mkdir build &&\
	cd build &&\
	cmake .. &&\
 	make

#Orb-Slam2
#The original has a small issue with missing 
#Import file https://github.com/raulmur/ORB_SLAM2/

RUN git clone https://github.com/dknyxh/ORB_SLAM2 ORB_SLAM2 &&\
	cd ORB_SLAM2 &&\
	chmod +x build.sh &&\
	./build.sh


