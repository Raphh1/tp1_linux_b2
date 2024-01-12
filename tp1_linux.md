# Sudo c pas bo

### 🌞 Ajouter votre utilisateur au groupe docker

```
[raph@localhost /]$ sudo groupadd -f docker
[raph@localhost /]$ sudo chown root:docker /var/run/docker.sock
[raph@localhost /]$ sudo usermod -a -G docker raph
[raph@localhost /]$ newgrp docker
[raph@localhost /]$ sudo systemctl restart docker
[raph@localhost /]$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
```

# 4. Un premier conteneur en vif

### 🌞 Lancer un conteneur NGINX

```
[raph@localhost /]$ docker run -d -p 9999:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
af107e978371: Pull complete
336ba1f05c3e: Pull complete
8c37d2ff6efa: Pull complete
51d6357098de: Pull complete
782f1ecce57d: Pull complete
5e99d351b073: Pull complete
7b73345df136: Pull complete
Digest: sha256:2bdc49f2f8ae8d8dc50ed00f2ee56d00385c6f8bc8a8b320d0a294d9e3b49026
Status: Downloaded newer image for nginx:latest
3c3a9fbcda4de37fa237af6b540fea62ed3b9a6c4c9a1375dc26dc164a394a77
```

### 🌞 Visitons

