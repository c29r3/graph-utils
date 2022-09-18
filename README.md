# graph-utils

## Install Golang  
```bash
curl -s https://gist.githubusercontent.com/c29r3/3130b5cd51c4a94f897cc58443890c28/raw/134d86f8a90b2bbb7c68cd6bb663c60c5846ae31/install_golang.sh | bash -s - 1.18
```

## Install Erigon  
```bash
cd ~ \
&& git clone https://github.com/ledgerwatch/erigon.git \
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

## Nethermind Archive_Node (testnet)

```
sudo apt update && \
sudo add-apt-repository ppa:nethermindeth/nethermind && \
sudo apt install nethermind -y && \
sudo bash -c 'echo "nethermind soft nofile 1000000" > /etc/security/limits.d/nethermind.conf'
```


```
echo '
[Unit]
Description=Nethermind Node
After=network.target

[Service]
User=root
#EnvironmentFile=/root/nethermind/data/.env
WorkingDirectory=/root/nethermind
Restart=on-failure
LimitNOFILE=1000000
ExecStart=/usr/bin/nethermind \
  --datadir /root/nethermind/data \
  --config xdai_archive \
  --Merge.Enabled=True \
  --Network.P2PPort=30303 \
  --Network.DiscoveryPort=30303 \
  --JsonRpc.Enabled=True \
  --JsonRpc.Timeout=20000 \
  --JsonRpc.Host="127.0.0.1" \
  --JsonRpc.Port=8545 \
  --JsonRpc.EnabledModules="Eth,Subscribe,Trace,TxPool,Web3,Personal,Proof,Net,Parity,Health" \
  --JsonRpc.EnginePort=8551 \
  --JsonRpc.EngineHost="127.0.0.1" \
  --JsonRpc.JwtSecretFile="/root/nethermind/data/jwt-secret"


[Install]
WantedBy=default.target' > /etc/systemd/system/nethermind.service ; \
sudo systemctl daemon-reload; \
sudo systemctl enable nethermind; \
sudo systemctl restart nethermind; \
journalctl -u nethermind -f --no-hostname
```
