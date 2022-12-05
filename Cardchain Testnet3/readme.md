 ***Updated daily at 13:00*** 748M

                    



```

systemctl stop Cardchaind.service

cp $HOME/.Cardchain/data/priv_validator_state.json $HOME/.Cardchain/priv_validator_state.json.backup

rm -rf ~/.Cardchain/data; \
mkdir -p ~/.Cardchain/data; \
cd ~/.Cardchain/data


SNAP_NAME=$(curl -s http://snapshots.bccnodes.com/testnets/cardchain/ | egrep -o ">testnet3.*\.tar" | tail -n 1 | tr -d '>'); \
wget -O - http://snapshots.bccnodes.com/testnets/cardchain/${SNAP_NAME} | tar xf -

mv $HOME/.Cardchain/priv_validator_state.json.backup $HOME/.Cardchain/data/priv_validator_state.json


wget -O $HOME/.Cardchain/config/addrbook.json "https://raw.githubusercontent.com/BccNodes/Snapshot-Statesync/main/Acre%20Chain%20Mainnet/addrbook.json"



systemctl start Cardchaind.service; \
journalctl -u Cardchaind.service -f --no-hostname

```
