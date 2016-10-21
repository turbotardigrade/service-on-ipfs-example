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