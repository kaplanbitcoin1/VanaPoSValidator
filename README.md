<img width="1536" alt="Ekran Resmi 2024-09-24 21 46 13" src="https://github.com/user-attachments/assets/07a9235f-768c-4c05-9e8e-afc95dabd354">




[Website](https://www.vana.org/)<br>
[Faucet](https://faucet.vana.org/moksha)<br>
[Discord](https://discord.gg/6d4bf2vG)<br>
[Docs](https://docs.vana.org/vana)<br>




# System Requirements
| Components	 | Minimum Requirements | 
| ------------ | ------------ |
| CPU | 4 Core |
| RAM | 8 GB RAM |
| Storage | 100 GB Nvme |





# Update the Server

```
sudo apt update && sudo apt upgrade -y
sudo apt install jq -y
```


# Install Docker
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

# Install OpenSSL
```
sudo apt-get install openssl
```


# Let's Pull the Repository to Our Server with Git
```
git clone https://github.com/vana-com/vana.git
cd vana
```

# Prepare the Configuration File

```
cp .env.example .env
```


# Now we need to edit the .env file

```
nano .env
```

* `WITHDRAWAL_ADDRESS` Your EVM Wallet Address
* `DEPOSIT_PRIVATE_KEY` EVM Wallet Private Key
* `USE_VALIDATOR` Should be True
* `EXTERNAL_IP` Your Server IP Address. CommandX/CommandY=Enter


<img width="1057" alt="Ekran Resmi 2024-09-24 20 39 51" src="https://github.com/user-attachments/assets/cd959970-063b-432d-a161-04e034dc8211">


* Her şey tamamsa şimdi validator keyimizi oluşturacağız. Bu işlem bir müddet sürebilir



```
docker compose --profile init --profile manual run --rm validator-keygen
```


### İlk kısma görseldeki gibi .env içerisindeki Evm cüzdan adresini yazalım


<img width="876" alt="Ekran Resmi 2024-09-24 20 53 46" src="https://github.com/user-attachments/assets/3ba97a22-cf97-449d-9092-700884c9ee18">


### İkinci kısımda bir parola belirleyelim 😁 (Yazmıyor gibi görünür fakat aslında yazıyordur)
### Parolayı tekrar girmenizi isteyecek
(Parolayı unutmayın ve bir yere kaydedin daha sonra lazım olacak)

<img width="1027" alt="Ekran Resmi 2024-09-24 20 56 58" src="https://github.com/user-attachments/assets/a6bf3c84-0452-4661-84d5-c09ee2a05e21">


### Validator için kelimeleriniz oluştu. Bu kelimeleri bir yere kaydedip Enter tuşuna basın
### Sizden kelimeleri isteyecek, dolduralım

<img width="953" alt="Ekran Resmi 2024-09-24 21 06 11" src="https://github.com/user-attachments/assets/cc34b1ed-2ec2-4608-802f-8ef6e61c022d">


### Tebrikler anahtarımız oluştu. Enter deyip devam edelim

* Şimdi daha önce oluşturduğunuz şifreyi girin
* Sizden cüzdanınızı güvence altına almak için bir şifre belirlemenizi isteyecek. (Ben aynı şifreyi kullandım)

<img width="923" alt="Ekran Resmi 2024-09-24 21 14 22" src="https://github.com/user-attachments/assets/9cf82d77-025b-4275-8779-02a1a6f5d7e8">


### Yaptığımız işlemleri kontrol edelim

```
docker compose logs check-config
```


# Son olarak 3 adet birbiriyle haberleşen yapıyı başlatalım


```
docker compose --profile init --profile validator up -d
```

# Ayrı ayrı log kontrol

```
docker compose --profile=init --profile=node logs -f geth
```

```
docker compose --profile=init --profile=node logs -f beacon
```

```
docker compose --profile=init --profile=node logs -f validator
```

# Beacon bölümünün senkronize olmasını bekleyeceğiz

<img width="1536" alt="Ekran Resmi 2024-09-24 21 22 13" src="https://github.com/user-attachments/assets/52225843-98ff-406d-a2e5-30ef7237c5cd">


### Son olarak doğrulayıcımızın `Moksha` ağına ben de buradayım demesi için `35.000` adet token'a ihtiyacı var.
### Bu miktar muhtemelen birtakım eleme yöntemiyle ya da seçim süreciyle dağıtılacaktır.


# Eğer token bulduysak ben de buradayım demek için 😁


```
docker compose --profile init --profile manual run --rm submit-deposits
```



### Bir hizmete tek tek buna benzer işlemler alabilirsiniz. (Son kısımlarda isimleri değiştirmek yeterli) 
### (validator yerine geth, beacon gibi)


```
docker compose --profile=init --profile=node up -d validator
docker compose --profile=init --profile=node stop validator
docker compose --profile=init --profile=node restart validator
```


# Eski validator anahtarınızı içe aktarmak için

```
docker compose run --rm validator-import
```


### İşlemler tamamdır. Repoya ufak bir yıldız bırakırsanız sevinirim 🐅
