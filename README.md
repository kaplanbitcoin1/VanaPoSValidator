


# Sistem Gereksinimleri
| Bileşenler | Minimum Gereksinimler | 
| ------------ | ------------ |
| CPU | 4 Core |
| RAM | 8 GB RAM |
| Storage | 100 GB Nvme Disk |





# Sunucuyu Güncelleyelim

```
sudo apt update && sudo apt upgrade -y
sudo apt install jq -y
```


# Docker Kuralım
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt-get update
sudo apt-get install docker-ce docker-ce-cli containerd.io
docker version
```


# Docker Compose 

```
VER=$(curl -s https://api.github.com/repos/docker/compose/releases/latest | grep tag_name | cut -d '"' -f 4)
curl -L "https://github.com/docker/compose/releases/download/"$VER"/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

chmod +x /usr/local/bin/docker-compose
docker-compose --version
```

# OpenSSL Yükleyelim
```
sudo apt-get install openssl
```


# Git ile repoyu sunucumuza çekelim
```
git clone https://github.com/vana-com/vana.git
cd vana
```

# Yapılandırma Dosyasını Hazırlayalım

```
cp .env.example .env
```


# Şimdi .env dosyasını düzenlememiz gerekiyor

```
nano .env
```

* `WITHDRAWAL_ADDRESS` Evm Cüzdan Adresiniz
* `DEPOSIT_PRIVATE_KEY` Evm Cüzdan Private Key
* `USE_VALIDATOR` True Olacak
* `EXTERNAL_IP` Sunucu IP Adresiniz. CommandX/CommandY=Enter


<img width="1057" alt="Ekran Resmi 2024-09-24 20 39 51" src="https://github.com/user-attachments/assets/cd959970-063b-432d-a161-04e034dc8211">


# Her şey tamamsa şimdi validator keyimizi oluşturacağız. Bunun için:



```
docker compose --profile init --profile manual run --rm validator-keygen
```
