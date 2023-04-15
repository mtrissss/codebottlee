# codebottlee
hi
from email import message
from gc import callbacks
from operator import call
from tracemalloc import start
from turtle import done
import telebot
from telebot import types
from telebot.types import InlineKeyboardButton, InlineKeyboardMarkup
bot = telebot.TeleBot("6016693612:AAEyse4-dSHWdV03FLIxVkku97TqIgKsTDw")

@bot.message_handler(commands=['start'])
def send_welcome(message):
    bot.reply_to(message, "dưới đây là danh sách")
    markup = types.ReplyKeyboardMarkup(row_width=2)
    itembtn1 = types.KeyboardButton('Red')
    itembtn2 = types.KeyboardButton('Blue')
    markup.add(itembtn1, itembtn2)
    bot.reply_to(message, "Chọn một màu sắc:", reply_markup=markup)
@bot.callback_query_handler(func=lambda call: call.data == 'done')
def handle_callback(call):
    
    chat_id = call.message.chat.id
    
    bot.send_message(chat_id=chat_id, text="Done")
@bot.message_handler(func=lambda message: True)
def echo_all(message):
    if message.text == 'Red':
        bot.reply_to(message, "Bạn đã chọn màu đỏ.")
    elif message.text == 'Blue':
        bot.reply_to(message, "Bạn đã chọn màu xanh.")
        
@bot.message_handler(content_types=['photo'])
def handle_photo(message):
    
    file_info = bot.get_file(message.photo[-1].file_id)
    downloaded_file = bot.download_file(file_info.file_path)
    with open("image.jpg", 'wb') as new_file:
        new_file.write(downloaded_file)
    
    group_id = "-943261582"
    with open("image.jpg", 'rb') as photo:
        
        
        button = InlineKeyboardButton("DONE", callback_data="done")
        markup = InlineKeyboardMarkup().add(button)
        bot.send_photo(chat_id=group_id, photo=photo, reply_markup=markup)
    if button.callback_data=="done":
         bot.reply_to(message,"done")

bot.polling()    

