<p align="center">
  <img height="100" height="auto" src="https://github.com/freshe4qa/elixir/assets/85982863/8e8e8d61-ccac-44b9-832b-2c9c0c200988">
</p>

# Elixir - Testnet v2

Official documentation:
>- [Guide](https://docs.elixir.finance)

Explorer:
>- [Explorer](https://dashboard.elixir.finance)

### Minimum Hardware Requirements
 - 2x CPUs; the faster clock speed the better
 - 4GB RAM
 - 40GB of storage (SSD or NVME)

```
sudo apt update && sudo apt upgrade -y
```

```
apt install curl iptables build-essential git wget jq make gcc nano tmux htop nvme-cli pkg-config libssl-dev libleveldb-dev tar clang bsdmainutils ncdu unzip libleveldb-dev -y
```
```
sudo apt install apt-transport-https ca-certificates curl software-properties-common -y
```
```
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
```
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"
```
```
sudo apt install docker-ce docker-ce-cli containerd.io docker-compose-plugin -y
```

Для запуска валидатора Elixir рекомендуется использовать новый кошелек Metamask.
Создав новый кошелек, сохраняем адрес и закрытый ключ.

```
wget https://files.elixir.finance/Dockerfile
```

Введите в файл адрес кошелька и закрытый ключ. Дайте своему валидатору имя.

```
nano Dockerfile
```

Сохраняем CTRL + O, CTRL + X

```
docker build . -f Dockerfile -t elixir-validator
```
```
docker run -d --restart unless-stopped --name ev elixir-validator
```

Переходим на сайт(https://dashboard.elixir.finance/) и подключаем кошелек, который используем для вадидатора. Клеймим токены. Нажимаем stake и стейкаем токены, минимально 100 токенов. Далее нажимаем enroll и регистрируем валидатора.

Полезные команды:

Рестарт контейнеров:
```
docker restart $(docker ps -a -q)
```
Посмотреть логи:
```
docker logs --follow  container_id
```
Удалить ноду:
```
docker stop $(docker ps -a -q)
docker rm $(docker ps -a -q)
```

Обновить ноду:
```
docker kill ev
docker rm ev
docker pull elixirprotocol/validator:testnet-2
docker build . -f Dockerfile -t elixir-validator
```

```
docker run -d --restart unless-stopped --name ev elixir-validator
```
