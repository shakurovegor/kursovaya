# Курсовая работа на тему:
# "Проектирование и разработка АИС библиотека"
## Платформа разработки: 1С Предприятие 8
<p align="center">
  <img src="https://github.com/shakurovegor/kursovaya/assets/170186126/fe51b96d-1bae-430d-aa2f-34c0d70c5ff5" alt="drawing" style="width:280px;"/>
</p>

## ER-diagram
![library-erd](https://github.com/shakurovegor/kursovaya/assets/170186126/914d90fc-74eb-4ce7-b383-92ad0e1759e8)
## Внешний вид конфигурации
![1cv8ct_Uu6zI2nWQv](https://github.com/shakurovegor/kursovaya/assets/170186126/226ffbbc-bcbd-40eb-bc7c-fda72dac7673)
## Примеры кода
```bsl
Процедура Печать (ТабДок, Ссылка) Экспорт
  //{{_КОНСТРУКТОРПЕЧАТИ (Печать)
  Макет = Документы.ФондКниг.ПолучитьМакет("Печать");
  Запрос Новый Запрос;
  Запрос.Текст =
  "ВЫБРАТЬ
  |  ФондКниг.Дата,   
  |  Фондкниг.Номер,
  |  ФондКниг.ТабличнаяЧасть1. (
  |    НомерСтроки,
  |    Книга,
  |    Количество
  |  )
  |ИЗ
  |  Документ.ФондКниг КАК ФОНДКниг 
  |ГДЕ
  |  ФондКниг.Ссылка В (&Ссылка)";
  Запрос.Параметры.Вставить("Ссылка", Ссылка);
  Выборка = Запрос.Выполнить().Выбрать();
  ОбластьЗаголовок = Макет.ПолучитьОбласть("Заголовок");
  Шапка = Макет.ПолучитьОбласть("Шапка");
  ОбластьТабличнаяЧасть1Шапка = Макет.Получитьобласть("ТабличнаяЧасть1Шапка");
  ОбластьТабличнаяЧасть1 = Макет.ПолучитьОбласть("ТабличнаяЧасть1");
  ТабДок.Очистить();
  ВставлятьРазделительСтраниц = Ложь;
  Пока Выборка.Следующий() Цикл
      Если Вставлять Разделитель Страниц Тогда
          ТабДок.ВывестиГоризонтальныйРазделительСтраниц();
      КонецЕсли;
      ТабДок.Вывести(ОбластьЗаголовок);
      Шапка.Параметры.Заполнить(Выборка);
      ТабДок.Вывести(Шапка, Выборка.Уровень());
      Табдок.Вывести(ОбластьТабличнаяЧасть1Шапка);
      ВыборкаТабличнаяЧасть1 = Выборка.ТабличнаяЧасть.Выбрать();
      Пока ВыборкаТабличнаяЧасть1.Следующий() Цикл
            ОбластьТабличнаяЧасть1.Параметры.Заполнить(ВыборкаТабличнаяЧасть1);
            ТабДок.Вывести(ОбластьТабличнаяЧасть, ВыборкаТабличнаяЧасть1.Уровень());
        КонецЦикла;
        Вставлять РазделительСтраниц Истина;
    КонецЦикла;
Конец Процедуры                                                        
```
