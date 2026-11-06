DYNATRACE ALERT TRACKER — NO-LOGIN SHARED TEAM VERSION
=====================================================

- Shared PostgreSQL database via Neon when DATABASE_URL is configured.
- No login or password required. Anyone with the site URL can view, add, edit, and delete alerts.
- Optional name fields record who entered/updated an alert (self-reported).
- Records page refreshes every 15 seconds.

SECURITY WARNING
This is intentionally public/no-login. Anyone who obtains the URL can change or delete records. Do not store sensitive data. Use only in a trusted environment.

LOCAL RUN (Windows PowerShell)
1. Install Python 3.11 or newer.
2. Open PowerShell in this project folder (the folder containing manage.py).
3. Run each command separately:
   py -m venv .venv
   .\.venv\Scripts\Activate.ps1
   python -m pip install -r requirements.txt
   python manage.py migrate
   python manage.py runserver
4. Open http://127.0.0.1:8000/

If PowerShell blocks activation, run this once in the same terminal:
   Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
Then activate the environment again.

NEON + VERCEL DEPLOYMENT
1. Create a PostgreSQL project at https://neon.tech/ and copy its pooled connection string.
2. In Vercel, open the project serving your alert site and add Production environment variables:
   DATABASE_URL = your Neon pooled connection string
   DJANGO_SECRET_KEY = a long random secret
   DJANGO_DEBUG = False
3. Commit and push the contents of this project folder to the GitHub repository connected to Vercel.
4. Redeploy the existing Vercel project.
5. Run migrations against Neon once from a local terminal, setting DATABASE_URL to the Neon direct connection string first:
   $env:DATABASE_URL = "YOUR_NEON_DIRECT_CONNECTION_STRING"
   python manage.py migrate

Do not paste database passwords into chat or commit them to GitHub.
