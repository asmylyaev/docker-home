## Установка и запуск Gitlab и Gitlab-runner в docker на Ubunty 20.04 (home-lab)

#### Установка Docker и Docker Compose
```
sudo apt update
sudo apt install docker.io containerd docker-compose -y
```
#### Добавление в автозагрузку и проверка статуса работы
```
sudo systemctl start docker
sudo systemctl enable docker
sudo systemctl status docker
```

#### Настройка рабочих каталогов
``` 
sudo mkdir -p /data/docker/gitlab/{data,config/ssl,logs}
sudo mkdir -p /data/docker/gitlab-runner/config

cd /data/docker
sudo nano .env
GITLAB_HOME=/data/docker/gitlab
```

##### Добавляем данные из docker-compose.yml на сервер/vm 
sudo nano docker-compose.yml

#####  Запускаем контейнеры и проверяем статус 
``` 
sudo docker-compose up -d
sudo docker compose ps
```

#### Gitlab - посмотреть текущий пароль root
``` 
sudo docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```
#### Регистрация runner в Gitlab
``` 
cd /data/docker
sudo docker compose exec gitlab-runner gitlab-runner register
```
``` 
GitLab instance URL - fqdn адрес gitlab
Registration token - Gitlab->Settings->CI/CD->Runners
tags for the runner - home
executor - docker
default Docker image - python 3.11-slim
```