[![Build Status](https://travis-ci.org/Alex-kku/Lab05.svg?branch=master)](https://travis-ci.org/Alex-kku/Lab05)

## Laboratory work V

<a href="https://yandex.ru/efir/?stream_id=vQw_LH0UfN6I"><img src="https://raw.githubusercontent.com/tp-labs/lab05/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению фреймворков для тестирования на примере **GTest**

```sh
$ open https://github.com/google/googletest
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab05** на сервисе **GitHub**
- [x] 2. Выполнить инструкцию учебного материала
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ $ export GITHUB_USERNAME=Alex-kku
$ alias gsed=sed # for *-nix system
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/Alex-kku/workspace ~/Alex-kku/workspace
$ source scripts/activate
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/Lab04 projects/Lab05
Клонирование в «projects/Lab05»…
remote: Enumerating objects: 161, done.
remote: Counting objects: 100% (161/161), done.
remote: Compressing objects: 100% (96/96), done.
remote: Total 161 (delta 64), reused 154 (delta 61), pack-reused 0
Получение объектов: 100% (161/161), 1.30 MiB | 1.13 MiB/s, готово.
Определение изменений: 100% (64/64), готово.
$ cd projects/Lab05
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab05
```

```sh
$ mkdir third-party
$ git submodule add https://github.com/google/googletest third-party/gtest
Клонирование в «/home/baha/Alex-kku/workspace/projects/Lab05/third-party/gtest»…
remote: Enumerating objects: 16, done.
remote: Counting objects: 100% (16/16), done.
remote: Compressing objects: 100% (13/13), done.
remote: Total 20450 (delta 6), reused 9 (delta 3), pack-reused 20434
Получение объектов: 100% (20450/20450), 7.59 MiB | 712.00 KiB/s, готово.
Определение изменений: 100% (15112/15112), готово.
$  cd third-party/gtest && git checkout release-1.8.1 && cd ../..
Примечание: переход на «release-1.8.1».

Вы сейчас в состоянии «отделённого HEAD». Вы можете осмотреться, сделать
экспериментальные изменения и закоммитить их, также вы можете отменить
изменения любых коммитов в этом состоянии не затрагивая любые ветки и
не переходя на них.

Если вы хотите создать новую ветку и сохранить свои коммиты, то вы
можете сделать это (сейчас или позже) вызвав команду checkout снова,
но с параметром -b. Например:

  git checkout -b <имя-новой-ветки>

HEAD сейчас на 2fe3bd99 Merge pull request #1433 from dsacre/fix-clang-warnings
$ git add third-party/gtest
$ git commit -m"added gtest framework"
[master 54dbf7d] added gtest framework
 2 files changed, 4 insertions(+)
 create mode 100644 .gitmodules
 create mode 160000 third-party/gtest
```

```sh
$ gsed -i '/option(BUILD_EXAMPLES "Build examples" OFF)/a\
> option(BUILD_TESTS "Build tests" OFF)
> ' CMakeLists.txt
$ cat >> CMakeLists.txt <<EOF
> 
> if(BUILD_TESTS)
>   enable_testing()
>   add_subdirectory(third-party/gtest)
>   file(GLOB \${PROJECT_NAME}_TEST_SOURCES tests/*.cpp)
>   add_executable(check \${\${PROJECT_NAME}_TEST_SOURCES})
>   target_link_libraries(check \${PROJECT_NAME} gtest_main)
>   add_test(NAME check COMMAND check)
> endif()
> EOF
```

```sh
$ mkdir tests
$ cat > tests/test1.cpp <<EOF
> #include <print.hpp>
> 
> #include <gtest/gtest.h>
> 
> TEST(Print, InFileStream)
> {
>   std::string filepath = "file.txt";
>   std::string text = "hello";
>   std::ofstream out{filepath};
> 
>   print(text, out);
>   out.close();
> 
>   std::string result;
>   std::ifstream in{filepath};
>   in >> result;
> 
>   EXPECT_EQ(result, text);
> }
> EOF
```

```sh
$ cmake -H. -B_build -DBUILD_TESTS=ON
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
-- Found PythonInterp: /usr/bin/python (found version "2.7.17") 
-- Looking for pthread.h
-- Looking for pthread.h - found
-- Looking for pthread_create
-- Looking for pthread_create - not found
-- Check if compiler accepts -pthread
-- Check if compiler accepts -pthread - yes
-- Found Threads: TRUE  
-- Configuring done
-- Generating done
-- Build files have been written to: /home/baha/Alex-kku/workspace/projects/Lab05/_build
$ cmake --build _build
Scanning dependencies of target gtest
[  8%] Building CXX object third-party/gtest/googlemock/gtest/CMakeFiles/gtest.dir/src/gtest-all.cc.o
[ 16%] Linking CXX static library libgtest.a
[ 16%] Built target gtest
Scanning dependencies of target gtest_main
[ 25%] Building CXX object third-party/gtest/googlemock/gtest/CMakeFiles/gtest_main.dir/src/gtest_main.cc.o
[ 33%] Linking CXX static library libgtest_main.a
[ 33%] Built target gtest_main
Scanning dependencies of target print
[ 41%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[ 50%] Linking CXX static library libprint.a
[ 50%] Built target print
Scanning dependencies of target check
[ 58%] Building CXX object CMakeFiles/check.dir/tests/test1.cpp.o
[ 66%] Linking CXX executable check
[ 66%] Built target check
Scanning dependencies of target gmock
[ 75%] Building CXX object third-party/gtest/googlemock/CMakeFiles/gmock.dir/src/gmock-all.cc.o
[ 83%] Linking CXX static library libgmock.a
[ 83%] Built target gmock
Scanning dependencies of target gmock_main
[ 91%] Building CXX object third-party/gtest/googlemock/CMakeFiles/gmock_main.dir/src/gmock_main.cc.o
[100%] Linking CXX static library libgmock_main.a
[100%] Built target gmock_main
$ cmake --build _build --target test
Running tests...
Test project /home/baha/Alex-kku/workspace/projects/Lab05/_build
    Start 1: check
1/1 Test #1: check ............................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.01 sec
```

```sh
$ _build/check
Running main() from /home/baha/Alex-kku/workspace/projects/Lab05/third-party/gtest/googletest/src/gtest_main.cc
[==========] Running 1 test from 1 test case.
[----------] Global test environment set-up.
[----------] 1 test from Print
[ RUN      ] Print.InFileStream
[       OK ] Print.InFileStream (0 ms)
[----------] 1 test from Print (0 ms total)

[----------] Global test environment tear-down
[==========] 1 test from 1 test case ran. (0 ms total)
[  PASSED  ] 1 test.
$ cmake --build _build --target test -- ARGS=--verbose
Running tests...
UpdateCTestConfiguration  from :/home/baha/Alex-kku/workspace/projects/Lab05/_build/DartConfiguration.tcl
UpdateCTestConfiguration  from :/home/baha/Alex-kku/workspace/projects/Lab05/_build/DartConfiguration.tcl
Test project /home/baha/Alex-kku/workspace/projects/Lab05/_build
Constructing a list of tests
Done constructing a list of tests
Updating test list for fixtures
Added 0 tests to meet fixture requirements
Checking test dependency graph...
Checking test dependency graph end
test 1
    Start 1: check

1: Test command: /home/baha/Alex-kku/workspace/projects/Lab05/_build/check
1: Test timeout computed to be: 9.99988e+06
1: Running main() from /home/baha/Alex-kku/workspace/projects/Lab05/third-party/gtest/googletest/src/gtest_main.cc
1: [==========] Running 1 test from 1 test case.
1: [----------] Global test environment set-up.
1: [----------] 1 test from Print
1: [ RUN      ] Print.InFileStream
1: [       OK ] Print.InFileStream (0 ms)
1: [----------] 1 test from Print (0 ms total)
1: 
1: [----------] Global test environment tear-down
1: [==========] 1 test from 1 test case ran. (0 ms total)
1: [  PASSED  ] 1 test.
1/1 Test #1: check ............................   Passed    0.00 sec

100% tests passed, 0 tests failed out of 1

Total Test time (real) =   0.00 sec
```

```sh
$ gsed -i 's/lab04/lab05/g' README.md
$ gsed -i 's/\(DCMAKE_INSTALL_PREFIX=_install\)/\1 -DBUILD_TESTS=ON/' .travis.yml
$ gsed -i '/cmake --build _build --target install/a\
> - cmake --build _build --target test -- ARGS=--verbose
> ' .travis.yml
```

```sh
$ travis lint
Hooray, .travis.yml looks valid :)
```

```sh
$ git add .travis.yml
$ git add tests
$ git add -p
diff --git a/CMakeLists.txt b/CMakeLists.txt
index 96a361e..aa7a323 100644
--- a/CMakeLists.txt
+++ b/CMakeLists.txt
@@ -4,6 +4,7 @@ set(CMAKE_CXX_STANDARD 11)
 set(CMAKE_CXX_STANDARD_REQUIRED ON)
 
 option(BUILD_EXAMPLES "Build examples" OFF)
+option(BUILD_TESTS "Build tests" OFF)
 
 project(print)
 
Stage this hunk [y,n,q,a,d,j,J,g,/,e,?]? y
@@ -34,3 +35,12 @@ install(TARGETS print
 
 install(DIRECTORY ${CMAKE_CURRENT_SOURCE_DIR}/include/ DESTINATION include)
 install(EXPORT print-config DESTINATION cmake)
+
+if(BUILD_TESTS)
+  enable_testing()
+  add_subdirectory(third-party/gtest)
+  file(GLOB ${PROJECT_NAME}_TEST_SOURCES tests/*.cpp)
+  add_executable(check ${${PROJECT_NAME}_TEST_SOURCES})
+  target_link_libraries(check ${PROJECT_NAME} gtest_main)
+  add_test(NAME check COMMAND check)
+endif()
Stage this hunk [y,n,q,a,d,K,g,/,e,?]? y

diff --git a/README.md b/README.md
index 053f5cd..467036e 100644
--- a/README.md
+++ b/README.md
@@ -2,7 +2,7 @@
 
 ## Laboratory work IV
 
-<a href="https://yandex.ru/efir/?stream_id=vCgeA9EiySzw"><img src="https://raw.githubusercontent.com/tp-labs/lab04/master/preview.png" width="640"/></a>
+<a href="https://yandex.ru/efir/?stream_id=vCgeA9EiySzw"><img src="https://raw.githubusercontent.com/tp-labs/lab05/master/preview.png" width="640"/></a>
 
 Данная лабораторная работа посвещена изучению систем непрерывной интеграции на примере сервиса **Travis CI**
 
Stage this hunk [y,n,q,a,d,j,J,g,/,e,?]? y
@@ -13,7 +13,7 @@ $ open https://travis-ci.org
 ## Tasks
 
 - [x] 1. Авторизоваться на сервисе **Travis CI** с использованием **GitHub** аккаунта
-- [x] 2. Создать публичный репозиторий с названием **lab04** на сервисе **GitHub**
+- [x] 2. Создать публичный репозиторий с названием **lab05** на сервисе **GitHub**
 - [x] 3. Ознакомиться со ссылками учебного материала
 - [x] 4. Включить интеграцию сервиса **Travis CI** с созданным репозиторием
 - [x] 5. Получить токен для **Travis CLI** с правами **repo** и **user**
Stage this hunk [y,n,q,a,d,K,g,/,e,?]? y

$ git commit -m"added tests"
[master b32b89d] added tests
 4 files changed, 33 insertions(+), 3 deletions(-)
 create mode 100644 tests/test1.cpp
$ git push origin master
Username for 'https://github.com': Alex-kku
Password for 'https://Alex-kku@github.com':*************
Подсчет объектов: 172, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (102/102), готово.
Запись объектов: 100% (172/172), 1.30 MiB | 408.00 KiB/s, готово.
Total 172 (delta 69), reused 158 (delta 64)
remote: Resolving deltas: 100% (69/69), done.
To https://github.com/Alex-kku/Lab05
 * [new branch]      master -> master
```

```sh
$ travis login --auto
Successfully logged in as Alex-kku!
$ travis enable
Detected repository as Alex-kku/Lab05, is this correct? |yes| y
Alex-kku/Lab05: enabled :)
```

```sh
$ mkdir artifacts
$ sleep 20s && gnome-screenshot --file artifacts/screenshot.png
# open https://github.com/${GITHUB_USERNAME}/lab05
```

## Report

```sh
$ popd
$ export LAB_NUMBER=05
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links

- [C++ CI: Travis, CMake, GTest, Coveralls & Appveyor](http://david-grs.github.io/cpp-clang-travis-cmake-gtest-coveralls-appveyor/)
- [Boost.Tests](http://www.boost.org/doc/libs/1_63_0/libs/test/doc/html/)
- [Catch](https://github.com/catchorg/Catch2)

```
Copyright (c) 2015-2020 The ISC Authors
```
