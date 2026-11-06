# YugKrit — "From Problems to Solutions"

YugKrit is a societal innovation and collaboration platform that connects Government, Universities, ULBs/NGOs, Students, and Citizens. It is a Flask application with a SQLAlchemy database, Jinja templates, and static assets.

## Deployment

This application requires a Python web host and a database; GitHub Pages cannot run the Flask server. A Render Blueprint is provided in `render.yaml` to define the web service and PostgreSQL database. Follow [`DEPLOYMENT.md`](DEPLOYMENT.md) to deploy it.

## Local setup

Requires Python 3.10+ and pip.

```bash
python -m venv venv
# Windows: venv\\Scripts\\activate
source venv/bin/activate
pip install -r requirements.txt
python app.py
```

Open http://127.0.0.1:5000. Configure production secrets and database values in the hosting provider's environment settings; do not commit `.env` or credentials.

See the rest of this repository's documentation for features, account flows, tests, and database details.
