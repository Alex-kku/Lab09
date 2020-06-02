## Laboratory work II

<a href="https://yandex.ru/efir/?stream_id=vMPJl0nEKr_0"><img src="https://raw.githubusercontent.com/tp-labs/lab02/master/preview.png" width="640"/></a>

Данная лабораторная работа посвещена изучению систем контроля версий на примере **Git**.

```bash
$ open https://git-scm.com
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab02** и с лиценцией **MIT**
- [x] 2. Сгенирировать токен для доступа к сервису **GitHub** с правами **repo**
- [x] 3. Ознакомиться со ссылками учебного материала
- [x] 4. Выполнить инструкцию учебного материала
- [x] 5. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```sh
$ export GITHUB_USERNAME=Alex-kku
$ export GITHUB_EMAIL=leha.kushpelev@mai.ru
$ export GITHUB_TOKEN=*******************************
$ alias edit=subl
```

```sh
$ cd ${GITHUB_USERNAME}/workspace
$ source scripts/activate
```

```sh
$ mkdir ~/.config
$ cat > ~/.config/hub <<EOF
github.com:
- user: ${GITHUB_USERNAME}
  oauth_token: ${GITHUB_TOKEN}
  protocol: https
EOF
$ git config --global hub.protocol https
```

```sh
$ mkdir projects/lab02 && cd projects/lab02
$ git init
Инициализирован пустой репозиторий Git в /home/baha/Alex-kku/workspace/projects/lab02/.git/
$ git config --global user.name ${GITHUB_USERNAME}
$ git config --global user.email ${GITHUB_EMAIL}
# check your git global settings
$ git config -e --global
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab02.git
$ git pull origin master
remote: Enumerating objects: 93, done.
remote: Counting objects: 100% (93/93), done.
remote: Compressing objects: 100% (62/62), done.
remote: Total 93 (delta 30), reused 93 (delta 30), pack-reused 0
Распаковка объектов: 100% (93/93), готово.
Из https://github.com/Alex-kku/lab02
 * branch            master     -> FETCH_HEAD
 * [новая ветка]     master     -> origin/master
$ touch README.md
$ git status
На ветке master
нечего коммитить, нет изменений в рабочем каталоге
$ git add README.md
$ git commit -m"added README.md"
На ветке master
нечего коммитить, нет изменений в рабочем каталоге
$ git push origin master
Username for 'https://github.com': Alex-kku
Password for 'https://Alex-kku@github.com': *************
Everything up-to-date
```

Добавить на сервисе **GitHub** в репозитории **lab02** файл **.gitignore**
со следующем содержимом:

```sh
*build*/
*install*/
*.swp
.idea/
```

```sh
$ git pull origin master
remote: Enumerating objects: 8, done.
remote: Counting objects: 100% (8/8), done.
remote: Compressing objects: 100% (5/5), done.
remote: Total 6 (delta 2), reused 0 (delta 0), pack-reused 0
Распаковка объектов: 100% (6/6), готово.
Из https://github.com/Alex-kku/lab02
 * branch            master     -> FETCH_HEAD
   af8687b..257420e  master     -> origin/master
Обновление af8687b..257420e
Fast-forward
 .gitignore |  4 ++++
 README.md  | 34 +++++++++++++++++++++++++---------
 2 files changed, 29 insertions(+), 9 deletions(-)
 create mode 100644 .gitignore
$ git log
commit 257420e6e377dded291edfc5a3bfc22826a8ce82 (HEAD -> master, origin/master)
Author: Alex-kku <61166074+Alex-kku@users.noreply.github.com>
Date:   Tue Jun 2 16:28:37 2020 +0300

    Create .gitignore

commit ed018f8867d4fcba83ee7e64a6d43e32b3358b2b
Author: Alex-kku <61166074+Alex-kku@users.noreply.github.com>
Date:   Tue Jun 2 16:25:12 2020 +0300

    Update README.md


```

```sh
$ mkdir sources
$ mkdir include
$ mkdir examples
$ cat > sources/print.cpp <<EOF
#include <print.hpp>

void print(const std::string& text, std::ostream& out)
{
  out << text;
}

void print(const std::string& text, std::ofstream& out)
{
  out << text;
}
EOF
```

```sh
$ cat > include/print.hpp <<EOF
#include <fstream>
#include <iostream>
#include <string>

