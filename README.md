# Fractal-Bitcoin

# Cấu hình tối thiểu 👻

CPU : 2+
RAM : Min 4 GB
Storage : Min 100 GB SSD 

# Chạy 2 câu lệnh update ( bắt buộc )

```
sudo apt-get update && sudo apt-get upgrade -y
```
```
sudo apt install curl build-essential pkg-config libssl-dev git wget jq make gcc chrony -y
```

# Tạo file data
```
git clone https://github.com/fractal-bitcoin/fractald-release.git
```
```
cd /root/fractald-release/fractald-x86_64-linux-gnu
```
```
mkdir data
```
```
cp ./bitcoin.conf ./data
```

# Tạo file service

```
tee /etc/systemd/system/fractald.service > /dev/null <<EOF
[Unit]
Description=Fractal Node
After=network.target
[Service]
User=root
ExecStart=/root/fractald-release/fractald-x86_64-linux-gnu/bin/bitcoind -datadir=/root/fractald-release/fractald-x86_64-linux-gnu/data/ -maxtipage=504576000
Restart=always
RestartSec=3
LimitNOFILE=infinity
[Install]
WantedBy=multi-user.target
EOF
```

# Khởi chạy

```
sudo systemctl daemon-reload
```
```
sudo systemctl enable fractald
```
```
sudo systemctl start fractald
```
```
sudo journalctl -u fractald -fo cat
```

# Tạo ví

# ( NHỚ ĐỔI TÊN VÍ )

```
echo 'export WALLETW="walletname"' >> $HOME/.bashrc && source $HOME/.bashrc
```

```
cd /root/fractald-release/fractald-x86_64-linux-gnu/bin
```

```
./bitcoin-wallet -wallet="$WALLETW" -legacy create
```

# Lấy Privatekey
```
cd /root/fractald-release/fractald-x86_64-linux-gnu/bin
./bitcoin-wallet -wallet=/root/.bitcoin/wallets/$WALLETW/wallet.dat -dumpfile=/root/.bitcoin/wallets/$WALLETW/MyPK.dat dump
cd
cat .bitcoin/wallets/$WALLETW/MyPK.dat
```
