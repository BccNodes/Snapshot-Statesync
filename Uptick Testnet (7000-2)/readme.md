***2022-12-03_20:58:22    |  LAST_BLOCK_HEIGHT 183422    |   2.4G***               ***Updated daily at 13:00***  

                    



```

systemctl stop uptickd.service

cp $HOME/.uptickd/data/priv_validator_state.json $HOME/.uptickd/priv_validator_state.json.backup

rm -rf ~/.uptickd/data; \
mkdir -p ~/.uptickd/data; \
cd ~/.uptickd/data


SNAP_NAME=$(curl -s http://snapshots.bccnodes.com/tesnets/uptick/ | egrep -o ">uptick_7000-2.*\.tar" | tail -n 1 | tr -d '>'); \
wget -O - http://snapshots.bccnodes.com/testnets/uptick/${SNAP_NAME} | tar xf -

mv $HOME/.uptickd/priv_validator_state.json.backup $HOME/.uptickd/data/priv_validator_state.json


wget -O $HOME/.uptickd/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Acre%20Chain%20Mainnet/addrbook.json"



systemctl start uptickd.service; \
journalctl -u uptickd.service -f --no-hostname

```
