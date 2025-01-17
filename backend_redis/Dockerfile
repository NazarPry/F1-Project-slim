# Використання Python 3.11 як базового образу
FROM python:3.11-slim

# Вимкнення кешування .pyc-файлів і буферизації Python
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Встановлення робочої директорії
WORKDIR /app

# Оновлення системи та встановлення необхідних пакетів
RUN apt-get update && apt-get install -y --no-install-recommends \
    build-essential \
    python3-distutils \
    && rm -rf /var/lib/apt/lists/*

# Створення віртуального середовища
RUN python -m venv /opt/venv

# Додавання шляху до віртуального середовища в PATH
ENV PATH="/opt/venv/bin:$PATH"

# Копіювання файлу requirements.txt та встановлення залежностей
COPY requirements.txt /app/
RUN pip install --no-cache-dir --upgrade pip && pip install -r requirements.txt

# Копіювання всіх файлів додатку в контейнер
COPY . /app/

# Вказання команди для запуску Django-сервера
CMD ["python", "manage.py", "runserver", "0.0.0.0:8001"]

EXPOSE 8001