******


```

systemctl stop althea

cp $HOME/.althea/data/priv_validator_state.json $HOME/.althea/priv_validator_state.json.backup

rm -rf ~/.althea/data; \
mkdir -p ~/.althea/data; \
cd ~/.althea/data


SNAP_NAME=$(curl -s https://snapshots-3.bccnodes.com/althea/ | egrep -o ">althea_7357-1_2023-03-04.tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots-3.bccnodes.com/althea/${SNAP_NAME} | tar xf -

mv $HOME/.althea/priv_validator_state.json.backup $HOME/.althea/data/priv_validator_state.json


wget -O $HOME/.althea/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Althea%20Testnet/addrbook.json"



systemctl start althea; \
journalctl -u althea -f --no-hostname

```
