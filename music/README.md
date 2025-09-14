# Music Stack Docker Template

This repository provides a template for setting up a home music management stack using Docker. Currently, it includes **Lidarr**, and is designed to easily expand with other Starr apps (Sonarr, Radarr) or a future music streaming service.

---

## Features

* Fully configurable via `.env` file
* Persistent storage for configuration and media data
* User and group permissions for safe file access
* Easy to add additional services
* Healthchecks for container monitoring

---

## Requirements

* Docker & Docker Compose installed
* Linux host (preferred for UID/GID compatibility)
* Basic knowledge of Docker and networking

---

## Setup

### 1. Clone this repository

```bash
git clone <your-repo-url> music-stack
cd music-stack
```

### 2. Configure your `.env` file

Create a `.env` file based on `env.example`:

```dotenv
### Global Settings
RESTART_POLICY=unless-stopped
BIND_ADDRESS=0.0.0.0
TZ=Europe/London
PUID=1000
PGID=1000
CONFIG_DIR=/config
DATA_DIR=/data

### Lidarr Settings
# LIDARR_PORT=8686
# LIDARR_API_KEY=your_api_key_here
```

* Adjust paths (`CONFIG_DIR` and `DATA_DIR`) to your host directories
* Set `PUID` and `PGID` to match the user running Docker
* Optional: set `LIDARR_PORT` and `LIDARR_API_KEY`

### 3. Launch the stack

```bash
docker compose up -d
```

* Containers will use the restart policy defined in `.env`
* Logs can be viewed via `docker compose logs -f lidarr`

### 4. Access Lidarr

* Open your browser: `http://<host-ip>:8686`
* Initial setup wizard will guide you through library and download client configuration

---

## Adding Future Services

* Add new services to `docker-compose.yml` following the same template:

  * Use `.env` variables for ports, paths, and UID/GID
  * Connect to `music_net` for network isolation and service discovery

### Example placeholder for a music streaming service

```yaml
  musicstream:
    image: <image>
    container_name: musicstream
    restart: ${RESTART_POLICY}
    environment:
      TZ: ${TZ}
      PUID: ${PUID}
      PGID: ${PGID}
    ports:
      - "${BIND_ADDRESS}:${MUSICSTREAM_PORT:-5500}:5500"
    volumes:
      - "${CONFIG_DIR}/musicstream:/config"
      - "${DATA_DIR}:/data"
    networks:
      - music_net
```

---

## Notes

* Ensure that your `.env` file is **never committed with sensitive API keys**.
* Healthchecks help ensure services are running correctly.
* Permissions should always be checked when adding new volumes.

---

## License

This project is provided as a template for personal use and can be adapted for any home media setup.
