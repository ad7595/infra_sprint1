# Проекты 14 спринта Taski и Kittygram

- **Kittygram** - https://aadgnv.hopto.org/
- **Task** - https://ad7595.hopto.org/

## Установка проекта:

Клонируйте репрозторий и перейдите в него в командной строке:

`git clone git@github.com:ad7595/infra_sprint1.git

`cd infra_sprint1`


Создайте и активируйте вируальное окружение:

`cd backend`

`python3 -m venv env`

`source venv/bin/activate`


Установите зависимости из файла requirements.txt:

`python3 -m pip install --upgrade pip`

`pip install -r requirements.txt`


Выполните миграции:

`python3 manage.py migrate`

Создаём суперпользователя:

`python3 manage.py createsuperuser`

Измените свои данные для Gunicorn:

1. В параметре WorkingDirectory:

`sudo nano /etc/systemd/system/gunicorn.service`

> Путь к директории проекта:
> 
> /home/<имя-пользователя-в-системе>/
> 
> <директория-с-проектом>/<директория-с-файлом-manage.py>/
> 
> Например:

`WorkingDirectory=/home/yc-user/taski/backend/`

2. В параметре ExecStart:

> Команду, которую вы запускали руками, теперь будет запускать systemd:
>
> /home/<имя-пользователя-в-системе>/
> 
> <директория-с-проектом>/<путь-до-gunicorn-в-виртуальном-окружении> --bind 0.0.0.0:8000 backend.wsgi

`ExecStart=/home/yc-user/taski/backend/venv/bin/gunicorn --bind 0.0.0.0:8000 backend.wsgi`

Запустите Gunicorn:

`sudo systemctl start gunicorn`


Запустите Nginx:

`sudo systemctl start nginx`

##Запуск проекта:

Запустите backend проекта в первом терминале:

`cd infra_sprint1/backend`

`python manage.py runserver`


Запустите frontend проекта во втором терминале:

`cd infra_sprint1/frontend`

```
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
sudo apt-get install -y nodejs
```

`npm i`

`npm run start`
