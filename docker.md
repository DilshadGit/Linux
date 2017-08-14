                  ## ## ##        ==
               ## ## ## ## ##    ===
           /"""""""""""""""""\___/ ===
      ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
           \______ o           __/
             \    \         __/
              \____\_______/


docker is configured to use the default machine with IP 192.168.99.100
For help getting started, check out the docs at https://docs.docker.com

dilmac:~ DilMac$ docker info
Containers: 0
 Running: 0
 Paused: 0
 Stopped: 0
Images: 0
Server Version: 17.06.0-ce
Storage Driver: aufs
 Root Dir: /mnt/sda1/var/lib/docker/aufs
 Backing Filesystem: extfs
 Dirs: 0
 Dirperm1 Supported: true
Logging Driver: json-file
Cgroup Driver: cgroupfs
Plugins: 
 Volume: local
 Network: bridge host macvlan null overlay
 Log: awslogs fluentd gcplogs gelf journald json-file logentries splunk syslog
Swarm: inactive
Runtimes: runc
Default Runtime: runc
Init Binary: docker-init
containerd version: cfb82a876ecc11b5ca0977d1733adbe58599088a
runc version: 2d41c047c83e09a6d61d464906feb2a2f3c52aa4
init version: 949e6fa
Security Options:
 seccomp
  Profile: default
Kernel Version: 4.4.74-boot2docker
Operating System: Boot2Docker 17.06.0-ce (TCL 7.2); HEAD : 0672754 - Thu Jun 29 00:06:31 UTC 2017
OSType: linux
Architecture: x86_64
CPUs: 1
Total Memory: 1.955GiB
Name: default
ID: ZUWU:P76H:AG4P:PA54:UL45:UYKQ:RXEA:HMUC:NZ6Z:2XSR:QI2C:7KI2
Docker Root Dir: /mnt/sda1/var/lib/docker
Debug Mode (client): false
Debug Mode (server): true
 File Descriptors: 16
 Goroutines: 25
 System Time: 2017-08-13T19:51:23.599734734Z
 EventsListeners: 0
Registry: https://index.docker.io/v1/
Labels:
 provider=virtualbox
Experimental: false
Insecure Registries:
 127.0.0.0/8
Live Restore Enabled: false

dilmac:~ DilMac$ 

	Docker important Concept:

- 	Image are read only templates used to create containers
- 	Images are created with the docker build command, either by us or by other docker users.
- 	Images are composed of layers of other images
- 	Images are stored in a docker registry


	Container:
- 	if an image is a class, then a container is an instance of a class - a runtime object.
- 	Containers are lightweight and portable encapsulations of an environment in which to run applications.
- 	Containers are created from images. Inside a container, it has all the binaries and depencies needed to run the applications.
- 	Containers are created from images. Inside a container, it has all the binaries and dependencies needed to run the application.


	Registries and Repositories.
- 	A registry is where we store our images.
- 	You can host your own registry, or you can use Docker's public registry which is called DockerHub.
- 	Inside a registry, images are stored in repositories.
- 	Docker repository is a collection of different docker images with the same name, that have different tags, each tag usually represents a different
  	version of the image.


	DockerHub: https://hub.docker.com/explore/
	Why using official Images
- 	Clear Documentation
-	Dedicated Team for Reviewing Image Content 
- 	Security Update ina Timely Manner

Run First Hello World Docker Container:
dilmac:~ DilMac$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
dilmac:~ DilMac$ 

docker run repository:tag command[arguments]

dilmac$ docker run busybox:1.27 echo ' Welcome to docker tutorials'

dilmac:~ DilMac$ docker run busybox:1.27 echo ' Welcome to docker tutorials'
Unable to find image 'busybox:1.27' locally
1.27: Pulling from library/busybox
9e87eff13613: Pull complete 
Digest: sha256:2605a2c4875ce5eb27a9f7403263190cd1af31e48a2044d400320548356251c4
Status: Downloaded newer image for busybox:1.27
 Welcome to docker tutorials

dilmac:~ DilMac$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
busybox             1.27                efe10ee6727f        3 weeks ago         1.13MB

dilmac:~ DilMac$ docker run busybox:1.27 echo ' Welcome to docker tutorials'
 Welcome to docker tutorials
dilmac:~ DilMac$ 

dilmac:~ DilMac$ docker run busybox:1.27 ls /
bin
dev
etc
home
proc
root
sys
tmp
usr
var
dilmac:~ DilMac$ 

INFO:

The -i flag starts an interactive container 
The -t flag creates a pseudi-TTY that attaches stdin and stdout

Create contaer:
dilmac:~ DilMac$ docker run -i -t busybox:1.27
/ # ls
bin   dev   etc   home  proc  root  sys   tmp   usr   var
/ # touch al.txt
/ # ls
al.txt  bin     dev     etc     home    proc    root    sys     tmp     usr     var
/ # exit
dilmac:~ DilMac$ docker run -i -t busybox:1.27
/ # ls
bin   dev   etc   home  proc  root  sys   tmp   usr   var
/ # 

Deep Dive into Docker Containers:
	1. running containers in detached mode
	2. docker ps command
	3. docker container name 
	4. docker inspect command	


The Linux sleep command is used to delay for a specified amount of time 
dilmac:~ DilMac$ docker run -d busybox:1.27 sleep 1000
0776d26d2742f55855f174f26bfcf06842f21b5601a1f30b7302fbd5ddcdf838
dilmac:~ DilMac$ 

This is container ID >> 0776d26d2742f55855f174f26bfcf06842f21b5601a1f30b7302fbd5ddcdf838

The docker ps commad used to running all docker container in background:

dilmac:~ DilMac$ docker ps
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
0776d26d2742        busybox:1.27        "sleep 1000"        3 minutes ago       Up 3 minutes  


dilmac:~ DilMac$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
0776d26d2742        busybox:1.27        "sleep 1000"             5 minutes ago       Up 5 minutes                                    quizzical_jang
6d0eaeea76c5        busybox:1.27        "sh"                     11 minutes ago      Exited (0) 5 minutes ago                        unruffled_beaver
827166497d50        busybox:1.27        "sh"                     12 minutes ago      Exited (0) 11 minutes ago                       zen_agnesi
72373e4de39c        busybox:1.27        "ls /"                   16 minutes ago      Exited (0) 16 minutes ago                       mystifying_turing
34c2fbe72195        busybox:1.27        "echo ' Welcome to..."   23 minutes ago      Exited (0) 23 minutes ago                       tender_morse
d07cc6234914        busybox:1.27        "echo ' Welcome to..."   25 minutes ago      Exited (0) 25 minutes ago                       fervent_hopper


dilmac:~ DilMac$ docker run --rm busybox:1.27 sleep 1
dilmac:~ DilMac$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
0776d26d2742        busybox:1.27        "sleep 1000"             6 minutes ago       Up 6 minutes                                    quizzical_jang
6d0eaeea76c5        busybox:1.27        "sh"                     13 minutes ago      Exited (0) 7 minutes ago                        unruffled_beaver
827166497d50        busybox:1.27        "sh"                     13 minutes ago      Exited (0) 13 minutes ago                       zen_agnesi
72373e4de39c        busybox:1.27        "ls /"                   17 minutes ago      Exited (0) 17 minutes ago                       mystifying_turing
34c2fbe72195        busybox:1.27        "echo ' Welcome to..."   24 minutes ago      Exited (0) 24 minutes ago                       tender_morse
d07cc6234914        busybox:1.27        "echo ' Welcome to..."   26 minutes ago      Exited (0) 26 minutes ago                       fervent_hopper
dilmac:~ DilMac$ 


dilmac:~ DilMac$ docker run --name Welcome_to_docker_tutorials busybox:1.27
dilmac:~ DilMac$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                      PORTS               NAMES
e09d2ef6accf        busybox:1.27        "sh"                     5 seconds ago       Exited (0) 4 seconds ago                        Welcome_to_docker_tutorials
0776d26d2742        busybox:1.27        "sleep 1000"             9 minutes ago       Up 9 minutes                                    quizzical_jang
6d0eaeea76c5        busybox:1.27        "sh"                     16 minutes ago      Exited (0) 10 minutes ago                       unruffled_beaver
827166497d50        busybox:1.27        "sh"                     16 minutes ago      Exited (0) 16 minutes ago                       zen_agnesi
72373e4de39c        busybox:1.27        "ls /"                   20 minutes ago      Exited (0) 20 minutes ago                       mystifying_turing
34c2fbe72195        busybox:1.27        "echo ' Welcome to..."   27 minutes ago      Exited (0) 27 minutes ago                       tender_morse
d07cc6234914        busybox:1.27        "echo ' Welcome to..."   29 minutes ago      Exited (0) 29 minutes ago                       fervent_hopper
dilmac:~ DilMac$ 



Docker inspect displays the low level information about a container or image:

dilmac:~ DilMac$ docker run -d busybox:1.27 sleep 200
d9573849f303093375ede78375ea7a0400ffce63da87633711d5ef53769dbf7f
dilmac:~ DilMac$ docker inspect d9573849f303093375ede78375ea7a0400ffce63da87633711d5ef53769dbf7f
[
    {
        "Id": "d9573849f303093375ede78375ea7a0400ffce63da87633711d5ef53769dbf7f",
        "Created": "2017-08-13T23:26:32.546208927Z",
        "Path": "sleep",
        "Args": [
            "200"
        ],
        "State": {
            "Status": "running",
            "Running": true,
            "Paused": false,
            "Restarting": false,
            "OOMKilled": false,
            "Dead": false,
            "Pid": 7533,
            "ExitCode": 0,
            "Error": "",
            "StartedAt": "2017-08-13T23:26:32.695505545Z",
            "FinishedAt": "0001-01-01T00:00:00Z"
        },
        "Image": "sha256:efe10ee6727fe52d2db2eb5045518fe98d8e31fdad1cbdd5e1f737018c349ebb",
        "ResolvConfPath": "/mnt/sda1/var/lib/docker/containers/d9573849f303093375ede78375ea7a0400ffce63da87633711d5ef53769dbf7f/resolv.conf",
        "HostnamePath": "/mnt/sda1/var/lib/docker/containers/d9573849f303093375ede78375ea7a0400ffce63da87633711d5ef53769dbf7f/hostname",
        "HostsPath": "/mnt/sda1/var/lib/docker/containers/d9573849f303093375ede78375ea7a0400ffce63da87633711d5ef53769dbf7f/hosts",
        "LogPath": "/mnt/sda1/var/lib/docker/containers/d9573849f303093375ede78375ea7a0400ffce63da87633711d5ef53769dbf7f/d9573849f303093375ede78375ea7a0400ffce63da87633711d5ef53769dbf7f-json.log",
        "Name": "/eager_montalcini",
        "RestartCount": 0,
        "Driver": "aufs",
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
            "PortBindings": {},
            "RestartPolicy": {
                "Name": "no",
                "MaximumRetryCount": 0
            },
            "AutoRemove": false,
            "VolumeDriver": "",
            "VolumesFrom": null,
            "CapAdd": null,
            "CapDrop": null,
            "Dns": [],
            "DnsOptions": [],
            "DnsSearch": [],
            "ExtraHosts": null,
            "GroupAdd": null,
            "IpcMode": "",
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
            "ConsoleSize": [
                0,
                0
            ],
            "Isolation": "",
            "CpuShares": 0,
            "Memory": 0,
            "NanoCpus": 0,
            "CgroupParent": "",
            "BlkioWeight": 0,
            "BlkioWeightDevice": null,
            "BlkioDeviceReadBps": null,
            "BlkioDeviceWriteBps": null,
            "BlkioDeviceReadIOps": null,
            "BlkioDeviceWriteIOps": null,
            "CpuPeriod": 0,
            "CpuQuota": 0,
            "CpuRealtimePeriod": 0,
            "CpuRealtimeRuntime": 0,
            "CpusetCpus": "",
            "CpusetMems": "",
            "Devices": [],
            "DeviceCgroupRules": null,
            "DiskQuota": 0,
            "KernelMemory": 0,
            "MemoryReservation": 0,
            "MemorySwap": 0,
            "MemorySwappiness": -1,
            "OomKillDisable": false,
            "PidsLimit": 0,
            "Ulimits": null,
            "CpuCount": 0,
            "CpuPercent": 0,
            "IOMaximumIOps": 0,
            "IOMaximumBandwidth": 0
        },
        "GraphDriver": {
            "Data": null,
            "Name": "aufs"
        },
        "Mounts": [],
        "Config": {
            "Hostname": "d9573849f303",
            "Domainname": "",
            "User": "",
            "AttachStdin": false,
            "AttachStdout": false,
            "AttachStderr": false,
            "Tty": false,
            "OpenStdin": false,
            "StdinOnce": false,
            "Env": [
                "PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin"
            ],
            "Cmd": [
                "sleep",
                "200"
            ],
            "Image": "busybox:1.27",
            "Volumes": null,
            "WorkingDir": "",
            "Entrypoint": null,
            "OnBuild": null,
            "Labels": {}
        },
        "NetworkSettings": {
            "Bridge": "",
            "SandboxID": "bd77da3a18c5b9a7fed8051a4f1e6b28749a68d11fe47cbd3eb91cfe80a95146",
            "HairpinMode": false,
            "LinkLocalIPv6Address": "",
            "LinkLocalIPv6PrefixLen": 0,
            "Ports": {},
            "SandboxKey": "/var/run/docker/netns/bd77da3a18c5",
            "SecondaryIPAddresses": null,
            "SecondaryIPv6Addresses": null,
            "EndpointID": "29448e84f85d0f83673a6e2caf2ae74af2128d7a897454db47d90080735a657c",
            "Gateway": "172.17.0.1",
            "GlobalIPv6Address": "",
            "GlobalIPv6PrefixLen": 0,
            "IPAddress": "172.17.0.3",
            "IPPrefixLen": 16,
            "IPv6Gateway": "",
            "MacAddress": "02:42:ac:11:00:03",
            "Networks": {
                "bridge": {
                    "IPAMConfig": null,
                    "Links": null,
                    "Aliases": null,
                    "NetworkID": "8a6aa3ee748097f06f981dad2618145eff8674338c50f0ee33e2e004dc56547d",
                    "EndpointID": "29448e84f85d0f83673a6e2caf2ae74af2128d7a897454db47d90080735a657c",
                    "Gateway": "172.17.0.1",
                    "IPAddress": "172.17.0.3",
                    "IPPrefixLen": 16,
                    "IPv6Gateway": "",
                    "GlobalIPv6Address": "",
                    "GlobalIPv6PrefixLen": 0,
                    "MacAddress": "02:42:ac:11:00:03",
                    "DriverOpts": null
                }
            }
        }
    }
]
dilmac:~ DilMac$ 

##########################################################################################
Question 1:
Which docker command will display low-level information on a container?


docker ps

docker inspect == correct

docker info 

docker logs
##########################################################################################
                        ##         .
                  ## ## ##        ==
               ## ## ## ## ##    ===
           /"""""""""""""""""\___/ ===
      ~~~ {~~ ~~~~ ~~~ ~~~~ ~~~ ~ /  ===- ~~~
           \______ o           __/
             \    \         __/
              \____\_______/


docker is configured to use the default machine with IP 192.168.99.100
For help getting started, check out the docs at https://docs.docker.com 

Docker Port Mapping and Docker Logs:
https://hub.docker.com/_/tomcat/

dilmac:~ DilMac$ docker run -it -p 8888:8080 tomcat:8.0
Unable to find image 'tomcat:8.0' locally
8.0: Pulling from library/tomcat
ad74af05f5a2: Pull complete 
2b032b8bbe8b: Pull complete 
99a5213ead46: Pull complete 
7de34ca31efd: Pull complete 
9b22e57d98bb: Pull complete 
12cd7a66c3fd: Pull complete 
880bb942de44: Pull complete 
6ada99602995: Pull complete 
90451a97de52: Pull complete 
646677f3b1ed: Pull complete 
c10d6538fe29: Pull complete 
63e2edd468f7: Pull complete 
Digest: sha256:1f34d503e3e339433a84df80615fb658ab16491361353b6d7e1342b2b80cf7f0
Status: Downloaded newer image for tomcat:8.0
Using CATALINA_BASE:   /usr/local/tomcat
Using CATALINA_HOME:   /usr/local/tomcat
Using CATALINA_TMPDIR: /usr/local/tomcat/temp
Using JRE_HOME:        /docker-java-home/jre
Using CLASSPATH:       /usr/local/tomcat/bin/bootstrap.jar:/usr/local/tomcat/bin/tomcat-juli.jar
13-Aug-2017 23:36:34.485 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server version:        Apache Tomcat/8.0.45
13-Aug-2017 23:36:34.488 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server built:          Jun 26 2017 20:06:07 UTC
13-Aug-2017 23:36:34.488 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server number:         8.0.45.0
13-Aug-2017 23:36:34.489 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log OS Name:               Linux
13-Aug-2017 23:36:34.489 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log OS Version:            4.4.74-boot2docker
13-Aug-2017 23:36:34.489 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Architecture:          amd64
13-Aug-2017 23:36:34.490 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Java Home:             /usr/lib/jvm/java-7-openjdk-amd64/jre
13-Aug-2017 23:36:34.490 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log JVM Version:           1.7.0_131-b00
13-Aug-2017 23:36:34.490 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log JVM Vendor:            Oracle Corporation
13-Aug-2017 23:36:34.491 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log CATALINA_BASE:         /usr/local/tomcat
13-Aug-2017 23:36:34.491 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log CATALINA_HOME:         /usr/local/tomcat
13-Aug-2017 23:36:34.492 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.util.logging.config.file=/usr/local/tomcat/conf/logging.properties
13-Aug-2017 23:36:34.492 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager
13-Aug-2017 23:36:34.492 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djdk.tls.ephemeralDHKeySize=2048
13-Aug-2017 23:36:34.492 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.protocol.handler.pkgs=org.apache.catalina.webresources
13-Aug-2017 23:36:34.493 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.endorsed.dirs=/usr/local/tomcat/endorsed
13-Aug-2017 23:36:34.493 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dcatalina.base=/usr/local/tomcat
13-Aug-2017 23:36:34.493 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dcatalina.home=/usr/local/tomcat
13-Aug-2017 23:36:34.493 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.io.tmpdir=/usr/local/tomcat/temp
13-Aug-2017 23:36:34.494 INFO [main] org.apache.catalina.core.AprLifecycleListener.lifecycleEvent Loaded APR based Apache Tomcat Native library 1.2.12 using APR version 1.5.1.
13-Aug-2017 23:36:34.494 INFO [main] org.apache.catalina.core.AprLifecycleListener.lifecycleEvent APR capabilities: IPv6 [true], sendfile [true], accept filters [false], random [true].
13-Aug-2017 23:36:34.497 INFO [main] org.apache.catalina.core.AprLifecycleListener.initializeSSL OpenSSL successfully initialized (OpenSSL 1.1.0f  25 May 2017)
13-Aug-2017 23:36:34.630 INFO [main] org.apache.coyote.AbstractProtocol.init Initializing ProtocolHandler ["http-apr-8080"]
13-Aug-2017 23:36:34.648 INFO [main] org.apache.coyote.AbstractProtocol.init Initializing ProtocolHandler ["ajp-apr-8009"]
13-Aug-2017 23:36:34.651 INFO [main] org.apache.catalina.startup.Catalina.load Initialization processed in 1062 ms
13-Aug-2017 23:36:34.703 INFO [main] org.apache.catalina.core.StandardService.startInternal Starting service Catalina
13-Aug-2017 23:36:34.727 INFO [main] org.apache.catalina.core.StandardEngine.startInternal Starting Servlet Engine: Apache Tomcat/8.0.45
13-Aug-2017 23:36:34.745 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory /usr/local/tomcat/webapps/manager
13-Aug-2017 23:36:35.883 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory /usr/local/tomcat/webapps/manager has finished in 1,138 ms
13-Aug-2017 23:36:35.885 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory /usr/local/tomcat/webapps/host-manager
13-Aug-2017 23:36:35.960 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory /usr/local/tomcat/webapps/host-manager has finished in 75 ms
13-Aug-2017 23:36:35.960 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory /usr/local/tomcat/webapps/ROOT
13-Aug-2017 23:36:35.993 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory /usr/local/tomcat/webapps/ROOT has finished in 33 ms
13-Aug-2017 23:36:35.998 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory /usr/local/tomcat/webapps/examples
13-Aug-2017 23:36:36.711 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory /usr/local/tomcat/webapps/examples has finished in 713 ms
13-Aug-2017 23:36:36.735 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory /usr/local/tomcat/webapps/docs
13-Aug-2017 23:36:36.796 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory /usr/local/tomcat/webapps/docs has finished in 61 ms
13-Aug-2017 23:36:36.799 INFO [main] org.apache.coyote.AbstractProtocol.start Starting ProtocolHandler ["http-apr-8080"]
13-Aug-2017 23:36:36.846 INFO [main] org.apache.coyote.AbstractProtocol.start Starting ProtocolHandler ["ajp-apr-8009"]
13-Aug-2017 23:36:36.905 INFO [main] org.apache.catalina.startup.Catalina.start Server startup in 2253 ms


CHECK the browser with the IP address 192.168.99.100:8888

To close control + c 
To check the tomcat containe: docker ps -a 

dilmac:~ DilMac$ docker ps -a
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                         PORTS               NAMES
ddeb0880de1f        tomcat:8.0          "catalina.sh run"        6 minutes ago       Exited (130) 7 seconds ago                         sleepy_hugle
d9573849f303        busybox:1.27        "sleep 200"              16 minutes ago      Exited (0) 12 minutes ago                          eager_montalcini
e09d2ef6accf        busybox:1.27        "sh"                     19 minutes ago      Exited (0) 19 minutes ago                          Welcome_to_docker_tutorials
0776d26d2742        busybox:1.27        "sleep 1000"             28 minutes ago      Exited (0) 12 minutes ago                          quizzical_jang
6d0eaeea76c5        busybox:1.27        "sh"                     35 minutes ago      Exited (0) 29 minutes ago                          unruffled_beaver
827166497d50        busybox:1.27        "sh"                     35 minutes ago      Exited (0) 35 minutes ago                          zen_agnesi
72373e4de39c        busybox:1.27        "ls /"                   39 minutes ago      Exited (0) 39 minutes ago                          mystifying_turing
34c2fbe72195        busybox:1.27        "echo ' Welcome to..."   About an hour ago   Exited (0) About an hour ago                       tender_morse
d07cc6234914        busybox:1.27        "echo ' Welcome to..."   About an hour ago   Exited (0) About an hour ago                       fervent_hopper


Find container ID: 
dilmac:~ DilMac$ docker run -it -d -p 8888:8080 tomcat:8.0
69a7b62204558064645556913d1a4d715e9c0d8c5a7f705485b4fe5d441a4639


dilmac:~ DilMac$ docker logs 69a7b62204558064645556913d1a4d715e9c0d8c5a7f705485b4fe5d441a4639
Using CATALINA_BASE:   /usr/local/tomcat
Using CATALINA_HOME:   /usr/local/tomcat
Using CATALINA_TMPDIR: /usr/local/tomcat/temp
Using JRE_HOME:        /docker-java-home/jre
Using CLASSPATH:       /usr/local/tomcat/bin/bootstrap.jar:/usr/local/tomcat/bin/tomcat-juli.jar
13-Aug-2017 23:43:49.349 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server version:        Apache Tomcat/8.0.45
13-Aug-2017 23:43:49.358 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server built:          Jun 26 2017 20:06:07 UTC
13-Aug-2017 23:43:49.358 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Server number:         8.0.45.0
13-Aug-2017 23:43:49.359 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log OS Name:               Linux
13-Aug-2017 23:43:49.359 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log OS Version:            4.4.74-boot2docker
13-Aug-2017 23:43:49.359 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Architecture:          amd64
13-Aug-2017 23:43:49.360 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Java Home:             /usr/lib/jvm/java-7-openjdk-amd64/jre
13-Aug-2017 23:43:49.360 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log JVM Version:           1.7.0_131-b00
13-Aug-2017 23:43:49.360 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log JVM Vendor:            Oracle Corporation
13-Aug-2017 23:43:49.361 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log CATALINA_BASE:         /usr/local/tomcat
13-Aug-2017 23:43:49.361 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log CATALINA_HOME:         /usr/local/tomcat
13-Aug-2017 23:43:49.362 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.util.logging.config.file=/usr/local/tomcat/conf/logging.properties
13-Aug-2017 23:43:49.362 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.util.logging.manager=org.apache.juli.ClassLoaderLogManager
13-Aug-2017 23:43:49.363 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djdk.tls.ephemeralDHKeySize=2048
13-Aug-2017 23:43:49.363 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.protocol.handler.pkgs=org.apache.catalina.webresources
13-Aug-2017 23:43:49.363 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.endorsed.dirs=/usr/local/tomcat/endorsed
13-Aug-2017 23:43:49.363 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dcatalina.base=/usr/local/tomcat
13-Aug-2017 23:43:49.364 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Dcatalina.home=/usr/local/tomcat
13-Aug-2017 23:43:49.364 INFO [main] org.apache.catalina.startup.VersionLoggerListener.log Command line argument: -Djava.io.tmpdir=/usr/local/tomcat/temp
13-Aug-2017 23:43:49.364 INFO [main] org.apache.catalina.core.AprLifecycleListener.lifecycleEvent Loaded APR based Apache Tomcat Native library 1.2.12 using APR version 1.5.1.
13-Aug-2017 23:43:49.365 INFO [main] org.apache.catalina.core.AprLifecycleListener.lifecycleEvent APR capabilities: IPv6 [true], sendfile [true], accept filters [false], random [true].
13-Aug-2017 23:43:49.371 INFO [main] org.apache.catalina.core.AprLifecycleListener.initializeSSL OpenSSL successfully initialized (OpenSSL 1.1.0f  25 May 2017)
13-Aug-2017 23:43:49.542 INFO [main] org.apache.coyote.AbstractProtocol.init Initializing ProtocolHandler ["http-apr-8080"]
13-Aug-2017 23:43:49.569 INFO [main] org.apache.coyote.AbstractProtocol.init Initializing ProtocolHandler ["ajp-apr-8009"]
13-Aug-2017 23:43:49.578 INFO [main] org.apache.catalina.startup.Catalina.load Initialization processed in 1162 ms
13-Aug-2017 23:43:49.687 INFO [main] org.apache.catalina.core.StandardService.startInternal Starting service Catalina
13-Aug-2017 23:43:49.687 INFO [main] org.apache.catalina.core.StandardEngine.startInternal Starting Servlet Engine: Apache Tomcat/8.0.45
13-Aug-2017 23:43:49.704 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory /usr/local/tomcat/webapps/manager
13-Aug-2017 23:43:51.987 WARNING [localhost-startStop-1] org.apache.catalina.util.SessionIdGeneratorBase.createSecureRandom Creation of SecureRandom instance for session ID generation using [SHA1PRNG] took [1,183] milliseconds.
13-Aug-2017 23:43:52.013 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory /usr/local/tomcat/webapps/manager has finished in 2,309 ms
13-Aug-2017 23:43:52.014 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory /usr/local/tomcat/webapps/host-manager
13-Aug-2017 23:43:52.055 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory /usr/local/tomcat/webapps/host-manager has finished in 41 ms
13-Aug-2017 23:43:52.056 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory /usr/local/tomcat/webapps/ROOT
13-Aug-2017 23:43:52.092 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory /usr/local/tomcat/webapps/ROOT has finished in 36 ms
13-Aug-2017 23:43:52.093 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory /usr/local/tomcat/webapps/examples
13-Aug-2017 23:43:52.881 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory /usr/local/tomcat/webapps/examples has finished in 788 ms
13-Aug-2017 23:43:52.895 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deploying web application directory /usr/local/tomcat/webapps/docs
13-Aug-2017 23:43:52.960 INFO [localhost-startStop-1] org.apache.catalina.startup.HostConfig.deployDirectory Deployment of web application directory /usr/local/tomcat/webapps/docs has finished in 65 ms
13-Aug-2017 23:43:52.971 INFO [main] org.apache.coyote.AbstractProtocol.start Starting ProtocolHandler ["http-apr-8080"]
13-Aug-2017 23:43:53.019 INFO [main] org.apache.coyote.AbstractProtocol.start Starting ProtocolHandler ["ajp-apr-8009"]
13-Aug-2017 23:43:53.058 INFO [main] org.apache.catalina.startup.Catalina.start Server startup in 3478 ms

#######################################################################################################################################
Question 1:
What is the format for port mapping in Docker run command?


container_port : host_port

host_port : container_port   == Corect

#######################################################################################################################################


DOCKER IMAGE LAYERS
dilmac:~ DilMac$ docker history busybox:1.27
IMAGE               CREATED             CREATED BY                                      SIZE                COMMENT
efe10ee6727f        3 weeks ago         /bin/sh -c #(nop)  CMD ["sh"]                   0B                  
<missing>           3 weeks ago         /bin/sh -c #(nop) ADD file:0516fc7a5988ef4...   1.13MB  

The above results display two layers 
1. All changes made into the running containers will be written into the writable layer 
2. When the container is deleted, the writable layer also deleted, but the underlying image remains unchanged
3. Multiple containers can share access to the same underlaying image.

#######################################################################################################################################
Question 1:
Which is of the following statements is NOT true?


A Docker image is made up of a list of read-only layers that represent file system differences.

We can check the full set of layers which make up an image by running the docker images command. == Correct

When we create a new container, we add a new, thin, writable layer on top of the underlying image layers

#######################################################################################################################################





















