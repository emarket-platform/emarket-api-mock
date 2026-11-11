# emarket-api-mock

Git repo: https://github.com/emarket-platform/emarket-api-mock

Git Issues: https://github.com/emarket-platform/emarket-api-mock/issues

Documentation: https://github.com/emarket-platform/emarket-docs


# Для локального запуска:
```bash
  docker network create emarket-network
  docker compose up -d --build
```

# Проверка:
```bash
 curl http://localhost:8090/__admin/health
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
