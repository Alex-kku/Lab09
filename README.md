[![Build Status](https://travis-ci.org/Alex-kku/Lab08.svg?branch=master)](https://travis-ci.org/Alex-kku/Lab08)
## Laboratory work VIII

<a href="https://yandex.ru/efir/?stream_id=v0mnBi_R2Ldw"><img src="https://raw.githubusercontent.com/tp-labs/lab08/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению систем автоматизации развёртывания и управления приложениями на примере **Docker**

```sh
$ open https://docs.docker.com/get-started/
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab08** на сервисе **GitHub**
- [x] 2. Ознакомиться со ссылками учебного материала
- [x] 3. Выполнить инструкцию учебного материала
- [x] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=Alex-kku
```

```
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/Alex-kku/workspace ~/Alex-kku/workspace
$ source scripts/activate
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/Lab07 projects/Lab08
Клонирование в «projects/Lab08»…
remote: Enumerating objects: 226, done.
remote: Counting objects: 100% (226/226), done.
remote: Compressing objects: 100% (126/126), done.
remote: Total 226 (delta 90), reused 219 (delta 87), pack-reused 0
Получение объектов: 100% (226/226), 1.76 MiB | 952.00 KiB/s, готово.
Определение изменений: 100% (90/90), готово.
$ cd projects/Lab08
$ git submodule update --init
Подмодуль «tools/polly» (https://github.com/ruslo/polly) зарегистрирован по пути «tools/polly»
Клонирование в «/home/baha/Alex-kku/workspace/projects/Lab08/tools/polly»…
Подмодуль по пути «tools/polly»: забрано состояние «0b3806e193b668fbb9b70c9aa70735b29396323d»
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab08
```

```sh
$ sudo groupadd docker
$ sudo usermod -aG docker $USER
$ newgrp docker
```

```sh
$ cat > Dockerfile <<EOF
> FROM ubuntu:18.04
> EOF
```

```sh
$ cat >> Dockerfile <<EOF
> 
> RUN apt update
> RUN apt install -yy gcc g++ cmake
> EOF
```

```sh
$ cat >> Dockerfile <<EOF
> 
> COPY . print/
> WORKDIR print
> EOF
```

```sh
$ cat >> Dockerfile <<EOF
> 
> RUN cmake -H. -B_build -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=_install
> RUN cmake --build _build
> RUN cmake --build _build --target install
> EOF
```

```sh
$ cat >> Dockerfile <<EOF
> 
> ENV LOG_PATH /home/logs/log.txt
> EOF
```

```sh
$ cat >> Dockerfile <<EOF
> 
> VOLUME /home/logs
> EOF
```

```sh
$ cat >> Dockerfile <<EOF
> 
> WORKDIR _install/bin
> EOF
```

```sh
$ cat >> Dockerfile <<EOF

ENTRYPOINT ./demo
EOF
```

```sh
$ docker build -t logger .
Sending build context to Docker daemon  7.585MB
Step 1/12 : FROM ubuntu:18.04
18.04: Pulling from library/ubuntu
23884877105a: Pull complete 
bc38caa0f5b9: Pull complete 
2910811b6c42: Pull complete 
36505266dcc6: Pull complete 
Digest: sha256:3235326357dfb65f1781dbc4df3b834546d8bf914e82cce58e6e6b676e23ce8f
Status: Downloaded newer image for ubuntu:18.04
 ---> c3c304cb4f22
Step 2/12 : RUN apt update
 ---> Running in d7450c8bcfd0
....................................
Step 11/12 : WORKDIR _install/bin
 ---> Running in 2c7ecddf5f8e
Removing intermediate container 2c7ecddf5f8e
 ---> 1073d2c17646
Step 12/12 : ENTRYPOINT ./demo
 ---> Running in d601c08c8c54
Removing intermediate container d601c08c8c54
 ---> 3ae9bae78996
Successfully built 3ae9bae78996
Successfully tagged logger:latest
```

```sh
$ docker images
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
logger              latest              3ae9bae78996        22 seconds ago      346MB
ubuntu              18.04               c3c304cb4f22        6 weeks ago         64.2MB
```

```sh
$ mkdir logs
$ docker run -it -v "$(pwd)/logs/:/home/logs/" logger /bin/bash
text1
text2
text3
```

```sh
$ docker inspect logger
[
    {
        "Id": "sha256:3ae9bae789963b0e93b4219117d257c8b538dd8502cdeecb97ba58398b9ed3c2",
        "RepoTags": [
            "logger:latest"
        ],
        "RepoDigests": [],
        "Parent": "sha256:1073d2c17646101ffdf8b21b54b1a1128e1e92f48f5d0f7c0ce9f7a6ee64c8d0",
        "Comment": "",
        "Created": "2020-06-05T14:23:08.89214958Z",
        "Container": "d601c08c8c54f6cbd881081748245e13629141e0b1095bf4385516b46dedec69",
        "ContainerConfig": {
            "Hostname": "d601c08c8c54",
.......................................
                "sha256:40f670a076424cdb3f73df3e441f4fb314fd5a65996f8d7e868fb3ed6e41c699",
                "sha256:da432ea8782f95d90d959b9abdd9cc0b8a1ac3ca9ab5e44db0d32ddaab9f1622"
            ]
        },
        "Metadata": {
            "LastTagTime": "2020-06-05T17:23:08.938017142+03:00"
        }
    }
]
```

```sh
$ cat logs/log.txt
text1
text2
text3
```

```sh
$ sed -i 's/Lab07/Lab08/g' README.md
```

```sh
$ vim .travis.yml
/lang<CR>o
services:
- docker<ESC>
jVGdo
script:
- docker build -t logger .<ESC>
:wq
```

```sh
$ git add Dockerfile
$ git add .travis.yml
$ git add README.md
$ git commit -m"adding Dockerfile"
$ git push origin master
[master fcc1048] adding Dockerfile
 3 files changed, 45 insertions(+), 36 deletions(-)
 create mode 100644 Dockerfile
$ git push origin master
Username for 'https://github.com': Alex-kku
Password for 'https://Alex-kku@github.com':*************
Подсчет объектов: 231, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (128/128), готово.
Запись объектов: 100% (231/231), 1.76 MiB | 1.67 MiB/s, готово.
Total 231 (delta 92), reused 225 (delta 90)
remote: Resolving deltas: 100% (92/92), done.
To https://github.com/Alex-kku/Lab08
 * [new branch]      master -> master
```

```sh
$ travis login --auto
Successfully logged in as Alex-kku!
$ travis enable
Detected repository as Alex-kku/Lab08, is this correct? |yes| y
Alex-kku/Lab08: enabled :)
```

## Report

```sh
$ popd
$ export LAB_NUMBER=08
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links

- [Book](https://www.dockerbook.com)
- [Instructions](https://docs.docker.com/engine/reference/builder/)

```
Copyright (c) 2015-2019 The ISC Authors
```
