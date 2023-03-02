******


```

systemctl stop andromad.service

cp $HOME/.androma/data/priv_validator_state.json $HOME/.androma/priv_validator_state.json.backup

rm -rf ~/.androma/data; \
mkdir -p ~/.androma/data; \
cd ~/.androma/data


SNAP_NAME=$(curl -s https://snapshots-2.bccnodes.com/testnets/androma/ | egrep -o ">androma-1_2023-03-02.tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots-2.bccnodes.com/testnets/androma/${SNAP_NAME} | tar xf -

mv $HOME/.androma/priv_validator_state.json.backup $HOME/.androma/data/priv_validator_state.json


wget -O $HOME/.androma/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Androma%20Testnet/addrbook.json"



systemctl start andromad.service; \
journalctl -u andromad.service -f --no-hostname

```
