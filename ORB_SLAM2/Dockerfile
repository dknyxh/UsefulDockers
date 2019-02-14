FROM ubuntu:16.04
MAINTAINER Kenan Deng <kenand@andrew.cmu.edu>

ENV OPENCV_VERSION=3.4.2
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
	cmake -DWITH_QT=ON -DWITH_OPENGL=ON -DFORCE_VTK=ON -DWITH_TBB=ON -DWITH_GDAL=ON -DBUILD_TIFF=ON -DWITH_XINE=ON -DBUILD_EXAMPLES=ON -DENABLE_PRECOMPILED_HEADERS=OFF .. && \
	make -j4 && \ 
	make install && \
	ldconfig