```
[raph@localhost /]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS
 NAMES
3c3a9fbcda4d   nginx     "/docker-entrypoint.…"   2 minutes ago   Up 2 minutes   0.0.0.0:9999->80/tcp, :::9999->80/tcp   intelligent_goldwasser

[raph@localhost /]$ docker logs  intelligent_goldwasser
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2023/12/22 13:19:24 [notice] 1#1: using the "epoll" event method
2023/12/22 13:19:24 [notice] 1#1: nginx/1.25.3
2023/12/22 13:19:24 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2023/12/22 13:19:24 [notice] 1#1: OS: Linux 5.14.0-362.13.1.el9_3.x86_64
2023/12/22 13:19:24 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1073741816:1073741816
2023/12/22 13:19:24 [notice] 1#1: start worker processes
2023/12/22 13:19:24 [notice] 1#1: start worker process 28

[raph@localhost /]$ docker inspect intelligent_goldwasser
[
    {
        "Id": "3c3a9fbcda4de37fa237af6b540fea62ed3b9a6c4c9a1375dc26dc164a394a77",
        "Created": "2023-12-22T13:19:24.290086065Z",
        "Path": "/docker-entrypoint.sh",
        "Args": [
            "nginx",
            "-g",
            "daemon off;"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 1875,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2023-12-22T13:19:24.677113082Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:d453dd892d9357f3559b967478ae9cbc417b52de66b53142f6c16c8a275486b9",
        "ResolvConfPath": "/var/lib/docker/containers/3c3a9fbcda4de37fa237af6b540fea62ed3b9a6c4c9a1375dc26dc164a394a77/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/3c3a9fbcda4de37fa237af6b540fea62ed3b9a6c4c9a1375dc26dc164a394a77/hostname",
        "HostsPath": "/var/lib/docker/containers/3c3a9fbcda4de37fa237af6b540fea62ed3b9a6c4c9a1375dc26dc164a394a77/hosts",
        "LogPath": "/var/lib/docker/containers/3c3a9fbcda4de37fa237af6b540fea62ed3b9a6c4c9a1375dc26dc164a394a77/3c3a9fbcda4de37fa237af6b540fea62ed3b9a6c4c9a1375dc26dc164a394a77-json.log",
        "Name": "/intelligent_goldwasser",
        "RestartCount": 0,
        "Driver": "overlay2",
        "Platform": "linux",
        "MountLabel": "",
        "ProcessLabel": "",
        "AppArmorProfile": "",
        "ExecIDs": null,
        "HostConfig": {
            "Binds": null,
            "ContainerIDFile": "",
            "LogConfig": {
                "Type": "json-file",
                "Config": {}
            },
            "NetworkMode": "default",
            "PortBindings": {
                "80/tcp": [
                    {
                        "HostIp": "",
                        "HostPort": "9999"
                    }
                ]
            },
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "ConsoleSize": [
                30,
                120
            ],
            "CapAdd": null,
            "CapDrop": null,
            "CgroupnsMode": "private",
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "private",
            "Cgroup": "",
            "Links": null,
            "OomScoreAdj": 0,
            "PidMode": "",
            "Privileged": false,
            "PublishAllPorts": false,
            "ReadonlyRootfs": false,
            "SecurityOpt": null,
            "UTSMode": "",
            "UsernsMode": "",
            "ShmSize": 67108864,
            "Runtime": "runc",
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": [],
            "BlkioDeviceReadBps": [],
            "BlkioDeviceWriteBps": [],
            "BlkioDeviceReadIOps": [],
            "BlkioDeviceWriteIOps": [],
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DeviceRequests": null,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": null,
            "OomKillDisable": null,
            "PidsLimit": null,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0,
            "MaskedPaths": [
                "/proc/asound",
                "/proc/acpi",
                "/proc/kcore",
                "/proc/keys",
                "/proc/latency_stats",
                "/proc/timer_list",
                "/proc/timer_stats",
                "/proc/sched_debug",
                "/proc/scsi",
                "/sys/firmware",
                "/sys/devices/virtual/powercap"
            ],
            "ReadonlyPaths": [
                "/proc/bus",
                "/proc/fs",
                "/proc/irq",
                "/proc/sys",
                "/proc/sysrq-trigger"
            ]
        },
        "GraphDriver": {
            "Data": {
                "LowerDir": "/var/lib/docker/overlay2/660485dd2d816aa6ccc4d75fe8e0ea1d03b564e20e14b27d73a11161c22da2be-init/diff:/var/lib/docker/overlay2/d39df0981abf34b465ffbc14b620f3422313570942e8198b0532048219739a64/diff:/var/lib/docker/overlay2/18dc2bb557206598ed96a3ad6ca74c837e67f1492a48542755089b5d1198cdc4/diff:/var/lib/docker/overlay2/6cb1f39d1a768a6d0e9954d3a876cbcb7528dd74b5d03ef4f8af39d6225d0d6b/diff:/var/lib/docker/overlay2/c7540b9fa835433fced29ea643b62ebca1082e73fd178accf77d1a27dfc8bd64/diff:/var/lib/docker/overlay2/aff2cca2269118ad2721b6ff68cbe227ad3d8e522c952313616b3212a9a1a9f8/diff:/var/lib/docker/overlay2/e8718fe08d3227fe03c4b268743454058765f07b23d39fe0c5e0af2d40836a89/diff:/var/lib/docker/overlay2/667dd177852e3c5d423ea6f20384a43320f7f562b299f22d69c07124f06a8f82/diff",
                "MergedDir": "/var/lib/docker/overlay2/660485dd2d816aa6ccc4d75fe8e0ea1d03b564e20e14b27d73a11161c22da2be/merged",
                "UpperDir": "/var/lib/docker/overlay2/660485dd2d816aa6ccc4d75fe8e0ea1d03b564e20e14b27d73a11161c22da2be/diff",
                "WorkDir": "/var/lib/docker/overlay2/660485dd2d816aa6ccc4d75fe8e0ea1d03b564e20e14b27d73a11161c22da2be/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "3c3a9fbcda4d",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "ExposedPorts": {
                "80/tcp": {}
            },
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin",
                "NGINX_VERSION=1.25.3",
                "NJS_VERSION=0.8.2",
                "PKG_RELEASE=1~bookworm"
            ],
            "Cmd": [
                "nginx",
                "-g",
                "daemon off;"
            ],
            "Image": "nginx",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": [
                "/docker-entrypoint.sh"
            ],
            "OnBuild": null,
            "Labels": {
                "maintainer": "NGINX Docker Maintainers <docker-maint@nginx.com>"
            },
            "StopSignal": "SIGQUIT"
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "150abe572b3047831fb99f23f6e06b57b2390454ac32dc5a6af077afb1d0471a",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {
                "80/tcp": [
                    {
                        "HostIp": "0.0.0.0",
                        "HostPort": "9999"
                    },
                    {
                        "HostIp": "::",
                        "HostPort": "9999"
                    }
                ]
            },
            "SandboxKey": "/var/run/docker/netns/150abe572b30",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "b4575e441ae0d8afcb5cccc05043f130aabdd17e8c34f4c42aa69081f658f887",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.2",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:02",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "b4d5ce439db628a0acc0bd3aa6edc16cd46c062c3ee294c60207520a13f4ceef",
                    "EndpointID": "b4575e441ae0d8afcb5cccc05043f130aabdd17e8c34f4c42aa69081f658f887",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null
                }
            }
        }
    }
]


[raph@localhost /]$ sudo ss -lpnt
[sudo] password for raph:
State     Recv-Q    Send-Q       Local Address:Port       Peer Address:Port   Process
LISTEN    0         4096               0.0.0.0:9999            0.0.0.0:*       users:(("docker-proxy",pid=1833,fd=4))
LISTEN    0         128                0.0.0.0:22              0.0.0.0:*       users:(("sshd",pid=705,fd=3))
LISTEN    0         4096                  [::]:9999               [::]:*       users:(("docker-proxy",pid=1838,fd=4))
LISTEN    0         128                   [::]:22                 [::]:*       users:(("sshd",pid=705,fd=4))

[raph@localhost /]$ sudo firewall-cmd --add-port=9999/tcp
success
```

