# Docker
## 1. Image


## 2. Container
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


## 3. Network
### GET LIST NETWORK
(default sudah ada bawaan docker)
```
docker network ls
```

### CREATE NETWORK
```
docker network create --driver drive_type name_network
```
```
docker network create --drive bridge contohnetwork
```

### REMOVE NETWORK
(matikan kontainer yg menggunakan network yg akan d hapus terlebih dahulu)
```
docker network rm name_network
```

### REMOVE CONTAINER FROM NETWORK
```
docker network disconnect name_network name_container
```

### ADD EXISTSING CONTAINER TO NETWORK
```
docker network connect name_network name_container
```


## 4. Volume
### get list volume
```
docker volume ls
```

### remove volume
```
docker volume rm name_volume
```

### create volume
```
docker volume create name_volume
```

### resotre volume
```
docker container run --rm --name ubunturestore --mount "type=bind,source=/home/yoga/Labs/docker/mongodatabak,destination=/backup" --mount "type=volume,source=mongodatarestore,destination=/data" ubuntu:latest bash -c "cd /data && tar xvf /backup/backup.tar.gz --strip 1"
```