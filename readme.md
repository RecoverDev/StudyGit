# Изучаем Git вместе

---


## Это небольшая инструкция по использованию Git

**Git** - это система по управлению версиями. Она предназначена для отслеживания и ведения истории изменения файлов в проекте. Также ее можно использовать для совместной работы над проетом группы разработчиков.

Установить **Git** на свою машину можно скачав установщик по адресу [git](https://git-scm.com/downloads "Git dounload")


После установки необходимо запустить __Git Bash__. Откроется консоль **Git**.

Вот какие команды в ней можно использовать:

* mrdir - создание каталога
* touch - создание файла
* rm - удаление файла
* cd - перейти в указанный каталог
* pwd - показать текущий каталог
* ls - показать содержимое каталога

и многие другие.

## Создание локального репозитория

Создать локальный __репозиторий__ *(хранилище)* довольно просто.
Сначала нужно создать каталог, где будет находиться хранилище командой **mkdir**. Затем инициализировать его командой **git init**

```bash
$ mkdir /d/stidy-git # создали каталог с хранилищем
$ cd /d/study-git # перешли в созданный каталог
$ git init # инициализировали хранилище
```

## Подключение к удаленному репозиторию

В качестве удаленного хранилища будем использовать сервер **GitHub**.

Для этого ам необходимо зайти на сайт [GitHub](https://github.com) и загеристрироваться там. Далее авторизоваться под только что созданной учетной записью и выбрать пункт меню **Repositories** в левом верхем углу. Затем нажать на зеленую кнопку **NEW** для создания своего нового удаленного хранилища.

Назовем его, например, **Study-Git**.

Теперь подключим локальное хранилище к удаленному с помощью команды **git remote add**. Строку для подключения можно взять на сайте __GitHub__ на странице созданного нами репозитория.

```bash
$ git remote add origin git@github.com:RecoverDev/Study-Git.git
``` 

## Сохранение данных

Что что-то сохрать, это нужно сначала создать. Создадим файл **README.MD** _(этот файл)_ и попробуем сохранить его на удаленном хранилище.

Для создания файла используем команду **touch**.

После того, как мы отредактировали созданный файл любым в любом текстовом редакторе, подготовим его к сохранению в __Git__ с помощью команды **git add**, а затем сохраним его текущую версию с помощью команды **git commit**.

Результат нашей работы можно проверить командой **git status**.

Таким образом наш файл оказался сохраненным в локальном хранилище **Git**. 

Чтобы сохранить его в удаленном репозитории необходимо воспользоваться командой **git push**.

```bash
$ touch readme.md # создали файл readme.md

# отредактировали созданный файл
# в любом текстовом редакторе,
# который нам понравится

$ git add readme.md # подготовили файл к сохранению в системе Git
$ git commit -m "Сохранение файла README.MD" # сохранили версию файла с описанием ( -m "Описание")
$ git status # Проверили статус
$ git push -u origin master # сохранили на удаленном хранилище
```

__И вот теперь вы можете читать эти стоки, подключившись к моему удаленному хранилищу, которое я создал специально для вас!!!__



