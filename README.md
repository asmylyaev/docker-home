#### Установите Docker и Docker Compose
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

#### Настройка каталога GitLab
``` 
sudo mkdir -p /data/docker/gitlab/{data,config/ssl,logs}
sudo mkdir -p /data/docker/gitlab-runner/config

cd /data/docker
sudo nano .env
GITLAB_HOME=/data/docker/gitlab
```

#### Подготовка и запуск контейнеров
##### Добавляем данные в репозитории из docker-compose.yml на сервер 
sudo nano docker-compose.yml

#####  Запускаем и проверяем статус 
``` 
sudo docker-compose up -d
sudo docker ps
```

#### Gitlab посмотреть текущий пароль root
``` 
sudo docker exec -it gitlab grep 'Password:' /etc/gitlab/initial_root_password
```
#### Регистрация runner
``` 
cd /data/docker
docker compose exec gitlab-runner gitlab-runner register
```