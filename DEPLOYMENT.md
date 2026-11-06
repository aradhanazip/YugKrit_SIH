# Deployment

YugKrit is a Flask/Python web application, not a static site. GitHub Pages cannot run its Flask server or database. The failed `pages build and deployment` run therefore cannot deploy this application.

## Deploy on Render

The repository includes a Render Blueprint (`render.yaml`) that defines the Flask web service and PostgreSQL database, connects the database to the service as `DATABASE_URL`, generates a production `SECRET_KEY`, and starts Gunicorn on Render's `$PORT`.

1. Sign in to Render and choose **New → Blueprint**.
2. Connect `aradhanazip/YugKrit_SIH`, select the `main` branch, and deploy the blueprint. Review Render's plan and any billing/expiration terms before confirming resource creation.
3. Set the WhatsApp Cloud API secrets on the web service (`WHATSAPP_PHONE_NUMBER_ID`, `WHATSAPP_ACCESS_TOKEN`, `WHATSAPP_TEMPLATE_NAME`, `WHATSAPP_TEMPLATE_LANGUAGE`, and optionally `WHATSAPP_DEFAULT_COUNTRY_CODE`). The blueprint selects `WHATSAPP_PROVIDER=cloud_api`; OTP delivery requires valid provider credentials. Never commit secrets to the repository.
4. Wait for the `/` health check to pass and use the service URL shown by Render.

GitHub repository changes cannot connect an external Render account, accept its resource creation/billing prompts, or configure WhatsApp credentials. GitHub Pages is controlled by repository settings and is separate from the Render service; disable Pages in **Settings → Pages** if you no longer want that failed static deployment to run.

## Local run

```bash
pip install -r requirements.txt
python app.py
```
