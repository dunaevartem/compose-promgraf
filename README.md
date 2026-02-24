# Prometheus & Grafana Monitoring Stack
Репозиторий содержит готовую конфигурацию для развертывания системы мониторинга инфраструктуры на базе Docker Compose. Проект позволяет в один клик поднять связку для сбора и визуализации метрик сервера.
# Технологический стек
Prometheus — система сбора и хранения метрик (Time Series DB).
Grafana — платформа для визуализации и создания дашбордов.
Node Exporter — агент для сбора метрик ОС (CPU, RAM, Disk, Network).
Docker & Docker Compose — контейнеризация и оркестрация.
Архитектура системы
Node Exporter собирает низкоуровневые метрики хоста и отдает их по порту 9100.
Prometheus по заданному интервалу (15s) опрашивает (pull модель) Node Exporter и сохраняет данные.
Grafana подключается к Prometheus как к источнику данных (Data Source) и отображает их на графиках.
# Быстрый старт
# 1. Подготовка окружения
Создайте файл с переменными окружения для безопасности Grafana:
bash
cp dc-prom+graf.env.example dc-prom+graf.env
Отредактируйте пароль администратора в dc-prom+graf.env

# 2. Запуск стека
bash
docker-compose up -d

# 3. Доступ к интерфейсам
Grafana: http://localhost:3000 (логин: admin, пароль из вашего .env)
Prometheus: http://localhost:9090
# Особенности конфигурации
Безопасность: Пароль администратора Grafana не хранится в коде, а передается через Docker Environment Variables. \
Persistence: Использование Docker Volumes для сохранения данных Grafana (настройки и дашборды не сбрасываются при перезапуске). \
Custom Config: Prometheus настроен на автоматический сбор метрик с самого себя и с Node Exporter через внутреннюю сеть Docker.
