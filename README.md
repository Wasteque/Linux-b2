# I. Init
## 3. sudo c pa bo

**🌞 Ajouter votre utilisateur au groupe docker**
```
[ethan@node1 ~]$ docker ps
permission denied while trying to connect to the Docker daemon socket at unix:///var/run/docker.sock: Get "http://%2Fvar%2Frun%2Fdocker.sock/v1.47/containers/json": dial unix /var/run/docker.sock: connect: permission denied
[ethan@node1 ~]$ sudo docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[ethan@node1 ~]$ sudo usermod -aG docker ${USER}
[ethan@node1 ~]$ su - ${USER}
Password:
Last login: Wed Dec 11 10:22:28 CET 2024 from 10.1.1.1 on pts/0
[ethan@node1 ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[ethan@node1 ~]$
```

## 4. Un premier conteneur en vif

**🌞 Lancer un conteneur NGINX**

```
[ethan@node1 ~]$ docker run -d -p 9999:80 nginx
Unable to find image 'nginx:latest' locally
latest: Pulling from library/nginx
bc0965b23a04: Pull complete
650ee30bbe5e: Pull complete
8cc1569e58f5: Pull complete
362f35df001b: Pull complete
13e320bf29cd: Pull complete
7b50399908e1: Pull complete
57b64962dd94: Pull complete
Digest: sha256:fb197595ebe76b9c0c14ab68159fd3c08bd067ec62300583543f0ebda353b5be
Status: Downloaded newer image for nginx:latest
b20d59c0f6d894f20b5c22fd46fa0b77f7a10dc7348d79dd3c0a15ed5423245a
```

**🌞 Visitons**

