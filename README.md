[![Build Status](https://travis-ci.org/Alex-kku/Lab05.svg?branch=master)](https://travis-ci.org/Alex-kku/Lab05)

## Laboratory work IV

<a href="https://yandex.ru/efir/?stream_id=vCgeA9EiySzw"><img src="https://raw.githubusercontent.com/tp-labs/lab05/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**

```sh
$ open https://travis-ci.org
```

## Tasks

- [x] 1. Авторизоваться на сервисе **Travis CI** с использованием **GitHub** аккаунта
- [x] 2. Создать публичный репозиторий с названием **lab05** на сервисе **GitHub**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Включить интеграцию сервиса **Travis CI** с созданным репозиторием
- [x] 5. Получить токен для **Travis CLI** с правами **repo** и **user**
- [x] 6. Получить фрагмент вставки значка сервиса **Travis CI** в формате **Markdown**
- [x] 7. Выполнить инструкцию учебного материала
- [x] 8. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=Alex-kku
$ export GITHUB_TOKEN=*************************
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/Alex-kku/workspace ~/Alex-kku/workspace
$ source scripts/activate
```

```sh
$ \curl -sSL https://get.rvm.io | bash -s -- --ignore-dotfiles
Turning on ignore dotfiles mode.
Downloading https://github.com/rvm/rvm/archive/master.tar.gz
Installing RVM to /home/baha/.rvm/
Installation of RVM in /home/baha/.rvm/ is almost complete:

  * To start using RVM you need to run `source /home/baha/.rvm/scripts/rvm`
    in all your open shell windows, in rare cases you need to reopen all shell windows.
Thanks for installing RVM 🙏
Please consider donating to our open collective to help us maintain RVM.
$ echo "source $HOME/.rvm/scripts/rvm" >> scripts/activate
$ . scripts/activate
$ rvm autolibs disable
$ rvm install ruby-2.4.2
Searching for binary rubies, this might take some time.
Found remote file https://rvm_io.global.ssl.fastly.net/binaries/ubuntu/18.04/x86_64/ruby-2.4.2.tar.bz2
ruby-2.4.2 - #configure
ruby-2.4.2 - #download
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
100 17.5M  100 17.5M    0     0   449k      0  0:00:39  0:00:39 --:--:-- 1116k
ruby-2.4.2 - #validate archive
ruby-2.4.2 - #extract
ruby-2.4.2 - #validate binary
ruby-2.4.2 - #setup
ruby-2.4.2 - #gemset created /home/baha/.rvm/gems/ruby-2.4.2@global
ruby-2.4.2 - #importing gemset /home/baha/.rvm/gemsets/global.gems..................................
ruby-2.4.2 - #generating global wrappers.......
ruby-2.4.2 - #gemset created /home/baha/.rvm/gems/ruby-2.4.2
ruby-2.4.2 - #importing gemsetfile /home/baha/.rvm/gemsets/default.gems evaluated to empty gem list
ruby-2.4.2 - #generating default wrappers.......
$ rvm use 2.4.2 --default
Using /home/baha/.rvm/gems/ruby-2.4.2
$ gem install travis
Building native extensions. This could take a while...
Successfully installed ffi-1.13.0
Successfully installed ethon-0.12.0
Successfully installed typhoeus-0.8.0
Building native extensions. This could take a while...
Successfully installed json-2.3.0
Successfully installed websocket-1.2.8
Successfully installed pusher-client-0.6.2
Successfully installed travis-1.9.1
Parsing documentation for ffi-1.13.0
Installing ri documentation for ffi-1.13.0
Parsing documentation for ethon-0.12.0
Installing ri documentation for ethon-0.12.0
Parsing documentation for typhoeus-0.8.0
Installing ri documentation for typhoeus-0.8.0
Parsing documentation for json-2.3.0
Installing ri documentation for json-2.3.0
Parsing documentation for websocket-1.2.8
Installing ri documentation for websocket-1.2.8
Parsing documentation for pusher-client-0.6.2
Installing ri documentation for pusher-client-0.6.2
Parsing documentation for travis-1.9.1
Installing ri documentation for travis-1.9.1
Done installing documentation for ffi, ethon, typhoeus, json, websocket, pusher-client, travis after 14 seconds
7 gems installed
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/Lab03 projects/Lab04
Клонирование в «projects/Lab04»…
remote: Enumerating objects: 151, done.
remote: Counting objects: 100% (151/151), done.
remote: Compressing objects: 100% (99/99), done.
remote: Total 151 (delta 59), reused 132 (delta 48), pack-reused 0
Получение объектов: 100% (151/151), 1.30 MiB | 959.00 KiB/s, готово.
Определение изменений: 100% (59/59), готово.
$ cd projects/Lab04
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab04
```

```sh
$ cat > .travis.yml <<EOF
language: cpp
EOF
```

```sh
$ cat >> .travis.yml <<EOF

script:
- cmake -H. -B_build -DCMAKE_INSTALL_PREFIX=_install
- cmake --build _build
- cmake --build _build --target install
EOF
```

```sh
$ cat >> .travis.yml <<EOF

addons:
  apt:
    sources:
      - george-edison55-precise-backports
    packages:
      - cmake
      - cmake-data
EOF
```

```sh
$ travis login --github-token ${GITHUB_TOKEN}
Shell completion not installed. Would you like to install it now? |y| y
Successfully logged in as Alex-kku!
```

```sh
$ travis lint
Hooray, .travis.yml looks valid :)
```

```sh
$ ex -sc '1i|[![Build Status](https://travis-ci.com/Alex-kku/Lab04.svg?branch=master)](https://travis-ci.com/Alex-kku/Lab04)' -cx README.md
```

```sh
$ git add .travis.yml
$ git add README.md
$ git commit -m"Lab04 done"
[master 0585a51] Lab04 done
 2 files changed, 15 insertions(+)
 create mode 100644 .travis.yml
$ git push origin master
Username for 'https://github.com': Alex-kku
Password for 'https://Alex-kku@github.com':*************
Подсчет объектов: 155, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (92/92), готово.
Запись объектов: 100% (155/155), 1.30 MiB | 261.00 KiB/s, готово.
Total 155 (delta 61), reused 150 (delta 59)
remote: Resolving deltas: 100% (61/61), done.
To https://github.com/Alex-kku/Lab04
 * [new branch]      master -> master
```

```sh
$ travis lint
Hooray, .travis.yml looks valid :)
$ travis accounts
Alex-kku (Alex-kku): subscribed, 7 repositories
bmstu-iu8-11-cpp-2018 (Bmstu-iu8-11-cpp-2018): subscribed, 1 repository
$ travis sync
synchronizing: ... done
$ travis repos
Alex-kku/Homework02 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

