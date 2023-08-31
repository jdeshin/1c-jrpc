# 1С-JRPC
Библиотека для работы с JSON-RPC из 1С:Предприятие
## Описание
Библиотека предназначена для организации взаимодействия между прикладными решениями на платформе 1С:Предприятие, а также между прикладными решениями и сторонними серверами JRPC в соответствии со 
спецификацией [JSON-RPC 2.0](https://www.jsonrpc.org/specification).
Фактически, библиотека дает возможность из одного прикладного решения вызывать процедуры и функции общих модулей другого прикладного решения или функции стороннего JRPC сервера.

Библиотека состоит из нескольких подсистем:

**БиблиотекаСерверJRPC** - реализация сервера JRPC. Точка входа (endpoint) реализована с использованием механизма http-сервисов.

**БиблиотекаКлиентJRPC** - реализация клиента JRPC.

**ТестБиблиотекаJRPC** - пример использования библиотеки для взаимодействия между прикладными решениями.

## Использование
### Сервер JRPC

```1C
Функция ОбработчикВызоваHTTPСервиса(Запрос)
	
  // Добавляем модули и методы, вызов которых разрешен
  РазрешенныеМодули = Новый Массив;
  // Все процедуры/функции общего модуля ТестСерверJRPC
	РазрешенныеМодули.Добавить("ТестСерверJRPC.");
  // Все процедуры/функции общего модуля ТестСерверJRPC, имена которых начинаются на ФункцияJRPC 
	РазрешенныеМодули.Добавить("ТестСерверJRPC.ФункцияJRPC");
	// Выполняем вызов, возвращаем результат
	Возврат СерверJRPC.ОбработатьЗапрос(Запрос, РазрешенныеМодули);
	
КонецФункции
```

### Клиент JRPC

