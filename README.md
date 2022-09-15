# graph-utils

## Install Golang  
```bash
curl -s https://gist.githubusercontent.com/c29r3/3130b5cd51c4a94f897cc58443890c28/raw/134d86f8a90b2bbb7c68cd6bb663c60c5846ae31/install_golang.sh | bash -s - 1.18
```

## Install Erigon  
```bash
cd ~ \
&& git clone https://github.com/ledgerwatch/erigon.git; \
&& cd erigon \
&& git checkout alpha \
&& make erigon \
&& cp ~/erigon/build/bin/erigon ~/go/bin/
```

## Create Erigon service file  
```bash
curl -s https://raw.githubusercontent.com/c29r3/graph-utils/main/erigon.service > /etc/systemd/system/erigon.service ; \
systemctl daemon-reload ; \
systemctl enable erigon ; \
systemctl start erigon ; \
journalctl -u erigon -f --no-hostname
```

Check sync  
`curl -X POST -H "Content-Type: application/json" --data '{"jsonrpc": "2.0", "method":
"eth_blockNumber", "params": [], "id":1}' localhost:8545`

## Install Lighthouse 
``` 
cd ~; \
mkdir lighthouse; \
cd lighthouse ; \
wget -O - https://github.com/sigp/lighthouse/releases/download/v3.1.0/lighthouse-v3.1.0-x86_64-unknown-linux-gnu.tar.gz | tar xzf -; \
cp lighthouse ~/go/bin/ ; \
lighthouse --version
```

## Create Lighthouse service file  
```bash
curl -s https://raw.githubusercontent.com/c29r3/graph-utils/main/lighthouse.service > /etc/systemd/system/lighthouse.service ; \
systemctl daemon-reload ; \
systemctl enable lighthouse ; \
systemctl start lighthouse ; \
journalctl -u lighthouse -f --no-hostname
```
