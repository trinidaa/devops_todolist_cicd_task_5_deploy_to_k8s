# Stage 1: Build Stage
ARG PYTHON_VERSION=3.8
FROM python:${PYTHON_VERSION}-slim as builder

WORKDIR /app
COPY requirements.txt .
RUN pip install --user --no-cache-dir -r requirements.txt
COPY . .

# Stage 2: Run Stage
FROM python:${PYTHON_VERSION}-slim as run

WORKDIR /app
ENV PYTHONUNBUFFERED=1
COPY --from=builder /root/.local /root/.local
COPY --from=builder /app .

EXPOSE 8080

# Запуск только сервера, миграции выносятся в initContainer
ENTRYPOINT ["python", "manage.py", "runserver", "0.0.0.0:8080"]