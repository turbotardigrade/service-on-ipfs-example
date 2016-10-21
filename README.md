# Making your own IPFS service Example
Example provided [here](https://ipfs.io/ipfs/QmTkzDwWqPbnAh5YiV5VwcTLnGdwSNsNTn2aDxdXBFca7D/example#/ipfs/QmQwAP9vFjbCtKvD8RkJdCvPHqLQjZfW7Mqbbqx18zd8j7/api/service/readme.md) is not working anymore. Here is a (currently) working one and a walk through of getting it running.

## Get the dependencies

### Get Go1.7
Steps summarized from [here](https://github.com/moovweb/gvm)

#### Get GVM
```
zsh < <(curl -s -S -L https://raw.githubusercontent.com/moovweb/gvm/master/binscripts/gvm-installer)
```
Or if you are using bash just change zsh with bash

#### Install go1.4 first (needed for bootstrapping for go1.5+)

```
gvm install go1.4 -B
gvm use go1.4
```

#### Install go1.7

```
export GOROOT_BOOTSTRAP=$GOROOT
gvm install go1.7
```

#### Use go1.7 by default

```gvm use go1.7 --default```

### Get IPFS from source and install it:
Steps summarized from [here](go get -u -d github.com/ipfs/go-ipfs)

```
go get -u -d github.com/ipfs/go-ipfs
cd $GOPATH/src/github.com/ipfs/go-ipfs
make install
```

## Run server and client:
You will need to create two nodes on `~/.ipfs` and `~/.ipfs2`. See the section below, if you don't know how to create new nodes.

```
$ cd server
$ go run server.go

I am peer: [PeerID]
```

Make client connect to that PeerID:
```
$ cd client
$ IPFS_PATH=~/.ipfs2 go run client.go [PeerID]
```

## Running two nodes on a single machine

Usually, when you start with IPFS, you will use `ipfs init`, which will create a new node. The default data and config stored for that particular node are located at `~/.ipfs`. **In this example a new node at `~/.ipfs2` is needed.** Here is how you can create that node and config it so it can run besides your default node.

### 1. Create a new node

```
IPFS_PATH=~/.ipfs2 ipfs init
```
This will create a new node at ~/.ipfs2 (not using the default path).

### 2. Change Address Configs
As both of your nodes now bind to the same ports, you need to change the port configuration, so both nodes can run side by side. For this, open ~/.ipfs2/config` and find `Addresses`:

```
"Addresses": {
    "API": "/ip4/127.0.0.1/tcp/5001",
    "Gateway": "/ip4/127.0.0.1/tcp/8080",
    "Swarm": [
        "/ip4/0.0.0.0/tcp/4001",
        "/ip6/::/tcp/4001"
    ]
}
```

To for example the following:

```
"Addresses": {
    "API": "/ip4/127.0.0.1/tcp/5002",
    "Gateway": "/ip4/127.0.0.1/tcp/8081",
    "Swarm": [
        "/ip4/0.0.0.0/tcp/4002",
        "/ip6/::/tcp/4002"
    ]
}
```

## 