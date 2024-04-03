import telebot
import json
import datetime
import time
import keyboard
import pyfiglet

bot = telebot.TeleBot('6543001293:AAGOgCXLLk8gLabDyJPUKRfWThCkixl_clc')


@bot.message_handler(commands=['start'])
def g(message):

    months_translation = {
        "January": "Січень",
        "February": "Лютий",
        "March": "Березень",
        "April": "Квітень",
        "May": "Травень",
        "June": "Червень",
        "July": "Липень",
        "August": "Серпень",
        "September": "Вересень",
        "October": "Жовтень",
        "November": "Листопад",
        "December": "Грудень"
    }

    days = {
        "Monday": "Понеділок",
        "Tuesday": "Вівторок",
        "Wednesday": "Середа",
        "Thursday": "Четвер",
        "Friday": "П'ятниця",
        "Saturday": "Субота",
        "Sunday": "Неділя",
    }

    

    while True:
        d = datetime.datetime.now()
        our = d.strftime("%H")
        minets = d.strftime("%M")
        if our == "08" and minets == "00":
            time.sleep(0.5)
            d = datetime.datetime.now()
            
            month1 = d.strftime("%B")
            year = d.strftime("%Y")
            day1 = d.strftime("%A")
            our = d.strftime("%H")
            minets = d.strftime("%M")
            second = d.strftime("%S")
            day2 = d.strftime("%d")

            day2 = int(day2)



            with open(f"{month1}.json", 'r', encoding='utf-8') as f:
                April = json.load(f)

            
            month = months_translation.get(month1)
            day = days.get(day1)
            z = day2 % 10
            holiday1 = April.get(f"{z}")

            if holiday1 == None:
                holiday1 = "Немає"

            bot.send_message(message.chat.id, f"Зараз \nРік:{year}\nМісяць:{month}\nДень:{day}\nСв'ято:{holiday1}")
            
            #bot.send_message(message.chat.id, f"{our}:{minets}:{second}")
            time.sleep(64)




bot.polling(none_stop=True)
