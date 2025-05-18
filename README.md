# VK-Parser

Парсер постов и комментариев из групп VK с функцией определения вопросов

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Автоматический парсер для сбора постов и комментариев из групп ВКонтакте с сохранением результатов в CSV. Также поддерживает автоматическое определение вопросов в постах с помощью модели машинного обучения.

---

## 📋 Особенности

- Получение постов через API VK (`wall.get`).
- Сбор комментариев к каждому посту (`wall.getComments`).
- **Определение вопросов** в постах с помощью модели машинного обучения.
- Сохранение данных в CSV (посты, вопросы и комментарии отдельно).
- Обработка ошибок API (повторные запросы, ограничение лимитов).
- Поддержка нескольких групп за один запуск.

---

## ⚙️ Требования

- Python 3.11+
- Библиотеки:
  - `requests`
  - `pandas`
  - `python-dotenv`
  - `tqdm`
  - `transformers` - для определения вопросов

---

## 🛠️ Установка

1. **Клонируйте репозиторий:**

   ```bash
   git clone https://github.com/s7ar11/VK-Parser.git
   cd VK-Parser

    Установите зависимости:
    pip install -r requirements.txt
   ```

Создайте файл .env:

    VK_TOKEN=ваш_токен_vk_api
    VK_GROUPS=group1,group2,group3

Как получить VK API :
(https://smmplanner.com/blog/gaid-po-api-vk-kak-podkliuchit-i-ispolzovat/#02)

---

## 🚀 Использование

    Настройте список групп в main.py:

    GROUPS = [
        "pro_che",
        "secrets_of_teachers",
        # Добавьте свои группы (screen_name из URL)
    ]

Запустите парсер:

    python main.py

Результаты будут сохранены в папке output:

        posts.csv — все посты.

        questions.csv — посты, классифицированные как вопросы.

        comments.csv — комментарии к вопросам.

---

## 🤖 Определение вопросов

Парсер использует модель машинного обучения для автоматического определения вопросов в постах. По умолчанию используется модель `Vldln/bert-question-detector-russian` с пороговым значением 0.8.

Для изменения порогового значения вы можете использовать метод `set_threshold`:

```python
from predictor import QuestionPredictor

# Создание предиктора
predictor = QuestionPredictor()

# Изменение порогового значения
predictor.set_threshold(0.7)

# Проверка текста
is_question = predictor.predict("Это вопрос?")
```

---

## 📝 Лицензия

Этот проект распространяется под лицензией MIT.

Автор: s7ar11