```
[ethan@node1 ~]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED         STATUS         PORTS                                     NAMES
b20d59c0f6d8   nginx     "/docker-entrypoint.…"   4 minutes ago   Up 4 minutes   0.0.0.0:9999->80/tcp, [::]:9999->80/tcp   clever_dubinsky
[ethan@node1 ~]$ docker logs b2
/docker-entrypoint.sh: /docker-entrypoint.d/ is not empty, will attempt to perform configuration
/docker-entrypoint.sh: Looking for shell scripts in /docker-entrypoint.d/
/docker-entrypoint.sh: Launching /docker-entrypoint.d/10-listen-on-ipv6-by-default.sh
10-listen-on-ipv6-by-default.sh: info: Getting the checksum of /etc/nginx/conf.d/default.conf
10-listen-on-ipv6-by-default.sh: info: Enabled listen on IPv6 in /etc/nginx/conf.d/default.conf
/docker-entrypoint.sh: Sourcing /docker-entrypoint.d/15-local-resolvers.envsh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/20-envsubst-on-templates.sh
/docker-entrypoint.sh: Launching /docker-entrypoint.d/30-tune-worker-processes.sh
/docker-entrypoint.sh: Configuration complete; ready for start up
2024/12/11 10:08:51 [notice] 1#1: using the "epoll" event method
2024/12/11 10:08:51 [notice] 1#1: nginx/1.27.3
2024/12/11 10:08:51 [notice] 1#1: built by gcc 12.2.0 (Debian 12.2.0-14)
2024/12/11 10:08:51 [notice] 1#1: OS: Linux 5.14.0-284.11.1.el9_2.x86_64
2024/12/11 10:08:51 [notice] 1#1: getrlimit(RLIMIT_NOFILE): 1073741816:1073741816
2024/12/11 10:08:51 [notice] 1#1: start worker processes
2024/12/11 10:08:51 [notice] 1#1: start worker process 28
[ethan@node1 ~]$ docker inspect b2
[
    {
        "Id": "b20d59c0f6d894f20b5c22fd46fa0b77f7a10dc7348d79dd3c0a15ed5423245a",
        "Created": "2024-12-11T10:08:51.238612881Z",
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
            "Pid": 13239,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2024-12-11T10:08:51.399510836Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:66f8bdd3810c96dc5c28aec39583af731b34a2cd99471530f53c8794ed5b423e",
        "ResolvConfPath": "/var/lib/docker/containers/b20d59c0f6d894f20b5c22fd46fa0b77f7a10dc7348d79dd3c0a15ed5423245a/resolv.conf",
        "HostnamePath": "/var/lib/docker/containers/b20d59c0f6d894f20b5c22fd46fa0b77f7a10dc7348d79dd3c0a15ed5423245a/hostname",
        "HostsPath": "/var/lib/docker/containers/b20d59c0f6d894f20b5c22fd46fa0b77f7a10dc7348d79dd3c0a15ed5423245a/hosts",
        "LogPath": "/var/lib/docker/containers/b20d59c0f6d894f20b5c22fd46fa0b77f7a10dc7348d79dd3c0a15ed5423245a/b20d59c0f6d894f20b5c22fd46fa0b77f7a10dc7348d79dd3c0a15ed5423245a-json.log",
        "Name": "/clever_dubinsky",
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
            "NetworkMode": "bridge",
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
                72,
                271
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
            "Ulimits": [],
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
                "LowerDir": "/var/lib/docker/overlay2/9bd0542ecca5a69e145baad541ea903b347c1efd46c6dc1c6b8bc70d9598446c-init/diff:/var/lib/docker/overlay2/cffaa2dd3e7cbe6aa811e9f3cb4b1dab97ba2de2207215e965607a3d2998240e/diff:/var/lib/docker/overlay2/be82b639a07a016cad33bbb03b10b3a4e691aba58b45ffa36b856ecf360e33b6/diff:/var/lib/docker/overlay2/ec2e07eaae8b5989e700c8f25c5d1e78220efe8738e75d1a25c877f0212a7af7/diff:/var/lib/docker/overlay2/7227aca579cf220058b3692a77cfa6c4c7f5a0186a5a9219540a9b52c95fa63d/diff:/var/lib/docker/overlay2/f78048545fad2e5721cb75811018e3317b761d7a89007fd8aa27042f94b4818f/diff:/var/lib/docker/overlay2/1a352658379d88eb721d7a9ebad47feb4d8e200c63f2dcd3285cd3fee065c955/diff:/var/lib/docker/overlay2/59024976aca777c88e4b8c2c4318ac1ce26835ffd79d9f66f15d4554acf983ec/diff",
                "MergedDir": "/var/lib/docker/overlay2/9bd0542ecca5a69e145baad541ea903b347c1efd46c6dc1c6b8bc70d9598446c/merged",
                "UpperDir": "/var/lib/docker/overlay2/9bd0542ecca5a69e145baad541ea903b347c1efd46c6dc1c6b8bc70d9598446c/diff",
                "WorkDir": "/var/lib/docker/overlay2/9bd0542ecca5a69e145baad541ea903b347c1efd46c6dc1c6b8bc70d9598446c/work"
            },
            "Name": "overlay2"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "b20d59c0f6d8",
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
                "NGINX_VERSION=1.27.3",
                "NJS_VERSION=0.8.7",
                "NJS_RELEASE=1~bookworm",
                "PKG_RELEASE=1~bookworm",
                "DYNPKG_RELEASE=1~bookworm"
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
            "SandboxID": "96a313d5fb6b69d119535b0d77737333cfa0e6cfcd2660f4f9e606ecc53cade6",
            "SandboxKey": "/var/run/docker/netns/96a313d5fb6b",
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
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "1b83b3c612f5518f9346539b5da45334476d3399ae2139c414a337e320e3cf7c",
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
                    "MacAddress": "02:42:ac:11:00:02",
                    "DriverOpts": null,
                    "NetworkID": "38731ce61797d11d58ccaf97bccd1862f834c1b1ad44e7ffce8ccc7c365e2cc4",
                    "EndpointID": "1b83b3c612f5518f9346539b5da45334476d3399ae2139c414a337e320e3cf7c",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.2",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "DNSNames": null
                }
            }
        }
    }
]
[ethan@node1 ~]$ sudo systemctl status firewalld
[sudo] password for ethan:
● firewalld.service - firewalld - dynamic firewall daemon
     Loaded: loaded (/usr/lib/systemd/system/firewalld.service; enabled; preset: enabled)
     Active: active (running) since Wed 2024-12-11 10:22:19 CET; 56min ago
       Docs: man:firewalld(1)
   Main PID: 659 (firewalld)
      Tasks: 3 (limit: 4674)
     Memory: 38.6M
        CPU: 911ms
     CGroup: /system.slice/firewalld.service
             └─659 /usr/bin/python3 -s /usr/sbin/firewalld --nofork --nopid

Dec 11 10:25:25 node1.lan1.tp2 firewalld[659]: WARNING: COMMAND_FAILED: '/usr/sbin/ip6tables -w10 -t nat -F DOCKER' failed: ip6tables: No chain/target/match by that name.
Dec 11 10:25:25 node1.lan1.tp2 firewalld[659]: WARNING: COMMAND_FAILED: '/usr/sbin/ip6tables -w10 -t nat -X DOCKER' failed: ip6tables: No chain/target/match by that name.
Dec 11 10:25:25 node1.lan1.tp2 firewalld[659]: WARNING: COMMAND_FAILED: '/usr/sbin/ip6tables -w10 -t filter -F DOCKER' failed: ip6tables: No chain/target/match by that name.
Dec 11 10:25:25 node1.lan1.tp2 firewalld[659]: WARNING: COMMAND_FAILED: '/usr/sbin/ip6tables -w10 -t filter -X DOCKER' failed: ip6tables: No chain/target/match by that name.
Dec 11 10:25:25 node1.lan1.tp2 firewalld[659]: WARNING: COMMAND_FAILED: '/usr/sbin/ip6tables -w10 -t filter -F DOCKER-ISOLATION-STAGE-1' failed: ip6tables: No chain/target/match by that name.
Dec 11 10:25:25 node1.lan1.tp2 firewalld[659]: WARNING: COMMAND_FAILED: '/usr/sbin/ip6tables -w10 -t filter -X DOCKER-ISOLATION-STAGE-1' failed: ip6tables: No chain/target/match by that name.
Dec 11 10:25:25 node1.lan1.tp2 firewalld[659]: WARNING: COMMAND_FAILED: '/usr/sbin/ip6tables -w10 -t filter -F DOCKER-ISOLATION-STAGE-2' failed: ip6tables: No chain/target/match by that name.
Dec 11 10:25:25 node1.lan1.tp2 firewalld[659]: WARNING: COMMAND_FAILED: '/usr/sbin/ip6tables -w10 -t filter -X DOCKER-ISOLATION-STAGE-2' failed: ip6tables: No chain/target/match by that name.
Dec 11 10:25:25 node1.lan1.tp2 firewalld[659]: WARNING: COMMAND_FAILED: '/usr/sbin/ip6tables -w10 -t filter -F DOCKER-ISOLATION' failed: ip6tables: No chain/target/match by that name.
Dec 11 10:25:25 node1.lan1.tp2 firewalld[659]: WARNING: COMMAND_FAILED: '/usr/sbin/ip6tables -w10 -t filter -X DOCKER-ISOLATION' failed: ip6tables: No chain/target/match by that name.
[ethan@node1 ~]$ sudo systemctl start firewalld
[ethan@node1 ~]$
[ethan@node1 ~]$ sudo systemctl start firewalld
[ethan@node1 ~]$
[ethan@node1 ~]$ sudo systemctl enable firewalld
[ethan@node1 ~]$ sudo firewall-cmd --add-port=8080/tcp --permanent
success
[ethan@node1 ~]$ sudo firewall-cmd --reload
success
[ethan@node1 ~]$ sudo firewall-cmd --list-ports
8080/tcp
[ethan@node1 ~]$ sudo firewall-cmd --add-port=9999/tcp --permanent
success
[ethan@node1 ~]$ sudo firewall-cmd --reload
success
[ethan@node1 ~]$ sudo firewall-cmd --list-ports
8080/tcp 9999/tcp
[ethan@node1 ~]$ ip a
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
    inet 127.0.0.1/8 scope host lo
       valid_lft forever preferred_lft forever
    inet6 ::1/128 scope host
       valid_lft forever preferred_lft forever
2: enp0s3: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:4e:88:f6 brd ff:ff:ff:ff:ff:ff
    inet 10.1.1.11/24 brd 10.1.1.255 scope global noprefixroute enp0s3
       valid_lft forever preferred_lft forever
    inet6 fe80::a00:27ff:fe4e:88f6/64 scope link
       valid_lft forever preferred_lft forever
3: enp0s8: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UP group default qlen 1000
    link/ether 08:00:27:6c:8a:d3 brd ff:ff:ff:ff:ff:ff
    inet 10.0.3.15/24 brd 10.0.3.255 scope global dynamic noprefixroute enp0s8
       valid_lft 82890sec preferred_lft 82890sec
    inet6 fe80::a00:27ff:fe6c:8ad3/64 scope link noprefixroute
       valid_lft forever preferred_lft forever
4: docker0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue state UP group default
    link/ether 02:42:d7:97:b9:33 brd ff:ff:ff:ff:ff:ff
    inet 172.17.0.1/16 brd 172.17.255.255 scope global docker0
       valid_lft forever preferred_lft forever
    inet6 fe80::42:d7ff:fe97:b933/64 scope link
       valid_lft forever preferred_lft forever
8: veth07fe1c0@if7: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc noqueue master docker0 state UP group default
    link/ether 7a:8b:70:7c:7b:71 brd ff:ff:ff:ff:ff:ff link-netnsid 0
    inet6 fe80::788b:70ff:fe7c:7b71/64 scope link
       valid_lft forever preferred_lft forever
[ethan@node1 ~]$ curl 10.1.1.11:9999
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx!</title>
<style>
html { color-scheme: light dark; }
body { width: 35em; margin: 0 auto;
font-family: Tahoma, Verdana, Arial, sans-serif; }
</style>
</head>
<body>
<h1>Welcome to nginx!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a>.<br/>
Commercial support is available at
<a href="http://nginx.com/">nginx.com</a>.</p>

<p><em>Thank you for using nginx.</em></p>
</body>
</html>
[ethan@node1 ~]$
```


