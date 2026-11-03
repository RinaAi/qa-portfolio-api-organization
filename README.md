# Тестирование REST API: создание организации (Postman)

![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)
![Type](https://img.shields.io/badge/Type-REST_API-blue?style=flat-square)
![Tool](https://img.shields.io/badge/Tool-Postman-orange?style=flat-square)
![Requests](https://img.shields.io/badge/Requests-59-lightgrey?style=flat-square)
![Tests](https://img.shields.io/badge/Tests-59_requests-green?style=flat-square)

Коллекция Postman для тестирования POST-метода создания организации по документации API.

В **каждом из 59 запросов** есть Test Scripts (assertions): время ответа, статус-код, JSON, наличие ошибки/токена/id — в зависимости от типа сценария.

Хост, токены и учётные данные заказчика удалены. Для запуска задайте переменные коллекции: `baseUrl`, `bearer_token_0pt6`, а для запроса получения токена также `username` и `password`.

## Покрытие

59 запросов в 9 папках: авторизация, позитивные сценарии, валидация `name`, `inn`, `ogrn`, `address`, `phone`, `head` и тела запроса.

| Тип сценария | Assertions |
|---|---|
| Авторизация (токен) | 200, наличие `access_token` |
| Без токена | 401 |
| Невалидный токен | ожидаем 401 (фактически 500 — дефект) |
| Позитивные | 200/201, JSON, id организации |
| Валидация / негатив | 4xx, JSON с текстом ошибки |
| Все запросы | `responseTime < 5000ms` |

Подробнее: [Подход к тестированию](./docs/test-approach.md).

## Запуск через Newman

```bash
npm install -g newman newman-reporter-htmlextra

# environment.json — файл с baseUrl, bearer_token_0pt6 (не коммитить секреты)
newman run collection.json \
  -e environment.json \
  --reporters cli,htmlextra \
  --reporter-htmlextra-export reports/newman-report.html
```

Отчёт: `reports/newman-report.html` (папка `reports/` в `.gitignore`).

Пример environment (шаблон):

```json
{
  "values": [
    { "key": "baseUrl", "value": "https://your-api.example" },
    { "key": "bearer_token_0pt6", "value": "your-token" },
    { "key": "username", "value": "" },
    { "key": "password", "value": "" }
  ]
}
```

## Результаты

1. **Невалидный токен:** API возвращает 500 Internal Server Error вместо ожидаемого 401 Unauthorized.
2. **ОГРН при ИНН из 12 цифр:** API принимает ОГРН из 14 цифр. Документация противоречива: таблица валидации требует 13 цифр, а алгоритм описывает проверку только для ИНН из 10 цифр. Требование нуждается в уточнении.

## Файлы

- [Коллекция Postman](./collection.json) — 59 запросов **с Test Scripts**
- [Подход к тестированию](./docs/test-approach.md)
- [Шаблон environment](./environment.template.json)

Сохранённые примеры ответов удалены из экспорта, чтобы исключить чувствительные данные.
