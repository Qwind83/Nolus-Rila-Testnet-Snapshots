# Nolus-Rila-Testnet-Snapshots
Snapshot allows you to sync Nolus Rila Testnet node by downloading data and wasm folders.

Guide

1. Stop service file, create backup of priv_validator_state file.
```
systemctl stop nolusd
cp $HOME/.nolus/data/priv_validator_state.json $HOME/.nolus/priv_validator_state.json.backup
```
2. Remove existing database.
```
rm -rf $HOME/.nolus/data
rm -rf $HOME/.nolus/wasm
```
3. Get data folder.
```
wget http://194.163.174.222/nolus/data_nolus-rila.tar
tar -xf data_nolus-rila.tar -C $HOME/.nolus/data/
rm data_nolus-rila.tar
```
4. Get wasm folder.
```
wget http://194.163.174.222/nolus/wasm_nolus-rila.tar
mkdir $HOME/.nolus/wasm/
tar -xf wasm_nolus-rila.tar -C $HOME/.nolus/wasm/
rm wasm_nolus-rila.tar
```
5. Recover backup of priv_validator_state file.
```
mv $HOME/.nolus/priv_validator_state.json.backup $HOME/.nolus/data/priv_validator_state.json
```
6. Re-launch service.
```
systemctl restart nolusd
journalctl -u nolusd -f -o cat
```