**🌞 On va ajouter un site Web au conteneur NGINX**

```
[ethan@node1 ~]$ mkdir nginx
[ethan@node1 ~]$ ls
mkdir  nginx
[ethan@node1 ~]$ cd nginx/
[ethan@node1 nginx]$ sudo vi index.html
[sudo] password for ethan:
[ethan@node1 nginx]$ cat index.html
<h1>MEOOOW</h1>
[ethan@node1 nginx]$ sudo nano site_nul.conf
[ethan@node1 nginx]$ docker run -d -p 9999:8080 -v /home/<USER>/nginx/index.html:/var/www/html/index.html -v /home/<USER>/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf nginx
-bash: USER: No such file or directory
[ethan@node1 nginx]$ docker run -d -p 9999:8080 -v /home/ethan/nginx/index.html:/var/www/html/index.html -v /home/ethan/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf nginx
d3bc26cccd8f6b4fa636e2c5cb2784716f771636be807b459674ba3653bc07da
docker: Error response from daemon: driver failed programming external connectivity on endpoint happy_kare (0bc5a1d46ae7f5dab743a050d0413e807722faf32fff701567800c0af03b5785): Bind for 0.0.0.0:9999 failed: port is already allocated.
[ethan@node1 nginx]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED          STATUS          PORTS                                     NAMES
b20d59c0f6d8   nginx     "/docker-entrypoint.…"   28 minutes ago   Up 28 minutes   0.0.0.0:9999->80/tcp, [::]:9999->80/tcp   clever_dubinsky
[ethan@node1 nginx]$ docker rm -f b2
b2
[ethan@node1 nginx]$ docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
[ethan@node1 nginx]$ docker run -d -p 9999:8080 -v /home/ethan/nginx/index.html:/var/www/html/index.html -v /home/ethan/nginx/site_nul.conf:/etc/nginx/conf.d/site_nul.conf nginx
8b703636158af451b3bfb93b4899686603f670a9d5785d4b27e7ddc5976e7281
[ethan@node1 nginx]$
```

