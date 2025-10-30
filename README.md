# Vite React + Express TypeScript Projekt

Dieses Projekt besteht aus einem Frontend (Vite + React + TypeScript) und einem Backend (Express + TypeScript).

## Projektstruktur

```
.
├── frontend/          # Vite React TypeScript Frontend
└── backend/           # Express TypeScript Backend
```

## Frontend

### Installation
```bash
cd frontend
npm install
```

### Entwicklungsserver starten
```bash
npm run dev
```

Der Frontend-Server läuft auf http://localhost:5173

### Build
```bash
npm run build
```

## Backend

### Installation
```bash
cd backend
npm install
```

### Entwicklungsserver starten
```bash
npm run dev
```

Der Backend-Server läuft auf http://localhost:3000

### Build
```bash
npm run build
```

### Produktionsserver starten
```bash
npm start
```

## API-Endpunkte

- `GET /` - Willkommensnachricht
- `GET /api/hello` - Test-Endpunkt

## Entwicklung

1. Backend starten: `cd backend && npm run dev`
2. Frontend starten: `cd frontend && npm run dev`
3. Im Browser öffnen: http://localhost:5173

---

## Docker Deployment

Das Projekt kann vollständig mit Docker containerisiert und deployed werden.

### Voraussetzungen

- Docker (>= 20.10)
- Docker Compose (>= 2.0)

### Schnellstart mit Docker

#### Einfache Deployment (ohne Reverse Proxy)

```bash
# Alle Services bauen und starten
docker-compose up -d

# Logs anzeigen
docker-compose logs -f

# Services stoppen
docker-compose down
```

Nach dem Start ist die Anwendung verfügbar:
- Frontend: http://localhost (Port 80)
- Backend API: http://localhost:3000

#### Production Deployment (mit Nginx Reverse Proxy)

Für Production-Umgebungen mit SSL-Support und erweiterten Features:

```bash
# Mit Production-Konfiguration starten
docker-compose -f docker-compose.prod.yml up -d

# Logs anzeigen
docker-compose -f docker-compose.prod.yml logs -f

# Services stoppen
docker-compose -f docker-compose.prod.yml down
```

Nach dem Start:
- Anwendung: http://localhost (Port 80)
- API-Endpunkte: http://localhost/api/*
- Health Check: http://localhost/health

### Docker-Befehle

```bash
# Alle Images neu bauen
docker-compose build

# Bestimmten Service neu bauen
docker-compose build frontend
docker-compose build backend

# Logs eines bestimmten Service anzeigen
docker-compose logs -f frontend
docker-compose logs -f backend

# Services neu starten
docker-compose restart

# In Container einloggen
docker exec -it app-frontend sh
docker exec -it app-backend sh

# Alle Container, Volumes und Images löschen
docker-compose down -v --rmi all
```

### SSL/HTTPS einrichten

Für HTTPS-Support:

1. SSL-Zertifikate in `nginx/ssl/` ablegen:
   ```
   nginx/ssl/cert.pem
   nginx/ssl/key.pem
   ```

2. In `nginx/nginx.conf` den HTTPS-Server-Block auskommentieren und Domain anpassen

3. Services neu starten:
   ```bash
   docker-compose -f docker-compose.prod.yml restart nginx
   ```

**Tipp**: Für Let's Encrypt Zertifikate kann Certbot verwendet werden:
```bash
# Certbot installieren
sudo apt-get install certbot

# Zertifikat erstellen
sudo certbot certonly --standalone -d your-domain.com
```

### Deployment auf eigenem Server

1. Repository auf den Server klonen:
   ```bash
   git clone <repository-url>
   cd <project-directory>
   ```

2. Docker und Docker Compose installieren (falls nicht vorhanden):
   ```bash
   # Docker installieren
   curl -fsSL https://get.docker.com -o get-docker.sh
   sudo sh get-docker.sh

   # Docker Compose installieren
   sudo apt-get install docker-compose-plugin
   ```

3. Anwendung starten:
   ```bash
   # Einfach
   docker-compose up -d

   # Oder mit Reverse Proxy
   docker-compose -f docker-compose.prod.yml up -d
   ```

4. Firewall-Regeln anpassen:
   ```bash
   sudo ufw allow 80/tcp
   sudo ufw allow 443/tcp
   ```

### Monitoring

```bash
# Ressourcen-Nutzung anzeigen
docker stats

# Container-Status prüfen
docker-compose ps

# Health Checks prüfen
docker inspect app-frontend | grep -A 10 Health
docker inspect app-backend | grep -A 10 Health
```

### Projektstruktur (Docker)

```
.
├── frontend/
│   ├── Dockerfile              # Multi-stage build (Node.js → Nginx)
│   ├── nginx.conf              # Nginx-Konfiguration für SPA
│   └── .dockerignore
├── backend/
│   ├── Dockerfile              # Multi-stage build
│   └── .dockerignore
├── nginx/
│   ├── nginx.conf              # Reverse Proxy Konfiguration
│   ├── ssl/                    # SSL-Zertifikate (nicht im Repo)
│   └── logs/                   # Nginx-Logs
├── docker-compose.yml          # Basis-Konfiguration
└── docker-compose.prod.yml     # Production mit Reverse Proxy
```