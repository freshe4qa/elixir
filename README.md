<p align="center">
  <img height="100" height="auto" src="https://github.com/freshe4qa/elixir/assets/85982863/8e8e8d61-ccac-44b9-832b-2c9c0c200988">
</p>

# Elixir - Testnet v3

Official documentation:
>- [Guide](https://docs.elixir.finance)

Explorer:
>- [Explorer](https://dashboard.elixir.finance)

### Minimum Hardware Requirements
 - 2x CPUs; the faster clock speed the better
 - 4GB RAM
 - 40GB of storage (SSD or NVME)
 - Ubuntu 20.04

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
wget https://files.elixir.finance/validator.env
```

Заполняем данные:

STRATEGY_EXECUTOR_DISPLAY_NAME=Придумайте имя валидатору
STRATEGY_EXECUTOR_BENEFICIARY=Адрес кошелька Metamask
SIGNER_PRIVATE_KEY=Приватный ключ от этого кошелька Metamask

```
nano validator.env
```

Сохраняем CTRL + O, CTRL + X

Сеть Testnet v3 работает на токенах MOCK в тестовой сети Ethereum Sepolia. Чтобы получить токены MOCK, вам понадобится небольшое количество Sepolia ETH в любом кошельке. Перейдите на [панель Elixir Network Testnet v3 Dashboard](https://testnet-3.elixir.xyz) и подключите свой кошелек. Убедитесь, что вы подключены к сети Ethereum Sepolia, а затем нажмите кнопку "MINT 1,000 MOCK". Подтвердите транзакцию в своем кошельке. Примечание: Этот кошелек должен отличаться от того, который вы используете для валидатора.

После того как вы получили токены MOCK с приборной панели, вам нужно одобрить их для траты на цепочке, а затем застейкать. В окне Stake MOCK введите сумму токенов MOCK, которую вы хотите поставить на кон. Нажмите "APPROVE MOCK FOR STAKING" и подтвердите транзакцию в своем кошельке. Дождитесь завершения транзакции на цепочке, затем нажмите "STAKE <сумма> MOCK" и подтвердите транзакцию.

Нажмите кнопку "CUSTOM VALIDATOR" над списком активных валидаторов. В появившемся модале "Пользовательский валидатор" введите адрес публичного кошелька вашего валидатора, созданный для валидатора, и нажмите кнопку "DELEGATE". Подтвердите транзакцию и дождитесь ее завершения на цепочке. Теперь вы готовы запустить свой валидатор.

```
docker pull elixirprotocol/validator:v3
```
```
docker run -d \
  --env-file $HOME/validator.env \
  --name elixir \
  --restart unless-stopped \
  elixirprotocol/validator:v3
```

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
docker kill elixir
docker rm elixir
docker pull elixirprotocol/validator:v3
```