void print(const std::string& text, std::ofstream& out);
void print(const std::string& text, std::ostream& out = std::cout);
EOF
```

```sh
$ cat > examples/example1.cpp <<EOF
#include <print.hpp>

int main(int argc, char** argv)
{
  print("hello");
}
EOF
```

```sh
$ cat > examples/example2.cpp <<EOF
#include <print.hpp>

#include <fstream>

int main(int argc, char** argv)
{
  std::ofstream file("log.txt");
  print(std::string("hello"), file);
}
EOF
```

```sh
$ edit README.md
```

```sh
$ git status
На ветке master
Неотслеживаемые файлы:
  (используйте «git add <файл>…», чтобы добавить в то, что будет включено в коммит)

	examples/
	include/
	sources/

ничего не добавлено в коммит, но есть неотслеживаемые файлы (используйте «git add», чтобы отслеживать их)
$ git add .
$ git commit -m"added sources"
[master f321971] added sources
 4 files changed, 32 insertions(+)
 create mode 100644 examples/example1.cpp
 create mode 100644 examples/example2.cpp
 create mode 100644 include/print.hpp
 create mode 100644 sources/print.cpp
$ git push origin master
Username for 'https://github.com': Alex-kku
Password for 'https://Alex-kku@github.com':*************
Подсчет объектов: 9, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (7/7), готово.
Запись объектов: 100% (9/9), 1000 bytes | 1000.00 KiB/s, готово.
Total 9 (delta 0), reused 0 (delta 0)
remote: This repository moved. Please use the new location:
remote:   https://github.com/Alex-kku/Lab02.git
To https://github.com/Alex-kku/lab02.git
   257420e..f321971  master -> master
```

## Report

```sh
$ cd ~/Alex-kku/workspace
$ export LAB_NUMBER=02
$ git clone https://github.com/tp-labs/lab${LAB_NUMBER}.git tasks/lab${LAB_NUMBER}
$ mkdir reports/lab${LAB_NUMBER}
$ cp tasks/lab${LAB_NUMBER}/README.md reports/lab${LAB_NUMBER}/REPORT.md
$ cd reports/lab${LAB_NUMBER}
$ edit REPORT.md
$ gist REPORT.md
```

## Homework

### Part I

1. Создайте пустой репозиторий на сервисе github.com (или gitlab.com, или bitbucket.com).
2. Выполните инструкцию по созданию первого коммита на странице репозитория, созданного на предыдещем шаге.
3. Создайте файл `hello_world.cpp` в локальной копии репозитория (который должен был появиться на шаге 2). Реализуйте программу **Hello world** на языке C++ используя плохой стиль кода. Например, после заголовочных файлов вставьте строку `using namespace std;`.
4. Добавьте этот файл в локальную копию репозитория.
5. Закоммитьте изменения с *осмысленным* сообщением.
6. Изменитьте исходный код так, чтобы программа через стандартный поток ввода запрашивалось имя пользователя. А в стандартный поток вывода печаталось сообщение `Hello world from @name`, где `@name` имя пользователя.
7. Закоммитьте новую версию программы. Почему не надо добавлять файл повторно `git add`?
8. Запуште изменения в удалёный репозиторий.
9. Проверьте, что история коммитов доступна в удалёный репозитории.

### Part II

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. В локальной копии репозитория создайте локальную ветку `patch1`.
2. Внесите изменения в ветке `patch1` по исправлению кода и избавления от `using namespace std;`.
3. **commit**, **push** локальную ветку в удалённый репозиторий.
4. Проверьте, что ветка `patch1` доступна в удалёный репозитории.
5. Создайте pull-request `patch1 -> master`.
6. В локальной копии в ветке `patch1` добавьте в исходный код комментарии.
7. **commit**, **push**.
8. Проверьте, что новые изменения есть в созданном на **шаге 5** pull-request
9. В удалённый репозитории выполните  слияние PR `patch1 -> master` и удалите ветку `patch1` в удаленном репозитории.
10. Локально выполните **pull**.
11. С помощью команды **git log** просмотрите историю в локальной версии ветки `master`.
12. Удалите локальную ветку `patch1`.

### Part III

**Note:** *Работать продолжайте с теми же репоззиториями, что и в первой части задания.*
1. Создайте новую локальную ветку `patch2`.
2. Измените *code style* с помощью утилиты [**clang-format**](http://clang.llvm.org/docs/ClangFormat.html). Например, используя опцию `-style=Mozilla`.
3. **commit**, **push**, создайте pull-request `patch2 -> master`.
4. В ветке **master** в удаленном репозитории измените комментарии, например, расставьте знаки препинания, переведите комментарии на другой язык.
5. Убедитесь, что в pull-request появились *конфликтны*.
6. Для этого локально выполните **pull** + **rebase** (точную последовательность команд, следует узнать самостоятельно). **Исправьте конфликты**.
7. Сделайте *force push* в ветку `patch2`
8. Убедитель, что в pull-request пропали конфликтны. 
9. Вмержите pull-request `patch2 -> master`.

## Homework

### Part I

1)
2)
```sh
$ mkdir homework02
$ cd homework02
$ subl README.md
$ echo "# Homework02" >> README.md
$ git init
Инициализирован пустой репозиторий Git в /home/baha/Alex-kku/workspace/projects/homework02/.git/
$ git add README.md
$ git commit -m "first commit"
[master (корневой коммит) 27d596e] first commit
 1 file changed, 1 insertion(+)
 create mode 100644 README.md
