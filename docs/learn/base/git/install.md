# Установка и настройка Git (Linux)

Установка Git выполняется с помощью пакетного менеджера

* Debian, Ubuntu: `sudo apt install git`
* Fedora: `sudo dnf install git-all`

Также Git можно установить из исходников, в таком случае мы получаем более свежую версию. Для этого нужно выполнить
следующие инструкции:

* Устанавливаем зависимости для сборки:

```bash
$ sudo apt install dh-autoreconf \
    libcurl4-gnutls-dev \
    libexpat1-dev \
    gettext \
    libz-dev \
    libssl-dev \
    install-info
```

* Для сборки документации в различных форматах:

```bash
$ sudo apt install asciidoc xmlto docbook2x
```

* Т.к. имена бинарных файлов могут отличаться выполняем следующий шаг:

```bash
$ sudo ln -s /usr/bin/db2x_docbook2texi /usr/bin/docbook2x-texi
```

* Теперь мы можем скачать архив с исходниками:

```bash
$ curl -o git.tar.gz https://mirrors.edge.kernel.org/pub/software/scm/git/git-2.43.0.tar.gz
```

* Разархивируем в текущий каталог:

```bash
$ tar -zxf git.tar.gz
$ cd git-2.43.0
```

* Выполняем сборку и компиляцию:

```bash
$ make configure
$ ./configure --prefix=/usr
$ make all doc info
$ sudo make install install-doc install-html install-info
```

Базовые настройки:

```bash
$ git config --global user.name "NetoGeek"
$ git config --global user.email "wion272@gmail.com"
$ git config --global init.defaultBranch master
$ git config --global core.editor vim
$ git config --global core.autocrlf input
$ git config --global color.ui true
$ git config --global alias.hist 'log --pretty=format:"%C(cyan)%h%Creset %C(red)%an%Creset %ad %ar - %C(magenta)%s%Creset %d" --graph --abbrev-commit --date=format:"%d-%m-%Y"'
```

Алиас позволяет добавить сокращение к большой или часто выполняемой команде

!!! Note "Git хранит настройки в трех местах."

    1. /etc/gitconfig - git config --system
    2. .gitconfig - git config --global
    3. .git/config - git config --local

!!! Info

    Скачать
https://raw.githubusercontent.com/git/git/v2.43.0/contrib/completion/git-completion.bash
