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

