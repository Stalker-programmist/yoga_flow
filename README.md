Yoga on Telegram — FastAPI app

Overview
- Sells subscriptions to Telegram-based yoga courses. Users can register/login, pick a plan, submit a consultation request, and create a pending subscription (payment stub).

Quickstart
- Python 3.10+
- Install: `pip install fastapi uvicorn[standard] jinja2 python-multipart passlib[bcrypt] itsdangerous pydantic-settings pillow`
- Run: `uvicorn app.main:app --reload`
- Open: http://localhost:8000

Environment
- Copy `.env.example` to `.env` or create `.env` in project root:

  SECRET_KEY=change_me
  ENV=dev
  BASE_URL=http://localhost:8000

Project structure
- app/: FastAPI app with routes and helpers
- templates/: Jinja2 templates (pages + partials)
- static/: CSS/JS assets
- data/: JSON storage files (users, plans, subscriptions, consultations)

Routes
- GET / → home (hero, how-it-works, benefits, consultation form + inline pricing)
- GET /pricing → pricing page with plan cards
- GET /dashboard → user dashboard (requires login)
- GET /auth/login, /auth/register → forms
- POST /auth/login, /auth/register, /auth/logout
- POST /consult → saves consultation and redirects with flash
- POST /subscribe → creates pending subscription, redirects to dashboard
- GET /api/plans → returns data/plans.json

Notes
- Passwords: bcrypt via passlib
- Sessions: signed cookie via itsdangerous (HttpOnly, SameSite=Lax; Secure in prod)
- JSON storage is file-based; for production use a DB.
- Minimal validation for email/phone in `app/api/validators.py`.

Next steps (TODO)
- Payment gateway integration
- Telegram invites/link generation
- CSRF token for forms, rate limiting for login
