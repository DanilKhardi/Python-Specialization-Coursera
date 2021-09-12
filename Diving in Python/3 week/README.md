# ***Неделя 3***
## Задание по программированию: Реализация простого класса для чтения из файла
___
Первое задание на этой неделе — не сложное, для разогрева. Ваша задача: написать python-модуль **solution.py**, внутрь которого необходимо поместить код класса **FileReader**. Конструктор этого класса принимает один параметр: путь до файла на диске. В классе **FileReader** должен быть реализован метод **read**, возвращающий строку - содержимое файла, путь к которому был указан при создании экземпляра класса. Python модуль должен быть написан таким образом, чтобы импорт класса **FileReader** из него не вызвал ошибок.

При написании реализации метода **read**, вам нужно учитывать случай, когда при инициализации был передан путь к несуществующему файлу. Требуется обработать возникающее при этом исключение **FileNotFoundError** и вернуть из метода **read** пустую строку.

Пример работы:
``` python
>>> from solution import FileReader
>>> reader = FileReader('not_exist_file.txt')
>>> text = reader.read()
>>> text
''
>>> with open('some_file.txt', 'w') as file:
...     file.write('some text')
...
9
>>> reader = FileReader('some_file.txt')
>>> text = reader.read()
>>> text
'some text'
>>> type(reader)
<class 'solution.FileReader'>
```
___
## Задание по программированию: Классы и наследование
___
Как правило задачи про классы не носят вычислительный характер. Обычно нужно написать классы, которые отвечают определенным интерфейсам. Насколько удобны эти интерфейсы и как сильно связаны классы между собой, определит легкость их использования в будущих программах.

Предположим есть данные о разных автомобилях и спецтехнике. Данные представлены в виде таблицы с характеристиками. Вся техника разделена на три вида: спецтехника, легковые и грузовые автомобили. Обратите внимание на то, что некоторые характеристики присущи только определенному виду техники. Например, у легковых автомобилей есть характеристика «кол-во пассажирских мест», а у грузовых автомобилей — габариты кузова: «длина», «ширина» и «высота».

<table border = '0'  width="50%" cellpadding = '5'>
<tr>
<th>Тип (car_type)</th>
<th>Марка (brand)</th>
<th>Кол-во мест(passenger_seats_count)</th> 
<th>Фото (photo_file_name)</th>
<th>Кузов ДхШхВ, м (body_whl)</th>
<th>Грузоподъемность, Тонн (carrying)</th>
<th>Дополнительно (extra)</th>
</tr>
<tr>
<th>car</th>
<th>Nissan xTrail</th>
<th>4</th> 
<th>f1.jpeg</th>
<th></th>
<th>2.5</th>
<th></th>
</tr>
<tr>
<th>truck</th>
<th>Man</th>
<th></th> 
<th>f2.jpeg</th>
<th>8x3x2.5</th>
<th>20</th>
<th></th>
</tr>
<tr>
<th>car</th>
<th>Mazda 6</th>
<th>4</th> 
<th>f3.jpeg</th>
<th></th>
<th>2.5</th>
<th></th>
</tr>
<tr>
<th>spec_machine</th>
<th>Hitachi</th>
<th></th> 
<th>f4.jpeg</th>
<th></th>
<th>1.2</th>
<th>Любая техника для уборки снега</th>
</tr>
</table>

Вам необходимо создать свою иерархию классов для данных, которые описаны в таблице. Классы должны называться **CarBase** (базовый класс для всех типов машин), **Car** (легковые автомобили), **Truck** (грузовые автомобили) и **SpecMachine** (спецтехника). Все объекты имеют обязательные атрибуты:

- **car_type**, значение типа объекта и может принимать одно из значений: «car», «truck», «spec_machine».

- **photo_file_name**, имя файла с изображением машины, допустимы названия файлов изображений с расширением из списка: «.jpg», «.jpeg», «.png», «.gif»

- **brand**, марка производителя машины

- **carrying**, грузоподъемность

