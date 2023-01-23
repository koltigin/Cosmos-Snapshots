# Anlık Görüntülerle Kendi Yedekleme Sunucunuzu Çalıştırın

## Sistemi Güncelleme ve Docker Kurulumu
```bash
sudo apt update && \
sudo apt install curl git docker.io -y
```

## Repoyu Kolnlama
```
git clone https://github.com/koltigin/Cosmos-Snapshots.git && cd Cosmos-Snapshots
```

## snapshots Dosyası Oluşturma 
```
mkdir $HOME/snapshots/
```

## Docker ile Nginx'i Başlatma
```bash
cd $HOME; \
docker run --name snapshots \
--restart always \
-v $(pwd)/default.conf:/etc/nginx/conf.d/default.conf \
-v $(pwd)/snapshots/:/root/ \
-p 80:80 \
-d nginx
```

## `example_snapshot.sh` Dosyasında Değişkenleri Ayarlama
```
CHAIN_ID="okp4-nemeton-1"
SNAP_PATH="$HOME/snapshots/okp4"
LOG_PATH="$HOME/snapshots/okp4/okp4_log.txt"
DATA_PATH="$HOME/.okp4d/data/"
SERVICE_NAME="okp4d.service"
```

Değişkenleri dğzenlediğimiz `example_snapshot.sh` dosyasını `okp4_snapshot.sh` şeklinde değiştiriyoruz.

## Yeni Snapshot Oluşturma
`./Cosmos-Snapshots/scripts/okp4_snapshot.sh`  

## Snapshotu Kontrol Etme  
```bash
MY_IP=$(curl -s 2ip.ru); \
curl -s http://${MY_IP}
```

## Snapshot Alınmasını Otomatikleştirme  
Anlık görüntü alınma zamanını aşağıdaki kodla düzenleyebilirsiniz. 
```cron
# her gun saat 00:00'da baslat
0 0 * * * /bin/bash -c '/root/okp4_snapshot.sh'
```
