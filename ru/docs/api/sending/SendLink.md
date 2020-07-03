# SendLink

Метод предназначен для отправки сообщения со ссылкой, по которой будут добавлены превью изображения, заголовок и описание.
Картинка, заголовок и описание получаются из Open Graph разметки страницы, на которую указывает ссылка.
Сообщение будет добавлено в очередь на отправку.

## Запрос {#request}

### Параметры запроса {#request-parameters}

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`chatId` | **string** | Да | [Идентификатор чата](/api/chat-id)
`urlLink` | **string** | Да | Адрес ссылки

### Пример тела запроса {#request-example-body}

Отправка сообщения в личный чат:
```json
{
    "chatId": "79001234567@c.us",
    "urlLink": "https://my.site.com"
}
```

Отправка сообщения в групповой чат:
```json
{
    "chatId": "79001234567-1581234048@g.us",
    "urlLink": "https://my.site.com"
}
```

## Ответ {#response}

### Поля ответа {#response-parameters}

Поле | Тип |  Описание
----- | ----- | -----
`idMessage ` | **string** | Идентификатор отправленного сообщения 

### Пример тела ответа {#response-example-body}

```json
{
    "idMessage": "3EB0C767D097B7C7C030"
}
```

### Ошибки SendLink {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](/api/common-errors)

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/waInstance{{idInstance}}/sendLink/{{apiTokenInstance}}"

payload = "{\r\n\t\"chatId\": \"79001234567@c.us\",\r\n\t\"urlLink\": \"https://www.youtube.com/watch?v=00000000000\"\r\n}\r\n"
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```