Alex-kku/Homework03 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

Alex-kku/Lab01 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

Alex-kku/Lab02 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

Alex-kku/Lab03 (active: no, admin: yes, push: yes, pull: yes)
Description: ???

Alex-kku/Lab04 (active: yes, admin: yes, push: yes, pull: yes)
Description: ???

Alex-kku/hello-world (active: no, admin: yes, push: yes, pull: yes)
Description: ???

bmstu-iu8-11-cpp-2018/lab-00-Alex-kku (active: no, admin: no, push: yes, pull: yes)
Description: lab-00-Alex-kku created by GitHub Classroom
$ travis enable
Detected repository as Alex-kku/Lab04, is this correct? |yes| y
Alex-kku/Lab04: enabled :)
$ travis whatsup
Alex-kku/Lab04 passed: #1
$ travis branches
master:  #1    passed     Lab04 done
$ travis history
#1 passed:       master Lab04 done
$ travis show
Job #1.1:  Lab04 done
State:         passed
Type:          push
Branch:        master
Commit:        0585a51
Compare URL:   https://github.com/Alex-kku/Lab04/compare/550513f0218a^...0585a518cb8f
Duration:      45 sec
Started:       2020-06-04 12:26:06
Finished:      2020-06-04 12:26:51
Allow Failure: false
Config:        os: linux
```

## Report

```sh
$ popd
$ export LAB_NUMBER=04
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

Вы продолжаете проходить стажировку в "Formatter Inc." (см [подробности](https://github.com/tp-labs/lab03#Homework)).

В прошлый раз ваше задание заключалось в настройке автоматизированной системы **CMake**.

Сейчас вам требуется настроить систему непрерывной интеграции для библиотек и приложений, с которыми вы работали в [прошлый раз](https://github.com/tp-labs/lab03#Homework). Настройте сборочные процедуры на различных платформах:
* используйте [TravisCI](https://travis-ci.com/) для сборки на операционной системе **Linux** с использованием компиляторов **gcc** и **clang**;
* используйте [AppVeyor](https://www.appveyor.com/) для сборки на операционной системе **Windows**.

## Links

- [Travis Client](https://github.com/travis-ci/travis.rb)
- [AppVeyour](https://www.appveyor.com/)
- [GitLab CI](https://about.gitlab.com/gitlab-ci/)

```
Copyright (c) 2015-2020 The ISC Authors
```
