# Модель данных системы "Умный дом"

## Сущности и их атрибуты

### User (Пользователь)
- **id** (UUID) - первичный ключ
- **username** (String) - имя пользователя
- **email** (String) - электронная почта
- **password_hash** (String) - хеш пароля
- **created_at** (Timestamp) - дата создания
- **updated_at** (Timestamp) - дата обновления

### House (Дом)
- **id** (UUID) - первичный ключ
- **name** (String) - название дома
- **address** (String) - адрес
- **user_id** (UUID) - внешний ключ к User
- **created_at** (Timestamp) - дата создания
- **updated_at** (Timestamp) - дата обновления

### DeviceType (Тип устройства)
- **id** (UUID) - первичный ключ
- **name** (String) - название типа
- **description** (String) - описание
- **capabilities** (JSON) - возможности устройства

### Device (Устройство)
- **id** (UUID) - первичный ключ
- **name** (String) - название устройства
- **serial_number** (String) - серийный номер
- **type_id** (UUID) - внешний ключ к DeviceType
- **house_id** (UUID) - внешний ключ к House
- **status** (String) - текущее состояние
- **created_at** (Timestamp) - дата создания
- **updated_at** (Timestamp) - дата обновления

### Module (Модуль)
- **id** (UUID) - первичный ключ
- **name** (String) - название модуля
- **device_id** (UUID) - внешний ключ к Device
- **type** (String) - тип модуля
- **status** (String) - текущее состояние
- **created_at** (Timestamp) - дата создания
- **updated_at** (Timestamp) - дата обновления

### TelemetryData (Телеметрия)
- **id** (UUID) - первичный ключ
- **device_id** (UUID) - внешний ключ к Device
- **module_id** (UUID) - внешний ключ к Module
- **value** (Double) - значение
- **timestamp** (Timestamp) - время измерения
- **metadata** (JSON) - дополнительные данные

## Связи между сущностями

1. **User - House** (один-ко-многим)
   - Один пользователь может владеть несколькими домами
   - Каждый дом принадлежит одному пользователю

2. **House - Device** (один-ко-многим)
   - Один дом может содержать несколько устройств
   - Каждое устройство принадлежит одному дому

3. **DeviceType - Device** (один-ко-многим)
   - Один тип устройства может быть присвоен нескольким устройствам
   - Каждое устройство имеет один тип

4. **Device - Module** (один-ко-многим)
   - Одно устройство может содержать несколько модулей
   - Каждый модуль принадлежит одному устройству

5. **Device - TelemetryData** (один-ко-многим)
   - Одно устройство может генерировать множество записей телеметрии
   - Каждая запись телеметрии связана с одним устройством

6. **Module - TelemetryData** (один-ко-многим)
   - Один модуль может генерировать множество записей телеметрии
   - Каждая запись телеметрии связана с одним модулем

## Особенности модели

1. **Идентификаторы**
   - Использование UUID для всех первичных ключей
   - Автоматическая генерация идентификаторов

2. **Аудит**
   - Поля created_at и updated_at для отслеживания изменений
   - Автоматическое обновление временных меток

3. **Гибкость**
   - JSON поля для хранения неструктурированных данных
   - Расширяемая структура для новых типов устройств

4. **Нормализация**
   - Минимизация дублирования данных
   - Четкое разделение ответственности между сущностями

## ER-диаграмма

[ER-диаграмма](er-diagram.puml) визуализирует структуру данных и связи между сущностями. 