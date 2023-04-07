```
sudo systemctl stop defundd

cp $HOME/.defund/data/priv_validator_state.json $HOME/.defund/priv_validator_state.json.backup

rm -rf $HOME/.defund/data
```

```
curl -L https://snapshots.bccnodes.com/testnets/defund/defund_*.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.defund

mv $HOME/.defund/priv_validator_state.json.backup $HOME/.defund/data/priv_validator_state.json
```

```
sudo systemctl start defundd && sudo journalctl -u defundd -f --no-hostname -o cat
```
