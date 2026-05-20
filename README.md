# Домашнее задание к занятию "`Оркестрация группой Docker контейнеров на примере Docker Compose`" - `Манукян Степан`


### Инструкция по выполнению домашнего задания

   1. Сделайте `fork` данного репозитория к себе в Github и переименуйте его по названию или номеру занятия, например, https://github.com/имя-вашего-репозитория/git-hw или  https://github.com/имя-вашего-репозитория/7-1-ansible-hw).
   2. Выполните клонирование данного репозитория к себе на ПК с помощью команды `git clone`.
   3. Выполните домашнее задание и заполните у себя локально этот файл README.md:
      - впишите вверху название занятия и вашу фамилию и имя
      - в каждом задании добавьте решение в требуемом виде (текст/код/скриншоты/ссылка)
      - для корректного добавления скриншотов воспользуйтесь [инструкцией "Как вставить скриншот в шаблон с решением](https://github.com/netology-code/sys-pattern-homework/blob/main/screen-instruction.md)
      - при оформлении используйте возможности языка разметки md (коротко об этом можно посмотреть в [инструкции  по MarkDown](https://github.com/netology-code/sys-pattern-homework/blob/main/md-instruction.md))
   4. После завершения работы над домашним заданием сделайте коммит (`git commit -m "comment"`) и отправьте его на Github (`git push origin`);
   5. Для проверки домашнего задания преподавателем в личном кабинете прикрепите и отправьте ссылку на решение в виде md-файла в вашем Github.
   6. Любые вопросы по выполнению заданий спрашивайте в чате учебной группы и/или в разделе “Вопросы по заданию” в личном кабинете.
   
Желаем успехов в выполнении домашнего задания!
   
### Дополнительные материалы, которые могут быть полезны для выполнения задания

1. [Руководство по оформлению Markdown файлов](https://gist.github.com/Jekins/2bf2d0638163f1294637#Code)

---

### Задание 1

`Сценарий выполнения задачи:
Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: {"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}
Зарегистрируйтесь и создайте публичный репозиторий с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
скачайте образ nginx:1.29.0;
Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:`
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
```
`Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП).
Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general`


### Ответ
1: `[https://hub.docker.com//thebad1996/custom-nginx/general](https://hub.docker.com/r/thebad1996/custom-nginx)`

2: `docker pull thebad1996/custom-nginx:1.0.0`

---

### Задание 2 
Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
имя контейнера "ФИО-custom-nginx-t2"
контейнер работает в фоне
контейнер опубликован на порту хост системы 127.0.0.1:8080
Не удаляя, переименуйте контейнер в "custom-nginx-t2"
Выполните команду date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

### Ответ

Пополнение баланса телефона - со стороны оператора связи

```
root@cicd:~/custom-nginx# docker pull thebad1996/custom-nginx:1.0.0
1.0.0: Pulling from thebad1996/custom-nginx
Digest: sha256:406067213d0284470de7e21da7a060a5d55748f642abf0dd57a4034d9ce259ba
Status: Image is up to date for thebad1996/custom-nginx:1.0.0
docker.io/thebad1996/custom-nginx:1.0.0
root@cicd:~/custom-nginx# docker run -d --name "stepan-manukyan-custom-nginx-t2" -p 127.0.0.1:8080:80 thebad1996/custom-nginx:1.0.0
5aea386cef88f34575029ca516bb798835f5c1060235d536ef91b6379a7a492b
root@cicd:~/custom-nginx# docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED          STATUS         PORTS                    NAMES
5aea386cef88   thebad1996/custom-nginx:1.0.0   "/docker-entrypoint.…"   11 seconds ago   Up 9 seconds   127.0.0.1:8080->80/tcp   stepan-manukyan-custom-nginx-t2
root@cicd:~/custom-nginx# docker rename stepan-manukyan-custom-nginx-t2 custom-nginx-t2
root@cicd:~/custom-nginx# docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED          STATUS          PORTS                    NAMES
5aea386cef88   thebad1996/custom-nginx:1.0.0   "/docker-entrypoint.…"   40 seconds ago   Up 39 seconds   127.0.0.1:8080->80/tcp   custom-nginx-t2
root@cicd:~/custom-nginx# date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html
20-05-2026 17:39:16.389467411 MSK
CONTAINER ID   IMAGE                           COMMAND                  CREATED              STATUS              PORTS                    NAMES
5aea386cef88   thebad1996/custom-nginx:1.0.0   "/docker-entrypoint.…"   About a minute ago   Up About a minute   127.0.0.1:8080->80/tcp   custom-nginx-t2
LISTEN 0      4096       127.0.0.1:8080       0.0.0.0:*    users:(("docker-proxy",pid=1632,fd=4))
2026/05/20 14:37:47 [notice] 1#1: start worker process 28
PGh0bWw+CjxoZWFkPgpIZXksIE5ldG9sb2d5CjwvaGVhZD4KPGJvZHk+CjxoMT5JIHdpbGwgYmUg
RGV2T3BzIEVuZ2luZWVyITwvaDE+CjwvYm9keT4KPC9odG1sPgo=
root@cicd:~/custom-nginx# curl http://127.0.0.1:8080
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
```
![TASK2](/img/Screenshot_1.png)

---

### Задание 3 

`Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
Выполните docker ps -a и объясните своими словами почему контейнер остановился.
Перезапустите контейнер
Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
Запомните(!) и выполните команду nginx -s reload, а затем внутри контейнера curl http://127.0.0.1:80 ; curl http://127.0.0.1:81.
Выйдите из контейнера, набрав в консоли exit или Ctrl-D.
Проверьте вывод команд: ss -tlpn | grep 127.0.0.1:8080 , docker port custom-nginx-t2, curl http://127.0.0.1:8080. Кратко объясните суть возникшей проблемы.
Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. пример источника
Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.`


### Ответ
```
root@cicd:~/custom-nginx# docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS         PORTS                    NAMES
5aea386cef88   thebad1996/custom-nginx:1.0.0   "/docker-entrypoint.…"   6 minutes ago   Up 6 minutes   127.0.0.1:8080->80/tcp   custom-nginx-t2
root@cicd:~/custom-nginx# docker attach custom-nginx-t2
^C2026/05/20 14:44:49 [notice] 1#1: signal 2 (SIGINT) received, exiting
2026/05/20 14:44:49 [notice] 28#28: exiting
2026/05/20 14:44:49 [notice] 28#28: exit
2026/05/20 14:44:49 [notice] 1#1: signal 17 (SIGCHLD) received from 28
2026/05/20 14:44:49 [notice] 1#1: worker process 28 exited with code 0
2026/05/20 14:44:49 [notice] 1#1: exit
root@cicd:~/custom-nginx# docker ps -a
CONTAINER ID   IMAGE                           COMMAND                  CREATED         STATUS                        PORTS                                                  NAMES
5aea386cef88   thebad1996/custom-nginx:1.0.0   "/docker-entrypoint.…"   7 minutes ago   Exited (0) 7 seconds ago                                                             custom-nginx-t2
e242cb41efc1   mysql:8.0                       "docker-entrypoint.s…"   8 days ago      Exited (255) 30 minutes ago   33060/tcp, 0.0.0.0:3307->3306/tcp, :::3307->3306/tcp   mysql-slave
8861083086a7   mysql:8.0                       "docker-entrypoint.s…"   8 days ago      Exited (255) 30 minutes ago   0.0.0.0:3306->3306/tcp, :::3306->3306/tcp, 33060/tcp   mysql-master
root@cicd:~/custom-nginx# docker ps
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
root@cicd:~/custom-nginx# docker start custom-nginx-t2
custom-nginx-t2
root@cicd:~/custom-nginx# docker exec -it custom-nginx-t2 bash
root@5aea386cef88:/# apt-get install -y nano
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
Package nano is not available, but is referred to by another package.
This may mean that the package is missing, has been obsoleted, or
is only available from another source

E: Package 'nano' has no installation candidate
root@5aea386cef88:/# apt-get update
Get:1 http://deb.debian.org/debian bookworm InRelease [151 kB]
Get:2 http://deb.debian.org/debian bookworm-updates InRelease [55.4 kB]
Get:3 http://deb.debian.org/debian-security bookworm-security InRelease [48.0 kB]
Get:4 http://deb.debian.org/debian bookworm/main amd64 Packages [8790 kB]
Get:5 http://deb.debian.org/debian bookworm-updates/main amd64 Packages [6924 B]
Get:6 http://deb.debian.org/debian-security bookworm-security/main amd64 Packages [306 kB]
Fetched 9357 kB in 2s (5339 kB/s)
Reading package lists... Done
root@5aea386cef88:/# apt install nano
Reading package lists... Done
Building dependency tree... Done
Reading state information... Done
The following additional packages will be installed:
  libgpm2 libncursesw6
Suggested packages:
  gpm hunspell
The following NEW packages will be installed:
  libgpm2 libncursesw6 nano
0 upgraded, 3 newly installed, 0 to remove and 40 not upgraded.
Need to get 838 kB of archives.
After this operation, 3339 kB of additional disk space will be used.
Do you want to continue? [Y/n] y
Get:1 http://deb.debian.org/debian bookworm/main amd64 libncursesw6 amd64 6.4-4 [134 kB]
Get:2 http://deb.debian.org/debian bookworm/main amd64 nano amd64 7.2-1+deb12u1 [690 kB]
Get:3 http://deb.debian.org/debian bookworm/main amd64 libgpm2 amd64 1.20.7-10+b1 [14.2 kB]
Fetched 838 kB in 0s (1934 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libncursesw6:amd64.
(Reading database ... 7582 files and directories currently installed.)
Preparing to unpack .../libncursesw6_6.4-4_amd64.deb ...
Unpacking libncursesw6:amd64 (6.4-4) ...
Selecting previously unselected package nano.
Preparing to unpack .../nano_7.2-1+deb12u1_amd64.deb ...
Unpacking nano (7.2-1+deb12u1) ...
Selecting previously unselected package libgpm2:amd64.
Preparing to unpack .../libgpm2_1.20.7-10+b1_amd64.deb ...
Unpacking libgpm2:amd64 (1.20.7-10+b1) ...
Setting up libgpm2:amd64 (1.20.7-10+b1) ...
Setting up libncursesw6:amd64 (6.4-4) ...
Setting up nano (7.2-1+deb12u1) ...
update-alternatives: using /bin/nano to provide /usr/bin/editor (editor) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/editor.1.gz because associated file /usr/share/man/man1/nano.1.gz (of link group editor) doesn't exist
update-alternatives: using /bin/nano to provide /usr/bin/pico (pico) in auto mode
update-alternatives: warning: skip creation of /usr/share/man/man1/pico.1.gz because associated file /usr/share/man/man1/nano.1.gz (of link group pico) doesn't exist
Processing triggers for libc-bin (2.36-9+deb12u10) ...
root@5aea386cef88:/# nano /etc/nginx/conf.d/default.conf
root@5aea386cef88:/# nginx -s reload
2026/05/20 14:47:26 [notice] 177#177: signal process started
root@5aea386cef88:/# curl http://127.0.0.1:80 ; curl http://127.0.0.1:81
curl: (7) Failed to connect to 127.0.0.1 port 80 after 0 ms: Couldn't connect to server
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
root@5aea386cef88:/#
root@5aea386cef88:/# exit
exit
root@cicd:~/custom-nginx# ss -tlpn | grep 127.0.0.1:8080
LISTEN 0      4096       127.0.0.1:8080       0.0.0.0:*    users:(("docker-proxy",pid=1912,fd=4))
root@cicd:~/custom-nginx# docker port custom-nginx-t2
80/tcp -> 127.0.0.1:8080
root@cicd:~/custom-nginx# curl http://127.0.0.1:8080
curl: (52) Empty reply from server
root@cicd:~/custom-nginx# docker rm -f custom-nginx-t2
custom-nginx-t2
root@cicd:~/custom-nginx#
```
3. `Контейнер остановился, потому что при нажатии Ctrl-C был завершён основной процесс контейнера (nginx), который и поддерживал работу контейнера. В Docker контейнер прекращает свою работу, когда завершается его основной процесс.`
10. `Проблема возникает потому, что мы изменили порт внутри контейнера, но не изменили маппинг портов на хосте. Теперь nginx слушает на порту 81 внутри контейнера, но хост всё ещё пытается направлять трафик на порт 80 контейнера.`

![TASK3](/img/Screenshot_2.png)

---
### Задание 4

`Задача 4
Запустите первый контейнер из образа centos c любым тегом в фоновом режиме, подключив папку текущий рабочий каталог $(pwd) на хостовой машине в /data контейнера, используя ключ -v.
Запустите второй контейнер из образа debian в фоновом режиме, подключив текущий рабочий каталог $(pwd) в /data контейнера.
Подключитесь к первому контейнеру с помощью docker exec и создайте текстовый файл любого содержания в /data.
Добавьте ещё один файл в текущий каталог $(pwd) на хостовой машине.
Подключитесь во второй контейнер и отобразите листинг и содержание файлов в /data контейнера.
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.`

### Ответ
```
root@cicd:~/custom-nginx# pwd
/root/custom-nginx
root@cicd:~/custom-nginx# ls
Dockerfile  index.html
root@cicd:~/custom-nginx# docker run -d --name centos-container -v $(pwd):/data centos:7 tail -f /dev/null
89ee88d9cbd0937c290d84c3456614e46187e4e88618874fb61642c57319b026
root@cicd:~/custom-nginx# docker run -d --name debian-container -v $(pwd):/data debian:latest tail -f /dev/null
0fa77facd891975303b2c8f30894255840543fa8d5dc3d63768906e3f0e16a69
root@cicd:~/custom-nginx# docker ps
CONTAINER ID   IMAGE           COMMAND               CREATED         STATUS         PORTS     NAMES
0fa77facd891   debian:latest   "tail -f /dev/null"   3 seconds ago   Up 2 seconds             debian-container
89ee88d9cbd0   centos:7        "tail -f /dev/null"   6 seconds ago   Up 5 seconds             centos-container
root@cicd:~/custom-nginx# docker exec -it centos-container bash
[root@89ee88d9cbd0 /]# echo "Hello" > /data/from-centos.txt
[root@89ee88d9cbd0 /]# cat /data/from-centos.txt
Hello
[root@89ee88d9cbd0 /]# exit
exit
root@cicd:~/custom-nginx# echo "Hello HOST" > from-host.txt
root@cicd:~/custom-nginx# ls -la
итого 24
drwxr-xr-x  2 root root 4096 мая 20 18:06 .
drwx------ 11 root root 4096 мая 20 17:26 ..
-rw-r--r--  1 root root   67 мая 20 17:21 Dockerfile
-rw-r--r--  1 root root    6 мая 20 18:06 from-centos.txt
-rw-r--r--  1 root root   11 мая 20 18:06 from-host.txt
-rw-r--r--  1 root root   95 мая 20 17:20 index.html
root@cicd:~/custom-nginx# docker exec -it debian-container bash
root@0fa77facd891:/# ls -la /data/
total 24
drwxr-xr-x 2 root root 4096 May 20 15:06 .
drwxr-xr-x 1 root root 4096 May 20 15:05 ..
-rw-r--r-- 1 root root   67 May 20 14:21 Dockerfile
-rw-r--r-- 1 root root    6 May 20 15:06 from-centos.txt
-rw-r--r-- 1 root root   11 May 20 15:06 from-host.txt
-rw-r--r-- 1 root root   95 May 20 14:20 index.html
root@0fa77facd891:/# cat /data/from-centos.txt
Hello
root@0fa77facd891:/# cat /data/from-host.txt
Hello HOST
root@0fa77facd891:/#
```
![TASK4](/img/Screenshot_3.png)

---

### Задание 5
`Задача 5
Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него. "compose.yaml" с содержимым:
version: "3"
services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
"docker-compose.yaml" с содержимым:
version: "3"
services:
  registry:
    image: registry:2
    ports:
    - "5000:5000"
И выполните команду "docker compose up -d". Какой из файлов был запущен и почему? (подсказка: https://docs.docker.com/compose/compose-application-model/#the-compose-file )
Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)
Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/
Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.(логин и пароль адмнистратора)
Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз:
version: '3'
services:
  nginx:
    image: 127.0.0.1:5000/custom-nginx
    ports:
      - "9090:80"
Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".
Удалите любой из манифестов компоуза(например compose.yaml). Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.
В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод, файл compose.yaml , скриншот portainer c задеплоенным компоузом.`

### Ответ
```
root@cicd:/tmp/netology/docker/task5# pwd
/tmp/netology/docker/task5
root@cicd:/tmp/netology/docker/task5# touch compose.yaml
root@cicd:/tmp/netology/docker/task5# touch docker-compose.yaml
root@cicd:/tmp/netology/docker/task5# nano compose.yaml
root@cicd:/tmp/netology/docker/task5# nano docker-compose.yaml
root@cicd:/tmp/netology/docker/task5# docker compose up -d
WARN[0000] Found multiple config files with supported names: /tmp/netology/docker/task5/compose.yaml, /tmp/netology/docke                                                                                                    r/task5/docker-compose.yaml
WARN[0000] Using /tmp/netology/docker/task5/compose.yaml
WARN[0000] /tmp/netology/docker/task5/compose.yaml: the attribute `version` is obsolete, it will be ignored, please remov                                                                                                    e it to avoid potential confusion
[+] up 10/10
 ✔ Image portainer/portainer-ce:latest Pulled                                                                        6.2s
 ✔ Container task5-portainer-1         Started                                                                       2.9s
root@cicd:/tmp/netology/docker/task5# docker ps
CONTAINER ID   IMAGE                           COMMAND        CREATED          STATUS         PORTS     NAMES
07e4631d5aca   portainer/portainer-ce:latest   "/portainer"   11 seconds ago   Up 7 seconds             task5-portainer-1
root@cicd:/tmp/netology/docker/task5# nano compose.yaml
root@cicd:/tmp/netology/docker/task5# docker compose up -d
WARN[0000] Found multiple config files with supported names: /tmp/netology/docker/task5/compose.yaml, /tmp/netology/docke                                                                                                    r/task5/docker-compose.yaml
WARN[0000] Using /tmp/netology/docker/task5/compose.yaml
WARN[0000] /tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, pleas                                                                                                    e remove it to avoid potential confusion
WARN[0000] /tmp/netology/docker/task5/compose.yaml: the attribute `version` is obsolete, it will be ignored, please remov                                                                                                    e it to avoid potential confusion
[+] up 3/3
 ✔ Network task5_default       Created                                                                               0.1s
 ✔ Container task5-registry-1  Started                                                                               0.6s
 ✔ Container task5-portainer-1 Running                                                                               0.0s
root@cicd:/tmp/netology/docker/task5# docker ps
CONTAINER ID   IMAGE                           COMMAND                  CREATED          STATUS          PORTS                                                                                                                                             NAMES
bba7391995e4   registry:2                      "/entrypoint.sh /etc…"   6 seconds ago    Up 5 seconds    0.0.0.0:5000->50                                                                                                    00/tcp, [::]:5000->5000/tcp   task5-registry-1
07e4631d5aca   portainer/portainer-ce:latest   "/portainer"             44 seconds ago   Up 41 seconds                                                                                                                                                     task5-portainer-1
root@cicd:/tmp/netology/docker/task5# cat compose.yaml
version: "3"
include:
  - docker-compose.yaml
services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
root@cicd:/tmp/netology/docker/task5# docker pull thebad1996/custom-nginx:1.0.0`
> ^C
root@cicd:/tmp/netology/docker/task5# docker pull thebad1996/custom-nginx:1.0.0
1.0.0: Pulling from thebad1996/custom-nginx
Digest: sha256:406067213d0284470de7e21da7a060a5d55748f642abf0dd57a4034d9ce259ba
Status: Image is up to date for thebad1996/custom-nginx:1.0.0
docker.io/thebad1996/custom-nginx:1.0.0
root@cicd:/tmp/netology/docker/task5# docker tag thebad1996/custom-nginx:1.0.0 localhost:5000/custom-nginx:latest
root@cicd:/tmp/netology/docker/task5# docker push 127.0.0.1:5000/custom-nginx:latest
The push refers to repository [127.0.0.1:5000/custom-nginx]
An image does not exist locally with the tag: 127.0.0.1:5000/custom-nginx
root@cicd:/tmp/netology/docker/task5# docker push localhost:5000/custom-nginx:latest
The push refers to repository [localhost:5000/custom-nginx]
1e7a1a8f509a: Pushed
2e174fd56089: Pushed
727839498dfa: Pushed
508937af8963: Pushed
e9b5d470f331: Pushed
5e1b8f458cec: Pushed
d89e58119fc7: Pushed
eb5f13bce993: Pushed
latest: digest: sha256:6d62a03063c1f57eac4b19faa4155698d723ee6447e0dce85af16130f5812eae size: 1985
root@cicd:/tmp/netology/docker/task5# rm compose.yaml
root@cicd:/tmp/netology/docker/task5# docker compose up -d
WARN[0000] /tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
WARN[0000] Found orphan containers ([task5-portainer-1]) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.
[+] up 1/1
 ✔ Container task5-registry-1 Running                                                                                                                                                                                    0.0s
root@cicd:/tmp/netology/docker/task5# docker compose down -v
WARN[0000] /tmp/netology/docker/task5/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion
[+] down 2/2
 ✔ Container task5-registry-1 Removed                                                                                                                                                                                    0.4s
 ✔ Network task5_default      Removed                                                                                                                                                                                    0.2s
root@cicd:/tmp/netology/docker/task5#
```

1. `Был запущен файл compose.yaml, так как Docker по умолчанию ищет файл с именем docker-compose.yaml и compose.yaml, но compose.yaml имеет приоритет.`
7. `Получаем предупреждение, о том что были обнаружены осиротевшие контейнеры (orphan containers), которые относятся к проекту, но не указаны в текущем Compose-файле. И предлагается выполнить очистку выполнив команду: --remove-orphans`

compose.yaml
```
root@cicd:/tmp/netology/docker/task5# cat compose.yaml
version: "3"
include:
  - docker-compose.yaml
services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```
![TASK5](/img/Screenshot_6.png)
![TASK5](/img/Screenshot_4.png)
![TASK5](/img/Screenshot_5.png)
