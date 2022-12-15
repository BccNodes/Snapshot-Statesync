*** Updated daily at 13:00 | 6.0G***


```

systemctl stop humansd.service

cp $HOME/.humans/data/priv_validator_state.json $HOME/.humans/priv_validator_state.json.backup

rm -rf ~/.humans/data; \
mkdir -p ~/.humans/data; \
cd ~/.humans/data


SNAP_NAME=$(curl -s https://snapshots.bccnodes.com/testnets/humans/ | egrep -o ">testnet-1.*tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots.bccnodes.com/testnets/humans/${SNAP_NAME} | tar xf -

mv $HOME/.humans/priv_validator_state.json.backup $HOME/.humans/data/priv_validator_state.json


wget -O $HOME/.humans/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Chain4Energy%20Mainnet/addrbook.json"



systemctl start humansd.service; \
journalctl -u humansd.service -f --no-hostname

```
