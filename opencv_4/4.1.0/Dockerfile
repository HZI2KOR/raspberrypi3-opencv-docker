FROM --platform=linux/arm/v7 resin/raspberrypi3-python:2.7

# Update the Debian repository sources list to point to archived repositories
RUN printf "deb [trusted=yes] http://archive.debian.org/debian/ jessie main\n\
deb-src [trusted=yes] http://archive.debian.org/debian/ jessie main\n\
deb [trusted=yes] http://archive.debian.org/debian-security/ jessie/updates main\n\
deb-src [trusted=yes] http://archive.debian.org/debian-security/ jessie/updates main" > /etc/apt/sources.list

# Install dependencies needed for building and running OpenCV
RUN apt-get update && apt-get install -y --no-install-recommends \
    wget \
    unzip \
    build-essential cmake pkg-config \
    checkinstall yasm \
    libjpeg-dev libtiff-dev libjasper-dev libpng12-dev libtiff5-dev \
    libavcodec-dev libavformat-dev libswscale-dev \
    libxine2-dev libv4l-dev \
    libgstreamer0.10-dev libgstreamer-plugins-base0.10-dev \
    libgtk2.0-dev \
    libatlas-base-dev gfortran \
    libtbb2 libtbb-dev qt5-default \
    libmp3lame-dev libtheora-dev \
    libvorbis-dev libxvidcore-dev libx264-dev \
    libopencore-amrnb-dev libopencore-amrwb-dev \
    libavresample-dev \
    x264 v4l-utils \
    && rm -rf /var/lib/apt/lists/* \
    && apt-get -y autoremove

# Create a symlink for videodev.h
RUN ln -s -f /usr/include/linux/libv4l1-videodev.h /usr/include/linux/videodev.h

# Install Python packages
RUN pip install --no-cache-dir \
    numpy \
    ipython \
    && find /usr/local \
       \( -type d -a -name test -o -name tests \) \
       -o \( -type f -a -name '*.pyc' -o -name '*.pyo' \) \
       -exec rm -rf '{}' + \
    && rm -rf /usr/src/python ~/.cache

# Install OpenCV
COPY download_build_install_opencv.sh download_build_install_opencv.sh
RUN ./download_build_install_opencv.sh
