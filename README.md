# Nolus Rila Testnet

<p align="center">
  <img src="https://github.com/quxeed/snap/blob/main/1500x500.jpg" alt="alt text" width="750" height="250">
</p>

Nolus Protocol is a Web3 financial suite that offers an innovative approach to money markets with a novel lease solution to develop the DeFi space further. The Protocol utilizes a lightning-fast semi-permissioned proof-of-stake Layer-1 blockchain built using the Cosmos SDK, where smart contracts are developed in Rust and executed within the isolated sandboxing model by CosmWASM enforcing robust security and multi-chain compatibility.

# How To Process Nolus Snapshot

### 1. Install lz4 if needed

```
sudo apt update
sudo apt install snapd -y
sudo snap install lz4
```

### 2. Set pruning to `nothing`
app.toml
```
pruning = "nothing"
```

### 3. Set indexer to `null`
config.toml
```
indexer = "null"
```

### 4. Stop your node and backup your `priv_validator_state.json`
```
sudo systemctl stop nolusd
cp $HOME/.nolus/data/priv_validator_state.json $HOME/.nolus/data/priv_validator_state.json.backup
rm -rf $HOME/.nolus/data
```

### 5.Download snapshot
## Height `1249114` 05.03.2023 19.2gb
```
wget http://185.202.223.124:8100/nolus-snap-05032023.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.nolus
mv $HOME/.nolus/priv_validator_state.json.backup $HOME/.nolus/data/priv_validator_state.json
```

### 6. Restart the service and check the log
```
sudo systemctl start nolusd && sudo journalctl -u nolusd -f --no-hostname -o cat
```
