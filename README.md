# docker-nginx-reverse-proxy

Live
https://rlyehnet.dev
Stack

Docker + Docker Compose — запуск Nginx в контейнере
Nginx — reverse proxy, раздача статики, редирект HTTP→HTTPS
Ansible — деплой конфига site.conf на сервер через шаблон
GitHub Actions — CI (проверка сборки Docker образа)
Let's Encrypt — SSL-сертификаты (монтируются в контейнер)

Структура проекта
.
├── ansible/
│   ├── group_vars/all/
│   │   ├── vars.yml          # переменные (домен, пути к сертификатам)
│   │   └── vars.example      # пример — заполни и переименуй в vars.yml
│   ├── inventory/
│   │   ├── hosts             # адреса серверов
│   │   └── hosts.example     # пример inventory
│   ├── templates/
│   │   └── site.conf.j2      # шаблон конфига Nginx
│   └── nginx_conf.yml        # Ansible playbook
├── docker_nginx/
│   ├── Dockerfile            # образ на базе nginx:stable + curl
│   ├── docker-compose.yml    # запуск контейнера
│   └── site/html/            # статика сайта
└── .github/workflows/        # CI pipeline