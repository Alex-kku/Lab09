[![Build Status](https://travis-ci.org/Alex-kku/Lab09.svg?branch=master)](https://travis-ci.org/Alex-kku/Lab09)
## Laboratory work IX

<a href="https://yandex.ru/efir/?stream_id=vYrKRcFKi46o"><img src="https://raw.githubusercontent.com/tp-labs/lab09/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению процесса создания артефактов на примере **Github Release**

```sh
$ open https://help.github.com/articles/creating-releases/
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab09** на сервисе **GitHub**
- [x] 2. Ознакомиться со ссылками учебного материала
- [x] 3. Получить токен для доступа к репозиториям сервиса **GitHub**
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_TOKEN=****************************************
$ export GITHUB_USERNAME=Alex-kku
$ export PACKAGE_MANAGER=apt
$ export GPG_PACKAGE_NAME=gpg
```

```sh
# for *-nix system
$ sudo ${PACKAGE_MANAGER} install xclip
$ alias gsed=sed
$ alias pbcopy='xclip -selection clipboard'
$ alias pbpaste='xclip -selection clipboard -o'
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/Alex-kku/workspace ~/Alex-kku/workspace
$ source scripts/activate
$ go get github.com/aktau/github-release
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/Lab08 projects/Lab09
Клонирование в «projects/Lab09»…
remote: Enumerating objects: 234, done.
remote: Counting objects: 100% (234/234), done.
remote: Compressing objects: 100% (129/129), done.
remote: Total 234 (delta 93), reused 230 (delta 92), pack-reused 0
Получение объектов: 100% (234/234), 1.76 MiB | 517.00 KiB/s, готово.
Определение изменений: 100% (93/93), готово.
$ cd projects/lab09
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab09
```

```sh
$ gsed -i 's/Lab08/Lab09/g' README.md
```

```sh
$ sudo ${PACKAGE_MANAGER} install ${GPG_PACKAGE_NAME} 
Чтение списков пакетов… Готово
Построение дерева зависимостей
Чтение информации о состоянии… Готово
Уже установлен пакет gpg самой новой версии (2.2.4-1ubuntu1.2).
gpg помечен как установленный вручную.
Обновлено 0 пакетов, установлено 0 новых пакетов, для удаления отмечено 0 пакетов, и 25 пакетов не обновлено.
$ gpg --list-secret-keys --keyid-format LONG
$ gpg --full-generate-key
gpg (GnuPG) 2.2.4; Copyright (C) 2017 Free Software Foundation, Inc.
This is free software: you are free to change and redistribute it.
There is NO WARRANTY, to the extent permitted by law.

Выберите тип ключа:
   (1) RSA и RSA (по умолчанию)
   (2) DSA и Elgamal
   (3) DSA (только для подписи)
   (4) RSA (только для подписи)
Ваш выбор? 1
длина ключей RSA может быть от 1024 до 4096.
Какой размер ключа Вам необходим? (3072) 1024
Запрошенный размер ключа - 1024 бит
Выберите срок действия ключа.
         0 = не ограничен
      <n>  = срок действия ключа - n дней
      <n>w = срок действия ключа - n недель
      <n>m = срок действия ключа - n месяцев
      <n>y = срок действия ключа - n лет
Срок действия ключа? (0) 
Срок действия ключа не ограничен
Все верно? (y/N) y

GnuPG должен составить идентификатор пользователя для идентификации ключа.

Ваше полное имя: Alexei Kushpelev
Адрес электронной почты: leha.kushpelev@mail.ru
Примечание: Add new key
Вы выбрали следующий идентификатор пользователя:
    "Alexei Kushpelev (Add new key) <leha.kushpelev@mail.ru>"

Сменить (N)Имя, (C)Примечание, (E)Адрес; (O)Принять/(Q)Выход? o
Необходимо получить много случайных чисел. Желательно, чтобы Вы
в процессе генерации выполняли какие-то другие действия (печать
на клавиатуре, движения мыши, обращения к дискам); это даст генератору
случайных чисел больше возможностей получить достаточное количество энтропии.
Необходимо получить много случайных чисел. Желательно, чтобы Вы
в процессе генерации выполняли какие-то другие действия (печать
на клавиатуре, движения мыши, обращения к дискам); это даст генератору
случайных чисел больше возможностей получить достаточное количество энтропии.
gpg: ключ 2F76B2C0E13B0789 помечен как абсолютно доверенный
gpg: сертификат отзыва записан в '/home/baha/.gnupg/openpgp-revocs.d/5974EAF607E593F5C5FD63D82F76B2C0E13B0789.rev'.
открытый и секретный ключи созданы и подписаны.

pub   rsa1024 2020-06-05 [SC]
      5974EAF607E593F5C5FD63D82F76B2C0E13B0789
uid                      Alexei Kushpelev (Add new key) <leha.kushpelev@mail.ru>
sub   rsa1024 2020-06-05 [E]

$ gpg --list-secret-keys --keyid-format LONG
/home/baha/.gnupg/pubring.kbx
-----------------------------
sec   rsa3072/F97B9C021AC3C0B8 2020-06-05 [SC]
      C3FBAE185B92861FFF1544B2F97B9C021AC3C0B8
uid               [  абсолютно ] Kushpelev Alexei (Lab09) <leha.kushpelev@mail.ru>
ssb   rsa3072/5ABDEB8F08DDD342 2020-06-05 [E]

$ gpg -K ${GITHUB_USERNAME}
$ GPG_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep ssb | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')
$ GPG_SEC_KEY_ID=$(gpg --list-secret-keys --keyid-format LONG | grep sec | tail -1 | awk '{print $2}' | awk -F'/' '{print $2}')
$ gpg --armor --export ${GPG_KEY_ID} | pbcopy
$ pbpaste
-----BEGIN PGP PUBLIC KEY BLOCK-----
.
.
.
-----END PGP PUBLIC KEY BLOCK-----
$ open https://github.com/settings/keys
$ git config user.signingkey ${GPG_SEC_KEY_ID}
$ git config gpg.program gpg
```

```sh
$ test -r ~/.bash_profile && echo 'export GPG_TTY=$(tty)' >> ~/.bash_profile
$ echo 'export GPG_TTY=$(tty)' >> ~/.profile
```

```sh
$ cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
 cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
-- The C compiler identification is GNU 7.5.0
-- The CXX compiler identification is GNU 7.5.0
-- Check for working C compiler: /usr/bin/cc
-- Check for working C compiler: /usr/bin/cc -- works
-- Detecting C compiler ABI info
-- Detecting C compiler ABI info - done
-- Detecting C compile features
-- Detecting C compile features - done
-- Check for working CXX compiler: /usr/bin/c++
-- Check for working CXX compiler: /usr/bin/c++ -- works
-- Detecting CXX compiler ABI info
-- Detecting CXX compiler ABI info - done
-- Detecting CXX compile features
-- Detecting CXX compile features - done
-- [hunter] Calculating Toolchain-SHA1
-- [hunter] Calculating Config-SHA1
-- [hunter] HUNTER_ROOT: /home/levon/.hunter
-- [hunter] [ Hunter-ID: 5659b15 | Toolchain-ID: 9b2c9d4 | Config-ID: 8a1641b ]
-- [hunter] GTEST_ROOT: /home/levon/.hunter/_Base/5659b15/9b2c9d4/8a1641b/Install (ver.: 1.10.0)
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Looking for pthread_create
-- Looking for pthread_create - not found
-- Looking for pthread_create in pthreads
-- Looking for pthread_create in pthreads - not found
-- Looking for pthread_create in pthread
-- Looking for pthread_create in pthread - found
-- Found Threads: TRUE 
-- Configuring done
-- Generating done
-- Build files have been written to: /home/baha/Alex-kku/workspace/projects/Lab09/_build
$ cmake --build _build --target package
Scanning dependencies of target print
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
Scanning dependencies of target demo
[ 75%] Building CXX object CMakeFiles/demo.dir/demo/main.cpp.o
[100%] Linking CXX executable demo
[100%] Built target demo
Run CPack packaging tool...
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print
CPack: Create package
CPack: - package: /home/baha/Alex-kku/workspace/projects/Lab09/_build/print-0.1.0.0-Linux.tar.gz generated.
```

```sh
$ travis login --auto
Successfully logged in as Alex-kku!
$ travis enable
Detected repository as Alex-kku/Lab08, is this correct? |yes| y
Alex-kku/Lab08: enabled :)
```

```sh
$ git tag -s v0.1.0.0
$ git tag -v v0.1.0.0
object ed5b66t5c6b0td7bc1b41b4169340h06e06ebabc56
type commit
тег v0.1.0.0
tagger Alexei Kushpelev < leha.kushpelev@mail.ru > 1594345369 +0300

Add new key
gpg: Подпись сделана Пт 05 июн 2020 19:10:24 мск
gpg: ключом RSA с идентификатором 5974EAF607E593F5C5FD63D82F76B2C0E13B0789
gpg: Действительная подпись пользователя " Alexei Kushpelev (.) <leha.kushpelev@mail.ru> " [абсолютное]
$ git show v0.1.0.0
$ git push origin master --tags
Username for 'https://github.com': Alex-kku
Password for 'https://levon-avackimyanc@github.com': *************
Подсчет объектов: 228, готово.
Delta compression using up to 4 threads.
Сжатие объектов: 100% (129/129), готово.
Запись объектов: 100% (228/228), 1.84 MiB | 2.46 MiB/s, готово.
Total 228 (delta 86), reused 226 (delta 86)
remote: Resolving deltas: 100% (86/86), done.
To https://github.com/levon-avackimyanc/Lab-09
 * [new branch]      master -> master
 * [new tag]         v0.1.0.0 -> v0.1.0.0
```

```sh
$ github-release --version
github-release v0.8.1
$ github-release info -u ${GITHUB_USERNAME} -r Lab09
tags:
- v0.1.0.0 (commit: https://api.github.com/repos/Alex-kku/Lab-09/commits/ed5b66t5c6b0td7bc1b41b4169340h06e06ebabc56)
releases:
$ github-release release \
    --user ${GITHUB_USERNAME} \
    --repo lab09 \
    --tag v0.1.0.0 \
    --name "libprint" \
    --description "my first release"
```

```sh
$ export PACKAGE_OS=`uname -s` PACKAGE_ARCH=`uname -m` 
$ export PACKAGE_FILENAME=print-${PACKAGE_OS}-${PACKAGE_ARCH}.tar.gz
$ github-release upload \
    --user ${GITHUB_USERNAME} \
    --repo lab09 \
    --tag v0.1.0.0 \
    --name "${PACKAGE_FILENAME}" \
    --file _build/*.tar.gz
```

```sh
$ github-release info -u ${GITHUB_USERNAME} -r Lab09
- v0.1.0.0 (commit: https://api.github.com/repos/levon-avackimyanc/Lab-09/commits/ed5b66t5c6b0td7bc1b41b4169340h06e06ebabc56))
releases:
- v0.1.0.0, name: 'libprint', description: 'my first release', id: 26329050, tagged: 05/06/2020 at 19:35, published: 05/06/2020 at 19:45, draft: ✗, prerelease: ✗
  - artifact: print-Darwin-x86_64.tar.gz, downloads: 0, state: uploaded, type: application/octet-stream, size: 20 kB, id: 20559779
$ wget https://github.com/${GITHUB_USERNAME}/Lab-09/releases/download/v0.1.0.0/${PACKAGE_FILENAME}
--2020-06-05 19:51:56--  https://github.com/levon-avackimyanc/Lab-09/releases/download/v0.1.0.0/print-Darwin-x86_64.tar.gz
...
Сохранение в: «print-Darwin-x86_64.tar.gz»
print-Darwin-x86_64 100%[===================>]  19,44K   178KB/s    за 0,2s 
2020-06-05 19:59:22 (178 KB/s) - «print-Darwin-x86_64.tar.gz» сохранён [19909/19909]
$ tar -ztf ${PACKAGE_FILENAME}
print-0.1.0.0-Darwin/cmake/
print-0.1.0.0-Darwin/cmake/print-config-noconfig.cmake
print-0.1.0.0-Darwin/cmake/print-config.cmake
print-0.1.0.0-Darwin/bin/
print-0.1.0.0-Darwin/bin/demo
print-0.1.0.0-Darwin/include/
print-0.1.0.0-Darwin/include/print.hpp
print-0.1.0.0-Darwin/lib/
print-0.1.0.0-Darwin/lib/libprint.a
$ tar -ztf ${PACKAGE_FILENAME}
```

```sh
$ git add .
$ git commit -m"Lab09 done"
[master 9290024] Lab09 done
 1 file changed, 311 insertions(+), 256 deletions(-)
 rewrite README.md (80%)
$ git push origin master
Username for 'https://github.com': Alex-kku
Password for 'https://Alex-kku@github.com':*************
Подсчет объектов: 237, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (131/131), готово.
Запись объектов: 100% (237/237), 1.76 MiB | 404.00 KiB/s, готово.
Total 237 (delta 94), reused 233 (delta 93)
remote: Resolving deltas: 100% (94/94), done.
To https://github.com/Alex-kku/Lab09
 * [new branch]      master -> master
```

## Report

```sh
$ popd
$ export LAB_NUMBER=09
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gistup -m "lab${LAB_NUMBER}"
```

## Links

- [Create Release](https://help.github.com/articles/creating-releases/)
- [Get GitHub Token](https://help.github.com/articles/creating-a-personal-access-token-for-the-command-line/)
- [Signing Commits](https://help.github.com/articles/signing-commits-with-gpg/)
- [Go Setup](http://www.golangbootcamp.com/book/get_setup)
- [github-release](https://github.com/aktau/github-release)

```
Copyright (c) 2015-2020 The ISC Authors
```

