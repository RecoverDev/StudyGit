# Изучаем Git вместе

---


## Это небольшая инструкция по использованию Git

**Git** - это система по управлению версиями. Она предназначена для отслеживания и ведения истории изменения файлов в проекте. Также ее можно использовать для совместной работы над проетом группы разработчиков.

Установить **Git** на свою машину можно скачав установщик по адресу [git](https://git-scm.com/downloads "Git download")


После установки необходимо запустить __Git Bash__. Откроется консоль **Git**.

Вот какие команды в ней можно использовать:

* __mrdir__ - создание каталога
* __touch__ - создание файла
* __rm__ - удаление файла
* __cd__ - перейти в указанный каталог
* __pwd__ - показать текущий каталог
* __ls__ - показать содержимое каталога

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

Для этого нам необходимо зайти на сайт [GitHub](https://github.com) и загеристрироваться там. Далее авторизоваться под только что созданной учетной записью и выбрать пункт меню **Repositories** в левом верхем углу. Затем нажать на зеленую кнопку **NEW** для создания своего нового удаленного хранилища.

Назовем его, например, **Study-Git**.

Теперь подключим локальное хранилище к удаленному с помощью команды **git remote add**. Строку для подключения можно взять на сайте __GitHub__ на странице созданного нами репозитория.

```bash
$ git remote add origin git@github.com:RecoverDev/Study-Git.git
``` 

## Организация защищенного канала связи с GitHub (SSH)

Для того, чтобы ваше удаленное хранилище было закрыто от посторонних глаз, можно организовать защищенный канал связи. Можно использовать сетевой протокол **SSH**.

### Проверка наличия ключей для протокола SSH

**Git** хранит сгенерированные ключи в домашнем каталоге в подкаталоге **/.ssh**.
Проверить их наличие можно командой

```bash
$ cd ~/.ssh # перешли в каталог с ключами
$ ls -la # вывели список созданных ключей
```

Если в каталоге есть ключи и вы их не создавали, то удалите их.

### Генерация ключей

Для генерации ключей используется команда **ssh-keygen**

```bash
$ ssh-keygen -t ed25519 -C "recover@list.ru" # указывается электронная почта к которой привязан аккаунт на GitHub
$ ls -la # проверим, что получилось
```

В каталоге должны появиться файлы

```bash
id_ed25519 # закрытый ключ
id_ed25519.pub # открытый ключ (public)
```

### Привязка ключа к GitHub

Копируем содержимое **ОТКРЫТОГО** ключа в буфер обмена.
```bash
$ clip < ~/.ssh/id_ed25519.pub
```

Затем на сайте **GitHub** выбирам пункт меню **Setting** в меню аккаунта (верхний правый угол) и в нем подпункт **SSH and GPG keys**.

На открывшейся вкладке нажимаем зеленую кнопку **New SSH key** и копируем в поле __Key__ содержимое буфера обмена. В поле **Key type** указываем **Authentication Key**, в поле **Title** пишем любое название, например **"Личный ключ"**.

Нажимаем кнопку **Add SSH key**. Готово.

Теперь общение будет проходить по защищенному каналу.

_**Важное замечание**_:Защищенный канал связи можно организовать только с приватным хранилищем (при создании вы его объявили как **Private**). При организации защищенного канала связи строка подключения к удаленному репозиторию выглядит так

```bash
$ git remote add origin git@github.com:RecoverDev/Study-Git.git
``` 

Если репозиторий **Public**, то строка подключения выглядит так

```bash
$ git remote add origin https://github.com/RecoverDev/Study-Git.git
```


## Сохранение данных

Чтобы что-то сохранить, это нужно сначала создать. Создадим файл **README.MD** _(этот файл)_ и попробуем сохранить его на удаленном хранилище.

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
Вообще то команду **git push** используют без ключей. Ключи **-u origin master** используют только при первом сохранении, чтобы синхронизировать ветки на локальном и удаленном хранилище.


## Тонкости работы команды git log

Команда **git log**  выводит на экран информацию о каждом коммите в текущем хранилище и выглядит это так
```bash
commit 3922244375f058da12e8d56eda6796a40d334c72 (origin/master)
Author: Dev <recover@list.ru>
Date:   Wed Jan 3 21:33:37 2024 +0300

    Изменен формат списка в файле readme.md

commit a5a982ac2df5e12195ef5ea5f4539739fc811a82 # хеш коммита
Author: Dev <recover@list.ru> # автор коммита
Date:   Wed Jan 3 21:29:35 2024 +0300 # время коммита

    Добавление файла readme.md # описание коммита

```
Если коммитов много, то становится неудобно просматривать такое количество информации.

Для просмотра сокращенной информации существует команда **git log --oneline**. эта команда выводит информацию о коммите в одну строку

```bash
3922244 (origin/master) Изменен формат списка в файле readme.md
a5a982a Добавление файла readme.md

```

В строке указан только часть хеша и описание.

__И вот теперь вы можете читать эти стоки, подключившись к моему удаленному хранилищу, которое я создал специально для вас!!!__



