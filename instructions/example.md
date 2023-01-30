# Son Anlık Görüntüyü İndirme
Bu örnek dosyada değişmesi gereken yerler;
`cosmosd` burası node sistem dosyası adıyla değiştirilecek.

## Node Servisini Durdurma
```
sudo systemctl stop cosmosd.service`  
```

## `~/.cosmosd/data` Dizininde Bulunan Eski Verileri Silme
```
rm -rf ~/.cosmosd/data; \
mkdir -p ~/.cosmosd/data; \
cd ~/.cosmosd/data
```

## Anlık görüntüyü İndirme  
```bash
SNAP_NAME=$(curl -s https://adres.com/snapshots/testnet/cosmos/ | egrep -o ">cosmos-3.*tar" | tr -d ">"); \
wget -O - https://adres.com/snapshots/testnet/cosmos/${SNAP_NAME} | tar xf -
```

## Servisi Başlatma ve Logları Kontrol Etme
```
sudo systemctl start agoricd.service; \
sudo journalctl -u agoricd.service -f --no-hostname
```
