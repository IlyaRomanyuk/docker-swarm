1) psql -h localhost -d test -U admin - войти внутрь бд внутри контейнера

Профили
1) docker compose config - посмотреть как переменные пробрасываются в docker-compose из .env
2) docker compose --profile backend-migrations up -d - Настройка --profile позволит запустить только тот сервис, который имеет профиль backend-migrations в docker-compose.yml записывается в виде ключ-значение: profiles: ["backend-migrations"]
Второй вариант через проброс переменной COMPOSE_PROFILES=backend-migrations docker compose up -d

Комбинирование/Shared docker-compose-манифестов
1) Необходимо для улучшения читабельности общего docker-compose.yml. А также для удобной подстановки dev-переменных и prod-переменных(чтобы не было нужы вести 2 отдельный манифеста для prod и dev среды)
api
    extends:
        file: docker-compose.api.yml (В этом файле указаные необходимые клюси для запуска)
        service: api (найти сервис с именем api в этом файле docker-compose.api.yml)
    depends_on:
    - rmq