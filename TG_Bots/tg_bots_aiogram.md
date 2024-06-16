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
