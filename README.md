# Storingsmelder - Labo 3: Applicatie en Database

Dit project bevat de Storingsmelder-applicatie, gekoppeld aan een PostgreSQL 17 database via Docker Compose. De stack is voorzien van persistentie via volumes, een healthcheck voor gesynchroniseerde opstart en configuratie via omgevingsvariabelen.

## Vereisten

- Git
- Docker Desktop (inclusief Docker Compose)

## Installatie en Opstarten

Volg onderstaande stappen om het project lokaal te clonen en op te starten:

### 1. Repository clonen

Clone de repository en open de projectmap:

git clone https://github.com/migelangelo9/cloud-computing.git
cd cloud-computing

### 2. Omgevingsvariabelen instellen (.env)

Het bestand met inloggegevens (.env) staat niet in Git vanwege beveiligingsredenen. Er is een voorbeeldbestand (.env.example) aanwezig.

Maak een kopie van .env.example en noem deze .env:

In PowerShell:
Copy-Item .env.example .env

Vul in het nieuw aangemaakte .env bestand de gewenste database-inloggegevens in:
POSTGRES_USER=student
POSTGRES_PASSWORD=t
POSTGRES_DB=storingsmelder

### 3. Services starten via Docker Compose

Start de containers op de achtergrond:

docker compose up -d

De webapplicatie start pas op nadat PostgreSQL via de interne healthcheck (pg_isready) heeft bevestigd dat TCP-verbindingen worden geaccepteerd.

Controleer de status van de containers:

docker compose ps

De database hoort de status "Up (healthy)" te hebben en de web-container de status "Up".

### 4. Applicatie gebruiken

Open een browser en ga naar:
http://localhost:8000

Hier kunnen meldingen worden bekeken en toegevoegd. Deze worden persistent opgeslagen in PostgreSQL.

## Afsluiten en Opruimen

- Containers stoppen en netwerk verwijderen (met behoud van data in het named volume):
  docker compose down

- Containers en named volumes volledig wissen (schone herstart):
  docker compose down -v

## Container Registry

Het image voor de webapplicatie is publiek beschikbaar op de GitHub Container Registry (GHCR):
ghcr.io/migelangelo9/storingsmelder:1.0

Dit image kan rechtstreeks worden binnengehaald met:
docker pull ghcr.io/migelangelo9/storingsmelder:1.0
