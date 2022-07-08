# Morocco-1: Setting Up Chronic Chain Node or Validator

## Run a fullnode / validator by compiling source code (not recommended for new users).

<aside>
💡 chtd is a blockchain application built using **Cosmos SDK** and **Tendermint**.

You can run the validator software using the binary or by compiling it from source

Before you start, you might want to ensure your system is up to date.

</aside>

### Installing Prerequisites

```bash
sudo apt-get update && sudo apt upgrade -y
sudo apt-get install make build-essential git jq chrony -y
```

```bash
sudo apt install gcc
```

### Increasing the default open files limit.

If we don't raise this value, nodes will crash once the network grows large enough.

```bash
sudo su -c "echo 'fs.file-max = 65536' >> /etc/sysctl.conf"
sudo sysctl -p
```

### Install Go from source

```bash
curl https://dl.google.com/go/go1.18.2.linux-amd64.tar.gz | sudo tar -C/usr/local -zxvf -
```

### Update environment variables:  (copy & paste all)

```bash
cat <<'EOF' >>$HOME/.profile
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export GOBIN=$HOME/go/bin
export PATH=$PATH:/usr/local/go/bin:$GOBIN
EOF

source $HOME/.profile
```
### Download Starport: 
```bash
curl https://get.starport.network/starport! | bash
```

### Clone the source repo:

```bash
git clone https://github.com/ChronicNetwork/cht.git
cd cht
git checkout
```

### Build the chain:

```bash
starport chain build
```

### Initialize the blockchain:

```bash
chtd init Foundation-node-1 —chain-id morocco-1
```

### Create new key’s, Or, import existing wallet with BEP32 mnenomic phrase

```bash
chtd keys add <KEY_NAME> --keyring-backend os
```

Or, to recover existing wallet:

```bash
chtd keys add foundation-node-1 --keyring-backend os --recover
```

### Create environment Variable:

```bash
MY_VALIDATOR_ADDRESS=$(chtd keys show <KEY_NAME> -a --keyring-backend os)
```

### Add Persistent Peers:

```bash
TBD
```
### Add Seed Nodes:
```bash
TBD
```

### Copy genesis file:

```bash
	cd $HOME
wget -O $HOME/.cht/config/genesis.json https://raw.githubusercontent.com/ChronicNetwork/net/main/mainnet/v1.1/genesis.json
```
### Set Minimum Gas Prices:
```bash
TBD
```

### Start the network:

```bash
chtd start
```

Your node should now be catching up to the current state of the network!

If you want to participate in the active validator set , please reach out into the discord with your chronic wallet address and tokens from the development wallet can be sent for the delegation minimum and gas fee’s.

### Create Validator Command

```bash
chtd tx staking create-validator \
  --amount=100000000ucht \
  --pubkey=$(chtd tendermint show-validator) \
  --moniker="your-moniker" \
  --chain-id=morocco-1 \
  --commission-rate="0.05" \
  --commission-max-rate="0.20" \
  --commission-max-change-rate="0.01" \
  --min-self-delegation="1" \
  --fees="250000ucgas" \
  --gas="700000" \
  --from=(keyofyourvalidator)
```

### Setup chtd systemd service (copy and paste all to create the file service. Enable and activate the chtd service.

```bash
sudo touch /etc/systemd/system/chtd.service && \
sudo nano /etc/systemd/system/chtd.service 
```

### Insert content into chtd.service

```bash
[Unit]
Description=Chronic Node
After=network-online.target

[Service]
User=root
ExecStart=/root/go/bin/chtd start
Restart=always
RestartSec=3
LimitNOFILE=4096

[Install]
WantedBy=multi-user.target
```

### Move file to systemd folder

```bash
sudo mv /etc/systemd/system/chtd.service /lib/systemd/system/
sudo systemctl enable chtd.service && sudo systemctl start chtd.service
```

### Check info about node:

```bash
curl -s localhost:26657/status  | jq .result.sync_info.catching_up
#true output is syncing - false is synced
curl -s localhost:26657/status | jq .result.sync_info.latest_block_height
#this output is your last block synced
curl -s "http://:26657/status?"  | jq .result.sync_info.latest_block_height
#this output the public node last block synced
```

###
