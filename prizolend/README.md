Please, do not remove this README.
http://www.youtube.com/watch?v=3o0XSedkPTY
<<<<<<< HEAD
GLONASS is a video games presentation system.
GLOW means "Game Likes One Word"
=======

Подготовка и запуск функциональных тестов на CI сервере
=======

### Требования
Установлены:
-mysql

Следующие модули Python:
- virtualenv
- pip

### Развертывание

## Получение файлов и виртуальная среда окружения

Клонируем репозиторий
```bash
git clone git@github.com:LevelUp2/people.git
```

Переходим в папку с проектом:
```bash
cd people
```

Создаем виртуальную среду окружения:
```bash
virtualenv .env
```

Активируем созданное окружение
```bash
source .env/bin/activate
```

Создаем Makefile путем копирования шаблона:
```bash
cp Makefile.example Makefile
```

Устанавливаем зависимости:
```bash
make requirements
```
Возможно MySQL-python не захочет установится с первого раза,
нужно будет запустить:
```bash
easy_install -U distribute
```
и снова 
```bash
make requirements
```

## Подготовка базы данных

Создаем базу данных:
```bash
mysql -h localhost -P 3306  -uroot -p -e 'create database glonass default character set utf8 collate utf8_general_ci';
```
Создаём отдельного пользователя СУБД, которому выдаём соответствующие привилегии
```bash
mysql -h localhost -P 3306 -uroot -p -e "GRANT ALL PRIVILEGES ON \`glonass%\`.* TO 'glow'@'localhost' IDENTIFIED BY 'evol';
```
Создаем файл локальных настроек glonass/settings/local.py путем копирования шаблона:
```bash
cp glonass/settings/local.py.template glonass/settings/local.py
```
Далее, выполняем следующие команды:
```bash
make createdb
```
Загружаем хранимые процедуры, которые будут использоваться для изменения баланса игрока:
```bash
python manage.py dbshell < common/sql/stored_procedures.sql
```

## Запуск тестов

Перейти в папку с проектом:
```bash
cd people
```
Обновить файлы проекта:
```bash
git pull origin master
```
Активировать виртуальное окружение:
```bash
source .env/bin/activate
```
Обновить python-зависимости:
```bash
make requirements
```
Вычистить проект от скомпилированных скриптов и кешей:
```bash
make clean
```
Обновить БД:
```bash
python manage.py syncdb --no-initial-data --noinput -v 0
python manage.py migrate --noinput -v 0
```
Прогнать тесты
```bash
make cleanfunctests
```
people
======

Simple, but useful SSO and user matching for Django.
>>>>>>> a8a4e43ff994fb609797dc3adfd767305f613973
