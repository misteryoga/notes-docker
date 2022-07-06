# Docker
## 1. Container
### Get list container running
```
docker container ls
```

### Get all list container
```
docker container ls -a
```

### Remove container
```
docker container rm name_container
```

### Run container
```
docker container start name_container
```

### Stop container
```
docker container stop name_container
```

### Create container 
```
docker container create --name name_container image:tag
```
```
docker container create --name name_container redis:latest
```
#### create container + publish
```
docker container create --name name_container --publish access_port_os:port_image image:tag
```
```
docker container create --name name_container --publish 3000:80 nginx:latest
```
#### create container + mount(bind) + env
```
docker container create --name name_container --publish access_port_os:port_image --mount "type=bind,source=/path/os/,destination=/path/image" --env cek_documentation_image=value image:tag
```
```
docker container create --name name_container --publish 27018:27017 --mount "type=bind,source=/home/yoga/Labs/docker/mongodata,destination=/data/db" --env MONGO_INITDB_ROOT_USERNAME=yoga --env MONGO_INITDB_ROOT_PASSWORD=yoga mongo:latest
```
#### create container + mount(volume) + env
```
docker container create --name name_container --publish access_port_os:port_image --mount "type=volume,source=name_volume,destination=/path/image" --env cek_documentation_image=value image:tag
```
```
docker container create --name name_container --publish 27018:27017 --mount "type=volume,source=mongodata2,destination=/data/db" --env MONGO_INITDB_ROOT_USERNAME=yoga --env MONGO_INITDB_ROOT_PASSWORD=yoga mongo:latest
```
#### create container with network
```
docker container create --name name_container --network name_network image:tag
```

### Sample Backup
```
docker container create --name nginxbackup --mount "type=bind,source=/home/yoga/labs/docker/mongodatabak,destination=/backup" --mount "type=volume,source=mongovolume2,destination=/data" nginx:latest
```
#### enter nginx bin bash
```
docker container exec -i -t nginxbackup /bin/bash
```
#### tar gz file to folder backup
tar cvf destination_backup select_data_will_backup
```
tar cvf /backup/backup.tar.gz /data
```
#### backup with container run (after run then remove container)(
```
docker container run --rm --name ubuntucontainer --mount "type=bind,source=/home/yoga/Labs/docker/mongodatabak,destination=/backup" --mount "type=volume,source=mongovolume2,destination=/data" ubuntu:latest tar cvf /backup/backup-backup.tar.gz /data
```