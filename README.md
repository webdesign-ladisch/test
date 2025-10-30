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