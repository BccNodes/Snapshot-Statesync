*** Updated daily at 13:00 ***             

                    



```

systemctl stop defundd.service

cp $HOME/.defund/data/priv_validator_state.json $HOME/.defund/priv_validator_state.json.backup

rm -rf ~/.defund/data; \
mkdir -p ~/.defund/data; \
cd ~/.defund/data


SNAP_NAME=$(curl -s https://snapshots.bccnodes.com/tesnets/defund/ | egrep -o ">defund-private-4_*\.tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots.bccnodes.com/testnets/defund/${SNAP_NAME} | tar xf -

mv $HOME/.defund/priv_validator_state.json.backup $HOME/.defund/data/priv_validator_state.json


wget -O $HOME/.defund/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Defund-private-4%20Testnet/addrbook.json"



systemctl start defundd.service; \
journalctl -u defundd.service -f --no-hostname

```
