# Matrix + Element + Traefik + TURN Deployment

This repository contains a ready-to-use setup for a Matrix homeserver with Element web client and TURN server, all behind Traefik with automatic HTTPS certificates.

---

## Components

- Synapse (Matrix server)
- Element Web (Matrix client)
- Coturn (TURN/STUN server for voice and video)
- Traefik v3 (reverse proxy and SSL automation)
- Docker Compose (single-command deployment)

---

## Quick Deployment

### 1. Clone the repository

```bash
git clone https://github.com/yourusername/matrix-deploy.git
cd matrix-deploy
```

### 2. Configure environment variables

Copy `.env.example` to `.env` and edit:

```
DOMAIN=example.com
EMAIL=your@email.com
```

### 3. Generate password hash for Traefik

```bash
htpasswd -nbB admin yourpassword
```

Insert the hash into `docker-compose.yml`:

```yaml
- "traefik.http.middlewares.dashboard-auth.basicauth.users=admin:yourhash"
```

### 4. Configure TURN server

Create or edit `turnserver.conf`:

```ini
listening-port=3478
tls-listening-port=5349
fingerprint
lt-cred-mech
use-auth-secret
static-auth-secret=yoursecret
realm=matrix.example.com
cert=/etc/letsencrypt/live/matrix.example.com/fullchain.pem
pkey=/etc/letsencrypt/live/matrix.example.com/privkey.pem
no-multicast-peers
```

### 5. Run everything

```bash
docker compose up -d
```

Access the services:
- Element: https://chat.example.com
- Matrix: https://matrix.example.com
- Traefik Dashboard: https://panel.example.com

---

## Notes

- TURN credentials are automatically linked to Synapse.
- Required open ports: 80, 443, 3478, 5349.
- On iOS and Android, use `matrix.example.com` as the homeserver.

---

# Русская версия

## Matrix + Element + Traefik + TURN сервер

Этот репозиторий содержит готовое окружение для развёртывания собственного Matrix-сервера, Element-клиента и TURN-сервера. Всё работает через Traefik с автоматическим HTTPS.

---

## Компоненты

- Synapse (сервер Matrix)
- Element Web (веб-клиент)
- Coturn (сервер для звонков)
- Traefik v3 (обратный прокси и сертификаты)
- Docker Compose (единый запуск)

---

## Развёртывание

### 1. Клонирование

```bash
git clone https://github.com/yourusername/matrix-deploy.git
cd matrix-deploy
```

### 2. Настройка окружения

Создайте `.env` из `.env.example` и отредактируйте:

```
DOMAIN=example.com
EMAIL=your@email.com
```

### 3. Генерация пароля для Traefik

```bash
htpasswd -nbB quieet yourpassword
```

Добавьте хэш в `docker-compose.yml`:

```yaml
- "traefik.http.middlewares.dashboard-auth.basicauth.users=quieet:yourhash"
```

### 4. Настройка TURN

Файл `turnserver.conf`:

```ini
listening-port=3478
tls-listening-port=5349
fingerprint
lt-cred-mech
use-auth-secret
static-auth-secret=yoursecret
realm=matrix.example.com
cert=/etc/letsencrypt/live/matrix.example.com/fullchain.pem
pkey=/etc/letsencrypt/live/matrix.example.com/privkey.pem
no-multicast-peers
```

### 5. Запуск

```bash
docker compose up -d
```

После запуска:
- Element: https://chat.example.com
- Matrix: https://matrix.example.com
- Traefik Dashboard: https://panel.example.com

---

## Примечания

- TURN автоматически связывается с Matrix.
- Откройте порты: 80, 443, 3478, 5349.
- Для мобильных клиентов используйте `matrix.example.com` как адрес сервера.

---

© 2025 — Matrix Deployment Template by Quieet
