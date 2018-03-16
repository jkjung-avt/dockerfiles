## Dockerfile to build opencv with python3 binding and with CUDA support

FROM nvidia/cuda:9.0-devel

# ARG https_proxy
# ARG http_proxy

ARG DEBIAN_FRONTEND=noninteractive
ARG OPENCV_VERSION=3.4.0
ARG OPENCV_INSTALL_PATH=/usr/local

RUN ln -sf cuda-9.0 /usr/local/nvidia && \
    apt-get update && \
    apt-get purge -y python-numpy python3-numpy && \
    apt-get install -y apt-utils && \
    apt-get install -y --only-upgrade g++-5 cpp-5 gcc-5 && \
    apt-get install -y wget curl rsync git zip unzip \
                       build-essential make cmake cmake-curses-gui \
                       pkg-config vim yasm \
                       g++ libavformat-dev libavutil-dev \
                       libswscale-dev libv4l-dev libeigen3-dev \
                       libglew-dev libgtk2.0-dev \
                       libdc1394-22-dev libxine2-dev \
                       libgstreamer1.0-dev \
                       libgstreamer-plugins-base1.0-dev \
                       libjpeg8-dev libjpeg-turbo8-dev libtiff5-dev \
                       libjasper-dev libpng12-dev libavcodec-dev \
                       zlib1g-dev  \
                       libxvidcore-dev libx264-dev libgtk-3-dev \
                       libatlas-base-dev gfortran \
                       qt5-default \
                       python3-dev python3-pip python3-tk && \
    pip3 install -U pip && \
    pip3 install numpy matplotlib && \
    ## Cleanup
    apt-get clean && \
    rm -rf /var/lib/apt/lists/*

WORKDIR /

## Build opencv (CUDA_ARCH_BIN="6.1" is for GTX-1080)
RUN wget https://github.com/opencv/opencv/archive/$OPENCV_VERSION.zip && \
    unzip $OPENCV_VERSION.zip && \
    mkdir -p /opencv-$OPENCV_VERSION/build && \
    cd /opencv-$OPENCV_VERSION/build && \
    cmake -D CMAKE_BUILD_TYPE=RELEASE -D CMAKE_INSTALL_PREFIX=/usr/local \
          -D WITH_CUDA=ON -D CUDA_ARCH_BIN="6.1" -D CUDA_ARCH_PTX="" \
          -D WITH_CUBLAS=ON -D ENABLE_FAST_MATH=ON -D CUDA_FAST_MATH=ON \
          -D WITH_LIBV4L=ON -D BUILD_TESTS=OFF \
          -D BUILD_PERF_TESTS=OFF -D BUILD_EXAMPLES=OFF \
          -D BUILD_opencv_python2=OFF -D BUILD_opencv_python3=ON \
          -D WITH_QT=ON -D WITH_OPENGL=ON .. && \
    make -j4 install && \
    rm /$OPENCV_VERSION.zip && \
    rm -r /opencv-$OPENCV_VERSION

## Compress the opencv files so we can extract them from the container easily 
# RUN tar cvzf opencv-$OPENCV_VERSION.tar.gz --directory=$OPENCV_INSTALL_PATH .
