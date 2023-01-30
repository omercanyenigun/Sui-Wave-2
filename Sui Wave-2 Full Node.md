![alt text](https://i.hizliresim.com/48dj5c8.jpg)


**Minimum Gereksinimler**

- **CPU: 10 core**
- **RAM: 32GB**
- **Disk: 1 TB**

```
sudo apt update \
&& apt-get install -y --no-install-recommends \
apt-transport-https \
ca-certificates \
curl \
software-properties-common
```

**Docker Kurulumu**

```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
sudo apt update
sudo apt install docker-ce
```

```
sudo usermod -aG docker ${USER}
```

**Docker Compose Yükleme**

```
sudo curl -L "https://github.com/docker/compose/releases/download/1.28.5/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose
sudo chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

![alt text](https://i.hizliresim.com/7ffpgc8.png)


```
mkdir -p $HOME/sui
cd $HOME/sui
```

**fullnode.yaml**

```
wget -O $HOME/sui/fullnode-template.yaml https://github.com/MystenLabs/sui/raw/main/crates/sui-config/data/fullnode-template.yaml
```

**genesis.blob**

```
wget -O $HOME/sui/genesis.blob  https://github.com/MystenLabs/sui-genesis/raw/main/testnet/genesis.blob
```

**docker-compose indirme ve içindeki Sui Node image güncelleme**

```
IMAGE="mysten/sui-node:02e461008df2cedf1a4f7766a7dd5f216de55148"
wget -O $HOME/sui/docker-compose.yaml https://raw.githubusercontent.com/MystenLabs/sui/main/docker/fullnode/docker-compose.yaml
sed -i.bak "s|image:.*|image: $IMAGE|" $HOME/sui/docker-compose.yaml
```


**Docker container'da Full Node'u başlatma**

```
docker-compose up -d
```

![alt text](https://i.hizliresim.com/bft8lmw.png)

**Container Id ile logsları kontrol etme**

```
docker ps -a
```

![alt text](https://i.hizliresim.com/a0r9hfx.png)


#size container Id'nizi verecek.

```
docker logs -f <container id>
```

![alt text](https://i.hizliresim.com/9t4iyy9.png)


**Node'unuz durumunu - **https://www.scale3labs.com/check/sui** sitesinden kontrol edebilirsiniz.**
**Network yerini Testnet seçmeyi unutmayın.**


![alt text](https://i.hizliresim.com/a952vot.png)


**1.3M blockta ve bazen 3.3M blockta takılma oluyor. Node'unuzun durumunu https://scale3labs.com/check/sui adresinden kontrol edin.
Eğer takılma olursa aşağıdaki kodları girin**


**Container'ı durdurun ve silin**

```
cd $HOME/sui
sudo docker compose down
```

**Docker image'i güncelleyin**

```
IMAGE="mysten/sui-node:2698314d139a3018c2333ddaa670a7cb70beceee"
sed -i.bak "s|image:.*|image: $IMAGE|" $HOME/sui/docker-compose.yaml
```

**Docker container'da Full Node'u başlatma**

```
docker-compose up -d
```


**Container Id ile logsları kontrol etme**

```
docker ps -a
```

#size container Id'nizi verecek.

```
docker logs -f <container id>
```


