# **Electronic retail**

Это проект, написанный на Python 3.11, с использованием следующих библиотек и фреймворков:
- Django 5.0.1
- Django REST framework 3.14.0
- drf-spectacular 0.27.1
- PostgreSQL 16.2

Модель сети по продаже электроники представлена в виде веб-приложения с API интерфейсом и админ-панелью.

Сеть состоит из иерархической структуры с 3 уровнями:
* Завод;
* Розничная сеть;
* Индивидуальный предприниматель. 

Каждое звено сети ссылается только на одного поставщика оборудования (не обязательно предыдущего по иерархии). Уровень иерархии определяется не названием звена, а отношением к остальным элементам сети: завод всегда находится на 0 уровне, розничная сеть, относящаяся напрямую к заводу, на 1 уровне.


## **Установка**
### Для установки проекта Electronic sales, следуйте инструкциям ниже:

**<p>1. Сделайте Fork этого репозитория. Репозиторий появится в ваших личных репозиториях на GitHub.</p>**

**1.1 Склонируйте форкнутый репозиторий локально: `git clone`**

**<p>2. Перейдите в папку с проектом.</p>**

**<p>3. Создайте и активируйте виртуальное окружение:</p>**

`python -m venv venv`

`source venv/bin/activate`

**<p>4. Установите зависимости проекта:</p>**

`pip install -r requirements.txt`

**<p>5. Создайте файл .env в корневой папке проекта и заполните данные для настройки проекта, используя пример файла .env.sample:</p>**

```ini
/.env/

# Django setting
DJANGO_SECRET_KEY=your django secret key

# PostgreSQL connection
DB_ENGINE=django.db.backends.engine
POSTGRES_DB=database name
POSTGRES_USER=postgresql username
POSTGRES_PASSWORD=postgresql password
POSTGRES_HOST=your host
POSTGRES_PORT=your port
```

**<p>6. Примените миграции:</p>**

`python manage.py migrate`

**<p>7. Установите русский язык:</p>**

`django-admin compilemessages`

**<p>8. Запустите сервер:</p>**

`python manage.py runserver`


Теперь вы можете работать с backend-частью локально для отладки. Документация доступна по адресу http://127.0.0.1:8000/api/docs/, а схема данных в формате .yaml — по адресу http://127.0.0.1:8000/api/schema/.

### Либо с помощью Docker
**<p>1. Создайте файл .env.docker в корневой папке проекта и заполните данные для настройки проекта из файла .env.sample.docker:</p>**
```ini
/.env.docker/

# Django setting
DJANGO_SECRET_KEY=your django secret key

# PostgreSQL connection
DB_ENGINE=django.db.backends.engine
POSTGRES_DB=database name
POSTGRES_USER=postgresql username
POSTGRES_PASSWORD=postgresql password
POSTGRES_HOST=container name (default "db")
POSTGRES_PORT=your port
```

**<p>2. Запустите проект:</p>**

`docker compose build`

`docker compose up`




## **Использование**
#### Проект поддерживает регистрацию новых пользователей через админ-панель Django или API. 
Также есть команда для создания суперпользователя `python manage.py csu` с данными из .env файла

#### Для тестирования вы можете заполнить базу данных данными из фикстур командой `python manage.py fixturedata`
или создать свои данные через админ-панель или API. 

Для поля network модели NetworkLink используются следующие варианты:
* plant
* retail_network
* individual_entrepreneur


Через админ-панель Django можно управлять задолженностями перед поставщиками или перейти на страницу поставщика. (обновление задолженности через API запрещено).

Использовать API могут только активные пользователи (флаг is_active).