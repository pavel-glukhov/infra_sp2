# YaMDb API

### Описание
Проект **YaMDb** собирает отзывы пользователей на произведения. Произведения делятся на категории: «Книги», «Фильмы», «Музыка».

### Алгоритм регистрации пользователей:
1. Пользователь отправляет запрос с параметром *email* на */auth/email/*.
2. **YaMDB** отправляет письмо с кодом подтверждения (*confirmation_code*) на адрес *email*.
3. Пользователь отправляет запрос с параметрами *email* и *confirmation_code* на */auth/token/*, в ответе на запрос ему приходит *token* (JWT-токен).
4. При желании пользователь отправляет PATCH-запрос на */users/me/* и заполняет поля в своём профайле (описание полей — в документации).

Проект написан на Django с использованием DRF. В качестве базы данных используется PostgreSQL. 

### Установка проекта
Проект собран в Docker 20.10.06 и содержит три образа:
- web - образ проекта
- postgres - образ базы данных PostgreSQL v 12.04
- nginx - образ web сервера nginx 

#### Запуск проекта:
- Первоначально необходимо установить Docker.
  Подробную документацию смотрите на официальном сайте: <https://docs.docker.com/engine/install/ubuntu/>

- Скачивание образа из dockerhub:
  **docker pull glukosoft/yamdb:0.1**

- Для запуска контейнера выполните команду:
  **docker-compose up**

- Процесс миграции можно посмотреть выполнив команду:
  **docker-compose logs -f --tail 100 web**

#### Первоначальная настройка Django:
- После запуска контейнера, необходимо произвести первоначальные настройки Django и создать суперюзера.
Для этого выполните команду: **docker-compose exec web sh setup_server.sh**

#### Загрузка тестовой фикстуры в базу:
- Для тестирования сервиса можно воспользоваться подготовленным дампом, для загрузки его выполните команду:
**docker-compose exec web python manage.py loaddata fixtures.json**

После установки пройдите по адресу: <http://127.0.0.1/admin/> и убедитесь, что админ панель доступна.

Подробная документация по работе с API сервиса доступна по адресу <http://127.0.0.1/redoc/>