$ git remote add origin https://github.com/Alex-kku/Homework02.git
$ git push -u origin master
Username for 'https://github.com': Alex-kku
Password for 'https://Alex-kku@github.com':*************
Подсчет объектов: 3, готово.
Запись объектов: 100% (3/3), 226 bytes | 226.00 KiB/s, готово.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/Alex-kku/Homework02.git
 * [new branch]      master -> master
Ветка «master» отслеживает внешнюю ветку «master» из «origin».
```
3)
```sh
$ mkdir hello_world.cpp
$ cd hello_world.cpp
$ cat > hello_world.cpp <<EOF
#include <iosrteam>

using namespase std;

int main()
{
cout << "Hello, world!" << endl;
return 0;
}
EOF
```
4)
```sh
$ git add .
```
5)
```sh
$ git commit -m"Aadded hello_world.cpp"
[master 4d3e1d8] Aadded hello_world.cpp
 1 file changed, 9 insertions(+)
 create mode 100644 hello_world.cpp/hello_world.cpp
 ```
6)
7)
```sh
$ git commit -a -m "New hello_world.cpp"
[master fef2d0f] New hello_world.cpp
 1 file changed, 6 insertions(+), 6 deletions(-)
#git add не надо выполнять повторно, посколько файл уже отслеживается
```
8)
```sh
$ git push origin master
Username for 'https://github.com': Alex-kku
Password for 'https://Alex-kku@github.com':*************
Подсчет объектов: 9, готово.
Delta compression using up to 8 threads.
Сжатие объектов: 100% (9/9), готово.
Запись объектов: 100% (9/9), 1.18 KiB | 1.18 MiB/s, готово.
Total 9 (delta 1), reused 0 (delta 0)
remote: Resolving deltas: 100% (1/1), done.
To https://github.com/Alex-kku/Homework02.git
   27d596e..fef2d0f  master -> master
```
9)
```sh
$  git log
commit fef2d0f9e05fb97f202a3217f4f32eb1d1e333ff (HEAD -> master, origin/master)
Author: Alex-kku <leha.kushpelev@mai.ru>
Date:   Tue Jun 2 19:24:22 2020 +0300

    New hello_world.cpp

commit 4d3e1d884f38e4764f97991ed31ff4f9e043d777
Author: Alex-kku <leha.kushpelev@mai.ru>
Date:   Tue Jun 2 19:05:43 2020 +0300

    Aadded hello_world.cpp

commit 27d596ebd3a7a5382b5015968a4f676e756201ab
Author: Alex-kku <leha.kushpelev@mai.ru>
Date:   Tue Jun 2 18:38:46 2020 +0300

    first commit
```
### Part II

1)





## Links

- [hub](https://hub.github.com/)
- [GitHub](https://github.com)
- [Bitbucket](https://bitbucket.org)
- [Gitlab](https://about.gitlab.com)
- [LearnGitBranching](http://learngitbranching.js.org/)

```
Copyright (c) 2015-2020 The ISC Authors
```
