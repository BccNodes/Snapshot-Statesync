******


```

systemctl stop c4ed.service

cp $HOME/.c4e-chain/data/priv_validator_state.json $HOME/.c4e-chain/priv_validator_state.json.backup

rm -rf ~/.c4e-chain/data; \
mkdir -p ~/.c4e-chain/data; \
cd ~/.c4e-chain/data


SNAP_NAME=$(curl -s https://c4e-snapshot.bccnodes.com/c4e/ | egrep -o ">perun-1.*tar" | tail -n 1 | tr -d '>'); \
wget -O - https://c4e-snapshot.bccnodes.com/c4e/${SNAP_NAME} | tar xf -

mv $HOME/.c4e-chain/priv_validator_state.json.backup $HOME/.c4e-chain/data/priv_validator_state.json


wget -O $HOME/.c4e-chain/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Chain4Energy%20Mainnet/addrbook.json"



systemctl start c4ed && journalctl -u c4ed.service -f --no-hostname

```
