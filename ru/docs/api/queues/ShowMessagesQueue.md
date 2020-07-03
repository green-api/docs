# ShowMessagesQueue

Метод предназначен для получения списка сообщений, находящихся в очереди на отправку

## Запрос {#request}

### Параметры запроса {#request-parameters}

Отсутствуют

## Ответ {#response}

### Поля ответа {#response-parameters}

Массив объектов с полями:

Поле | Тип |  Описание
----- | ----- | ----- 
`typeMessage` | **string** | Тип сообщения, возможные значения:
| | textMessage - текстовое сообщение
| | imageMessage - сообщение с изображением
| | videoMessage - видео сообщение
| | documentMessage - сообщение с файлом документа
| | audioMessage - аудио сообщение
| | locationMessage - сообщение геолокации
| | contactMessage - сообщение с контактом
| | extendedTextMessage - сообщение со ссылкой и превью
`chatId` | **string** | [Идентификатор чата](/api/chat-id) в который сообщение будет отправлено
`message` | **string** |  текст сообщения, если typeMessage = textMessage/locationMessage/contactMessage/extendedTextMessage
`fileName` | **string** | Имя отправляемого файла, если typeMessage = imageMessage/videoMessage/documentMessage/audioMessage

### Пример тела ответа {#response-example-body}

```json
[
    {
        "typeMessage": "textMessage",
        "chatId": "79001234567@c.us",
        "message": "Hello man"
    },
    {
        "typeMessage": "imageMessage",
        "chatId": "79001234567@c.us",
        "fileName": "image.jpg"
    }
]
```

### Ошибки ShowMessagesQueue {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](/api/common-errors)

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/waInstance{{idInstance}}/showMessagesQueue/{{apiTokenInstance}}"

payload = {}
headers= {}

response = requests.request("GET", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```