### 🌞 On va ajouter un site Web au conteneur NGINX

```
[raph@localhost nginx]$ sudo nano site_nul.conf
[raph@localhost nginx]$ cat site_nul.conf
server {
    listen        8080;

    location / {
        root /var/www/html;
    }
}

[raph@localhost nginx]$ cat index.html
<h1>MEOOOOOOW</h1>

pour créer j'ai utilisé mkdir dans raph puis touch puis nano pour ecrire les codes dans les fichiers
```

### 🌞 Visitons

```
[raph@localhost nginx]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS
             NAMES
6dcbce30d590   nginx     "/docker-entrypoint.…"   8 minutes ago   Up 8 minutes   80/tcp, 0.0.0.0:9999->8080/tcp, :::9999->8080/tcp   silly_jang

```

# 5. Un deuxième conteneur en vif

### 🌞 Lance un conteneur Python, avec un shell

```
[raph@localhost ~]$ docker run -it python bash
Unable to find image 'python:latest' locally
latest: Pulling from library/python
bc0734b949dc: Pull complete
b5de22c0f5cd: Pull complete
917ee5330e73: Pull complete
b43bd898d5fb: Pull complete
7fad4bffde24: Pull complete
d685eb68699f: Pull complete
107007f161d0: Pull complete
02b85463d724: Pull complete
Digest: sha256:3733015cdd1bd7d9a0b9fe21a925b608de82131aa4f3d397e465a1fcb545d36f
Status: Downloaded newer image for python:latest
```

### 🌞 Installe des libs Python

```
root@50e0b9ee9f97:/# pip install aiohttp
root@50e0b9ee9f97:/# pip install aioconsole

root@50e0b9ee9f97:/# python
Python 3.12.1 (main, Dec 19 2023, 20:14:15) [GCC 12.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import aiohttp

root@50e0b9ee9f97:/# ls
bin  boot  dev  etc  home  lib  lib32  lib64  libx32  media  mnt  opt  proc  root  run  sbin  srv  sys  tmp  usr  var
```

# II. Images

## 1. Images publiques

### 🌞 Récupérez des images

```
[raph@localhost ~]$ docker pull python
Using default tag: latest
latest: Pulling from library/python
Digest: sha256:3733015cdd1bd7d9a0b9fe21a925b608de82131aa4f3d397e465a1fcb545d36f
Status: Image is up to date for python:latest
docker.io/library/python:latest

[raph@localhost ~]$ docker pull mysql
Using default tag: latest
latest: Pulling from library/mysql
bce031bc522d: Extracting [==================================================>]  51.32MB/51.32MB
cf7e9f463619: Download complete
105f403783c7: Download complete
878e53a613d8: Download complete
2a362044e79f: Download complete
6e4df4f73cfe: Download complete
69263d634755: Downloading [==================================================>]  62.57MB/62.57MB
fe5e85549202: Download complete
5c02229ce6f1: Download complete
7320aa32bf42: Download complete
write /var/lib/docker/tmp/GetImageBlob611673824: no space left on device

[raph@localhost ~]$ docker pull wordpress
Using default tag: latest
latest: Pulling from library/wordpress
af107e978371: Already exists
6480d4ad61d2: Pull complete
95f5176ece8b: Extracting [===============================================>   ]  99.71MB/104.4MB
0ebe7ec824ca: Download complete
673e01769ec9: Download complete
74f0c50b3097: Download complete
1a19a72eb529: Download complete
50436df89cfb: Download complete
8b616b90f7e6: Download complete
df9d2e4043f8: Download complete
d6236f3e94a1: Download complete
59fa8b76a6b3: Download complete
99eb3419cf60: Download complete
22f5c20b545d: Downloading [==================================================>]  26.25MB/26.25MB
1f0d2c1603d0: Downloading [==================================================>]   29.5MB/29.5MB
4624824acfea: Download complete
79c3af11cab5: Download complete
e8d8239610fb: Download complete
a1ff013e1d94: Downloading [==================================================>]  24.31MB/24.31MB
31076364071c: Download complete
87728bbad961: Download complete
write /var/lib/docker/tmp/GetImageBlob1543616229: no space left on device

[raph@localhost ~]$ docker pull linuxserver/wikijs
Using default tag: latest
latest: Pulling from linuxserver/wikijs
8b16ab80b9bd: Pull complete
07a0e16f7be1: Pull complete
145cda5894de: Pull complete
1a16fa4f6192: Pull complete
84d558be1106: Pull complete
4573be43bb06: Extracting [==================================================>]    102MB/102MB
20b23561c7ea: Download complete
failed to register layer: mkdir /app/wiki/node_modules/@apollographql/graphql-upload-8-fork/node_modules/busboy: no space left on device

[raph@localhost ~]$ docker images
REPOSITORY   TAG       IMAGE ID       CREATED       SIZE
python       latest    fc7a60e86bae   2 weeks ago   1.02GB
nginx        latest    d453dd892d93   8 weeks ago   187MB


PS : J'AI REINSTALLER PYTHON EN 3.11
```

