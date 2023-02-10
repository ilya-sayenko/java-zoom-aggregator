# Задание: zoom отчеты

В [Zoom](http://zoom.us) в меню Отчеты -> Отчеты об использовании можно составлять отчеты об участниках созвонов. 
Есть необходимость составлять сводную отчетность по этим отчетам за несколько созвонов. 

### Формат данных
[Пример отчета](zoom_report_example.csv)

```csv
Идентификатор конференции,Тема,Время начала,Время завершения,Электронная почта пользователя,Продолжительность (минуты),Участники,
12345678,Название вебинара,Дата-время старта вебинара в формате 01.01.2023 00:00:00,Дата-время конца вебинара в формате 01.01.2023 00:00:00,email организатора,длительность вебинара в минутах,количество участников за исключением организатора,

Имя (настоящее имя),Электронная почта пользователя,Общая длительность (минут),Гость
Имя Организатора,email организатора,Время присутствия организатора,Нет
Имя Гостя 1,email гостя 1,Время присутсвия гостя в минутах,Да
Имя Гостя 2,email гостя 2,Время присутсвия гостя в минутах,Да
...
```

Таких отчетов может быть много. Поэтому в программу аргументом `--data /path/to/data/folder/` будет передаваться путь до папки с такими отчетами. Также для простоты обработки будет передаваться
файл со всеми пользователями в следующем формате

```csv
Имя Участника 1,email участника 1
Имя Участника 2,email участника 2
...
```

Файл с участниками передается в программу аргументом `--participants /path/to/participants.csv`. Всех участников, которые присутствуют в zoom отчетах, но 
нет в файле с участниками, можно игнорировать.

### Желаемый результат

Нужен сводный отчет по всем вебинарам их папки с отчетами и всеми участниками из файла с участниками в следующем формате:
```csv
               ,                 ,id вебинара 1 – Дата вебинара1                                            ,id вебинара1 – Дата вебинара 2                                            ,...
Имя участника 1,email участника 1,время присутствия на вебинаре 1                                           ,время присутствия на вебинаре 2                                           ,...,количество посещенных вебинаров – средний процент времени присутствия на вебинарах
Имя участника 2,email участника 2,время присутствия на вебинаре 1                                           ,время присутствия на вебинаре 2                                           ,...,количество посещенных вебинаров – средний процент времени присутствия на вебинарах
...
               ,                 ,количество участников на вебинаре 1 – процент от общего кол-во участников ,количество участников на вебинаре 2 – процент от общего кол-во участников ,
```

Пробелы и табуляция показаны для наглядности, можно не делать строго такими. Главное не забыть про 2 запятые на первой строчке в начале, чтобы csv табличка получилась правильной. Писать результат 
нужно в stdout.

### !Важно!
Участники могут иногда регистрироваться под разными именами с одним email. В таком случае нужно ориентироваться по email из файла со всеми участниками.
Если в файле с zoom отчетами встречаются дубликаты по id вебинара, то писать в консоль ошибку и завершать программу.