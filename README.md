# ros-rviz-docker

## Install Docker
https://docs.docker.com/engine/install/ubuntu/

## Install Nvidia Docker Drivers
https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker

## Try to launch
`sudo docker run --rm --runtime=nvidia --gpus all nvidia/cuda:9.2-base-ubuntu18.04 nvidia-smi`

## Launch roscore
`docker build -t roscore_c .`

`docker run -it --rm --privileged --net=host roscore_c /bin/bash`

## Launch rviz (another terminal window)
`docker build -t rviz_c .`

`xhost +local:docker`

`docker run -it --rm --privileged --net=host --env=NVIDIA_VISIBLE_DEVICES=all --env=NVIDIA_DRIVER_CAPABILITIES=all --env=DISPLAY --env=QT_X11_NO_MITSHM=1 -v /tmp/.X11-unix:/tmp/.X11-unix --runtime=nvidia -e NVIDIA_VISIBLE_DEVICES=0 rviz_c /bin/bash`

## Create empty world (in next terminal)
`docker build -t rviz_c .`

`rosrun tf static_transform_publisher 0 0 0 0 0 0 1 map world 5`
