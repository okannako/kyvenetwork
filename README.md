![0_6nZNquAdQ54CBzZ8](https://user-images.githubusercontent.com/73176377/166442048-557ed9da-81d7-4be2-98a2-9a6a1014e3cd.png)

# Sistem Gereksinimleri (Protocol Node)
- 1vCPU
- 4GB RAM
- 1GB DISK
- Ubuntu 20.04


+Siteye girip, Continue ye basıp, download yapıp, cüzdanı indirip, tweet atıp, onaylanmasını bekliyoruz. İnen dosyanın adını arweave.json olarak değiştirip winscp aracılığıyla /root/kyve/ yolunun içine atıyoruz. 
 https://faucet.arweave.net/
 
+Keplr cüzdan oluşturuyoruz. https://www.keplr.app/ (Bilmiyorsanız ---->>>> https://youtu.be/-P4j2NCz_c8?t=98 )

# Kurulum Adımları
```
sudo apt update && apt install unzip
mkdir -p /root/kyve
cd /root/kyve && wget https://github.com/kyve-org/zilliqa/releases/download/v1.0.0/kyve-zilliqa-linux.zip && unzip kyve-zilliqa-linux.zip
cd /root/kyve && ./kyve-zilliqa-linux --version
chmod +x kyve-zilliqa-linux
```

## Service Ayarlamak

```
sudo tee /etc/systemd/system/kyved.service > /dev/null <<EOF
[Unit]
Description=Kyve Node
After=network-online.target
[Service]
User=root
WorkingDirectory=/root/kyve/
ExecStart=/root/kyve/kyve-zilliqa-linux -m "mnemonic" -k /root/kyve/arweave.json -p 5 -v -s 300
Restart=on-failure
RestartSec=3
LimitNOFILE=65535
[Install]
WantedBy=multi-user.target
EOF
```
## Node Başlatma Kodları

```
sudo systemctl daemon-reload
sudo systemctl enable kyved
sudo systemctl start kyved
```
## Logları Görüntüleme
```
journalctl -f -u kyved
```

