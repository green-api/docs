# LocationMessage

Получено входящее сообщение с геолокацией

## webhook {#webhook}

### Поля webhook {#webhook-parameters}

Параметр | Тип | Описание
----- | ----- | -----
`typeWebhook` | **string** | Тип webhook уведомления. Возможные варианты stateInstanceChanged, outgoingMessageStatus, incomingMessageReceived, deviceInfo. В данном случае поле равняется incomingMessageReceived.
`instanceData` | **object** | Данные об аккаунте
`timestamp` | **integer** | Время наступления события в UNIX формате
`idMessage` | **string** | Идентификатор входящего сообщения
`senderData` | **object** | Данные об отправителе сообщения/файла
`messageData` | **object** | Данные о принятом сообщении/файле

Поля объекта instanceData

Параметр | Тип | Описание
----- | ----- | -----
`idInstance` | **integer** | Идентификатор аккаунта
`wid` | **string** | Идентификатор аккаунта в формате Whatsapp
`typeInstance` | **string** | Тип мессенджера для аккаунта

Поля объекта senderData

Параметр | Тип | Описание
----- | ----- | -----
`chatId` | **string** | [Идентификатор чата](/api/chat-id), в котором получено сообщение или файл
`sender` | **string** | Идентификатор отправителя сообщения или файла в формате [Идентификатора чата](/api/chat-id)
`senderName` | **string** | Имя отправителя

Поля объекта messageData

Параметр | Тип | Описание
----- | ----- | -----
`typeMessage` | **string** | Тип принятого сообщения, возможные значения: textMessage, imageMessage, videoMessage, documentMessage, audioMessage, locationMessage, contactMessage, extendedTextMessage. В данном случае поле принимает значение locationMessage
`locationMessageData` | **object** | Объект данных о принятой геолокации, когда typeMessage = locationMessage

Поля объекта locationMessageData

Параметр | Тип | Описание
----- | ----- | -----
`latitude` | **double** | Широта локации
`longitude` | **double** | Долгота локации
`jpegThumbnail` | **string** | Превью изображения в base64 кодировке

### Пример тела webhook {#webhook-example-body}

```json
{
    "typeWebhook": "incomingMessageReceived",
    "instanceData": {
        "idInstance": 1,
        "wid": "79001234567@c.us",
        "typeInstance": "whatsapp"
    },
    "timestamp": 1588091580,
    "idMessage": "F7AEC1B7086ECDC7E6E45923F5EDB825",
    "senderData": {
        "chatId": "79001234568@c.us",
        "sender": "79001234568@c.us",
        "senderName": "МТС Мой"
    },
    "messageData": {
        "typeMessage": "locationMessage",
        "locationMessageData": {
            "latitude": 12.345678910111213,
            "longitude": 14.151617181920212,
            "jpegThumbnail": "/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAYEBQYFBAYGBQYHBwYIChAKCgkJChQODwwQFx="
        }
    }
}
```