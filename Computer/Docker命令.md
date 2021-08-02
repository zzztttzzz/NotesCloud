# Docker命令

* `docker pull [imagename]`
  pull image
* `docker images`
  查看image
* `docker run -itd --name [specifiedName] [imagename] /bin/bash`
  使用交互式方式run一个image. `-i`交互式操作. `-t`终端. `-d`可以后台，不加`-d`直接进入image
* `docker ps -a`
  查看正在执行的container，`-a`可以查看已经退出的，从而后续可以使用`docker start [ID]`重新run.
* `docker exec -it [ID] /bin/bash`
  连接后台正在run的container
* `docker start [ID]`
  重新run已经退出的container
* `docker stop [ID]`
  中断某个container

