---
type: Outline
---
# Student Docker Containers - Guide

\# The Student's Digital Fortress: A Step-by-Step Setup Guide

Welcome to your all-in-one guide for deploying the five essential student Docker containers, secured with Tailscale for always-on access from anywhere. This booklet will walk you through the complete setup.

\## Prerequisites

Before starting, ensure you have:

- A machine (laptop, Raspberry Pi, or old PC) running Linux, macOS, or Windows with Docker and Docker Compose installed
- A Tailscale account (free at [tailscale.com](http://tailscale.com))
- Sufficient storage: Full offline Wikipedia can exceed 100GB, so plan accordingly

---

\## Step 1: Setup Tailscale Authentication

Before deploying any container, you need an authentication key for secure access.

1. Log in to your Tailscale admin console
2. Navigate to **Settings** → **Keys**
3. Click **Generate auth key**
4. Add a description (e.g., "Student Docker Setup") and leave other options default
5. **Copy the key immediately**—it won't be shown again

---

\## Step 2: Deploy Kanboard (Task Management)

Kanboard helps you visualize projects with a simple, free Trello alternative.

**Objective:** Run Kanboard with persistent data storage.

\### Using `docker run`:

\`\`\`bash

docker run -d --name kanboard \\

  -p 8080:80 \\

  -v kanboard\_data:/var/www/app/data \\

  -v kanboard\_plugins:/var/www/app/plugins \\

  kanboard/kanboard:latest

\`\`\`

\*Access at `http://localhost:8080`[\*](http://localhost:8080`*)

\### Using Docker Compose:

Create `docker-compose.yml`:

\`\`\`yaml

services:

  kanboard:

    image: kanboard/kanboard:latest

    container\_name: kanboard

    ports:

      - "8080:80"

    volumes:

      - kanboard\_data:/var/www/app/data
      - kanboard\_plugins:/var/www/app/plugins

    environment:

      - PLUGIN\_INSTALLER=true

volumes:

  kanboard\_data:

  kanboard\_plugins:

\`\`\`

Run with: `docker compose up -d`

---

\## Step 3: Deploy Nextcloud (Personal Storage)

Nextcloud provides private cloud storage for all your files.

**Objective:** Deploy Nextcloud All-in-One with persistent volumes.

Create `docker-compose.yml`:

\`\`\`yaml

services:

  nextcloud-db:

    image: mariadb:10.6

    container\_name: nextcloud-db

    command: --transaction-isolation=READ-COMMITTED --binlog-format=ROW

    volumes:

      - ./db:/var/lib/mysql

    environment:

      - MYSQL\_ROOT\_PASSWORD=your\_root\_password
      - MYSQL\_PASSWORD=your\_db\_password
      - MYSQL\_DATABASE=nextcloud
      - MYSQL\_USER=nextcloud

    restart: always

  nextcloud-redis:

    image: redis:alpine

    container\_name: nextcloud-redis

    restart: always

  nextcloud-app:

    image: nextcloud:latest

    container\_name: nextcloud-app

    ports:

      - "8081:80"

    volumes:

      - ./nextcloud\_data:/var/www/html

    environment:

      - MYSQL\_HOST=nextcloud-db
      - MYSQL\_PASSWORD=your\_db\_password
      - MYSQL\_DATABASE=nextcloud
      - MYSQL\_USER=nextcloud
      - REDIS\_HOST=nextcloud-redis

    depends\_on:

      - nextcloud-db
      - nextcloud-redis

    restart: always

\`\`\`

Run with: `docker compose up -d`

\*Access setup wizard at `http://localhost:8081` to create admin account.\*

---

\## Step 4: Deploy Paperless-ngx (Document Management)

Paperless-ngx digitizes and OCRs your notes, making them searchable.

**Objective:** Deploy full OCR pipeline with database and Redis cache.

Create `docker-compose.yml`:

\`\`\`yaml

services:

  paperless-redis:

    image: redis:7-alpine

    container\_name: paperless-redis

    restart: unless-stopped

  paperless-db:

    image: postgres:16-alpine

    container\_name: paperless-db

    environment:

      POSTGRES\_DB: paperless

      POSTGRES\_USER: paperless

      POSTGRES\_PASSWORD: paperless\_db\_password

    volumes:

      - paperless\_db:/var/lib/postgresql/data

    restart: unless-stopped

  paperless:

    image: ghcr.io/paperless-ngx/paperless-ngx:latest

    container\_name: paperless

    ports:

      - "8000:8000"

    volumes:

      - paperless\_data:/usr/src/paperless/data
      - paperless\_media:/usr/src/paperless/media
      - paperless\_consume:/usr/src/paperless/consume
      - paperless\_export:/usr/src/paperless/export

    environment:

      PAPERLESS\_REDIS: redis://paperless-redis:6379

      PAPERLESS\_DBHOST: paperless-db

      PAPERLESS\_DBUSER: paperless

      PAPERLESS\_DBPASS: paperless\_db\_password

      PAPERLESS\_DBNAME: paperless

      PAPERLESS\_SECRET\_KEY: your\_secret\_key\_here

      PAPERLESS\_ADMIN\_USER: admin

      PAPERLESS\_ADMIN\_PASSWORD: admin\_password

      PAPERLESS\_ADMIN\_MAIL: [admin@example.com](mailto:admin@example.com)

      PAPERLESS\_OCR\_LANGUAGE: eng

      PAPERLESS\_TIME\_ZONE: America/New\_York

    depends\_on:

      - paperless-db
      - paperless-redis

    restart: unless-stopped

volumes:

  paperless\_data:

  paperless\_media:

  paperless\_consume:

  paperless\_export:

  paperless\_db:

\`\`\`

Run with: `docker compose up -d`

\*Access at `http://localhost:8000`[\*](http://localhost:8000`*)

---

\## Step 5: Deploy Kiwix (Offline Knowledge)

Kiwix serves offline versions of websites like Wikipedia.

**Objective:** Run lightweight ZIM file server.

1. Download a ZIM file (e.g., Wikipedia) from Kiwix library
2. Place it in a directory (e.g., `./zim_files/`)

Run Kiwix server:

\`\`\`bash

docker run -d --name kiwix \\

  -p 8082:80 \\

  -v ./zim\_files:/data \\

  ghcr.io/kiwix/kiwix-serve:latest /data/\*.zim

\`\`\`

\*Access at `http://localhost:8082`[\*](http://localhost:8082`*)

---

\## Step 6: Connect to Tailscale (Always-On Access)

Now bind everything together with Tailscale for secure remote access.

**Objective:** Use Tailscale sidecar to expose services.

Create `docker-compose.yml`:

\`\`\`yaml

services:

  tailscale:

    image: tailscale/tailscale:latest

    container\_name: ts-sidecar

    hostname: student-server

    environment:

      - TS\_AUTHKEY=tskey-auth-xxxxx  # Replace with your key
      - TS\_STATE\_DIR=/var/lib/tailscale
      - TS\_USERSPACE=false
      - TS\_EXTRA\_ARGS=--advertise-tags=tag:container

    volumes:

      - ts-state:/var/lib/tailscale
      - /dev/net/tun:/dev/net/tun

    cap\_add:

      - NET\_ADMIN
      - SYS\_MODULE

    restart: unless-stopped

  kanboard:

    image: kanboard/kanboard:latest

    network\_mode: service:tailscale

    depends\_on:

      - tailscale

    volumes:

      - kanboard\_data:/var/www/app/data

    restart: unless-stopped

  nextcloud:

    image: nextcloud:latest

    network\_mode: service:tailscale

    depends\_on:

      - tailscale

    volumes:

      - nextcloud\_data:/var/www/html

    restart: unless-stopped

  paperless:

    image: ghcr.io/paperless-ngx/paperless-ngx:latest

    network\_mode: service:tailscale

    depends\_on:

      - tailscale

    volumes:

      - paperless\_data:/usr/src/paperless/data

    restart: unless-stopped

  kiwix:

    image: ghcr.io/kiwix/kiwix-serve:latest

    network\_mode: service:tailscale

    depends\_on:

      - tailscale

    volumes:

      - ./zim\_files:/data

    command: /data/\*.zim

    restart: unless-stopped

volumes:

  ts-state:

  kanboard\_data:

  nextcloud\_data:

  paperless\_data:

\`\`\`

Run with: `docker compose up -d`

---

\## Step 7: Verify & Access

1. Check Tailscale status:

   \`\`\`bash

   docker exec ts-sidecar tailscale status

   \`\`\`

2. Get your server's Tailscale IP:

   \`\`\`bash

   docker exec ts-sidecar tailscale ip -4

   \`\`\`

3. Access services from any device with Tailscale:
   - Kanboard: `http://[tailscale-ip]:8080`
   - Nextcloud: `http://[tailscale-ip]:8081`
   - Paperless: `http://[tailscale-ip]:8000`
   - Kiwix: `http://[tailscale-ip]:8082`

---

\## Quick Reference: Service Ports

| Service | Port (local) |

|---------|--------------|

| Kanboard | 8080 |

| Nextcloud | 8081 |

| Paperless-ngx | 8000 |

| Kiwix | 8082 |

---

**Congratulations!** You've built a complete digital ecosystem accessible from anywhere, securely, without exposing your server to the public internet.
