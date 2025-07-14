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

```
g5/
├── docker-compose.yml
├── grafana/
│   ├── dashboards/
│   │   ├── cadvisor.json
│   │   ├── fluentd.json
│   │   └── node_exporter.json
│   ├── dashboards.yml
│   └── datasource.yml
├── hosts.ini
├── playbook.yml
├── prometheus/
│   └── prometheus.yml
├── README.md
└── roles/
    ├── docker/
    │   ├── files/
    │   │   ├── daemon.json
    │   │   └── docker.list
    │   └── tasks/
    │       └── main.yml
    └── fluentd/
        ├── files/
        │   └── fluentd.conf
        └── tasks/
            └── main.yml
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
