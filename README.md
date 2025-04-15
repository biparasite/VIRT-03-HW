# Домашнее задание к занятию " `Оркестрация группой Docker контейнеров на примере Docker Compose` " - `Сулименков Алексей`

---

## Задача 1

Сценарий выполнения задачи:

Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: {"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}
Зарегистрируйтесь и создайте публичный репозиторий с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
скачайте образ nginx:1.21.1;
Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:

```html
<html>
  <head>
    Hey, Netology
  </head>
  <body>
    <h1>I will be DevOps Engineer!</h1>
  </body>
</html>
```

Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).
Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .

### Ответ

https://hub.docker.com/r/biparasite/nginx-my/tags

<details> <summary>docker_repo</summary>

![task1](https://github.com/biparasite/VIRT-03-HW/blob/main/task_1.png "task1")

</details>

---

## Задача 2

1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
   имя контейнера "ФИО-custom-nginx-t2"
   контейнер работает в фоне
   контейнер опубликован на порту хост системы 127.0.0.1:8080
2. Не удаляя, переименуйте контейнер в "custom-nginx-t2"
3. Выполните команду date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080 ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
   Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.
4. В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

### Ответ

1.

```bash
docker run -d -p 8080:80  --name SAV-custom-nginx-t2 biparasite/nginx-my:latest
```

<details> <summary>docker_run</summary>

![task2](https://github.com/biparasite/VIRT-03-HW/blob/main/task_2.png "task2")

</details>

2.

```bash
docker rename SAV-custom-nginx-t2 custom-nginx-t2
```

<details> <summary>docker_rename</summary>

![task2](https://github.com/biparasite/VIRT-03-HW/blob/main/task_2.1.png "task2")

</details>

3.

```bash
date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; lsof -i -n  -Tfqs | grep 127.0.0.1:8080 ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
```

<details> <summary>commad</summary>

![task2](https://github.com/biparasite/VIRT-03-HW/blob/main/task_2.2.png "task2")

</details>

4.

```bash
curl http://127.0.0.1:8080
```

<details> <summary>curl</summary>

![task2](https://github.com/biparasite/VIRT-03-HW/blob/main/task_2.3.png "task2")

</details>

---

## Задача 3

1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
2. Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
3. Выполните docker ps -a и объясните своими словами почему контейнер остановился.
4. Перезапустите контейнер
5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
7. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
8. Запомните(!) и выполните команду nginx -s reload, а затем внутри контейнера curl http://127.0.0.1:80 ; curl http://127.0.0.1:81.
9. Выйдите из контейнера, набрав в консоли exit или Ctrl-D.
10. Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. пример источника
11. Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

### Ответ

1.

```bash
docker exec -it custom-nginx-t2 sh
```

2. Не остановился :-)

<details> <summary>Ctrl-C</summary>

![task3](https://github.com/biparasite/VIRT-03-HW/blob/main/task_3.png "task3")

</details>

3. apt update && apt install mc

<details> <summary>apt install</summary>

![task3](https://github.com/biparasite/VIRT-03-HW/blob/main/task_3.1.png "task3")

</details>

4-8. Смена порта, релофд nginx, curl

<details> <summary>apt install</summary>

![task3](https://github.com/biparasite/VIRT-03-HW/blob/main/task_3.2.png "task3")

</details>
