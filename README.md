Test Net

## Installation and configuration environment
```bash
wget https://golang.org/dl/go1.16.linux-amd64.tar.gz

tar xvf go1.16.linux-amd64.tar.gz  -C  /usr/local

sudo sh -c 'echo "export PATH=$PATH:/usr/local/go/bin" >> /etc/profile'

source /etc/profile

apt update

apt install screen mesa-opencl-icd ocl-icd-opencl-dev gcc git bzr jq pkg-config curl clang build-essential hwloc libhwloc-dev wget -y && sudo apt upgrade -y


curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh

source $HOME/.cargo/env
```

## Set environment variables

```bash
export FFI_BUILD_FROM_SOURCE=1 

export RUSTFLAGS="-C target-cpu=native -g"

export FIL_PROOFS_PARAMETER_CACHE=/data/.parameter 

export FIL_PROOFS_PARENT_CACHE=/data/.parent
```
# if run in china
```bash
export IPFS_GATEWAY=https://proof-parameters.s3.cn-south-1.jdcloud-oss.com/ipfs/
```
## Install and compile
```bash
cd /root

git clone https://github.com/WorldDbs/test_net

git clone https://github.com/WorldDbu1/world_database_change

cd test_net

cd extern 

git clone https://github.com/filecoin-project/filecoin-ffi

git clone https://github.com/filecoin-project/serialization-vectors

git clone https://github.com/filecoin-project/test-vectors

cd ../

go clean -modcache

go mod tidy  

make 2k
```

## Compilation is complete

```bash
./lotus fetch-params 536870912

./lotus-seed pre-seal --sector-size 536870912 --num-sectors 1

./lotus-seed genesis new localnet.json 

./lotus-seed genesis add-miner localnet.json ~/.genesis-sectors/pre-seal-w01000.json
```

## start up
```bash
./lotus daemon --lotus-make-genesis=genesis.car --genesis-template=localnet.json --bootstrap=false
```
## Import wallet

```bash

./lotus wallet import --as-default ~/.genesis-sectors/pre-seal-w01000.key

```
## Configure founding miner miner operation
```bash
./lotus-miner init --genesis-miner --actor=w01000 --pre-sealed-sectors=/root/.genesis-sectors --pre-sealed-metadata=/root/.genesis-sectors/pre-seal-w01000.json --nosync
```

## Run miner
```bash
./lotus-miner run --nosync
```

## View address
```bash
./lotus net listen
```
## Join the master node
```bash
./lotus net connect /ip4/***.***.***.***/tcp/****/p2p/****
```