В базовом классе **CarBase** нужно реализовать метод **get_photo_file_ext** для получения расширения файла изображения. Расширение файла можно получить при помощи os.path.splitext.

Для грузового автомобиля необходимо в конструкторе класса определить атрибуты: **body_length, body_width, body_height,** отвечающие соответственно за габариты кузова — длину, ширину и высоту. Габариты передаются в параметре **body_whl** (строка, в которой размеры разделены латинской буквой «x»). Обратите внимание на то, что характеристики кузова должны быть вещественными числами и характеристики кузова могут быть не валидными (например, пустая строка). В таком случае всем атрибутам, отвечающим за габариты кузова, присваивается значение равное нулю.

Также для класса грузового автомобиля необходимо реализовать метод **get_body_volume**, возвращающий объем кузова.

В классе **Car** должен быть определен атрибут passenger_seats_count (количество пассажирских мест), а в классе SpecMachine — extra (дополнительное описание машины).

Полная информация о атрибутах классов приведена в таблице ниже, где 1 - означает, что атрибут обязателен для объекта, 0 - атрибут должен отсутствовать.<br>


<table border='0' width="100%" cellpadding = '5'>
<tr>
<th></th>
<th>Car</th>
<th>Truck</th>
<th>SpecMachine</th>
</tr>
<tr>
<th>car_type</th>
<th>1</th>
<th>1</th>
<th>1</th>
</tr>
<tr>
<th>photo_file_name</th>
<th>1</th>
<th>1</th>
<th>1</th>
</tr>
<tr>
<th>brand</th>
<th>1</th>
<th>1</th>
<th>1</th>
</tr>
<tr>
<th>carrying</th>
<th>1</th>
<th>1</th>
<th>1</th>
</tr>
<tr>
<th>passenger_seats_count</th>
<th>1</th>
<th>0</th>
<th>0</th>
</tr>
<tr>
<th>body_width</th>
<th>0</th>
<th>1</th>
<th>0</th>
</tr>
<tr>
<th>body_height</th>
<th>0</th>
<th>1</th>
<th>0</th>
</tr>
<tr>
<th>body_length</th>
<th>0</th>
<th>1</th>
<th>0</th>
</tr>
<tr>
<th>extra</th>
<th>0</th>
<th>0</th>
<th>1</th>
</tr><br>
</table>


Обратите внимание, что у каждого объекта из иерархии должен быть свой набор атрибутов и методов. Например, у класса легковой автомобиль не должно быть метода **get_body_volume** в отличие от класса грузового автомобиля. Имена атрибутов и методов должны совпадать с теми, что описаны выше.

Далее вам необходимо реализовать функцию **get_car_list**, на вход которой подается имя файла в формате **csv**. Файл содержит данные, аналогичные строкам из таблицы. Вам необходимо прочитать этот файл построчно при помощи модуля стандартной библиотеки **csv**. Затем проанализировать строки на валидность и создать список объектов с автомобилями и специальной техникой. Функция должна возвращать список объектов.

Вы можете использовать для отладки работы функции **get_car_list** csv-файл test.csv.

Первая строка в исходном файле — это заголовок **csv**, который содержит имена колонок. Нужно пропустить первую строку из исходного файла. Обратите внимание на то, что в некоторых строках исходного файла , данные могут быть заполнены некорректно, например, отсутствовать обязательные поля или иметь не валидное значение. В таком случае нужно проигнорировать подобные строки и не создавать объекты. Строки с пустым или не валидным значением для **body_whl** игнорироваться не должны.  Вы можете использовать стандартный механизм обработки исключений в процессе чтения, валидации и создания объектов из строк csv-файла. Проверьте работу вашего кода с входным файлом, прежде чем загружать задание для оценки.

Пример кода, демонстрирующего чтение csv файла:
``` python
import csv

with open(csv_filename) as csv_fd:
    reader = csv.reader(csv_fd, delimiter=';')
    next(reader)  # пропускаем заголовок
    for row in reader:
        print(row)
```