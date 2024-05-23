# Используем базовый образ Python
FROM python:3.8-slim

# Устанавливаем переменную окружения, чтобы Python не сохранял файлы .pyc
ENV PYTHONDONTWRITEBYTECODE 1

# Устанавливаем переменную окружения, чтобы Python выводил сообщения буферизированно
ENV PYTHONUNBUFFERED 1

# Создаем рабочую директорию
WORKDIR /app

# Копируем файл требований в рабочую директорию
COPY requirements.txt /app/

# Устанавливаем зависимости из файла требований
RUN pip install --no-cache-dir -r requirements.txt

# Копируем весь проект в рабочую директорию
COPY . /app/

# Запускаем сервер Django
CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]
