![Logo](https://github.com/CrazySerGo/Mainnets/raw/main/aura/aura-logo.png)
## Aura

RPC, API, Explorer: soon

## Install node
```bash
sudo apt update
sudo apt install curl make clang pkg-config libssl-dev build-essential git jq -y
```
#### Install go
```bash
cd $HOME
VERSION=1.20.2
wget -O go.tar.gz https://go.dev/dl/go$VERSION.linux-amd64.tar.gz
sudo rm -rf /usr/local/go && sudo tar -C /usr/local -xzf go$VERSION.linux-amd64.tar.gz
echo 'export GOROOT=/usr/local/go' >> $HOME/.bash_profile
echo 'export GOPATH=$HOME/go' >> $HOME/.bash_profile
echo 'export GO111MODULE=on' >> $HOME/.bash_profile
echo 'export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin' >> $HOME/.bash_profile && . $HOME/.bash_profile
go version
```
#### Build binary
```bash
cd $HOME
rm -rf aura
git clone https://github.com/aura-nw/aura.git
cd aura
git checkout aura_v0.4.4
make install
aurad version
```
#### Init node and download genesis
```bash
aurad init node --chain-id xstaxy-1
wget -O $HOME/.aura/config/genesis.json https://raw.githubusercontent.com/aura-nw/mainnet-artifacts/main/xstaxy-1/genesis.json
```
#### Config node
```bash
sed -i 's/^minimum-gas-prices *=.*/minimum-gas-prices = "0.001uaura"/' $HOME/.aura/config/app.toml
```
#### Create service
```bash
sudo tee /etc/systemd/system/aurad.service > /dev/null <<EOF
[Unit]
Description=Aura Node
After=network.target

[Service]
User=$USER
Type=simple
ExecStart=$HOME/go/bin/aurad start
Restart=on-failure
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target"
EOF
```
####  Start node
```bash
sudo systemctl daemon-reload
sudo systemctl enable aurad
sudo systemctl restart aurad
journalctl -fu aurad -o cat
```
## StateSync
```bash
soon
```
### Download addrbook.json (Updated every hour):
```bash
soon
```
