# Introduction
MPC wallet service is a distributed key generation and distributed signature service that can serve as a distributed custodial solution.

*Note : mpc is considered beta software. We make no warranties or guarantees of its security or stability.*

# Install the Docker version
## 1. Install Docker. This depends on your platform, on Ubuntu this works:
```
sudo apt update
sudo apt install docker.io
```
## 2. Download the Docker image and create and run the container:
- bootnode
```
docker run -d --name bootnode --network host --restart always -v /var/lib/docker/bootnode:/bootnode anyswap/bootnode --addr :48447
```
- mpcnode
```
docker run -d --name mpcnode --network host --restart always -v /var/lib/docker/mpcnode:/mpcnode anyswap/anympcnode
```
default: `rpcport 6669`, port 6661 bootnodes enode://cdefe85532587f6ee0bbc29790aca7d54bf633b9fc19c991fe9af1b67284460d586928003a6af69c210fba8a1cce9f009a37d695382e34034b10d05b3df3ac8f@47.88.26.170:48447
- mpcnode-client
```
docker exec mpcnode mpcnode-client --cmd ACCEPTREQADDR --url http://127.0.0.1:6669 --keystore keystore --passwd "123456" --key 0x...
```

# Install the Source version
# Prerequisites
1. VPS server with 1 CPU and 2G mem
2. Static public IP
3. Golang ^1.12

# Setting Up
## Clone The Repository
To get started, launch your terminal and download the latest version of the SDK.
```
mkdir -p $GOPATH/src/github.com/fsn-dev

cd $GOPATH/src/github.com/fsn-dev

git clone https://github.com/fsn-dev/dcrm-walletService.git
```
## Build
Next compile the code.  Make sure you are in dcrm-walletService directory.
```
cd dcrm-walletService && make
```

## Run
First generate the node key: 
```
./bin/cmd/gdcrm --genkey node1.key
```

then run the dcrm node 7x24 in the background:
```
nohup ./bin/cmd/gdcrm --nodekey node1.key &
```
The `gdcrm` will provide rpc service, the default RPC port is port 4449.

Note: 
Before use [walletService RPC API](https://github.com/fsn-dev/dcrm-walletService/wiki/walletService-RPC-API), please wait at least 5 minutes after running the node which need to prepare dcrm env.

# Front-end

After running the dcrm wallet rpc service and get the rpc IP:port, we can use [SMPCWallet](https://github.com/fsn-dev/SMPCWallet/releases) to connect the rpc service. This front-end can create distributed custodial account which support BTC/ETH/FSN.


