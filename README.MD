#  Инструкция по использованию модуля чтения CSV файлов
## 1 Задать конфигурацию в файле z20.ini
```INI
[Integration]
Type=CSVREADER
DirectWriteToZabotaDatabase=0

[Database]
Path=<PATH TO DIRECTORY WITH CSV FILES>
```

## 2 Задать карту CSV файлов
CSV файлы не являются типизированными файлами, невозможно автоматически определить тип содержимого файлов. Поэтому необходимо вручную присвоить столбцам типы, которые будут распознаны программой.
Карта CSV файлов представляет из себя ini файл с названием map.ini, который должен располагаться в директории с CSV файлами, указанной в z20.ini выше
Доступны следующие типы для распознавания:



- BIGINT - длинное число. Диапазон [-9223372036854775808; 9223372036854775807] 
- INT - число. Диапазон [-2147483648; 2147483647]
- STRING - строка
- BOOL - логический 0 или 1 (True/False)
- DATETIME - дата и время в формате yyyy-MM-dd HH:mm:ss
- FLOAT - число с плавающей точкой с низкой точностью
- DOUBLE - число с плавающей точкой с высокой точностю
- DECIMAL - десятичное дробное число
- UNIQUEIDENTIFIER - GUID Уникальный идентификтатор (Пример: 1b8fbc15-eeaf-4f78-bd1f-24d9bb55143f)

Вы должны описать каждый CSV файл, который будет считан. Объявление типов в map.ini должно представлять  конструкцию вида:

```INI
[<CSVFILE1>]
ColumnName1=<TYPE>
ColumnName2=<TYPE>
ColumnName3=<TYPE>
......
ColumnNameN=<TYPE>

[<CSVFILE2>]
ColumnName1=<TYPE>
ColumnName2=<TYPE>
ColumnName3=<TYPE>
......
ColumnNameN=<TYPE>
```

где ColumnNameX - имя столбца в CSV файле, TYPE - тип, описанный выше

Пример реального map.ini файла:
```INI
[doctors]
doctor_id=INT
code=STRING
surname=STRING
firstname=STRING
middlename=STRING

[patients]
practice_id=INT
patient_id=INT
card=STRING
surname=STRING
firstname=STRING
midname=STRING
dob=DATETIME
gender=STRING
email=STRING
cellphone=STRING
balance=INT
amount=INT
completed=INT
undone=INT
exclude=INT
```
