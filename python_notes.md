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
base = swlite3.connect('my_database.db')
cur = base.cursor()
```
### Создание таблицы.
```sql
base.execute( 'CREATE TABLE IF NOT EXISTS {} (login, password)' .format('data_members') ).base.commit()
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

# Telegram-bot (aiogram)
## Регистрация бота. Получение токена
Находим контакт BotFather, нажимаем запустить. И отправляем команду ``/newbot``.
Далее вводим имя нашего заведения. И имя нашего бота. :warning: Обязательно в конце нужно добавить слово 
bot.
Если все хорошо мы получим **ключ** который **нельзя разглашать**

Так как бот подключен к группе, то чтобы у него были права администратора группы нужно:
- отправить команду ``/setprivacy``
- отправить имя нашего боты
- выбираем Disable

Теперь создаем группу для нашего заведения.
Добавляем хотя бы одного участника + наш телеграмм-бот.

## Установка aiogram. Оформление проекта.
Создаем папку для кода нашего бота.
Через терминал, создаем виртуальную среду python
```
python -m venv venv
```

Далее виртуальную среду следует запустить. Для Linux
```
source /venv/bin/activate
```

Устанавливаем aiogram
```
(venv)	pip install aiogram
```

Создаем python-файл для кода.

## Эхо бот телеграмм.

Импорт классов.
```python
from aiogram import Bot, types # types нужен для того чтобы мы могли писать аннотации типов к функциям.
from aiogram.dispatcher import Dispatcher # Этот класс помогает улавливать события в чате.
from aiogram.utils import executor # запускает бота.

import os # нужен для чтения токена из переменной среды окружения.
```

Запуск бота. Бота можно запустить в двух режимах:
- LongPolling
- Webhook

**LongPolling**
Хорошо подходит для этапа тестирования бота. В этом режиме бот телеграмм постоянно опрашивает сервер на наличие сообщений для него. :warning: Есть проблемы с стабильностью работы на linux системах.

**Webhook**
Бот деплоится на каком-нибудь сервере. У него появляется API и URL-адрес. Отличается от LongPolling, тем, что не бот опрашивает сервер, а сервер присылает сообщения когда они появляются.


## Пример программы телеграм бота.
```python
from aiogram import Bot, types	# types нужен для того чтобы мы могли писать аннотации типов к функциям.
from aiogram.dispatcher import Dispatcher	# Этот класс помогает улавливать события в чате.
from aiogram.utils import executor	# запускает бота.

import os	# нужен для чтения токена из переменной среды окружения.
import json
import string


bot = Bot(token = "ID_TOKEN") # Выдает BotFather.
dp = Dispatcher(bot)

'''
@brief Выводит информацию при подключении бота к серверу.
@warning имя функции необходимо передать в executor.start_polling().
'''
async def on_startup(_):
	print("status bot: online")

''' Клиентская часть. '''


@dp.message_handler(commands = ["start", "help"])
async def command_start(message : types.Message):
	try:
		await bot.send_message(message.from_user.id, "Приятного аппетита")
		await message.delete()
	except:
		await message.reply("Для общения с ботом, отправьте ему сообщение:\nhttps://t.me/ipizza_hub_bot")

@dp.message_handler(commands=["Режим_работы"])
async def pizza_open_command(message : types.Message):
	await bot.send_message(message.from_user.id, "Вт-Чт с 9:00 - 20:00, Пт-Сб с 10:00 до 23:00")

@dp.message_handler(commands=["Расположение"])		
async def command_place_command(message : types.Message):
	await bot.send_message(message.from_user.id, "ул. Колбасная д.15")
 
@dp.message_handler()
async def echo_send(message: types.Message):
	#await message.answer(message.text)
	#await message.reply(message.text)
	#await bot.send_message(message.from_user.id, message.text)

	if {i.lower().translate(str.maketrans("", "", string.punctuation)) for i in message.text.split(" ")}.intersection(set(json.load(open("cenz.json")))) != set():
		await message.reply("Маты запрещены")
		await message.delete()


executor.start_polling(dp, skip_updates = True, on_startup = on_startup) # когда True, бот будет пропускать сообщения которые поступали когда он был не онлайн.
```




