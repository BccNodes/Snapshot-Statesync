*** Updated daily at 13:00***


```

systemctl stop nibid.service

cp $HOME/.nibid/data/priv_validator_state.json $HOME/.nibid/priv_validator_state.json.backup

rm -rf ~/.nibid/data; \
mkdir -p ~/.nibid/data; \
cd ~/.nibid/data


SNAP_NAME=$(curl -s https://snapshots.bccnodes.com/testnets/nibiru/ | egrep -o ">nibiru-testnet-2.*tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots.bccnodes.com/testnets/nibiru/${SNAP_NAME} | tar xf -

mv $HOME/.nibid/priv_validator_state.json.backup $HOME/.nibid/data/priv_validator_state.json


wget -O $HOME/.nibid/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Nibiru%20Testnet-2/addrbook.json"



systemctl start nibid.service; \
journalctl -u nibid.service -f --no-hostname

```
