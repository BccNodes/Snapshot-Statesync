```
sudo systemctl stop lavad

cp $HOME/.lava/data/priv_validator_state.json $HOME/.lava/priv_validator_state.json.backup

rm -rf $HOME/.source/data
```

```
curl -L https://snapshots-3.bccnodes.com/lava/lava-snapshot.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.lava

mv $HOME/.lava/priv_validator_state.json.backup $HOME/.lava/data/priv_validator_state.json
```

```
sudo systemctl start lavad && sudo journalctl -u lavad -f --no-hostname -o cat
```
