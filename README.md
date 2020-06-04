[![Build Status](https://travis-ci.org/Alex-kku/Lab07.svg?branch=master)](https://travis-ci.org/Alex-kku/Lab07)

<a href="https://yandex.ru/efir/?stream_id=vDHLoKtKoa3o"><img src="https://raw.githubusercontent.com/tp-labs/lab07/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению систем управления пакетами на примере **Hunter**

```sh
$ open https://github.com/ruslo/hunter
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab07** на сервисе **GitHub**
- [x] 2. Выполнить инструкцию учебного материала
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=Alex-kku
$ alias gsed=sed
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/Alex-kku/workspace ~/Alex-kku/workspace
$ source scripts/activate
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/Lab06 projects/Lab07
Клонирование в «projects/Lab07»…
remote: Enumerating objects: 202, done.
remote: Counting objects: 100% (202/202), done.
remote: Compressing objects: 100% (113/113), done.
remote: Total 202 (delta 82), reused 198 (delta 81), pack-reused 0
Получение объектов: 100% (202/202), 1.74 MiB | 880.00 KiB/s, готово.
Определение изменений: 100% (82/82), готово.
$ cd projects/Lab07
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab07
```

```sh
$ mkdir -p cmake
$ wget https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake -O cmake/HunterGate.cmake
--2020-06-05 01:33:07--  https://raw.githubusercontent.com/cpp-pm/gate/master/cmake/HunterGate.cmake
Распознаётся raw.githubusercontent.com (raw.githubusercontent.com)… 151.101.84.133
Подключение к raw.githubusercontent.com (raw.githubusercontent.com)|151.101.84.133|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 17070 (17K) [text/plain]
Сохранение в: «cmake/HunterGate.cmake»

cmake/HunterGate.cm 100%[===================>]  16,67K  --.-KB/s    за 0,05s   

2020-06-05 01:33:09 (307 KB/s) - «cmake/HunterGate.cmake» сохранён [17070/17070]

$ gsed -i '/cmake_minimum_required(VERSION 3.4)/a\
> \
> include("cmake/HunterGate.cmake")\
> HunterGate(\
>     URL "https://github.com/cpp-pm/hunter/archive/v0.23.251.tar.gz"\
>     SHA1 "5659b15dc0884d4b03dbd95710e6a1fa0fc3258d"\
> )\
> ' CMakeLists.txt
```

```sh
$ git rm -rf third-party/gtest
rm 'third-party/gtest'
$ gsed -i '/set(PRINT_VERSION_STRING "v\${PRINT_VERSION}")/a\
> \
> hunter_add_package(GTest)\
> find_package(GTest CONFIG REQUIRED)\
> ' CMakeLists.txt
$ gsed -i 's/add_subdirectory(third-party/gtest)//' CMakeLists.txt
$ gsed -i 's/gtest_main/GTest::gtest_main/' CMakeLists.txt
```

```sh
$ cmake -H. -B_builds -DBUILD_TESTS=ON
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
-- [hunter] HUNTER_ROOT: /home/baha/.hunter
-- [hunter] [ Hunter-ID: 5659b15 | Toolchain-ID: 9b2c9d4 | Config-ID: 8a1641b ]
-- [hunter] GTEST_ROOT: /home/baha/.hunter/_Base/5659b15/9b2c9d4/8a1641b/Install (ver.: 1.10.0)
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
-- Build files have been written to: /home/baha/Alex-kku/workspace/projects/Lab07/_builds
$ cmake --build _builds
Scanning dependencies of target print
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
Scanning dependencies of target check
[ 75%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[100%] Linking CXX executable check
[100%] Built target check
$ cmake --build _builds --target test
Running tests...
Test project /home/baha/Alex-kku/workspace/projects/Lab07/_builds
    Start 1: check
1/1 Test #1: check ............................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.00 sec
$ ls -la $HOME/.hunter
итого 12
drwxr-xr-x  3 baha baha 4096 июн  4 23:34 .
drwxr-xr-x 28 baha baha 4096 июн  5 01:17 ..
drwxr-xr-x  6 baha baha 4096 июн  4 23:34 _Base
```

```sh
$ git clone https://github.com/cpp-pm/hunter $HOME/projects/hunter
$ export HUNTER_ROOT=$HOME/projects/hunter
$ rm -rf _builds
$ cmake -H. -B_builds -DBUILD_TESTS=ON
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
-- [hunter] HUNTER_ROOT: /home/baha/projects/hunter
-- [hunter] [ Hunter-ID: xxxxxxx | Toolchain-ID: 9b2c9d4 | Config-ID: 960678b ]
-- [hunter] GTEST_ROOT: /home/baha/projects/hunter/_Base/xxxxxxx/9b2c9d4/960678b/Install (ver.: 1.10.0)
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
-- Build files have been written to: /home/baha/Alex-kku/workspace/projects/Lab07/_builds
$ cmake --build _builds
Scanning dependencies of target print
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
Scanning dependencies of target check
[ 75%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[100%] Linking CXX executable check
[100%] Built target check
$ cmake --build _builds --target test
Running tests...
Test project /home/baha/Alex-kku/workspace/projects/Lab07/_builds
    Start 1: check
1/1 Test #1: check ............................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.00 sec
```

```sh
$ cat $HUNTER_ROOT/cmake/configs/default.cmake | grep GTest
  hunter_default_version(GTest VERSION 1.7.0-hunter-6)
  hunter_default_version(GTest VERSION 1.10.0)
$ cat $HUNTER_ROOT/cmake/projects/GTest/hunter.cmake
# Copyright (c) 2013, Ruslan Baratov
# All rights reserved.

# !!! DO NOT PLACE HEADER GUARDS HERE !!!

include(hunter_add_version)
include(hunter_cacheable)
include(hunter_download)
include(hunter_pick_scheme)
include(hunter_cmake_args)
...........................
hunter_pick_scheme(DEFAULT url_sha1_cmake)
hunter_cacheable(GTest)
hunter_download(PACKAGE_NAME GTest PACKAGE_INTERNAL_DEPS_ID 1)
$ mkdir cmake/Hunter
$ cat > cmake/Hunter/config.cmake <<EOF
> hunter_config(GTest VERSION 1.7.0-hunter-9)
> EOF
```

```sh
$ mkdir demo
$ cat > demo/main.cpp <<EOF
> #include <print.hpp>
> 
> #include <cstdlib>
> 
> int main(int argc, char* argv[])
> {
>   const char* log_path = std::getenv("LOG_PATH");
>   if (log_path == nullptr)
>   {
>     std::cerr << "undefined environment variable: LOG_PATH" << std::endl;
>     return 1;
>   }
>   std::string text;
>   while (std::cin >> text)
>   {
>     std::ofstream out{log_path, std::ios_base::app};
>     print(text, out);
>     out << std::endl;
>   }
> }
> EOF

$ gsed -i '/endif()/a\
> \
> add_executable(demo ${CMAKE_CURRENT_SOURCE_DIR}/demo/main.cpp)\
> target_link_libraries(demo print)\
> install(TARGETS demo RUNTIME DESTINATION bin)\
> ' CMakeLists.txt
```

```sh
$ mkdir tools
$ git submodule add https://github.com/ruslo/polly tools/polly
Клонирование в «/home/baha/Alex-kku/workspace/projects/Lab07/tools/polly»…
remote: Enumerating objects: 29, done.
remote: Counting objects: 100% (29/29), done.
remote: Compressing objects: 100% (19/19), done.
remote: Total 6423 (delta 10), reused 24 (delta 10), pack-reused 6394
Получение объектов: 100% (6423/6423), 1.64 MiB | 729.00 KiB/s, готово.
Определение изменений: 100% (4418/4418), готово.
$ tools/polly/bin/polly.py --test
Python version: 3.6
Build dir: /home/baha/Alex-kku/workspace/projects/Lab07/_builds/default
Execute command: [
  `which`
  `cmake`
]
....................................
-
Log saved: /home/baha/Alex-kku/workspace/projects/Lab07/_logs/polly/default/log.txt
-
Generate: 0:00:04.078378s
Build: 0:00:01.728307s
Test: 0:00:00.037500s
-
Total: 0:00:05.844571s
-
SUCCESS

$ tools/polly/bin/polly.py --install
Python version: 3.6
Build dir: /home/baha/Alex-kku/workspace/projects/Lab07/_builds/default
Execute command: [
  `which`
  `cmake`
]

[/home/baha/Alex-kku/workspace/projects/Lab07]> "which" "cmake"

/usr/bin/cmake
Execute command: [
  `cmake`
  `--version`
]

[/home/baha/Alex-kku/workspace/projects/Lab07]> "cmake" "--version"

cmake version 3.10.2

CMake suite maintained and supported by Kitware (kitware.com/cmake).

== WARNING ==

Looks like cmake arguments changed. You have two options to fix it:
  * Remove build directory completely by adding '--clear' (works 100%)
  * Run configure again by adding '--reconfig' (you must understand how CMake cache variables works/updated)

- "cmake" "-H." "-B/home/baha/Alex-kku/workspace/projects/Lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=/home/baha/Alex-kku/workspace/projects/Lab07/tools/polly/default.cmake"
+ "cmake" "-H." "-B/home/baha/Alex-kku/workspace/projects/Lab07/_builds/default" "-DCMAKE_TOOLCHAIN_FILE=/home/baha/Alex-kku/workspace/projects/Lab07/tools/polly/default.cmake" "-DCMAKE_INSTALL_PREFIX=/home/baha/Alex-kku/workspace/projects/Lab07/_install/default"
?                                                                                                                                                                               +++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++

$ tools/polly/bin/polly.py --toolchain clang-cxx14
Python version: 3.6
Build dir: /home/baha/Alex-kku/workspace/projects/Lab07/_builds/clang-cxx14
Execute command: [
  `which`
  `cmake`
]
........................................
Scanning dependencies of target print
[ 25%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
Scanning dependencies of target demo
[ 75%] Building CXX object CMakeFiles/demo.dir/demo/main.cpp.o
[100%] Linking CXX executable demo
[100%] Built target demo
-
Log saved: /home/baha/Alex-kku/workspace/projects/Lab07/_logs/polly/clang-cxx14/log.txt
-
Generate: 0:00:05.691181s
Build: 0:00:01.816189s
-
Total: 0:00:07.507875s
-
SUCCESS
```
```sh
$ git add .
$ git commit -m"Lab07 done"
[master 1e23bf3] Lab07 done
 11 files changed, 865 insertions(+), 6 deletions(-)
 create mode 100644 _logs/polly/clang-cxx14/log.txt
 create mode 100644 _logs/polly/default/log-0.txt
 create mode 100644 _logs/polly/default/log-1.txt
 create mode 100644 _logs/polly/default/log-2.txt
 create mode 100644 _logs/polly/default/log.txt
 create mode 100644 cmake/HunterGate.cmake
 create mode 100644 demo/main.cpp
 delete mode 160000 third-party/gtest
 create mode 160000 tools/polly
$ git push origin master
Username for 'https://github.com': Alex-kku
Password for 'https://Alex-kku@github.com':*************
Подсчет объектов: 220, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (125/125), готово.
Запись объектов: 100% (220/220), 1.75 MiB | 1.76 MiB/s, готово.
Total 220 (delta 87), reused 200 (delta 82)
remote: Resolving deltas: 100% (87/87), done.
To https://github.com/Alex-kku/Lab07
 * [new branch]      master -> master
```

## Report

```sh
$ popd
$ export LAB_NUMBER=07
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links

- [Create Hunter package](https://docs.hunter.sh/en/latest/creating-new/create.html)
- [Custom Hunter config](https://github.com/ruslo/hunter/wiki/example.custom.config.id)
- [Polly](https://github.com/ruslo/polly)

```
Copyright (c) 2015-2020 The ISC Authors
```
