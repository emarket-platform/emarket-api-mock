# emarket-api-mock

Git repo: https://github.com/emarket-platform/emarket-api-mock

Git Issues: https://github.com/emarket-platform/emarket-api-mock/issues

Documentation: https://github.com/emarket-platform/emarket-docs

Swagger UI: http://localhost:8091


# Для локального запуска:
```bash
  docker network create emarket-network
  docker compose up -d --build
```

# Restart/stop docker container
```bash
docker restart <container_name_or_id>
docker stop <container_name_or_id>
```

# Как проверить что wiremock успешно запустился в docker
```bash
docker compose ps
curl http://localhost:8090/__admin/health
```
# Проверить логи контейнера
```bash
docker compose logs --tail=100 emarket-api-mock
```

# Следить за логами в реальном времени:
```bash
docker compose logs -f emarket-api-mock
```

# Получить список всех endpoints
```bash
curl -s http://localhost:8090/__admin/mappings
```

# Вывести только HTTP method + URL
С использованием jq:
```bash
curl -s http://localhost:8090/__admin/mappings \
  | jq -r '.mappings[] | "\(.request.method) \(.request.url // .request.urlPattern)"'
```

# Получить информацию о конкретном endpoint
```bash
curl -s http://localhost:8090/__admin/mappings \
  | jq '.mappings[] | select(.request.url == "/api/v1/web/users/me")'
```

# Swagger UI
Открой следующие адреса в Chrome.
```bash
http://localhost:8091
```
Здесь должна отображаться OpenAPI документация с возможностью выполнять запросы через Try it out.

# Все зарегистрированные WireMock endpoints
```bash
http://localhost:8090/__admin/mappings
```
# WireMock Admin API
```bash
http://localhost:8090/__admin/health
```

# Если Swagger UI не открывается
Проверь:
```bash
docker compose ps
```

Должны работать оба контейнера:
```text
emarket-api-mock    Up (healthy)
swagger-ui          Up
```