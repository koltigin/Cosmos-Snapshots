# Son Anlık Görüntüyü İndirme

## Node Servisini Durdurma
```
sudo systemctl stop okp4d.service`  
```

## `~/.cosmosd/data` Dizininde Bulunan Eski Verileri Silme
```
rm -rf ~/.okp4d/data; \
mkdir -p ~/.okp4d/data; \
cd ~/.okp4d/data
```

## Anlık görüntüyü İndirme  
```bash
SNAP_NAME=$(curl -s https://adres.com/snapshots/testnet/okp4/ | egrep -o ">okp4-nemeton-1.*tar" | tr -d ">"); \
wget -O - https://adres.com/snapshots/testnet/okp4/${SNAP_NAME} | tar xf -
```

## Servisi Başlatma ve Logları Kontrol Etme
```
sudo systemctl start okp4d.service; \
sudo journalctl -u okp4d -f -o cat
```
