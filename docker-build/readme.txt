How to set up the server:
    1. use lightdm instead of gdm on Ubuntu
       On ubuntu16.04: sudo apt-get -y install lightdm
       On ubuntu18   : sudo apt-get -y install slick-greeter

    2. make sure there is /etc/lightdm/lightdm.conf file
       if there is no such file, add the following contents to the file. cat /etc/lightdm/lightdm.conf
[SeatDefaults]
[Seat:seat*]
greeter-setup-script=xhost +LOCAL

How to pull the docker images:
    docker pull bme855/game-benchvnc

How to run docker image:
    docker run --init --runtime=nvidia --name=benchvnc-1 --rm -it -v /tmp/.X11-unix/X0:/tmp/.X11-unix/X0 -v /etc/X11/xinit/xinitrc:/etc/X11/xinit/xinitrc -v $PWD/../../BenchmarkSuite-Server:/BenchmarkSuite-Server -v $PWD/../savegame-0010.0adsave:/root/.local/share/0ad/saves/savegame-0010.0adsave -v $PWD/../autoexec.cfg:/root/.redeclipse/autoexec.cfg --net=host game-benchvnc

How to build:
    docker build -t benchvnc .
