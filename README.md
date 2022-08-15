![workflow](https://github.com/rodandr13/yamdb_final/actions/workflows/yamdb_workflow.yml/badge.svg)

# YaMDb API
Проект YaMDb собирает отзывы пользователей на произведения. Через API администратор может создавать произведения для отзывов, категории и жанры произведений. Пользователям предоставляется возможность писать отзывы на произведения и комментировать их.

## Как запустить проект:

Клонировать репозиторий и перейти в него в командной строке:
```
git clone https://github.com/rodandr13/infra_sp2.git

cd infra_sp2
```
Развернуть приложение:
```
docker-compose up -d --build
```
Выполнить миграции
```
docker-compose exec web python manage.py migrate
```
Заполнить базу данными
```
docker-compose exec web python manage.py loaddata fixtures.json
```
Загрузить статику
```
docker-compose exec web python manage.py collectstatic --no-input
```

## Пользовательские роли
```
Anonymous
Может просматривать описания произведений, читать отзывы и комментарии.

User
Может читать всё, как и Аноним, может публиковать отзывы и ставить оценки произведениям (фильмам/книгам/песенкам), может комментировать отзывы; может редактировать и удалять свои отзывы и комментарии, редактировать свои оценки произведений. Эта роль присваивается по умолчанию каждому новому пользователю.

Moderator
Те же права, что и у Аутентифицированного пользователя, плюс право удалять и редактировать любые отзывы и комментарии.

Admin
Полные права на управление всем контентом проекта. Может создавать и удалять произведения, категории и жанры. Может назначать роли пользователям

Суперюзер Django
Обладет правами администратора
```


### Регистрация нового пользователя
```
1. Отправить POST-запрос с параметрами email и username на эндпоинт /api/v1/auth/signup/.
2. YaMDB отправляет письмо с кодом подтверждения (confirmation_code) на указанный адрес email.
3. Отправить POST-запрос с параметрами username и confirmation_code на эндпоинт /api/v1/auth/token/, в ответе на запрос приходит token (JWT-токен).
```

### Создание категории
```POST /api/v1/categories/```
```json
{
    "name": "string",
    "slug": "string"
}
```

### Добавление произведения
```GET /api/v1/titles/```
```json
{
  "name": "string",
  "year": 0,
  "description": "string",
  "genre": [
    "string"
  ],
  "category": "string"
}
```

### Добавление нового отзыва
```GET /api/v1/titles/```
```json
{
  "text": "string",
  "score": 1
}
```
## Используемые технологии
- Python
- Django Rest Framework
- Joser
- Simple JWT
- Docker
- PostgreSQL
## Автор
Родителев Андрей