# Quasar-Network


sudo apt-get update -y 
sudo apt-get install curl build-essential wget jq git -y;


sudo rm -rf /usr/local/go;
curl https://dl.google.com/go/go1.19.2.linux-amd64.tar.gz | sudo tar -C/usr/local -zxvf - ;
cat <<'EOF' >>$HOME/.profile
export GOROOT=/usr/local/go
export GOPATH=$HOME/go
export GO111MODULE=on
export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin
EOF
source $HOME/.profile




cd $HOME
wget https://github.com/quasar-finance/binary-release/raw/main/v0.0.2-alpha-11/quasarnoded-linux-amd64
chmod +x quasarnoded-linux-amd64
mkdir -p $HOME/go/bin
sudo mv quasarnoded-linux-amd64 $HOME/go/bin/quasarnoded



moniker=<monikerAdi>
quasarnoded init $moniker --chain-id=qsr-questnet-04 --home $HOME/.quasarnode
quasarnoded config chain-id qsr-questnet-04



wget -O $HOME/.quasarnode/config/genesis.json https://raw.githubusercontent.com/quasar-finance/questnet/main/v04/definitive-genesis.json





PEERS="8a19aa6e874ed5720aad2e7d02567ec932d92d22@141.94.248.63:26656,444b80ce750976df59b88ac2e08d720e1dbbf230@68.183.75.239:26666,20b4f9207cdc9d0310399f848f057621f7251846@222.106.187.13:40606,7ef67269c8ec37ff8a538a5ae83ca670fd2da686@137.184.192.123:26656,19afe579cc0a2b38ca87143f779f45e9a7f18a2f@18.134.191.148:26656,a23f002bda10cb90fa441a9f2435802b35164441@38.146.3.203:18256,bba6e85e3d1f1d9c127324e71a982ddd86af9a99@88.99.3.158:18256,966acc999443bae0857604a9fce426b5e09a7409@65.108.105.48:18256 ,177144bed1e280a6f2435d253441e3e4f1699c6d@65.109.85.226:8090,769ebaa9942375e70cebc21a75a2cfda41049d99@135.181.210.186:26656,8937bdacf1f0c8b2d1ffb4606554eaf08bd55df4@5.75.255.107:26656,99a0695a7358fa520e6fcd46f91492f7cf205d4d@34.175.159.249:26656,47401f4ac3f934afad079ddbe4733e66b58b67da@34.175.244.202:26656"
seeds="7ed8e233e5fdb21bf70ac7f635130c7a8b0a4967@quasar-testnet-seed.swiss-staking.ch:10056"
sed -i.bak -e "s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.quasarnode/config/config.toml
sed -i.bak -e "s/^seeds *=.*/seeds = \"$seeds\"/" ~/.quasarnode/config/config.toml




pruning="custom" && \
pruning_keep_recent="100" && \
pruning_keep_every="0" && \
pruning_interval="10" && \
sed -i -e "s/^pruning *=.*/pruning = \"$pruning\"/" $HOME/.quasarnode/config/app.toml && \
sed -i -e "s/^pruning-keep-recent *=.*/pruning-keep-recent = \"$pruning_keep_recent\"/" $HOME/.quasarnode/config/app.toml && \
sed -i -e "s/^pruning-keep-every *=.*/pruning-keep-every = \"$pruning_keep_every\"/" $HOME/.quasarnode/config/app.toml && \
sed -i -e "s/^pruning-interval *=.*/pruning-interval = \"$pruning_interval\"/" $HOME/.quasarnode/config/app.toml





sudo tee <<EOF >/dev/null /etc/systemd/system/quasarnoded.service
[Unit]
Description=quasarnoded daemon
After=network-online.target
[Service]
User=$USER
ExecStart=$(which quasarnoded) start --home $HOME/.quasarnode
Restart=on-failure
RestartSec=3
LimitNOFILE=10000
[Install]
WantedBy=multi-user.target
EOF



sudo systemctl daemon-reload && \
sudo systemctl enable quasarnoded && \
sudo systemctl start quasarnoded



sudo journalctl -u quasarnoded -f




cd $HOME
sudo apt install snapd -y
snap install lz4
sudo systemctl stop quasarnoded
quasarnoded tendermint unsafe-reset-all --home $HOME/.quasarnode --keep-addr-book
cp $HOME/.quasarnode/data/priv_validator_state.json $HOME/.quasarnode/priv_validator_state.json.backup
wget -O quasar.tar.lz4 https://snapshot.silentvalidator.com/testnet/quasar/quasar-2023-02-19T15%3A14.tar.lz4  --inet4-only
wget -O wasm-quasar.tar.lz4 https://snapshot.silentvalidator.com/testnet/quasar/wasm-quasar-2023-02-19T15%3A14.tar.lz4 --inet4-only
quasarnoded tendermint unsafe-reset-all --home $HOME/.quasarnode --keep-addr-book
lz4 -c -d quasar.tar.lz4  | tar -x -C $HOME/.quasarnode
lz4 -c -d wasm-quasar.tar.lz4  | tar -x -C $HOME/.quasarnode
mv $HOME/.quasarnode/priv_validator_state.json.backup $HOME/.quasarnode/data/priv_validator_state.json
sudo systemctl restart quasarnoded && journalctl -u quasarnoded -f -o cat





daemon=quasarnoded
denom=uqsr
moniker=验证人名
chainid=qsr-questnet-04
$daemon tx staking create-validator \
    --amount=1000000$denom \
    --pubkey=$($daemon tendermint show-validator) \
    --moniker=$moniker \
    --chain-id=$chainid \
    --commission-rate=0.05 \
    --commission-max-rate=0.2 \
    --commission-max-change-rate=0.1 \
    --min-self-delegation=1000000 \
    --from=cüzdanAdi
    
    
    
    
    


