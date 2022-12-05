***UPDATED DAILY 13:00 - 72G***
```

systemctl stop rebusd.service

cp $HOME/.rebusd/data/priv_validator_state.json $HOME/.rebusd/priv_validator_state.json.backup

rm -rf ~/.rebusd/data; \
mkdir -p ~/.rebusd/data; \
cd ~/.rebusd/data


SNAP_NAME=$(curl -s https://snapshots.bccnodes.com/mainnets/rebus/ | egrep -o ">reb_1111-1.*\.tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots.bccnodes.com/mainnets/rebus/${SNAP_NAME} | tar xf -

mv $HOME/.rebusd/priv_validator_state.json.backup $HOME/.rebusd/data/priv_validator_state.json

systemctl start rebusd.service; \
journalctl -u rebusd.service -f --no-hostname

```
