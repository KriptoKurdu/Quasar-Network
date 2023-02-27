# Quasar-Network


### Kurulum

```
source <(curl -s https://raw.githubusercontent.com/KriptoKurdu/Quasar-Network/main/quasar.sh?token=GHSAT0AAAAAAB6LGPTX54GCNZYHADKMALSSY74WHUA)
```



### Snapshot
```
cd $HOME
sudo apt install snapd -y
snap install lz4
```
```
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
```

Senkronizasyon kontrol
```
quasarnoded status 2>&1 | jq .SyncInfo
```
## Explorer
```
https://testnet.ping.pub/quasar
```

### Cüzdan ekleme

```
quasard keys add wallet
```
## Faucet
```
 https://discord.gg/quasarfi
```
### Validator olusturma
```
quasard tx staking create-validator \
--amount=1000000uqsr \
--pubkey=$(quasard tendermint show-validator) \
--moniker="$NODE_MONIKER" \
--chain-id=qsr-questnet-04 \
--commission-rate=0.1 \
--commission-max-rate=0.2 \
--commission-max-change-rate=0.05 \
--min-self-delegation=1 \
--from=wallet \
-y
  ```
    
    
    
    


