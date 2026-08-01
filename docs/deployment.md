# Deployment

## Render Blueprint path

`render.yaml` defines:

- Docker web service `groe-beta`
- Free Singapore-region instance for beta
- PostgreSQL 18 database `groe-db`
- Automatic database URL injection
- Generated JWT secret
- Health-check path
- Keyless Open-Meteo endpoints

The Docker `CMD` executes `backend/scripts/start.sh`, which runs:

1. `alembic upgrade head`
2. idempotent `python scripts/seed.py`
3. Uvicorn on Render’s `$PORT`

## GitHub rules

The repository files must sit directly below one `groe/` root. The root must contain `render.yaml` and `Dockerfile`; no folder restructuring or build-command edits are required.

## Free database warning

Render free PostgreSQL instances are intended for previews and expire after the platform’s free-database retention period. Upgrade to a paid database before keeping irreplaceable user data.

## Production upgrade checklist

- Upgrade PostgreSQL to a persistent paid plan.
- Add centralized rate limiting if scaling to multiple web instances.
- Review CORS if hosting a separate frontend origin.
- Replace provisional agronomy fields after expert review.
- Add database backups and operational monitoring.
- Configure a real AI provider only after privacy, safety and cost review.
