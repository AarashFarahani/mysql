# MySQL Docker Setup

## Directory structure

```
mysql/
├── docker-compose.yml   # Compose config
├── .env                 # Credentials (do NOT commit)
├── config/
│   └── my.cnf          # MySQL server config (mounted read-only)
├── data/               # MySQL data directory (persisted on host)
└── initdb/             # Optional init scripts (.sql / .sh), run once on first start
```

## Usage

```bash
# Start
docker compose up -d

# Stop
docker compose down

# Stop and remove data volume (destructive!)
docker compose down -v

# View logs
docker compose logs -f mysql

# Open MySQL shell
docker compose exec mysql mysql -u root -p
```

## Notes
- Edit `.env` to set your passwords and database name before first run.
- Place any `*.sql` or `*.sh` init scripts in `initdb/` — they run automatically on the very first startup (when `data/` is empty).
- `data/` is gitignored by convention; add it to your `.gitignore`.
- `config/my.cnf` is mounted read-only; edit on the host and restart the container to apply changes.
- MySQL 8.4 keeps `mysql_native_password` disabled by default; this project enables it in `config/my.cnf` for older clients such as Seafile.
