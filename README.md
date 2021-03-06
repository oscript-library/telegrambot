# telegrambot
Библиотека для взаимодействия с [Telegram Bot API](https://core.telegram.org/bots/api)

### Установка telegrambot
----
Первый способ - установить через opm:

```
$ opm install telegrambot
```

Второй способ - скачать нужный релиз (https://github.com/pallid/telegrambot/releasess) и установить вручную:

```
$ opm install -f "path/to/file.ospx"
```

где path/to/file.ospx - путь к файлу реализа пакета для onescript.

### Пример

[Пример](https://github.com/pallid/example-telegrambot) реализации telegram bot на oscript-web

[Демо бот](https://t.me/oswebbot?start)

Библиотека к вашему проекту подключается с помощью директивы #Использовать telegrambot. После этого в области видимости скрипта будет доступен класс ТелеграмБот и модуль ТелеграмАПИ:

```

Бот = Новый ТелеграмБот;
Бот.УстановитьТокенАвторизации("ТВОЙ_ТОКЕН_БОТА");
Бот.УстановитьВебхук("ТВОЙ_АДРЕС_ДЛЯ_ХУКОВ");

///

ОбъектЗапрос = ПарсерJSON.ПрочитатьJSON(ТекстТелаЗапроса);
      
Если ОбъектЗапрос["message"] <> Неопределено Тогда
            
    ТекстСообщения = ОбъектЗапрос["message"]["text"];
    ПолучательИД = ОбъектЗапрос["message"]["chat"]["id"];

    Если ТекстСообщения = "/start" тогда
                  
        ТекстСообщения = "Привет, в низу меню для навигации";       
        Сообщение = ТелеграмАПИ.НовоеСообщение(ПолучательИД, ТекстСообщения);
        ТелеграмАПИ.ДобавитьКлавиатуру(Сообщение, ГлавноеМеню());
        Результат = Бот.Отправить(Сообщение); 
            
    КонецЕсли;      
            
КонецЕсли; 

///

Ответ = Новый РезультатДействияСодержимое();
Ответ.КодСостояния = 200;
Ответ.ТипСодержимого = "application/json;charset=UTF-8";
Ответ.Содержимое = Результат["ok"];
      
Возврат Ответ;

```

```
Функция ГлавноеМеню()

	КомандаКаталог = ТелеграмАПИ.НоваяКнопка("Каталог");
	КомандаКорзина = ТелеграмАПИ.НоваяКнопка("Корзина");

	ПервыйРяд = ТелеграмАПИ.ПолучитьРядКнопок(КомандаКаталог, КомандаКорзина);

	КомандаНашТелегон 	 = ТелеграмАПИ.НоваяКнопка("Наш телефон");
	КомандаЛичныйКабинет = ТелеграмАПИ.НоваяКнопка("Личный кабинет");

	ВторойРяд = ТелеграмАПИ.ПолучитьРядКнопок(КомандаНашТелегон, КомандаЛичныйКабинет);

	МассивРядов = ТелеграмАПИ.ПолучитьМассивРядовДляКлавиатуры(ПервыйРяд, ВторойРяд);

	Возврат ТелеграмАПИ.ПолучитьКлавиатуру(МассивРядов);

КонецФункции


```

На текущий момент реализовано получение данных только через WebHooks.

Разработка ведется в репозитории [oscript-library/telegrambot](https://github.com/oscript-library/telegrambot) по Git Flow.
Ждем ваши PR и Issues.



### Контрибьюторы:

| <img alt="Andreas Mehlsen" src="https://avatars1.githubusercontent.com/u/4147815?s=460&u=cec28755c1e7e9e2231e8bf34c30bede16e9759d&v=4" width="100"> | <img alt="Карим Шакиров" src="https://avatars2.githubusercontent.com/u/6420066?s=460&u=ba32acf3de4719bcb51819b0f494d9a05f8ca725&v=4" width="100">|
|:--------------------------------------------------:|:--------------------------------------------------:|
| [Василий Попов](https://github.com/pallid) | [Карим Шакиров](https://github.com/k2589) |
|Создатель                                               | Мейнтейнер                                                 |