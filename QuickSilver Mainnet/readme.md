 ***Updated daily at 13:00*** 2.5G 

                    



```

systemctl stop quicksilverd.service

cp $HOME/.quicksilverd/data/priv_validator_state.json $HOME/.quicksilverd/priv_validator_state.json.backup

rm -rf ~/.quicksilverd/data; \
mkdir -p ~/.quicksilverd/data; \
cd ~/.quicksilverd/data


SNAP_NAME=$(curl -s https://snapshots.bccnodes.com/mainnets/quicksilver/ | egrep -o ">quicksilver-1.*\.tar" | tail -n 1 | tr -d '>'); \
wget -O - https://snapshots.bccnodes.com/mainnets/quicksilver/${SNAP_NAME} | tar xf -

mv $HOME/.quicksilverd/priv_validator_state.json.backup $HOME/.quicksilverd/data/priv_validator_state.json


wget -O $HOME/.quicksilverd/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Acre%20Chain%20Mainnet/addrbook.json"



systemctl start quicksilverd.service; \
journalctl -u quicksilverd.service -f --no-hostname

```
