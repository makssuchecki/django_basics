# Django Polls App

A basic polls application built by following the official [Django tutorial](https://docs.djangoproject.com/en/6.1/intro/tutorial01/). Users can view published poll questions, vote on choices, and see results. Poll questions and choices are managed through the Django admin site.

## Features

- List view of the latest published poll questions
- Detail view for voting on a question's choices
- Results view showing vote counts per choice
- Questions with a future `pub_date` are hidden from the public site
- Full Django admin integration for creating/editing questions and choices (with inline choice editing)
- Unit tests covering model logic and view behavior

## Tech Stack

- Python 3.12
- Django 6.1
- SQLite (default development database)

## Project Structure

```
djangotutorial/
├── manage.py
├── db.sqlite3
├── mysite/            # Project configuration
│   ├── settings.py
│   ├── urls.py
│   └── wsgi.py / asgi.py
├── polls/              # Polls app
│   ├── models.py       # Question and Choice models
│   ├── views.py         # IndexView, DetailView, ResultsView, vote
│   ├── urls.py
│   ├── admin.py
│   ├── tests.py
│   ├── migrations/
│   ├── static/polls/
│   └── templates/polls/
└── templates/admin/    # Custom admin base template
```

## Setup

### 1. Clone the repository

```bash
git clone <repository-url>
cd djangotutorial
```

### 2. Create and activate a virtual environment

**Windows:**
```bash
python -m venv venv
venv\Scripts\activate
```

**macOS/Linux:**
```bash
python3 -m venv venv
source venv/bin/activate
```

### 3. Install dependencies

```bash
pip install django
```

### 4. Apply migrations

```bash
python manage.py migrate
```

### 5. Create a superuser (for admin access)

```bash
python manage.py createsuperuser
```

### 6. Run the development server

```bash
python manage.py runserver
```

The app will be available at http://127.0.0.1:8000/polls/, and the admin site at http://127.0.0.1:8000/admin/.

## Usage

1. Log into the admin site and add a few `Question` objects, each with a publish date and at least two `Choice` objects.
2. Visit `/polls/` to see the list of published questions.
3. Click a question to vote on one of its choices.
4. After voting, you're redirected to the results page showing the vote tally.

## Running Tests

```bash
python manage.py test polls
```

Tests cover:
- `Question.was_published_recently()` for future, old, and recent dates
- Index view filtering of past vs. future questions
- Detail view 404 behavior for future questions

## Notes

- `DEBUG = True` and the `SECRET_KEY` in `mysite/settings.py` are development defaults only — do not use them in production.
- `db.sqlite3` is used for local development and is excluded from version control via `.gitignore`.
