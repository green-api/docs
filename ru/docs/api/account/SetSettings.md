# SetSettings

Метод предназначен для установки настроек аккаунта. 

> При вызове данного метода аккаунт перезапускается.

## Запрос {#request}

Для установки настроек аккаунта требуется выполнить запрос по адресу:
```
POST https://api.green-api.com/waInstance{{idInstance}}/SetSettings/{{apiTokenInstance}}
```

Для получения параметров запроса `idInstance` и `apiTokenInstance` обратитесь к разделу [Перед началом работы](../../before-start.md#parameters).

### Параметры запроса {#request-parameters}

Допускается указывать параметры выборочно. Хотя бы один параметр должен быть указан.

Параметр | Тип | Обязательный | Описание
----- | ----- | ----- | -----
`countryInstance` | **string** | Нет | Код страны аккаунта по стандарту [ISO 3166-2](https://ru.wikipedia.org/wiki/ISO_3166-2)
`webhookUrl` | **string** | Нет | URL для отправки уведомлений. Если требуется отключить получение уведомлений, то укажите пустую строку
`delaySendMessagesMilliseconds` | **integer** | Нет | [Интервал отправки сообщений](../send-messages-delay.md) в миллисекундах. Минимальное значение 500 мсек
`markIncomingMessagesReaded` | **string** | Нет | Отмечать входящие сообщения прочитанными. Возможные значения: `yes`, `no`
`proxyInstance` | **string** | Нет | Прокси для аккаунта в формате `{ip}:{port}:{login}:{password}`, если вы хотите что бы аккаунт работал на вашем прокси, по умолчанию используются системные прокси
`outgoingWebhook` | **string** | Нет |Получать уведомления о статусах отправки/доставки/прочтении исходящих сообщений, возможные значения: `yes`, `no`
`outgoingMessageWebhook` | **string** | Нет |Получать уведомления о сообщениях, отправленных с телефона, возможные значения: `yes`, `no`
`stateWebhook` | **string** | Нет |Получать уведомления об изменении состояния авторизации аккаунта, возможные значения: `yes`, `no`
`incomingWebhook` | **string** | Нет |Получать уведомления о входящих сообщениях и файлах, возможные значения: `yes`, `no`
`deviceWebhook` | **string** | Нет |Получать уведомления об устройстве (телефоне) и уровне заряда батареи, возможные значения: `yes`, `no`

### Пример тела запроса {#request-example-body}

```json
{
    "countryInstance": "ru",
    "webhookUrl": "https://mysite.com/webhook/green-api/",
    "delaySendMessagesMilliseconds": 1000,
    "markIncomingMessagesReaded": "no",
    "proxyInstance": "100.100.100.100:3535:login:password",
    "outgoingWebhook": "yes",
    "outgoingMessageWebhook": "yes",
    "stateWebhook": "yes",
    "incomingWebhook": "yes",
    "deviceWebhook": "no"
}
```

## Ответ {#response}

### Поля ответа {#response-parameters}

Поле | Тип |  Описание
----- | ----- | ----- 
`saveSettings` | **boolean** | Флаг, что настройки сохранены

### Пример тела ответа {#response-example-body}

```json
{
    "saveSettings": true
}
```

### Ошибки SetSettings {#errors}

Перечень общих для всех методов ошибок смотрите в разделе [Стандартные ошибки](../common-errors.md)

## Пример кода на Python  {#request-example-python}

```python
import requests

url = "https://api.green-api.com/waInstance{{idInstance}}/setSettings/{{apiTokenInstance}}"

payload = "{\r\n\t\"countryInstance\": \"ru\",\r\n\t\"webhookUrl\": \"https://mysite.ru\",\r\n\t\"delaySendMessagesMilliseconds\": 1000,\r\n\t\"markIncomingMessagesReaded\": \"no\",\r\n\t\"proxyInstance\": \"123.456.78.910:39898:qGKqCo:Jb26Xz\",\r\n\t\"outgoingWebhook\": \"yes\",\r\n\t\"stateWebhook\": \"yes\",\r\n\t\"incomingWebhook\": \"yes\",\r\n\t\"deviceWebhook\": \"no\"\r\n}"
headers = {
  'Content-Type': 'application/json'
}

response = requests.request("POST", url, headers=headers, data = payload)

print(response.text.encode('utf8'))
```