**🌞 Visitons(2)**

```
[ethan@node1 nginx]$ docker ps
CONTAINER ID   IMAGE     COMMAND                  CREATED              STATUS              PORTS                                                 NAMES
8b703636158a   nginx     "/docker-entrypoint.…"   About a minute ago   Up About a minute   80/tcp, 0.0.0.0:9999->8080/tcp, [::]:9999->8080/tcp   musing_jackson
[ethan@node1 nginx]$ curl 10.1.1.11:9999
<h1>MEOOOW</h1>
[ethan@node1 nginx]$

```

## 5. Un deuxième conteneur en vif

**🌞 Lance un conteneur Python, avec un shell**

```
[ethan@node1 nginx]$ docker run -it python bash
root@a49b366f3aca:/#
```

**🌞 Installe des libs Python**

```
root@a49b366f3aca:/# pip install aiohttp
Collecting aiohttp
  Downloading aiohttp-3.11.10-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (7.7 kB)
Collecting aiohappyeyeballs>=2.3.0 (from aiohttp)
  Downloading aiohappyeyeballs-2.4.4-py3-none-any.whl.metadata (6.1 kB)
Collecting aiosignal>=1.1.2 (from aiohttp)
  Downloading aiosignal-1.3.1-py3-none-any.whl.metadata (4.0 kB)
Collecting attrs>=17.3.0 (from aiohttp)
  Downloading attrs-24.2.0-py3-none-any.whl.metadata (11 kB)
Collecting frozenlist>=1.1.1 (from aiohttp)
  Downloading frozenlist-1.5.0-cp313-cp313-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (13 kB)
Collecting multidict<7.0,>=4.5 (from aiohttp)
  Downloading multidict-6.1.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (5.0 kB)
Collecting propcache>=0.2.0 (from aiohttp)
  Downloading propcache-0.2.1-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (9.2 kB)
Collecting yarl<2.0,>=1.17.0 (from aiohttp)
  Downloading yarl-1.18.3-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl.metadata (69 kB)
Collecting idna>=2.0 (from yarl<2.0,>=1.17.0->aiohttp)
  Downloading idna-3.10-py3-none-any.whl.metadata (10 kB)
Downloading aiohttp-3.11.10-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (1.7 MB)
   ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 1.7/1.7 MB 2.3 MB/s eta 0:00:00
Downloading aiohappyeyeballs-2.4.4-py3-none-any.whl (14 kB)
Downloading aiosignal-1.3.1-py3-none-any.whl (7.6 kB)
Downloading attrs-24.2.0-py3-none-any.whl (63 kB)
Downloading frozenlist-1.5.0-cp313-cp313-manylinux_2_5_x86_64.manylinux1_x86_64.manylinux_2_17_x86_64.manylinux2014_x86_64.whl (267 kB)
Downloading multidict-6.1.0-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (131 kB)
Downloading propcache-0.2.1-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (227 kB)
Downloading yarl-1.18.3-cp313-cp313-manylinux_2_17_x86_64.manylinux2014_x86_64.whl (339 kB)
Downloading idna-3.10-py3-none-any.whl (70 kB)
Installing collected packages: propcache, multidict, idna, frozenlist, attrs, aiohappyeyeballs, yarl, aiosignal, aiohttp
Successfully installed aiohappyeyeballs-2.4.4 aiohttp-3.11.10 aiosignal-1.3.1 attrs-24.2.0 frozenlist-1.5.0 idna-3.10 multidict-6.1.0 propcache-0.2.1 yarl-1.18.3
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable.It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.
root@a49b366f3aca:/# pip install aioconsole
Collecting aioconsole
  Downloading aioconsole-0.8.1-py3-none-any.whl.metadata (46 kB)
Downloading aioconsole-0.8.1-py3-none-any.whl (43 kB)
Installing collected packages: aioconsole
Successfully installed aioconsole-0.8.1
WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager, possibly rendering your system unusable.It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv. Use the --root-user-action option if you know what you are doing and want to suppress this warning.
root@a49b366f3aca:/#
```

