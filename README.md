![](https://framagit.org/luc/lufi/raw/master/themes/default/public/img/lufi128.png)
![Build and Push](https://github.com/victor-rds/docker-lufi/workflows/Build%20and%20Push/badge.svg)

## Tag available
* latest, 0.04.6[(lufi/Dockerfile)](./Dockerfile)

## Description
What is [lufi](https://framagit.org/luc/lufi) ?

Lufi means Let's Upload that FIle.

It stores files and allows you to download them.

Is that all? No. All the files are encrypted by the browser! It means that your files never leave your computer unencrypted. The administrator of the Lufi instance you use will not be able to see what is in your file, neither will your network administrator, or your ISP.

**This image does not contain root processes**

## BUILD IMAGE

```shell
docker build -t victor-rds/lufi github.com/victor-rds/docker-lufi.git#master
```

## Configuration
### Environments
* UID : choose uid for launching lufi (default : 991)
* GID : choose gid for launching lufi (default : 991)
* WEBROOT : webroot of lufi (default : /)
* SECRET : random string used to encrypt cookies (default : will be generated on the first run)
* MAX_FILE_SIZE : maximum file size of an uploaded file in bytes (default : 10000000000)
* CONTACT : lufi contact (default : contact@domain.tld)
* DEFAULT_DELAY : default time limit for files in days (default : 1 (0 for unlimited))
* MAX_DELAY : number of days after which the files will be deleted (default : 0 for unlimited)
* THEME : theme for lufi (default : default)
* ALLOW_PWD_ON_FILES : enable download password (default : 1 (0 => disable, 1 => enable))

### Volumes
* /usr/lufi/lufi.conf : lufi's configuration file is here
* /usr/lufi/data : lufi's database is here
* /usr/lufi/files : Location of uploaded files

### Ports
* 8081

## Usage
### Simple launch
```shell
docker run -d -p 8081:8081 victor-rds/lufi
```
URI access : http://XX.XX.XX.XX:8081

### Advanced launch
```shell
docker run -d -p 8181:8081 \
    -v /docker/config/lufi/data:/usr/lufi/data \
    -v /docker/data/lufi:/usr/lufi/files \
    -e UID=1001 \
    -e GID=1001 \
    -e WEBROOT=/lufi \
    -e SECRET=$(date +%s | md5sum | head -c 32) \
    -e CONTACT=contact@mydomain.com \
    -e MAX_FILE_SIZE=250000000 \
    victorrds/lufi
```
URI access : http://XX.XX.XX.XX:8181/lufi

## Contributing
Any contributions are very welcome !