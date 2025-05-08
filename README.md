# paperlib

Local self-hosted version of paperless-ngx + paparless-ngx + paperless-ai.

This is an amalgamation of the following projects:

- [paperless-ngx](https://github.com/paperless-ngx/paperless-ngx)
- [paperless-ai](https://github.com/clusterzx/paperless-ai)
- [paperless-gpt](https://github.com/icereed/paperless-gpt)

## Setup Instructions

### 1. Create a .env file

Copy the .env.example file to .env and customize the values according to your needs.

### 2. Start the services

```bash
# Start all services
docker compose up -d

# Create a superuser for Paperless-ngx
docker compose exec webserver create_superuser
```

### 3. Access your services

- Paperless-ngx: <http://localhost:8000>
- Paperless-AI: <http://localhost:3000>

### 4. Stop the services

```bash
docker compose down
```

Or delete the containers and volumes manually:

```bash
docker compose down -v
```

## Additional Configuration

To add more OCR languages:

```bash
PAPERLESS_OCR_LANGUAGES=eng deu fra
```

To enable Apache Tika for Office document support, add this service to docker-compose.yaml:

```yaml
tika:
  image: apache/tika:latest
  restart: unless-stopped
```

And add to webserver environment:

```bash
PAPERLESS_TIKA_ENABLED=1
PAPERLESS_TIKA_ENDPOINT=http://tika:9998
PAPERLESS_TIKA_GOTENBERG_ENDPOINT=http://gotenberg:3000
```

## Roadmap

- [ ] Add Gotenberg.
- [ ] Add Apache Tika.
