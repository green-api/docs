# DeviceInfo

Получены данные об устройстве и уровне заряда батареи, на котором запущено приложение Whatsapp

## webhook {#webhook}

### Поля webhook {#webhook-parameters}

Параметр | Тип | Описание
----- | ----- | -----
`typeWebhook` | **string** | Тип webhook уведомления. Возможные варианты stateInstanceChanged, outgoingMessageStatus, incomingMessageReceived, deviceInfo. В данном случае поле равняется deviceInfo.
`instanceData` | **object** | Данные об аккаунте
`timestamp` | **integer** | Время наступления события в UNIX формате
`deviceData` | **object** | Данные об устройстве

Поля объекта instanceData

Параметр | Тип | Описание
----- | ----- | -----
`idInstance` | **integer** | Идентификатор аккаунта
`wid` | **string** | Идентификатор аккаунта в формате Whatsapp
`typeInstance` | **string** | Тип мессенджера для аккаунта

Поля объекта deviceData

Параметр | Тип | Описание
----- | ----- | -----
`platform` | **string** | Операционная система устройства на котором запущено приложение Whatsapp
`deviceManufacturer` | **string** | Производитель устройства
`deviceModel` | **string** | Модель устройства
`osVersion` | **string** | Версия операционной системы
`waVersion` | **string** | Версия приложения Whatsapp
`battery` | **integer** | Уровень заряда батареи

### Пример тела webhook {#webhook-example-body}

```json
{
    "typeWebhook": "deviceInfo",
    "instanceData": {
        "idInstance": 1,
        "wid": "79001234567@c.us",
        "typeInstance": "whatsapp"
    },
    "timestamp": 1586700802,
    "deviceData": {
        "platform": "iphone",
        "deviceManufacturer": "Apple",
        "deviceModel": "iPhone 11",
        "osVersion": "13.4.1",
        "waVersion": "2.20.42",
        "battery": 90
    }
}
```