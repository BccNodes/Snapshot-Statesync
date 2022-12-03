***2022-12-03_20:58:22    |  LAST_BLOCK_HEIGHT 183422    |   2.4G***               ***Updated daily at 13:00***  

                    



```

systemctl stop acred.service

cp $HOME/.acred/data/priv_validator_state.json $HOME/.acred/priv_validator_state.json.backup

rm -rf ~/.acred/data; \
mkdir -p ~/.acred/data; \
cd ~/.acred/data


SNAP_NAME=$(curl -s http://snapshots.bccnodes.com/mainnets/acre/ | egrep -o ">acre_9052-1.*\.tar" | tail -n 1 | tr -d '>'); \
wget -O - http://snapshots.bccnodes.com/mainnets/acre/${SNAP_NAME} | tar xf -

mv $HOME/.acred/priv_validator_state.json.backup $HOME/.acred/data/priv_validator_state.json


wget -O $HOME/.acred/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Chain4Energy%20Mainnet/addrbook.json"



systemctl start acred.service; \
journalctl -u acred.service -f --no-hostname

```
