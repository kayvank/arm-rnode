Rnode on raspberry pi 3b
-----
Deploying [Rchain node](https://github.com/kayvank/rchain) on [Raspberry pi 3b+](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/)
deployment:
* OS installation
* Prerequisite libraries and tools
* set up classpath
* rchain build

## OS installation
Rnode, at this time, required a 64 bit architecture.  For this project I selected [openSUSE](https://www.opensuse.org/). 
Installation binaries:  [rasperry pi openSUSE](https://en.opensuse.org/HCL:Raspberry_Pi3) 
Some good OS installation tutorials:
* [HCL Raspberry Pi3](https://en.opensuse.org/HCL:Raspberry_Pi3)
* [installation video](https://www.youtube.com/watch?v=UA9ByJwWhzs) 

Here are my  OS specifics:

```
pi@lucid-pi:~> cat /etc/os-release
NAME="openSUSE Leap"
VERSION="42.3"
ID=opensuse
ID_LIKE="suse"
VERSION_ID="42.3"
PRETTY_NAME="openSUSE Leap 42.3"
ANSI_COLOR="0;32"
CPE_NAME="cpe:/o:opensuse:leap:42.3"
BUG_REPORT_URL="https://bugs.opensuse.org"
HOME_URL="https://www.opensuse.org/"
```
## Prerequisite
all these tools are available thru [openSUSE YaSt](https://en.opensuse.org/Portal:YaST)
Install:
* jdk8-devel
* automake cmake
* apr-util 
* ninja
* gcc c++
* lmdb-devel 
* openSSL
* libtool
* tls 

Download and install [libsodium](https://download.libsodium.org/doc/installation/ ) as outlined in the wiki

To bring up node, follow the [rchain rnode instruction](# Rnode on raspberry pi 3b
Deploying [Rchain node](https://github.com/kayvank/rchain) on [Raspberry pi 3b+](https://www.raspberrypi.org/products/raspberry-pi-3-model-b/)
The  deployment 
* OS installation
* Prerequisite libraries and tools
* rchain build

## OS installation

Rnode, at this time, required a 64 bit architecture.  For this project I selected [openSUSE](https://www.opensuse.org/). 
Installation binaries:  [rasperry pi openSUSE](https://en.opensuse.org/HCL:Raspberry_Pi3) 
Some good OS installation tutorials:
* [HCL Raspberry Pi3](https://en.opensuse.org/HCL:Raspberry_Pi3)
* [installation video](https://www.youtube.com/watch?v=UA9ByJwWhzs) 

Here are my  OS specifics:

```
pi@lucid-pi:~> cat /etc/os-release
NAME="openSUSE Leap"
VERSION="42.3"
ID=opensuse
ID_LIKE="suse"
VERSION_ID="42.3"
PRETTY_NAME="openSUSE Leap 42.3"
ANSI_COLOR="0;32"
CPE_NAME="cpe:/o:opensuse:leap:42.3"
BUG_REPORT_URL="https://bugs.opensuse.org"
HOME_URL="https://www.opensuse.org/"
```
## Prerequisite
all these tools are available thru [openSUSE YaSt](https://en.opensuse.org/Portal:YaST)
Install:
* jdk8-devel
* automake cmake
* apr-util 
* ninja
* gcc c++
* lmdb-devel 
* openSSL
* libtool
* tls 

Download and install [libsodium](https://download.libsodium.org/doc/installation/ ) as outlined in the wiki
u)

## Set up CLASSPATH
add these to your ~/.profile
```
export M2_HOME=$HOME/.m2
export JAVA_OPTS="-Xms256m -Xmx512m"
export CLASSPATH="$CLASSPATH:$HOME/.local/share/java/java-cup-11b.jar"
export CLASSPATH="$CLASSPATH:$HOME/.local/share/java/java-cup-11b-runtime.jar"
export CLASSPATH=$CLASSPATH:$M2_HOME/repository/io/netty/netty-tcnative-boringssl-static/2.0.13.Final-SNAPSHOT/netty-tcnative-boringssl-static-2.0.13.Final-SNAPSHOT-linux-aarch_64.jar
export CLASSPATH=$CLASSPATH:$M2_HOME/repository/io/netty/netty-tcnative-boringssl-static/2.0.13.Final-SNAPSHOT/netty-tcnative-boringssl-static-2.0.13.Final-SNAPSHOT.jar
export SBT_OPTS="-Xms256m -Xmx512m"
```

## Deploy Rchain
* deploy the pi-built [image](./image) as outlined below
* deploy your locally-built image

### deploy pi-built image
Note that this is a special build of the rchain rnode for the purpose of the raspberry pi.  You may simply run the image as outlined below.  To run node on pi, follow [rchain rnode exexution instruction](https://github.com/rchain/rchain/tree/dev/node#32-bootstrapping-a-private-network)

```
git clone  git@github.com:kayvank/rchain-node-bin.git
cd rchain-node
run ./bin/rnode -s -p 4000
```

### deploy locally-built image
* This is based on my [fork of the rchain](https://github.com/kayvank/rchain/tree/raspberry-pi) project.  

```
git clone git@github.com:kayvank/rchain.git
## make sure you use the raspberry-pi branch
git checkout -b raspberry-pi && git pull origin raspberry-pi  
```

follow [Developers guide](https://github.com/kayvank/rchain/tree/raspberry-pi#deverloper-guide)

#### NOTE
#####This is a hack for now.  
for now you have to manually modify the ./bin/run script  add the system classpath to the script. See line [341 EOL](https://github.com/kayvank/rchain-node-bin/blob/master/bin-image/bin/rnode#L341)
