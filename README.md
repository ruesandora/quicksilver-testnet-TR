<h1 align="center">Quicksilver, killerqueen-1 testnet rehberi</h1>

# QuickSilver Türkiye Telegram Grubu: [Buradan katılabilirsiniz](https://t.me/QuicksilverTurkish)

![image](https://user-images.githubusercontent.com/101149671/175765082-1a35b43c-0cd4-4863-b103-00e9749641a1.png)


Sistem Gereksinimleri : 

|    Bellek   |       Cpu      |      Disk      |
|-------------|----------------|----------------|
|     8GB     |    4x CPUs     |     200GB      |


[Burada](https://is.gd/CONTABO) ki örnek VPS yeterli, isteyen diski 400 yapabilir.

# root kullanıcı oluyoruz:
```
sudo su
```

# root dizini altına gidiyoruz
```
cd /root
```

# Scriptimizi çalıştırıp kuruyoruz:
```
wget -q -O quicksilver.sh https://api.rues.info/quicksilver.sh && chmod +x quicksilver.sh && sudo /bin/bash quicksilver.sh
```

# Peer ekliyoruz:
```
PEERS="b281289df37c5180f9ff278be5e29964afa0c229@185.56.139.84:26656,4f35ab6008fc46cc50b103a337ec2266400eca2e@148.251.50.79:26656,90f4459126152d21983f42c8e86bc899cd618af6@116.202.15.183:11656,6ac91620bc5338e6f679835cc604769a213d362f@139.59.56.24:36366,f9d2dbf6c80f08d12d1bc8d07ffd3bafa4965160@95.214.55.43:26651,abe7397ff92a4ca61033ceac127b5fc3a9a4217f@65.108.98.218:25095,07bb0fd7af9dc819bb5bb850ea5d870281c3adfa@167.235.74.230:26656"
SEEDS="dd3460ec11f78b4a7c4336f22a356fe00805ab64@seed.killerqueen-1.quicksilver.zone:26656,8603d0778bfe0a8d2f8eaa860dcdc5eb85b55982@seed02.killerqueen-1.quicksilver.zone:27676"
sed -i -e "s/^seeds *=.*/seeds = \"$SEEDS\"/; s/^persistent_peers *=.*/persistent_peers = \"$PEERS\"/" $HOME/.quicksilverd/config/config.toml
systemctl restart quicksilverd
```

# Explorerdaki güncel blok sayısını yakalamaya çalışıyoruz:

[Buradan katılabilirsiniz](https://quicksilver.explorers.guru/) 

# Bu komut ile false çıktısı almanız gerekiyor: (True yazarsa eşleşmesini bekleyin)
```
quicksilverd status 2>&1 | jq .SyncInfo
```

# Cüzdan oluşturuyoruz. Çıkan kurtarma ifadelerini kaydetmeyi unutmayın: (Wallet kısmını siz düzeleyin) 
```
quicksilverd keys add WALLET
```

# Ardından discord kanalına giderek #qck-tap kanalında token istiyoruz:

Discord kanalları: [kanal linki](https://discord.gg/fWCGsb7sE7) 

Discorddan talep komutu: $request + cüzdan adresi ve sonuna killerqueen şeklinde. 1 kez alabiliyorsunuz 5 token veriliyor.

![image](https://user-images.githubusercontent.com/101149671/175772344-69161a63-1d58-473e-a97d-443878716ec0.png)


# Şimdi gelelim, Validator oluşturmaya: (wallet ve node isminiz değişecek)
```
quicksilverd tx staking create-validator \
  --amount 10000000uqck \
  --from wallet \
  --commission-max-change-rate "0.01" \
  --commission-max-rate "0.2" \
  --commission-rate "0.07" \
  --min-self-delegation "1" \
  --pubkey  $(quicksilverd tendermint show-validator) \
  --moniker node \
  --chain-id killerqueen-1
```

# quicksilver güncellemesi:

güncelleme geldi arkadaşlar 98 bininci bloğa ulaşanlar için (98 bine ulaşamadan güncelleme yapmayın!!!!!)

```
1- sudo su
2- cd
3- rm -rf quicksilver 
4- git clone https://github.com/ingenuity-build/quicksilver.git
5- cd quicksilver
6- git checkout v0.4.1
6- make build
7- sudo chmod +x ./build/quicksilverd && sudo mv ./build/quicksilverd /usr/local/bin/quicksilverd
8 -sudo systemctl restart quicksilverd
```

2. yöntem
```
cd
cd quicksilver
git pull
git checkout v0.4.1
make install 
sudo chmod +x ./build/quicksilverd && sudo mv ./build/quicksilverd /usr/local/bin/quicksilverd
sudo systemctl restart quicksilverd
```

# Quicksilver ödüllü Testnet görevleri: (oluşturduktan 24 saat sonra görevleri yapalım)

1-Tüm testnet boyunca jailed olmayın : 250 puan
2-Tüm testnet boyunca en az blok kaçırma rekoru kırın : 200 puan
3-Komisyon oranınızı %5.9 olarak ayarlayın : 25 puan

```
quicksilverd tx staking edit-validator --chain-id=killerqueen-1 --moniker=NodeName --commission-rate="0.059"  --from=walletName
```

4-Ödülleri kendimize çekin : 25 puan

```
quicksilverd tx distribution withdraw-all-rewards --from Cüzdanismi --chain-id killerqueen-1
```

5-Tokenleri Redelegate ediyoruz 25 puan:
```
quicksilverd tx staking redelegate KendiValoperAdresimiz quickvaloper1xzsg7sgws73nvjdd7ga0mw9vek0v7zg6f7xdej miktar000000uqck --chain-id killerqueen-1 --from cüzdanAdı --gas=auto -y
```

# QuickSilver Türkiye Telegram Grubu: [Buradan katılabilirsiniz](https://t.me/QuicksilverTurkish)

# Hesaplar:

[<img src="https://cdn-icons-png.flaticon.com/512/733/733579.png" width="16px"> Twitter   ](https://twitter.com/Ruesandora0) 

[<img src="https://cdn-icons-png.flaticon.com/512/1336/1336494.png" width="16px"> Forum   ](https://forum.rues.info/index.php)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Announcement   ](https://t.me/RuesAnnouncement)

[<img src="https://cdn-icons-png.flaticon.com/512/2111/2111646.png" width="16px"> Telegram Chat   ](https://t.me/RuesChat)

[Discord](https://discord.gg/ruescommunity)
