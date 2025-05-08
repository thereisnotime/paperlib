# paperlib

Local self-hosted version of paperless-ngx + paparless-ngx + paperless-ai.

This is an amalgamation of the following projects:

- [paperless-ngx](https://github.com/paperless-ngx/paperless-ngx)
- [paperless-ai](https://github.com/clusterzx/paperless-ai)
- [paperless-gpt](https://github.com/icereed/paperless-gpt)
- [docling](https://github.com/docling-project/docling)
- [gotenberg](https://github.com/gotenberg/gotenberg)
- [tika](https://github.com/apache/tika)

## Setup Instructions

### 1. Create a .env file

Copy the .env.example file to .env and customize the values according to your needs.

### 2. Start the services

```bash
# Start all services
docker compose up -d
```

```bash
# Create a superuser for Paperless-ngx
docker compose exec paperless-ngx python manage.py createsuperuser
```

### 3. Access your services

- Paperless-ngx: <http://localhost:8000>
- Paperless-AI: <http://localhost:3000>
- Paperless-GPT: <http://localhost:8080>

### 4. Stop the services

```bash
docker compose down
```

Or delete the containers and volumes manually:

```bash
docker compose down -v
```

## User Management

Create a superuser:

```bash
PASS=$(openssl rand -base64 32);
docker compose exec paperless-ngx python manage.py shell -c "from django.contrib.auth import get_user_model; User = get_user_model(); User.objects.filter(username='admin').delete()";
docker compose exec paperless-ngx python manage.py createsuperuser --username admin --email admin@example.com --noinput;
docker compose exec paperless-ngx bash -c "echo -e \"$PASS\n$PASS\" | python manage.py changepassword admin"
echo "Username: admin";
echo "Password: $PASS";
echo "Login at http://localhost:8000";
```

## Roadmap

- [ ] Add Gotenberg.
- [ ] Add Apache Tika.
- [ ] Add Docling.
