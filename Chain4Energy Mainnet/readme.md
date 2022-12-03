***2022-12-03_15:31:49    |  LAST_BLOCK_HEIGHT 1103710    |   2.0G***


```

systemctl stop c4ed.service

cp $HOME/.c4e-chain/data/priv_validator_state.json $HOME/.c4e-chain/priv_validator_state.json.backup

rm -rf ~/.c4e-chain/data; \
mkdir -p ~/.c4e-chain/data; \
cd ~/.c4e-chain/data


SNAP_NAME=$(curl -s http://snapshots.bccnodes.com/mainnets/c4e/ | egrep -o ">perun-1_2022-12-03.tar" | tail -n 1 | tr -d '>'); \
wget -O - http://snapshots.bccnodes.com/mainnets/jackal/${SNAP_NAME} | tar xf -

mv $HOME/.c4e-chain/priv_validator_state.json.backup $HOME/.c4e-chain/data/priv_validator_state.json


wget -O $HOME/.c4e-chain/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Jackal%20Mainnet/addrbook.json"



systemctl start c4ed.service; \
journalctl -u c4ed.service -f --no-hostname

```
