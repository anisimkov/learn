# Перевод learn.adacore.com

В этой ветке (`ru`) сделан [перевод нескольких глав](https://reznikmm.github.io/learn/)
книги "Introduction to Ada" (спасибо Сергею за этот тяжелый труд!).

Целью является улучшение перевода, в часности использование терминологии из
стандрата Ада 83. Из-за способа преобразования перевода в `RST` формат
появились некоторые несоответствия с оригиналом:

* интерактивные виджеты с Ада кодом заменены на листинги:

    sed -i -e 's/\.\. code:: ada.*$/.. code-block:: ada/g' *.rst

* отсутствуют листинги с выводом отмеченые

    .. only:: builder_html
       ...

Надеюсь их не сложно будет восстановить.

Присылайте ваши изменения в виде
[pull requests](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/about-pull-requests).

Последняя редакция доступна на [GitHub Pages](https://reznikmm.github.io/learn/)
в формате `HTML`.

# learn.adacore.com

Sources for AdaCore's learn.adacore.com website

---

![Typescript Test Suite](https://github.com/AdaCore/learn/workflows/Typescript%20Test%20Suite/badge.svg)
![Sphinx Plugin Tests](https://github.com/AdaCore/learn/workflows/Sphinx%20Plugin%20Tests/badge.svg)
![Sphinx Content Tests](https://github.com/AdaCore/learn/workflows/Sphinx%20Content%20Tests/badge.svg)

## Requirements

This project requires Vagrant and VirtualBox

## Getting started

To setup for development run:
```
$ vagrant up
```
This will spin up three vms:

web: Is the the build system for the frontend web content. This includes the
webpack build system and sphinx build.

server: Is the backend server with the widget API.

epub: Is the publishing server. This includes all packages needed to
generate the learn website.

To build and start the development server for the frontend, run:
```
$ vagrant ssh web

# The following commands will be run inside the vm

$ source /vagrant/venv/bin/activate
$ cd /vagrant/frontend
$ yarn run dev
```
This will run webpack on the typescript and scss, then sphinx for the rst
using `make local` which will point the widgets at 127.0.0.1:8000

You can then point your browser on your host to 127.0.0.1:8080 to see the learn
website being served from vagrant.

To build and start the development server for the backend, run:
```
$ vagrant ssh server

# The following commands will be run inside the vm

$ cd /vagrant
$ source venv/bin/activate
$ ./dev_server.sh
```

You can use ctrl-c to quit the bash script which will kill both the flask
and celery processes.

To build and start the publishing server, run:
```
$ vagrant ssh epub

# The following commands will be run inside the vm

$ cd /vagrant
$ source venv/bin/activate
$ make site
```
This will build the content for the learn website. You can find it in the
`/vagrant/frontend/dist` directory.
