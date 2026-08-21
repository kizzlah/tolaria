s---
type: Outline
---
# Student Docker Containers - Guide

# The Student's Digital Fortress: A Step-by-Step Setup Guide

Welcome to your all-in-one guide for deploying the five essential student Docker containers, secured with Tailscale for always-on access from anywhere. This booklet will walk you through the complete setup.

## Prerequisites

Before starting, ensure you have:

- A machine (laptop, Raspberry Pi, or old PC) running Linux, macOS, or Windows with Docker and Docker Compose installed
- A Tailscale account (free at [tailscale.com](http://tailscale.com))
- Sufficient storage: Full offline Wikipedia can exceed 100GB, so plan accordingly

---

## Step 1: Setup Tailscale Authentication

Before deploying any container, you need an authentication key for secure access.

1. Log in to your Tailscale admin console
2. Navigate to **Settings** → **Keys**
3. Click **Generate auth key**
4. Add a description (e.g., "Student Docker Setup") and leave other options default
5. **Copy the key immediately**—it won't be shown again

---

## Step 2: Deploy Kanboard (Task Management)

Kanboard helps you visualize projects with a simple, free Trello alternative.

**Objective:** Run Kanboard with persistent data storage.

```javascript
### Using docker run:
bash
docker run -d --name kanboard \
  -p 8080:80 \
  -v kanboard_data:/var/www/app/data \
  -v kanboard_plugins:/var/www/app/plugins \
  kanboard/kanboard:latest
```

\*Access at `http://localhost:8080`[\*](http://localhost:8080%60*)

---

~~~typescript
### Using Docker Compose:
Create docker-compose.yml:
```yaml
services:
  kanboard:
    image: kanboard/kanboard:latest
    container_name: kanboard
    ports:
      - "8080:80"
    volumes:
      - kanboard_data:/var/www/app/data
      - kanboard_plugins:/var/www/app/plugins
    environment:
      - PLUGIN_INSTALLER=true
volumes:
  kanboard_data:
  kanboard_plugins:
```
~~~

Run with: `docker compose up -d`

---

## Step 3: Deploy Nextcloud (Personal Storage)

Nextcloud provides private cloud storage for all your files.

**Objective:** Deploy Nextcloud All-in-One with persistent volumes.

Create `docker-compose.yml`:

~~~javascript
```yaml
services:
  nextcloud-db:
    image: mariadb:10.6
    container_name: nextcloud-db
    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW
    volumes:
      - ./db:/var/lib/mysql
    environment:
      - MYSQL_ROOT_PASSWORD=your_root_password
      - MYSQL_PASSWORD=your_db_password
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
    restart: always
  nextcloud-redis:
    image: redis:alpine
    container_name: nextcloud-redis
    restart: always
  nextcloud-app:
    image: nextcloud:latest
    container_name: nextcloud-app
    ports:
      - "8081:80"
    volumes:
      - ./nextcloud_data:/var/www/html
    environment:
      - MYSQL_HOST=nextcloud-db
      - MYSQL_PASSWORD=your_db_password
      - MYSQL_DATABASE=nextcloud
      - MYSQL_USER=nextcloud
      - REDIS_HOST=nextcloud-redis
    depends_on:
      - nextcloud-db
      - nextcloud-redis
    restart: always
```
~~~

Run with: `docker compose up -d`

\*Access setup wizard at `http://localhost:8081` to create admin account.\*

---

## Step 4: Deploy Paperless-ngx (Document Management)

Paperless-ngx digitizes and OCRs your notes, making them searchable.

**Objective:** Deploy full OCR pipeline with database and Redis cache.

Create `docker-compose.yml`:

~~~typescript
```yaml
services:
  paperless-redis:
    image: redis:7-alpine
    container_name: paperless-redis
    restart: unless-stopped
  paperless-db:
    image: postgres:16-alpine
    container_name: paperless-db
    environment:
      POSTGRES_DB: paperless
      POSTGRES_USER: paperless
      POSTGRES_PASSWORD: paperless_db_password
    volumes:
      - paperless_db:/var/lib/postgresql/data
    restart: unless-stopped
  paperless:
    image: ghcr.io/paperless-ngx/paperless-ngx:latest
    container_name: paperless
    ports:
      - "8000:8000"
    volumes:
      - paperless_data:/usr/src/paperless/data
      - paperless_media:/usr/src/paperless/media
      - paperless_consume:/usr/src/paperless/consume
      - paperless_export:/usr/src/paperless/export
    environment:
      PAPERLESS_REDIS: redis://paperless-redis:6379
      PAPERLESS_DBHOST: paperless-db
      PAPERLESS_DBUSER: paperless
      PAPERLESS_DBPASS: paperless_db_password
      PAPERLESS_DBNAME: paperless
      PAPERLESS_SECRET_KEY: your_secret_key_here
      PAPERLESS_ADMIN_USER: admin
      PAPERLESS_ADMIN_PASSWORD: admin_password
      PAPERLESS_ADMIN_MAIL: admin@example.com
      PAPERLESS_OCR_LANGUAGE: eng
      PAPERLESS_TIME_ZONE: America/New_York
    depends_on:
      - paperless-db
      - paperless-redis
    restart: unless-stopped
volumes:
  paperless_data:
  paperless_media:
  paperless_consume:
  paperless_export:
  paperless_db:
```
~~~

Run with: `docker compose up -d`

\*Access at `http://localhost:8000`[\*](http://localhost:8000%60*)

---

## Step 5: Deploy Kiwix (Offline Knowledge)

Kiwix serves offline versions of websites like Wikipedia.

**Objective:** Run lightweight ZIM file server.

1. Download a ZIM file (e.g., Wikipedia) from Kiwix library
2. Place it in a directory (e.g., `./zim_files/`)

Run Kiwix server:

~~~
```bash
docker run -d --name kiwix \
  -p 8082:80 \
  -v ./zim_files:/data \
  ghcr.io/kiwix/kiwix-serve:latest /data/*.zim
```
~~~

\*Access at `http://localhost:8082`[\*](http://localhost:8082%60*)

---

## Step 6: Connect to Tailscale (Always-On Access)

Now bind everything together with Tailscale for secure remote access.

**Objective:** Use Tailscale sidecar to expose services.

Create `docker-compose.yml`:

~~~javascript
```yaml
services:
  tailscale:
    image: tailscale/tailscale:latest
    container_name: ts-sidecar
    hostname: student-server
    environment:
      - TS_AUTHKEY=tskey-auth-xxxxx  # Replace with your key
      - TS_STATE_DIR=/var/lib/tailscale
      - TS_USERSPACE=false
      - TS_EXTRA_ARGS=--advertise-tags=tag:container
    volumes:
      - ts-state:/var/lib/tailscale
      - /dev/net/tun:/dev/net/tun
    cap_add:
      - NET_ADMIN
      - SYS_MODULE
    restart: unless-stopped
  kanboard:
    image: kanboard/kanboard:latest
    network_mode: service:tailscale
    depends_on:
      - tailscale
    volumes:
      - kanboard_data:/var/www/app/data
    restart: unless-stopped
  nextcloud:
    image: nextcloud:latest
    network_mode: service:tailscale
    depends_on:
      - tailscale
    volumes:
      - nextcloud_data:/var/www/html
    restart: unless-stopped
  paperless:
    image: ghcr.io/paperless-ngx/paperless-ngx:latest
    network_mode: service:tailscale
    depends_on:
      - tailscale
    volumes:
      - paperless_data:/usr/src/paperless/data
    restart: unless-stopped
  kiwix:
    image: ghcr.io/kiwix/kiwix-serve:latest
    network_mode: service:tailscale
    depends_on:
      - tailscale
    volumes:
      - ./zim_files:/data
    command: /data/*.zim
    restart: unless-stopped
volumes:
  ts-state:
  kanboard_data:
  nextcloud_data:
  paperless_data:
```
~~~

Run with: `docker compose up -d`

---

## Step 7: Verify & Access

1. Check Tailscale status:

~~~
   ```bash
   docker exec ts-sidecar tailscale status
   ```
~~~

1. Get your server's Tailscale IP:

~~~
   ```bash
   docker exec ts-sidecar tailscale ip -4
   ```
~~~

1. Access services from any device with Tailscale:
  - Kanboard: `http://[tailscale-ip]:8080`
  - Nextcloud: `http://[tailscale-ip]:8081`
  - Paperless: `http://[tailscale-ip]:8000`
  - Kiwix: `http://[tailscale-ip]:8082`

---

## Quick Reference: Service Ports

| Service | Port (local) |
| --- | --- |
| Kanboard | 8080 |
| Nextcloud | 8081 |
| Paperless-ngx | 8000 |
| Kiwix | 8082 |

---

**Congratulations!** You've built a complete digital ecosystem accessible from anywhere, securely, without exposing your server to the public internet.