# II. Images
## 1. Images publiques

**🌞 Récupérez des images**

````
    [ethan@node1 nginx]$ docker pull python:3.11
3.11: Pulling from library/python
fdf894e782a2: Already exists
5bd71677db44: Already exists
551df7f94f9c: Already exists
ce82e98d553d: Already exists
2371bf9a39a3: Pull complete
0b3239f18dfa: Pull complete
de07a735a679: Pull complete
Digest: sha256:2c80c66d876952e04fa74113864903198b7cfb36b839acb7a8fef82e94ed067c
Status: Downloaded newer image for python:3.11
docker.io/library/python:3.11
[ethan@node1 nginx]$ docker pull mysql:5.7
5.7: Pulling from library/mysql
20e4dcae4c69: Pull complete
1c56c3d4ce74: Pull complete
e9f03a1c24ce: Pull complete
68c3898c2015: Pull complete
6b95a940e7b6: Pull complete
90986bb8de6e: Pull complete
ae71319cb779: Pull complete
ffc89e9dfd88: Pull complete
43d05e938198: Pull complete
064b2d298fba: Pull complete
df9a4d85569b: Pull complete
Digest: sha256:4bc6bc963e6d8443453676cae56536f4b8156d78bae03c0145cbe47c2aad73bb
Status: Downloaded newer image for mysql:5.7
docker.io/library/mysql:5.7
[ethan@node1 nginx]$ docker pull worldpress
Using default tag: latest
Error response from daemon: pull access denied for worldpress, repository does not exist or may require 'docker login': denied: requested access to the resource is denied
[ethan@node1 nginx]$ docker pull wordpress
Using default tag: latest
latest: Pulling from library/wordpress
bc0965b23a04: Already exists
e0aa8e8bfd10: Pull complete
f45eeb7b7c66: Pull complete
2802fa207e46: Pull complete
2bc706e6dbbe: Pull complete
8f2b85a95cfd: Pull complete
2586d713206f: Pull complete
086063f0275c: Pull complete
61a388cf2f83: Pull complete
73fd6b827991: Pull complete
c2dd75e58cab: Pull complete
3b01564181f9: Pull complete
16d45113a90d: Pull complete
4f4fb700ef54: Pull complete
c4f8720ddb1e: Pull complete
d374174149dd: Pull complete
f09c82e22e1b: Pull complete
dd7711b88413: Pull complete
a89cceed0693: Pull complete
dab7a4cf5d37: Pull complete
e6f609a11365: Pull complete
1bbc7feeba6d: Pull complete
Digest: sha256:2f3572d5cd722489fe47d59ed45d947dc9507f5a019eb0567ddf24aedf9257ed
Status: Downloaded newer image for wordpress:latest
docker.io/library/wordpress:latest
[ethan@node1 nginx]$ docker pull linuxserver/wikijs
Using default tag: latest
latest: Pulling from linuxserver/wikijs
72387e7898ce: Pull complete
ec7680b185bf: Pull complete
b80232684b80: Pull complete
52e5d6eefe42: Pull complete
f224b10b4dc1: Pull complete
d179dce5799c: Pull complete
ff211b9bebf2: Pull complete
979004086415: Pull complete
Digest: sha256:45ecf23a3bf849a0bf0c9e2d832aede159e98efd29fef70bbc7ff4dd87522eba
Status: Downloaded newer image for linuxserver/wikijs:latest
docker.io/linuxserver/wikijs:latest
[ethan@node1 nginx]$
```





