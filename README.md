[![Build Status](https://travis-ci.org/woz91/lab09.svg?branch=master)](https://travis-ci.org/woz91/lab09)

## Laboratory work IX

Данная лабораторная работа посвещена изучению процесса создания пакета на примере **Github Release**

```ShellSession
$ open https://help.github.com/articles/creating-releases/
```

## Tasks

- [x] 1. Создать публичный репозиторий с названием **lab09** на сервисе **GitHub**
- [x] 2. Ознакомиться со ссылками учебного материала
- [x] 3. Получить токен для доступа к репозиториям сервиса **GitHub**
- [x] 4. Сгенерировать GPG ключ и добавить его к аккаунту сервиса **GitHub**
- [x] 5. Выполнить инструкцию учебного материала
- [x] 6. Составить отчет и отправить ссылку личным сообщением в **Slack**

## Tutorial

```ShellSession
$ export GITHUB_TOKEN=7fd2df81a4398f3af67d3368578960b57299c129
$ export GITHUB_USERNAME=woz91
$ alias gsed=sed # for *-nix system
```

```ShellSession
$ cd ${GITHUB_USERNAME}/workspace
$ pushd .
$ source scripts/activate
$ go get github.com/aktau/github-release
```

```ShellSession
$ git clone https://github.com/${GITHUB_USERNAME}/lab08 projects/lab09
$ cd projects/lab09
$ git remote remove origin
$ git remote add origin https://github.com/${GITHUB_USERNAME}/lab09
```

```ShellSession
$ gsed -i 's/lab08/lab09/g' README.md
```

```ShellSession
$ cmake -H. -B_build -DCPACK_GENERATOR="TGZ"
$ cmake --build _build --target package
```

```ShellSession
$ travis login --auto
$ travis enable
```

```ShellSession
$ git tag -s v0.1.0.0
$ git tag -v v0.1.0.0
$ git push origin master --tags
```

```ShellSession
$ github-release --version
$ github-release info -u ${GITHUB_USERNAME} -r lab09
$ github-release release \
    --user ${GITHUB_USERNAME} \
    --repo lab09 \
    --tag v0.1.0.0 \
    --name "libprint" \
    --description "my first release"
```

```ShellSession
$ export PACKAGE_OS=`uname -s` PACKAGE_ARCH=`uname -m` 
$ export PACKAGE_FILENAME=print-${PACKAGE_OS}-${PACKAGE_ARCH}.tar.gz
$ github-release upload \
    --user ${GITHUB_USERNAME} \
    --repo lab09 \
    --tag v0.1.0.0 \
    --name "${PACKAGE_FILENAME}" \
    --file _build/*.tar.gz
```

```ShellSession
$ github-release info -u ${GITHUB_USERNAME} -r lab09
$ wget https://github.com/${GITHUB_USERNAME}/lab09/releases/download/v0.1.0.0/${PACKAGE_FILENAME}
$ tar -ztf ${PACKAGE_FILENAME}
```

## Report

```ShellSession
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
Copyright (c) 2017 Братья Вершинины
```
# lab09
# lab09
