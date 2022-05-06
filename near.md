![Near](https://user-images.githubusercontent.com/73176377/167166280-e730c3c0-5157-4730-beeb-621a6c3e1229.png)


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
cd /root/kyve && wget https://github.com/kyve-org/near/releases/download/v0.0.0/kyve-near-linux.zip && unzip kyve-near-linux.zip
chmod +x kyve-near-linux
cd /root/kyve && ./kyve-near-linux --version
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
ExecStart=/root/kyve/kyve-near-linux -m "mnemonic" -k /root/kyve/arweave.json -p 6 -v -s 320
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

