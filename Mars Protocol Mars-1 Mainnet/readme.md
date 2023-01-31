*** Updated daily at 13:00***


```

systemctl stop marsd.service

cp $HOME/.mars/data/priv_validator_state.json $HOME/.mars/priv_validator_state.json.backup

rm -rf ~/.mars/data; \
mkdir -p ~/.mars/data; \
cd ~/.mars/data


SNAP_NAME=$(curl -s https://snapshots.bccnodes.com/mainnets/mars/ | egrep -o ">ares-1.*tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots.bccnodes.com/mainnets/mars/${SNAP_NAME} | tar xf -

mv $HOME/.mars/priv_validator_state.json.backup $HOME/.mars/data/priv_validator_state.json


wget -O $HOME/.mars/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Mars%20Protocol%20Mars-1%20Mainnet/addrbook.json"



systemctl start marsd.service; \
journalctl -u marsd.service -f --no-hostname

```
