# Deployment

This project is a **Flask/Python web application**, not a static site. GitHub Pages cannot run its Flask server or database. The failed `pages build and deployment` run is a Pages deployment timeout, so changing Pages files alone will not make the application deploy.

## Deploy on Render

The repository includes `render.yaml` and a `Procfile` for a Python web service.

1. In Render, choose **New → Blueprint**, connect `aradhanazip/YugKrit_SIH`, and deploy the blueprint from `main`.
2. Create a PostgreSQL database on Render (or use an existing PostgreSQL database), then set the web service's `DATABASE_URL` environment variable to its **internal connection URL**. The blueprint prompts for this value. PostgreSQL is needed because the app's local SQLite file is not durable across hosted service restarts/redeploys.
3. Set the WhatsApp Cloud API environment variables (`WHATSAPP_PHONE_NUMBER_ID`, `WHATSAPP_ACCESS_TOKEN`, `WHATSAPP_TEMPLATE_NAME`, `WHATSAPP_TEMPLATE_LANGUAGE`, and optionally `WHATSAPP_DEFAULT_COUNTRY_CODE`) in Render. The service uses `WHATSAPP_PROVIDER=cloud_api`; OTP signup/login delivery will not work until a valid provider is configured. Do not use console OTP mode in production.
4. Deploy and wait for the service health check at `/` to pass. Render supplies `$PORT`; Gunicorn binds to it. The app creates its tables and role/category catalog during startup.

Do **not** configure this Flask project as a GitHub Pages site. If Pages was enabled in repository settings, disable it or change its publishing source after the Render web service is set up. Repository commits cannot change the external hosting account or provider settings, so the Render connection, database, and WhatsApp secrets must be set in their respective dashboards.

## Local run

```bash
pip install -r requirements.txt
python app.py
```
