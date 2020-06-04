[![Build Status](https://travis-ci.org/Alex-kku/Lab06.svg?branch=master)](https://travis-ci.org/Alex-kku/Lab06)

## Laboratory work VI

<a href="https://yandex.ru/efir/?stream_id=vGWlFO3of-Rg"><img src="https://raw.githubusercontent.com/tp-labs/lab06/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению средств пакетирования на примере **CPack**

```sh
$ open https://cmake.org/Wiki/CMake:CPackPackageGenerators
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab06** на сервисе **GitHub**
- [x] 2. Выполнить инструкцию учебного материала
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME =Alex-kku
$ export GITHUB_EMAIL=leha.kushpelev@mail.ru
$ alias edit=vim
$ alias gsed=sed
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
~/Alex-kku/workspace ~/Alex-kku/workspace
$ source scripts/activate
```

```sh
$ git clone https://github.com/${GITHUB_USERNAME}/Lab05 projects/Lab06
Клонирование в «projects/Lab06»…
remote: Enumerating objects: 188, done.
remote: Counting objects: 100% (188/188), done.
remote: Compressing objects: 100% (112/112), done.
remote: Total 188 (delta 77), reused 171 (delta 69), pack-reused 0
Получение объектов: 100% (188/188), 1.74 MiB | 425.00 KiB/s, готово.
Определение изменений: 100% (77/77), готово.
$ cd projects/Lab06
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/Lab06
```

```sh
$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_STRING "v\${PRINT_VERSION}")
> ' CMakeLists.txt
$ gsed -i '/project(print)/a\
> set(PRINT_VERSION\
>   \${PRINT_VERSION_MAJOR}.\${PRINT_VERSION_MINOR}.\${PRINT_VERSION_PATCH}.\${PRINT_VERSION_TWEAK})
> ' CMakeLists.txt
$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_TWEAK 0)
> ' CMakeLists.txt
$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_PATCH 0)
> ' CMakeLists.txt
$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_MINOR 1)
> ' CMakeLists.txt
$ gsed -i '/project(print)/a\
> set(PRINT_VERSION_MAJOR 0)
> ' CMakeLists.txt
$ git diff
diff --git a/CMakeLists.txt b/CMakeLists.txt
index aa7a323..71b64e3 100644
--- a/CMakeLists.txt
+++ b/CMakeLists.txt
@@ -7,6 +7,13 @@ option(BUILD_EXAMPLES "Build examples" OFF)
 option(BUILD_TESTS "Build tests" OFF)
 
 project(print)
+set(PRINT_VERSION_MAJOR 0)
+set(PRINT_VERSION_MINOR 1)
+set(PRINT_VERSION_PATCH 0)
+set(PRINT_VERSION_TWEAK 0)
+set(PRINT_VERSION
+  ${PRINT_VERSION_MAJOR}.${PRINT_VERSION_MINOR}.${PRINT_VERSION_PATCH}.${PRINT_VERSION_TWEAK})
+set(PRINT_VERSION_STRING "v${PRINT_VERSION}")
 
 add_library(print STATIC ${CMAKE_CURRENT_SOURCE_DIR}/sources/print.cpp)
```

```sh
$ touch DESCRIPTION && edit DESCRIPTION
$ touch ChangeLog.md
$ export DATE="`LANG=en_US date +'%a %b %d %Y'`"
$ cat > ChangeLog.md <<EOF
> * ${DATE} ${GITHUB_USERNAME} <${GITHUB_EMAIL}> 0.1.0.0
> - Initial RPM release
> EOF
```

```sh
$ cat > CPackConfig.cmake <<EOF
> include(InstallRequiredSystemLibraries)
> EOF
```

```sh
$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_PACKAGE_CONTACT ${GITHUB_EMAIL})
> set(CPACK_PACKAGE_VERSION_MAJOR \${PRINT_VERSION_MAJOR})
> set(CPACK_PACKAGE_VERSION_MINOR \${PRINT_VERSION_MINOR})
> set(CPACK_PACKAGE_VERSION_PATCH \${PRINT_VERSION_PATCH})
> set(CPACK_PACKAGE_VERSION_TWEAK \${PRINT_VERSION_TWEAK})
> set(CPACK_PACKAGE_VERSION \${PRINT_VERSION})
> set(CPACK_PACKAGE_DESCRIPTION_FILE \${CMAKE_CURRENT_SOURCE_DIR}/DESCRIPTION)
> set(CPACK_PACKAGE_DESCRIPTION_SUMMARY "static C++ library for printing")
> EOF
```

```sh
$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_RESOURCE_FILE_LICENSE \${CMAKE_CURRENT_SOURCE_DIR}/LICENSE)
> set(CPACK_RESOURCE_FILE_README \${CMAKE_CURRENT_SOURCE_DIR}/README.md)
> EOF
```

```sh
$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_RPM_PACKAGE_NAME "print-devel")
> set(CPACK_RPM_PACKAGE_LICENSE "MIT")
> set(CPACK_RPM_PACKAGE_GROUP "print")
> set(CPACK_RPM_CHANGELOG_FILE \${CMAKE_CURRENT_SOURCE_DIR}/ChangeLog.md)
> set(CPACK_RPM_PACKAGE_RELEASE 1)
> EOF
```

```sh
$ cat >> CPackConfig.cmake <<EOF
> set(CPACK_DEBIAN_PACKAGE_NAME "libprint-dev")
> set(CPACK_DEBIAN_PACKAGE_PREDEPENDS "cmake >= 3.0")
> set(CPACK_DEBIAN_PACKAGE_RELEASE 1)
> EOF
```

```sh
$ cat >> CPackConfig.cmake <<EOF
> include(CPack)
> EOF
```

```sh
$ cat >> CMakeLists.txt <<EOF
> include(CPackConfig.cmake)
> EOF
```

```sh
$ gsed -i 's/lab05/lab06/g' README.md
```

```sh
$ git add .
$ git commit -m"added cpack config"
[master fcdb8e2] added cpack config
 5 files changed, 52 insertions(+), 17 deletions(-)
 create mode 100644 CPackConfig.cmake
 create mode 100644 ChangeLog.md
 create mode 100644 DESCRIPTION
$ git tag v0.1.0.0
$ git push origin master --tags
Username for 'https://github.com': Alex-kku
Password for 'https://Alex-kku@github.com':*************
Подсчет объектов: 195, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (110/110), готово.
Запись объектов: 100% (195/195), 1.74 MiB | 1.35 MiB/s, готово.
Total 195 (delta 80), reused 186 (delta 77)
remote: Resolving deltas: 100% (80/80), done.
To https://github.com/Alex-kku/Lab06
 * [new branch]      master -> master
 * [new tag]         v0.1.0.0 -> v0.1.0.0
```

```sh
$ travis login --auto
Successfully logged in as Alex-kku!
$ travis enable
Detected repository as Alex-kku/Lab06, is this correct? |yes| y
Alex-kku/Lab06: enabled :)
```

```sh
$ cmake -H. -B_build
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
-- Configuring done
-- Generating done
-- Build files have been written to: /home/baha/Alex-kku/workspace/projects/Lab06/_build
$ cmake --build _build
Scanning dependencies of target print
[ 50%] Building CXX object CMakeFiles/print.dir/sources/print.cpp.o
[100%] Linking CXX static library libprint.a
[100%] Built target print
$ cd _build
$ cpack -G "TGZ"
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print
CPack: Create package
CPack: - package: /home/baha/Alex-kku/workspace/projects/Lab06/_build/print-0.1.0.0-Linux.tar.gz generated.
$ cd ..
```

```sh
$ cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
-- Configuring done
-- Generating done
-- Build files have been written to: /home/baha/Alex-kku/workspace/projects/Lab06/_build
$ cmake --build _build --target package
[100%] Built target print
Run CPack packaging tool...
CPack: Create package using TGZ
CPack: Install projects
CPack: - Run preinstall target for: print
CPack: - Install project: print
CPack: Create package
CPack: - package: /home/baha/Alex-kku/workspace/projects/Lab06/_build/print-0.1.0.0-Linux.tar.gz generated.
```

```sh
$ mv _build/*.tar.gz artifacts
$ tree artifacts
artifacts
├── print-0.1.0.0-Linux.tar.gz
└── screenshot.png

0 directories, 2 files
```

## Report

```sh
$ popd
$ export LAB_NUMBER=06
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER} tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Links

- [DMG](https://cmake.org/cmake/help/latest/module/CPackDMG.html)
- [DEB](https://cmake.org/cmake/help/latest/module/CPackDeb.html)
- [RPM](https://cmake.org/cmake/help/latest/module/CPackRPM.html)
- [NSIS](https://cmake.org/cmake/help/latest/module/CPackNSIS.html)

```
Copyright (c) 2015-2020 The ISC Authors
```