### 🌞 Lancez un conteneur à partir de l'image Python

```
[raph@localhost ~]$ docker run -it python:3.11 bash
root@3664b5a2558e:/# python --version
Python 3.11.7
```

### 🌞 Ecrire un Dockerfile pour une image qui héberge une application Python

```
[raph@localhost ~]$ touch Dockerfile
[raph@localhost ~]$ sudo nano Dockerfile

[raph@localhost python_app_build]$ cat Dockerfile
# Use the official Debian base image
FROM debian:bullseye-slim

# Update the package list
RUN apt update

# Install Python
RUN apt install -y python3

# Install the Python emoji library
RUN pip install emoji

# Set the working directory in the container
WORKDIR /app

# Copy the application files into the container
COPY . /app

# Specify the default command to run on container startup
ENTRYPOINT ["python3", "your_app_script.py"]    

[raph@localhost ~]$ mkdir python_app_build
[raph@localhost ~]$ cd python_app_build
[raph@localhost python_app_build]$ touch app.py
```

### 🌞 Build l'image

```

```

# Docker Compose

### créer un fichier docker compose 

```
[raph@localhost ~]$ mkdir compose_test
[raph@localhost ~]$ sudo nano compose_test

le fichier yml a été créer quand j'ai save les lignes du nano
```

### 🌞 Lancez les deux conteneurs avec docker compose

```
[raph@localhost ~]$ docker compose up -d
[+] Running 3/3
 ✔ conteneur_flopesque Pulled                                                                                      2.3s
 ✔ conteneur_nul 1 layers [⣿]      0B/0B      Pulled                                                               2.3s
   ✔ 1b13d4e1a46e Already exists                                                                                   0.0s
[+] Running 3/3
 ✔ Network raph_default                  Created                                                                   0.2s
 ✔ Container raph-conteneur_flopesque-1  Started                                                                   0.0s
 ✔ Container raph-conteneur_nul-1        Started
```

### 🌞 Vérifier que les deux conteneurs tournent

```
[raph@localhost ~]$ docker compose ps
NAME                         IMAGE     COMMAND        SERVICE               CREATED         STATUS         PORTS
raph-conteneur_flopesque-1   debian    "sleep 9999"   conteneur_flopesque   7 minutes ago   Up 7 minutes
raph-conteneur_nul-1         debian    "sleep 9999"   conteneur_nul         7 minutes ago   Up 7 minutes
```

### 🌞 Pop un shell dans le conteneur conteneur_nul

```
root@34093866d8ec:/# apt-get install iputils-ping
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
...

root@34093866d8ec:/# ping raph-conteneur_flopesque-1
PING raph-conteneur_flopesque-1 (172.18.0.3) 56(84) bytes of data.
64 bytes from raph-conteneur_flopesque-1.raph_default (172.18.0.3): icmp_seq=1 ttl=64 time=0.062 ms
64 bytes from raph-conteneur_flopesque-1.raph_default (172.18.0.3): icmp_seq=2 ttl=64 time=0.182 ms
64 bytes from raph-conteneur_flopesque-1.raph_default (172.18.0.3): icmp_seq=3 ttl=64 time=0.217 ms
64 bytes from raph-conteneur_flopesque-1.raph_default (172.18.0.3): icmp_seq=4 ttl=64 time=0.120 ms
...
```