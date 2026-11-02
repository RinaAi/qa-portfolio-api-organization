# Тестирование REST API: создание организации (Postman)

![Status](https://img.shields.io/badge/Status-Completed-success?style=flat-square)
![Type](https://img.shields.io/badge/Type-REST_API-blue?style=flat-square)
![Tool](https://img.shields.io/badge/Tool-Postman-orange?style=flat-square)
![Requests](https://img.shields.io/badge/Requests-59-lightgrey?style=flat-square)

Коллекция Postman для тестирования POST-метода создания организации по документации API.

Хост, токены и учётные данные заказчика удалены. Для запуска нужно задать переменные коллекции: `baseUrl`, `bearer_token_0pt6`, а для запроса получения токена также `username` и `password`.

## Покрытие

59 запросов в 9 папках: авторизация, позитивные сценарии, валидация `name`, `inn`, `ogrn`, `address`, `phone`, `head` и тела запроса.

Подробное описание сценариев, техник и ограничений: [Подход к тестированию](./docs/test-approach.md).

## Результаты

1. **Невалидный токен:** API возвращает 500 Internal Server Error вместо ожидаемого 401 Unauthorized.
2. **ОГРН при ИНН из 12 цифр:** API принимает ОГРН из 14 цифр. Документация противоречива: таблица валидации требует 13 цифр, а алгоритм описывает проверку только для ИНН из 10 цифр. Требование нуждается в уточнении.

## Файлы

- [Коллекция Postman](./collection.json)
- [Подход к тестированию](./docs/test-approach.md)

Сохранённые примеры ответов удалены из экспорта, чтобы исключить чувствительные данные.
