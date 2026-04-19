# Work-bot-tiktok
   git clone https://github.com/StounhandJ/shorts_forward
   cd shorts_forward
   cp .env.example .env
   nano .env
      TG_BOT_TOKEN=ваш_токен_бота
   DOMAIN=ваш_домен_для_прокси
     make up
import os
import logging
from telegram import Update, InlineQueryResultVideo, InputTextMessageContent
from telegram.ext import Updater, InlineQueryHandler, CommandHandler, CallbackContext

# Настройка логирования
logging.basicConfig(format='%(asctime)s - %(name)s - %(levelname)s - %(message)s', level=logging.INFO)
logger = logging.getLogger(__name__)

# Функция для обработки inline-запросов
def inline_query(update: Update, context: CallbackContext) -> None:
    query = update.inline_query.query
    if not query:
        return

    # Здесь должна быть логика для получения видео из TikTok по ссылке
    # Для примера возвращаем заглушку
    results = [
        InlineQueryResultVideo(
            id='1',
            video_url='https://example.com/video.mp4',
            mime_type='video/mp4',
            thumb_url='https://example.com/thumb.jpg',
            title='Пример видео',
            description='Это пример видео из TikTok',
            input_message_content=InputTextMessageContent('Вот ваше видео!')
        )
    ]
    update.inline_query.answer(results)

# Команда /start
def start(update: Update, context: CallbackContext) -> None:
    update.message.reply_text('Привет! Отправь мне ссылку на видео из TikTok, и я пришлю его тебе.')

# Основная функция запуска бота
def main() -> None:
    token = os.getenv('TG_BOT_TOKEN')
    if not token:
        logger.error("Не указан токен бота!")
        return

    updater = Updater(token)
    dp = updater.dispatcher

    dp.add_handler(CommandHandler("start", start))
    dp.add_handler(InlineQueryHandler(inline_query))

    updater.start_polling()
    updater.idle()

if __name__ == '__main__':
    main()
    make up
