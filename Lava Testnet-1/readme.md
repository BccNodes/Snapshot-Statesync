*** Updated daily at 13:00*** 


```

systemctl stop lavad.service

cp $HOME/.lava/data/priv_validator_state.json $HOME/.lava/priv_validator_state.json.backup

rm -rf ~/.lava/data; \
mkdir -p ~/.lava/data; \
cd ~/.lava/data


SNAP_NAME=$(curl -s https://snapshots.bccnodes.com/testnets/lava/ | egrep -o ">lava-testnet-1_2023-01-23.tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots.bccnodes.com/testnets/lava/${SNAP_NAME} | tar xf -

mv $HOME/.lava/priv_validator_state.json.backup $HOME/.lava/data/priv_validator_state.json


wget -O $HOME/.lava/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Humans%20Testnet-1/addrbook.json"



systemctl start lavad.service; \
journalctl -u lavad.service -f --no-hostname

```
