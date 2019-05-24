﻿# Парсер конфигурации 1С

## Информация

Скрипты данной библиотеки используются для разбора конфигурации 1С выгруженной в исходные файлы.

## Установка

1. Склонировать репозиторий
2. Выполнить скрипт `installlocalhost.bat`

## Использование

1. Подключаем библиотеку `#Использовать bsl-parser`
2. Создаем парсер `Парсер = ПарсерBSL.ПарсерКонфигурации(КаталогИсходников);`
3. Читаем данные `Парсер.ПрочитатьСтруктуруКонфигурации();`
4. Обрабатываем результат `ОписаниеКонфигурации = Парсер.ОписаниеКонфигурации();`

Пример, выводит имена всех объектов конфигурации и имена всех методов

```bsl
    Парсер = ПарсерBSL.ПарсерКонфигурации(КаталогИсходников); // Создаем парсер
    Парсер.ПрочитатьСтруктуруКонфигурации(); // Читаем структуру
    ОписаниеКонфигурации = Парсер.ОписаниеКонфигурации();

    Для Каждого Объект Из ОписаниеКонфигурации.ОбъектыКонфигурации Цикл // Обрабатываем объекты

        // Обработаем объекты
        Сообщить(Объект.Тип + "." + Объект.Наименование);

    КонецЕсли;

    Парсер.НайтиМодулиКонфигурации(); // Находим все модули объектов

    Для Каждого Модуль Из ОписаниеКонфигурации.ОбъектыКонфигурации Цикл

        Для Каждого Блок Из Модуль.БлокиМодуля Цикл

            Если Блок.ТипБлока = ТипБлоковМодуля.ЗаголовокПроцедуры ИЛИ Блок.ТипБлока = ТипБлоковМодуля.ЗаголовокФункции Тогда

                Сообщить(ОписаниеБлока.ИмяМетода);

            КонецЕсли;

        КонецЦикла;

    КонецЦикла;
```