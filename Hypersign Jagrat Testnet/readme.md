***  Updated daily at 13:00     |  3.2G***             

                    



```

systemctl stop hid-noded.service

cp $HOME/.hid-node/data/priv_validator_state.json $HOME/.hid-node/priv_validator_state.json.backup

rm -rf ~/.hid-node/data; \
mkdir -p ~/.hid-node/data; \
cd ~/.hid-node/data


SNAP_NAME=$(curl -s https://snapshots.bccnodes.com/tesnets/hypersign/ | egrep -o ">jagrat.*\.tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots.bccnodes.com/testnets/hypersign/${SNAP_NAME} | tar xf -

mv $HOME/.hid-node/priv_validator_state.json.backup $HOME/.hid-node/data/priv_validator_state.json


wget -O $HOME/.hid-node/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Hypersign%20Jagrat%20Testnet/addrbook.json"



systemctl start hid-noded.service; \
journalctl -u hid-noded.service -f --no-hostname

```
