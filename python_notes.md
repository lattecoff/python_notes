# Списки


## Пустой список.
```python
my_list = list()
```


## Вложенный список.
```python
my_list = ["Bob", 40.0, ["dev, "mgr"]]
```

## Список последовательности чисел.
```python
my_list = list(range(-4, 4))
```

## Повторение.
```python
my_list * 3
```

## Методы увеличения.
```python
# Добавляет указанный элемент в конец списка.
my_list.append(4)

# Добавляет указанные элементы в конец списка
my_list.extend([5, 6, 7])

# Добавляет указанный элемент в список на указанную позицию.
my_list.insert(i, x)
```

## Методы поиска.
```python
# Ищет указанное значение в последовательности.
#Метод возвращает первую из позиций (индексов), на которой в последовательности обнаруживается искомое значение.
my_list.index(x)

# Возвращает количество вхождений указанного значения в список.
my_list.count(x)
```

## Методы: сортировки, обращения, копирования, очистки.
```python
my_list.sort()
my_list.reverse()
my_list.copy()
my_list.clear()
```

## Методы, операторы: уменьшения.
```python
my_list.pop(i)
my_list.remove(x)

del my_list(i)
del my_list[i:j]
my_list[i:j] = []
```

## Присвоение по индексу, присвоение по срезу:
```python
my_list[i]
my_list[i:j] = [5, 6, 7]

```

## Списковое включение.
```python
my_list = [x *2 for x in range(5))]
list(map(ord, "spam"))

# ord - возвращает числовое значение полученного символа.
# map - применяет указанную функцию к элементу последовательности/последовательностей.
```

# Словари


## Создание пустого словаря.
```python
my_dict = dict() # или
my_dict = {}
```

## Создание словаря с инициализацией.

```python
users = {1: "Tom", 2: "Bob", 3: "Bill"} 
elements = {"Au": "Золото", "Fe": "Железо", "H": "Водород", "O": "Кислород"}
```

## Конвертация списка в словарь.
```python
users_list = [ ["+111123455", "Tom"],
			   [+384767557", "Bob"],
			   ["+958758767", "Alice"]
]

users_dict = dict(users_list)
print(users_dict)	# users_list = {"+111123455": "Tom", +384767557": "Bob", "+958758767": "Alice"}


users = dict("+11111111": "Tom",
			 "+33333333": "Bob",
			 "+55555555": "Alice"
)
```

## Получить значение по ключу.
```python
print(users["+11111111"])	# Tom.

print(users.get("+11111111"))
```
```python
print(users.get("+11111111", default))
```
:warning: Если такого ключа не окажется то будет возвращено значение ``default``

## Присвоить значение по ключу.
```python
users["+33333333"] = "Bob Smith"
print(users["+33333333"])	#Bob Smith.
```

## При попытке присвоить значения к несуществующему ключу, он будет создан.
```python
users["+44444444"] = "Sam"
```

## При попытке получить значения от несуществующего ключа.
```python
users["+44444444"]	# KeyError
```

## Удаление элемента по ключу.
```python
users = dict("+11111111": "Tom",
			 "+33333333": "Bob",
			 "+55555555": "Alice"
)

del users["+55555555"]
```

```python
users.pop("+55555555") 
```
Если не найден, сгенерирует исключение ``KeyError``

```python
users.pop("+55555555", default) 
```
Если не найден, вернет ``default``

## Копирование словаря.
```python
users = dict("+11111111": "Tom",
			 "+33333333": "Bob",
			 "+55555555": "Alice"
)

users2 = users.copy()
```

## Обьединение словаря.
```python
users = dict("+11111111": "Tom",
			 "+33333333": "Bob",
			 "+55555555": "Alice"
)

users2 = dict("+22222222", "Sam",
			 "+66666666", "Kate",
)

users.update(users2)

print(users)	# "+11111111": "Tom", "+33333333": "Bob", "+55555555": "Alice", "+22222222": "Sam", "+66666666": "Kate".

```

# Базы Данных (SQLite)

## Создание таблиц. SQL запросы. Insert, Select, Update and Delete.

### Создание базы и подготовка к внесению изменений.
```sql
base = swlite3.connect(new.db)
cur = base.connect()
```
### Создание таблицы.
```sql
base.execute('CREATE TABLE OF NOT EXISTS {}(login, password)'.format('data '))
base.commit()
```

### Создание SQL-запроса c защитой от SQL-иньекций.
```sql
base.execute('INSERT INTO data VALUES(?, ?)', ('jonny123', '123456789')
base.commit()
```

### Создание SQL-запроса из файла с данными.
```sql
from my_data_file import my_list 
cur.executemany('INSERT INTO data VALUES(?, ?)', my_list)
base.commit()
```
