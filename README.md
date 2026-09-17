import os
import random
import telebot
import time
from datetime import datetime
from pytz import timezone
from telebot.types import InlineKeyboardMarkup, InlineKeyboardButton

api_key = '8808899339:AAGmI-Wum1E4co1DX0kb1QCkMdTYNLRajGA'
chat_id = '-1003921834186'

bot = telebot.TeleBot(token=api_key)

diretorio_script = os.path.dirname(os.path.abspath(__file__))
diretorio_imagens = os.path.join(diretorio_script, 'imagens')

arquivos = os.listdir(diretorio_imagens)

def enviar_imagem_aleatoria():
    imagem_escolhida = random.choice(arquivos)

    tz = timezone('Angola/Luanda')

    with open(os.path.join(diretorio_imagens, imagem_escolhida), 'rb') as imagem:
        keyboard = InlineKeyboardMarkup()
        url_button_1 = InlineKeyboardButton(text="JOGAR SINAL AGORA💎", url=url_link)
        keyboard.add(url_button_1)

        legenda = (
            "✅ PADRÃO CONFIRMADO ✅\n\n"
            "Teste Mines💎\n\n"
            "🎰 Minas: 3\n"
            "📊 % de acertos: 100.00%\n"
            "⏱️ Válido até às: (datetime.fromtimestamp(time.time() + 240, tz).strftime('%H:%M'))\n"
            "🎯 Nº de tentativas: 3"
        )

        bot.send_photo(chat_id, imagem, caption=legenda, parse_mode="Markdown", reply_markup=keyboard)

    time.sleep(240)
