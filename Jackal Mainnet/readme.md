***2022-12-03_14:35:49    |  LAST_BLOCK_HEIGHT 434364    |   3.5G***
```systemctl stop canined.service

cp $HOME/.canine/data/priv_validator_state.json $HOME/.canine/priv_validator_state.json.backup

rm -rf ~/.canine/data; \
mkdir -p ~/.canine/data; \
cd ~/.canine/data


SNAP_NAME=$(curl -s http://snapshots.bccnodes.com/mainnets/jackal/ | egrep -o ">jackal.*tar" | tail -n 1 | tr -d '>'); \
wget -O - http://snapshots.bccnodes.com/mainnets/jackal/${SNAP_NAME} | tar xf -

mv $HOME/.canine/priv_validator_state.json.backup $HOME/.canine/data/priv_validator_state.json


systemctl start canined.service; \
journalctl -u canined.service -f --no-hostname```
