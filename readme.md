[English doc]:https://github.com/LomotHo/minecraft-bedrock
[中文文档]:https://github.com/LomotHo/minecraft-bedrock/blob/master/readme_zh.md
[旧版文档]:https://github.com/LomotHo/minecraft-bedrock/blob/master/doc/zh/
[Docker Pulls]:https://img.shields.io/docker/pulls/lomot/minecraft-bedrock.svg
[How to install Docker]:https://docs.docker.com/install/linux/docker-ce/ubuntu/

[English doc] | [中文文档] | [旧版文档]

![Docker Pulls]

# a bedrock minecraft PE Server on docker
this documentation is for image lomot/minecraft-bedrock:1.10.0.7-r1, lomot/minecraft-bedrock:1.10.0.7-debian-r1

## start a server quickly
1. install docker on your server

  ```bash
  apt install docker.io
  ```
  or you can follow this documentation : [How to install Docker]

2. create folder for server data

  this folder is for your map data and some configuration files, it contains ```ops.json```,``` permissions.json```,```server.properties```,```whitelist.json```,```worlds```, if you use an empty folder, all the file will be created automatically, ```/opt/mcpe-data``` for an example

  ```bash
  mkdir -p /opt/mcpe-data
  ```

3. deploy the server

  ```bash
  docker run -d -it --name mcpe \
    -v /opt/mcpe-data:/data \
    -p 19132:19132/udp lomot/minecraft-bedrock:1.10.0.7-r1
  ```

## update the server
1. backup you data

  just backup the folder ```/opt/mcpe-data```

  ```bash
  cp /opt/mcpe-data /opt/mcpe-data.bak
  ```

2. exit and delete the old server

  ```bash
  docker container stop mcpe
  docker container rm mcpe
  ```
3. start a new version server

  ```bash
  docker run -d -it --name mcpe -v /opt/mcpe-data:/data -p 19132:19132/udp lomot/minecraft-bedrock:1.10.0.7-r1
  ```

## manage the server
### enter or quit the game console
```bash
docker attach mcpe
```
press ```ctrl + p + q``` to quit
do not use ```ctrl+c``` or ```ctrl+d```, this wii kill the process

### stop/start/restart/rm the server
```bash
docker container stop/start/restart/rm mcpe
```

### automatically restart when the server crashed
```bash
docker run -d --restart=on-failure:5 -it --name mcpe \
  -v /opt/mcpe-data:/data \
  -p 19132:19132/udp lomot/minecraft-bedrock:1.10.0.7-r1
```

## bin file from
https://minecraft.net/en-us/download/server/bedrock/

## Docker address
https://cloud.docker.com/repository/docker/lomot/minecraft-bedrock

## github address
https://github.com/LomotHo/minecraft-bedrock
