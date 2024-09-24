


| Minimum Sistem Gereksinimleri| 
| ------------ | ------------ |
| CPU | 4 Core - 	4 Core - The more cores you have, the better your performance will be |
| RAM | Minimum 4 GB RAM |
| Storage | 50 GB SSD - More space may be needed for future operations |
| GPU | CUDA-enabled GPUs are recommended. CPU mining is available but not valid for all models |





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


