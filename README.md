# linux_instructions



## От **Digitalize**

h5 Настройка LAMP для php на Debian
https://github.com/alexey-goloburdin/debian-set-up-for-php

h5 NGINX сервер для Django
https://github.com/alexey-goloburdin/debian-set-up-for-django

h5 Чистый шаблон Django проекта
https://github.com/alexey-goloburdin/django-clean-template

# SSH 
sudo apt install openssh-server
sudo systemctl enable sshd

sudo vim /etc/ssh/sshd_config
PermitRootLogin no
PubkeyAuthentication yes

sudo systemctl restart ssh

Генерируем ключи
ssh-keygen

Загружаем ключ на сервер
ssh-copy-id username@remote_host

Если после этого не дает зайти по ключу
cat ~/.ssh/id_rsa.pub | ssh username@remote_host "mkdir -p ~/.ssh && cat >> ~/.ssh/authorized_keys"

Подключение по SSH
ssh username@remote_host

Если имя пользователя совпадает можно просто 
ssh remote_host
---------------------------------------------------------------
