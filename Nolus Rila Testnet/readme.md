***  Updated daily at 13:00     |  112MB***             

                    



```

systemctl stop nolusd.service

cp $HOME/.nolus/data/priv_validator_state.json $HOME/.nolus/priv_validator_state.json.backup

rm -rf ~/.nolus/data; \
mkdir -p ~/.nolus/data; \
cd ~/.nolus/data


SNAP_NAME=$(curl -s https://snapshots.bccnodes.com/testnets/nolus/ | egrep -o ">nolus-rila.*\.tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots.bccnodes.com/testnets/nolus/${SNAP_NAME} | tar xf -

mv $HOME/.nolus/priv_validator_state.json.backup $HOME/.nolus/data/priv_validator_state.json


wget -O $HOME/.nolus/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Nolus%20Rila%20Testnet/addrbook.json"



systemctl start nolusd.service; \
journalctl -u nolusd.service -f --no-hostname

```
