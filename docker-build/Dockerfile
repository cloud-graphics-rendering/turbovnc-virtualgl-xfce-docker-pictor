# noVNC + TurboVNC + VirtualGL
# http://novnc.com
# https://turbovnc.org
# https://virtualgl.org

# xhost +si:localuser:root
# openssl req -new -x509 -days 365 -nodes -out self.pem -keyout self.pem
# docker build -t benchvnc .

# docker run --init --runtime=nvidia --name=benchvnc-1 -it -v /tmp/.X11-unix/X0:/tmp/.X11-unix/X0 -v /etc/X11/xinit/xinitrc:/etc/X11/xinit/xinitrc -v $PWD/../supertuxkart-1.0-linux:/supertuxkart-1.0-linux -p 5901:5901 benchvnc
# docker run --init --runtime=nvidia --name=benchvnc-3 -it -v /tmp/.X11-unix/X0:/tmp/.X11-unix/X0 -v /etc/X11/xinit/xinitrc:/etc/X11/xinit/xinitrc -v /media/lty/newspace/BenchmarkFrameWork/BenchmarkSuite-Server:/BenchmarkSuite-Server -v /home/lty/Documents/0ad:/0ad -p 59002:5901 benchvnc
# docker run --init --runtime=nvidia --name=benchvnc-1 -it -v /tmp/.X11-unix/X0:/tmp/.X11-unix/X0 -v /etc/X11/xinit/xinitrc:/etc/X11/xinit/xinitrc -v $PWD/../../BenchmarkSuite-Server:/BenchmarkSuite-Server -v /home/lty/Documents/0ad:/0ad -p 59001:5901 benchvnc
# docker run --init --runtime=nvidia --name=benchvnc-1 -it -v /tmp/.X11-unix/X0:/tmp/.X11-unix/X0 -v /etc/X11/xinit/xinitrc:/etc/X11/xinit/xinitrc -v $PWD/../../BenchmarkSuite-Server:/BenchmarkSuite-Server -v /home/lty/.local/share/0ad/saves/savegame-0010.0adsave:/root/.local/share/0ad/saves/savegame-0010.0adsave -v $PWD/../autoexec.cfg:/root/.redeclipse/autoexec.cfg --net=host game-benchvnc

FROM nvidia/opengl:1.0-glvnd-runtime

ARG TURBOVNC_VERSION=2.1.91
ARG VIRTUALGL_VERSION=2.6
ARG LIBJPEG_VERSION=2.0.1

ENV NVIDIA_DRIVER_CAPABILITIES ${NVIDIA_DRIVER_CAPABILITIES},display

COPY turbovnc_2.1.91_amd64.deb /tmp
COPY virtualgl_2.6_amd64.deb /tmp
COPY libsodium.so.23.1.0 /usr/lib/x86_64-linux-gnu/libsodium.so.23.1.0
COPY libsodium.so.23.1.0 /usr/lib/x86_64-linux-gnu/libsodium.so.23.1.0
COPY libgloox.so.17.0.0 /usr/lib/x86_64-linux-gnu/libgloox.so.17.0.0
#COPY BenchmarkSuite-Server /
RUN ln -s /usr/lib/x86_64-linux-gnu/libsodium.so.23.1.0 /usr/lib/x86_64-linux-gnu/libsodium.so.23.1 && \
    ln -s /usr/lib/x86_64-linux-gnu/libsodium.so.23.1.0 /usr/lib/x86_64-linux-gnu/libsodium.so.23 && \
    ln -s /usr/lib/x86_64-linux-gnu/libsodium.so.23.1.0 /usr/lib/x86_64-linux-gnu/libsodium.so && \
    ln -s /usr/lib/x86_64-linux-gnu/libgloox.so.17.0.0 /usr/lib/x86_64-linux-gnu/libgloox.so.17.0 && \
    ln -s /usr/lib/x86_64-linux-gnu/libgloox.so.17.0.0 /usr/lib/x86_64-linux-gnu/libgloox.so.17 && \
    ln -s /usr/lib/x86_64-linux-gnu/libgloox.so.17.0.0 /usr/lib/x86_64-linux-gnu/libgloox.so && \
    apt-get update && apt-get install -y --no-install-recommends \
        ca-certificates \
        curl \
        gcc \
        libc6-dev \
        libglu1 \
        libglu1:i386 \
        libsm6 \
        libxv1 \
        libxv1:i386 \
        make \
        vim \
        net-tools \
        python \
        gdebi-core \
        libsdl2-mixer-2.0-0 \
        libsdl2-image-2.0-0 \
        libsdl2-2.0-0 \
        libenet-dev \
        libboost-dev \
        libboost-filesystem-dev \
        libcurl4-gnutls-dev \
        libicu-dev \
        libminiupnpc-dev \
        libnspr4-dev \
        libnvtt-dev \
        libogg-dev \
        libopenal-dev \
        libpng-dev \
        libsdl2-dev \
        libvorbis-dev \
        libwxgtk3.0-dev \
        libxcursor-dev \
        libxml2-dev \
        subversion \
        zlib1g-dev \
        x11-xkb-utils \
        xauth \
        xfonts-base \
        xkb-data && \
    rm -rf /var/lib/apt/lists/* && \
    cd /tmp && \
    mkdir vgl && \
    curl -fsSL -O https://svwh.dl.sourceforge.net/project/libjpeg-turbo/${LIBJPEG_VERSION}/libjpeg-turbo-official_${LIBJPEG_VERSION}_amd64.deb \
               -O http://mirrors.kernel.org/ubuntu/pool/main/u/udev/libudev0_175-0ubuntu9_amd64.deb && \
    gdebi -n libudev0_175-0ubuntu9_amd64.deb && \
    rm -f /tmp/libudev0_175-0ubuntu9_amd64.deb && \
    dpkg -i *.deb && \
    rm -f /tmp/*.deb && \
    sed -i 's/$host:/unix:/g' /opt/TurboVNC/bin/vncserver && \
    apt-get clean && apt-get update && apt-get install -y locales && \
    locale-gen en_US.UTF-8 && \
    apt-get install -y --no-install-recommends xfce4 && \
    apt-get install -y --no-install-recommends gtk3-engines-xfce xfce4-notifyd \
      mousepad xfce4-taskmanager xfce4-terminal libgtk-3-bin

# Define working directory.
WORKDIR /data

# Define commonly used JAVA_HOME variable
ENV CGR_BENCHMARK_PATH /BenchmarkSuite-Server
ENV PATH ${PATH}:/opt/VirtualGL/bin:/opt/TurboVNC/bin

EXPOSE 5901
ENV DISPLAY :1

# Define default command.
CMD ["/bin/bash"]