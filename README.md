# Система мониторинга и сбора логов (Prometheus + Grafana + Fluentd)

## 📌 Описание

Данный проект разворачивает систему мониторинга с использованием **Docker Compose** и **Ansible**:

- **Prometheus** — сбор метрик, в том числе с Fluentd
- **Grafana** — визуализация метрик (http://<IP>:80)
- **Fluentd** — systemd-сервис, установленный **локально через Ansible**, собирающий логи контейнеров Grafana и Prometheus, записывающий их в `/var/log/test`, и предоставляющий метрики для Prometheus

---

## 🛠️ Требования

- Ubuntu 24.04
- Установлены:  
  - `Docker`  
  - `Docker Compose`  
  - `Ansible`  

---

## 📁 Структура проекта

g5/
├── docker-compose.yml                 # Docker Compose для Prometheus + Grafana
├── grafana/
│   ├── dashboards/                    # Дашборды Grafana
│   │   ├── cadvisor.json              # Дашборд для cAdvisor
│   │   ├── fluentd.json               # Дашборд для Fluentd
│   │   └── node_exporter.json         # Дашборд для Node Exporter
│   ├── dashboards.yml                 # Настройка автозагрузки дашбордов
│   └── datasource.yml                 # Настройка Prometheus как datasource
├── hosts.ini                          # Инвентарный файл Ansible
├── playbook.yml                       # Основной Ansible playbook
├── prometheus/
│   └── prometheus.yml                 # Конфигурация Prometheus (job’ы, targets)
├── README.md                          # Документация по проекту
└── roles/
    ├── docker/                        # Роль Ansible для настройки Docker
    │   ├── files/
    │   │   ├── daemon.json            # Конфигурация Docker daemon
    │   │   └── docker.list            # Источник репозитория Docker
    │   └── tasks/
    │       └── main.yml               # Основные задачи по установке Docker
    └── fluentd/                       # Роль Ansible для установки Fluentd
        ├── files/
        │   └── fluentd.conf           # Конфигурация Fluentd
        └── tasks/
            └── main.yml              # Основные задачи по установке Fluentd

---

## 🚀 Развёртывание

### 1. Клонирование проекта

```bash
git clone https://github.com/NurkanatShaken/g5.git
cd g5/
нужно добавить целевой хост в файл hosts.ini
и затем запустить playbook через команду
ansible-playbook -i hosts.ini playbook.yml

🔐 Доступ
Grafana:
http://<IP-адрес вашей машины>:80
Логин: admin
Пароль: admin
