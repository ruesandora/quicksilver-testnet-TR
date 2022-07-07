<h1 align="center">Quicksilver, kqcosmos-1 testnet rehberi</h1>

# QuickSilver Türkiye Telegram Grubu: [Buradan katılabilirsiniz](https://t.me/QuicksilverTurkish)

![image](https://user-images.githubusercontent.com/101149671/175813850-32287cc3-709f-49ed-83de-5976e6666b67.png)

<h1 align="center">Biliyorsunuz bir kaç gün önce killerqueen-1 testine katıldık, şimdi yeni görev olan kqcosmos-1'E katılacağız, aynı sunucuya olmaz, birbirlerinden farklılar, sadece aynı cüzdanları kullanacağız.</h1> 

# Sunucumuzu güncelleyelim:
```
sudo apt update && sudo apt upgrade -y
```

# Gerekli araçları indiriyoruz:
```
sudo apt install curl build-essential git wget jq make gcc tmux -y
```

# Go kurulumu:
```
ver="1.17.5"
cd $HOME
wget "https://golang.org/dl/go$ver.linux-amd64.tar.gz"
sudo rm -rf /usr/local/go
sudo tar -C /usr/local -xzf "go$ver.linux-amd64.tar.gz"
rm "go$ver.linux-amd64.tar.gz"
echo "export PATH=$PATH:/usr/local/go/bin:$HOME/go/bin" >> ~/.bash_profile
source ~/.bash_profile
go version
```

# Binary dosya kurulumu:
```
git clone https://github.com/ingenuity-build/interchain-accounts --branch main
cd interchain-accounts
make install
cp $HOME/go/bin/icad /usr/bin
```

# initialize işlemi: (node ismini girin)
```
icad init NodeName
```

# Genesis dosyaları: 
```
wget -qO $HOME/.ica/config/genesis.json "https://raw.githubusercontent.com/ingenuity-build/testnets/main/killerqueen/kqcosmos-1/genesis.json"
```

# Cüzdan recover ediyoruz. Burası killerqueen-1 testnetinde kullandığımız cüzdan adresini recover ediyoruz: (walletname değişin)
```
icad keys add walletName --recover
```

# Ardından discord kanalında #atom-tap kanalına giriyoruz ve dün ki gibi token talep ediyoruz.
```
$request WalletAdress killerqueen
```

# Seed eklemesi yapalım: 
```
SEEDS="66b0c16486bcc7591f2c3f0e5164d376d06ee0d0@65.108.203.151:26656"
sed -i -e "/seeds =/ s/= .*/= \"$SEEDS\"/"  $HOME/.ica/config/config.toml
```

# Servis dosyası oluşturuyoruz: 
```
sudo tee /etc/systemd/system/icad.service > /dev/null <<EOF
[Unit]
Description=icadQuicksilver
After=network-online.target

[Service]
User=$USER
ExecStart=/usr/bin/icad start
Restart=on-failure
RestartSec=3
LimitNOFILE=65535

[Install]
WantedBy=multi-user.target
EOF
```

# Servisimizi oluşturup başlatıyoruz:
```
sudo systemctl daemon-reload
sudo systemctl enable icad
sudo systemctl restart icad
```

# Node'umuz sync olmasını bekliyoruz
```
icad status 2>&1 | jq .SyncInfo
```

# sync olduktan sonra valdidator kuruyoruz:
```
icad tx staking create-validator \
  --from=WalletName \
  --amount=1000000uatom \
  --moniker=NodeName \
  --chain-id=kqcosmos-1 \
  --commission-rate=0.1 \
  --commission-max-rate=0.5 \
  --commission-max-change-rate=0.1 \
  --min-self-delegation=1 \
  --fees=500uatom \
  --pubkey=$(icad tendermint show-validator) \
  --yes
```

# QuickSilver Türkiye Telegram Grubu: [Buradan katılabilirsiniz](https://t.me/QuicksilverTurkish)

# Hesaplar:

[<img src="https://cdn-icons-png.flaticon.com/512/733/733579.png" width="16px"> Twitter   ](https://twitter.com/Ruesandora0) 

[<img src="https://cdn-icons-png.flaticon.com/512/1336/1336494.png" width="16px"> Forum   ](https://forum.rues.info/index.php)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Announcement   ](https://t.me/RuesAnnouncement)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Chat   ](https://t.me/RuesChat)

[Discord](https://discord.gg/ruescommunity)
