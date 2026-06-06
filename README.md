# Django Poll App

![Python](https://img.shields.io/badge/Python-3.11-blue)
![Django](https://img.shields.io/badge/Django-5.2.13-092E20)
![SQLite](https://img.shields.io/badge/Database-SQLite-003B57)
![Status](https://img.shields.io/badge/Status-Learning%20Project-brightgreen)
![License](https://img.shields.io/badge/License-MIT-lightgrey)

A clean, beginner-friendly polling web application built with Django. The project lets users view poll questions, select an answer, submit a vote, and see live vote results. It also includes Django Admin support for managing questions and choices from a secure admin dashboard.

This project was built as a practical introduction to Django's model-view-template workflow, database-backed web development, URL routing, form handling, CSRF protection, admin customization, and automated testing.

---

## Table of Contents

- [Project Overview](#project-overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [System Architecture](#system-architecture)
- [Project Structure](#project-structure)
- [Installation Guide](#installation-guide)
- [Application Routes](#application-routes)
- [Database Design](#database-design)
- [Security Implementation](#security-implementation)
- [Testing](#testing)
- [Learning Journey](#learning-journey)
- [Challenges and Solutions](#challenges-and-solutions)
- [Screenshots](#screenshots)
- [Future Enhancements](#future-enhancements)
- [Resume Impact](#resume-impact)
- [Recruiter Highlights](#recruiter-highlights)

---

## Project Overview

The Django Poll App solves a simple but real web development problem: collecting votes from users and displaying results in a structured way. Although the application is intentionally small, it demonstrates the same backend patterns used in larger production systems.

Users can:

- Browse available poll questions.
- Open a poll detail page.
- Select one option from multiple choices.
- Submit a vote securely using a POST request.
- View updated voting results.
- Manage questions and choices through Django Admin.

This project is useful for:

- Students learning Django.
- Beginners practicing backend development.
- Developers reviewing Django's official polls workflow.
- Recruiters evaluating core web development fundamentals.
- Anyone learning how server-rendered applications connect views, templates, models, and a database.

### Real-World Use Cases

- Classroom voting systems.
- Event feedback collection.
- Internal team decision polls.
- Product preference surveys.
- Lightweight community polls.

---

## Features

| Feature | Beginner-Friendly Explanation | Technical Explanation | Benefit |
|---|---|---|---|
| Poll listing | Shows all recent poll questions. | Uses Django `ListView` to query and render recent `Question` records. | Keeps the home page simple and dynamic. |
| Poll detail page | Lets users choose an answer. | Uses Django `DetailView` and template rendering for a selected question. | Separates poll display from voting logic. |
| Vote submission | Saves the user's selected answer. | Handles POST data, validates choice selection, increments vote count, and redirects. | Prevents duplicate form resubmission and improves user flow. |
| Results page | Shows vote counts for each choice. | Uses a detail template to display related `Choice` records. | Gives immediate feedback after voting. |
| Django Admin | Lets admins create and edit polls. | Registers `Question` with inline `Choice` editing using `StackedInline`. | Makes content management easy without building a custom dashboard. |
| Automated test | Checks model behavior. | Uses Django `TestCase` to verify `was_published_recently()` for future questions. | Protects important business logic from regressions. |
| Static CSS | Adds basic styling support. | Uses Django static files with `polls/style.css`. | Demonstrates frontend asset handling in Django. |

---

## Tech Stack

| Technology | What It Is | Why It Was Chosen | How It Is Used |
|---|---|---|---|
| Python 3.11 | A high-level programming language. | Readable, beginner-friendly, and widely used for backend development. | Powers the application logic, models, views, and tests. |
| Django 5.2.13 | A full-stack Python web framework. | Provides routing, ORM, templates, admin, forms, security, and testing tools. | Handles the backend, page rendering, database operations, and admin dashboard. |
| SQLite | A lightweight relational database. | Simple setup with no external database server required. | Stores poll questions, choices, and vote counts. |
| Django ORM | Django's object-relational mapper. | Allows database work through Python classes instead of raw SQL. | Defines `Question` and `Choice` models and relationships. |
| Django Templates | Server-side HTML rendering system. | Keeps HTML separate from Python logic. | Renders poll list, detail, and result pages. |
| HTML/CSS | Core frontend technologies. | Required for displaying web pages in the browser. | Builds forms, links, result lists, and basic styling. |
| Django Admin | Built-in administration interface. | Speeds up data management for backend projects. | Creates and manages polls from `/admin/`. |

---

## System Architecture

This is a server-rendered Django application using the Model-View-Template pattern.

```text
Browser
   |
   | HTTP request
   v
Django URL Router
   |
   v
View / Class-Based View
   |
   v
Django ORM
   |
   v
SQLite Database
   |
   v
Template Rendering
   |
   v
HTML Response to Browser
```

### Data Flow

1. A user opens `/polls/`.
2. Django routes the request to `IndexView`.
3. `IndexView` queries the latest `Question` records.
4. Django renders `polls/index.html`.
5. The user selects a question and opens its detail page.
6. The user submits a vote through a POST request.
7. The `vote()` view validates the selected choice.
8. The selected choice's vote count increases by one.
9. The user is redirected to the results page.

### Backend Workflow

- `mysite/urls.py` includes the `polls` app routes.
- `polls/urls.py` maps URLs to views.
- `polls/views.py` contains class-based views and vote handling.
- `polls/models.py` defines the database schema.
- `polls/admin.py` configures Django Admin.

### Frontend Workflow

- Templates live in `polls/templates/polls/`.
- `index.html` displays available polls.
- `detail.html` renders a voting form.
- `results.html` displays vote totals.
- Static styling is loaded from `polls/static/polls/style.css`.

### Database Workflow

- `Question` records represent poll questions.
- `Choice` records represent options for a question.
- Each `Choice` belongs to one `Question`.
- Vote counts are stored in the `votes` field.

### Authentication Workflow

The public poll pages do not require authentication. Authentication is handled by Django Admin for staff users:

1. Admin visits `/admin/`.
2. Django displays the admin login page.
3. Credentials are checked against Django's user system.
4. Authenticated staff users can create and update polls.

### API Workflow

This project does not expose a REST API. It uses traditional server-rendered Django routes. Each route returns HTML or redirects after form submission.

---

## Project Structure

```text
poll_app/
├── .gitignore
├── README.md
├── html_profile/
├── mysite/
│   ├── db.sqlite3
│   ├── manage.py
│   ├── mysite/
│   │   ├── __init__.py
│   │   ├── asgi.py
│   │   ├── settings.py
│   │   ├── urls.py
│   │   └── wsgi.py
│   └── polls/
│       ├── admin.py
│       ├── apps.py
│       ├── models.py
│       ├── tests.py
│       ├── urls.py
│       ├── views.py
│       ├── migrations/
│       ├── static/
│       │   └── polls/
│       │       └── style.css
│       └── templates/
│           └── polls/
│               ├── index.html
│               ├── detail.html
│               └── results.html
└── venv/
```

### Important Files

| File / Folder | Responsibility |
|---|---|
| `mysite/manage.py` | Command-line entry point for running Django tasks. |
| `mysite/mysite/settings.py` | Main Django configuration file. |
| `mysite/mysite/urls.py` | Project-level URL routing. |
| `mysite/polls/models.py` | Defines `Question` and `Choice` database models. |
| `mysite/polls/views.py` | Contains page logic for listing, detail, results, and voting. |
| `mysite/polls/urls.py` | App-level URL patterns for the polls feature. |
| `mysite/polls/admin.py` | Registers models and customizes Django Admin. |
| `mysite/polls/tests.py` | Contains automated tests for model behavior. |
| `mysite/polls/templates/polls/` | Stores HTML templates for the app. |
| `mysite/polls/static/polls/style.css` | Stores CSS used by poll templates. |
| `.gitignore` | Excludes virtual environment, database, cache files, and environment files from Git. |

---

## Development Process

| Step | Work Completed |
|---|---|
| 1. Planning | Defined a simple poll system with questions, choices, voting, and results. |
| 2. Research | Studied Django project structure, URL routing, templates, models, and admin. |
| 3. Environment Setup | Created a Python virtual environment and installed Django. |
| 4. Backend Development | Created the `polls` app, models, views, and URL routes. |
| 5. Frontend Development | Built templates for poll listing, detail form, and result display. |
| 6. Database Integration | Used Django migrations and SQLite to persist poll data. |
| 7. Testing | Added a model test for recent publication logic. |
| 8. Deployment Preparation | Added Git ignore rules and documented setup steps for GitHub. |

---

## Installation Guide

### Prerequisites

Make sure you have:

- Python 3.11 or newer
- Git
- PowerShell, Command Prompt, or a terminal

### Clone Repository

```bash
git clone https://github.com/your-username/django-poll-app.git
cd django-poll-app
```

### Create and Activate Virtual Environment

Windows PowerShell:

```powershell
python -m venv venv
.\venv\Scripts\Activate.ps1
```

macOS / Linux:

```bash
python3 -m venv venv
source venv/bin/activate
```

### Install Dependencies

If a `requirements.txt` file is added:

```bash
pip install -r requirements.txt
```

For the current project, install Django directly:

```bash
pip install Django==5.2.13
```

### Configure Environment Variables

This learning version currently keeps development settings in `settings.py`. For production, move sensitive values into environment variables:

```env
SECRET_KEY=your-secret-key
DEBUG=False
ALLOWED_HOSTS=your-domain.com
```

### Run Database Migrations

```bash
cd mysite
python manage.py migrate
```

### Create Admin User

```bash
python manage.py createsuperuser
```

### Run Development Server

```bash
python manage.py runserver
```

Open the app:

```text
http://127.0.0.1:8000/polls/
```

Open Django Admin:

```text
http://127.0.0.1:8000/admin/
```

### Verify Installation

Run tests:

```bash
python manage.py test polls
```

Expected result:

```text
OK
```

---

## Application Routes

Because this is a server-rendered Django app, these are HTML routes instead of JSON API endpoints.

| Route | Method | Purpose | Parameters | Response |
|---|---|---|---|---|
| `/polls/` | GET | Display latest poll questions. | None | HTML page with poll list. |
| `/polls/<id>/` | GET | Display a single poll and choices. | `id` or `pk`: Question ID | HTML voting form. |
| `/polls/<id>/vote/` | POST | Submit a selected choice. | `question_id`, POST field `choice` | Redirect to results page. |
| `/polls/<id>/results/` | GET | Display vote totals. | `id` or `pk`: Question ID | HTML results page. |
| `/admin/` | GET/POST | Django Admin login and management. | Admin credentials | Admin dashboard. |

### Example Vote Request

```http
POST /polls/1/vote/ HTTP/1.1
Content-Type: application/x-www-form-urlencoded

choice=3
```

### Example Vote Response

```http
HTTP/1.1 302 Found
Location: /polls/1/results/
```

### Example Results Output

```text
Favorite programming language?

Python -- 10 votes
JavaScript -- 4 votes
Java -- 2 votes
```

---

## Database Design

### Tables

#### Question

| Field | Type | Description |
|---|---|---|
| `id` | AutoField / BigAutoField | Primary key. |
| `question_text` | CharField | Poll question text, maximum 200 characters. |
| `pub_date` | DateTimeField | Date and time when the question was published. |

#### Choice

| Field | Type | Description |
|---|---|---|
| `id` | AutoField / BigAutoField | Primary key. |
| `question_id` | ForeignKey | Links each choice to a question. |
| `choice_text` | CharField | Choice text, maximum 200 characters. |
| `votes` | IntegerField | Number of votes received. |

### Relationship

```text
Question 1 ---- many Choice
```

One question can have many choices. Each choice belongs to exactly one question. When a question is deleted, its related choices are deleted automatically because the model uses `on_delete=models.CASCADE`.

---

## Security Implementation

| Area | Current Implementation |
|---|---|
| CSRF Protection | Voting form uses `{% csrf_token %}` to protect POST requests. |
| Authentication | Django Admin uses Django's built-in authentication system. |
| Authorization | Only staff/admin users can access admin management screens. |
| Password Encryption | Django hashes admin passwords automatically. |
| Environment Variables | Recommended for production secrets, but not yet fully implemented in this learning version. |
| API Security | No public JSON API is exposed; voting is handled through server-rendered POST requests. |
| SQL Injection Protection | Django ORM parameterizes database operations. |

---

## Testing

The project includes a Django test case for model behavior.

```bash
python manage.py test polls
```

### Unit Testing

- Tests `Question.was_published_recently()`.
- Verifies future-dated questions are not treated as recently published.

### Integration Testing

Recommended next steps:

- Test poll list page response.
- Test detail page behavior.
- Test vote submission.
- Test result page vote count changes.

### Manual Testing Checklist

- Start the development server.
- Open `/polls/`.
- Create a question and choices in `/admin/`.
- Confirm the question appears on the poll list.
- Submit a vote.
- Confirm vote count increases on the results page.

---

## Learning Journey

### What I Learned

- How Django projects and apps are organized.
- How URL routing connects browser requests to Python views.
- How Django models map Python classes to database tables.
- How migrations create and update database structure.
- How templates render dynamic HTML.
- How forms submit data through POST requests.
- How CSRF protection secures form submissions.
- How Django Admin can manage backend data quickly.
- How automated tests protect important logic.

### Technical Concepts Practiced

- Model-View-Template architecture.
- Class-based views.
- Foreign key relationships.
- Server-side rendering.
- Form validation.
- Redirect-after-POST pattern.
- Admin customization.
- Test-driven thinking.

---

## Challenges and Solutions

| Challenge | Cause | Solution | Outcome |
|---|---|---|---|
| Understanding Django project structure | Django separates project settings and app logic into different folders. | Studied the role of `mysite/` and `polls/` separately. | Clear understanding of project-level vs app-level responsibilities. |
| Connecting URLs to views | Routes must be defined in both project and app URL files. | Used `include("polls.urls")` in the project router. | Clean modular routing for the polls app. |
| Handling vote submission | User input arrives through `request.POST`. | Read the selected `choice`, handled missing choices, and redirected after saving. | Reliable voting flow with user-friendly error handling. |
| Managing related choices | Choices must belong to a question. | Used a `ForeignKey` from `Choice` to `Question`. | Each poll can have multiple answer options. |
| Avoiding future-date logic bugs | Future questions should not appear as recently published. | Added date validation in `was_published_recently()`. | More accurate model behavior. |
| Running the app correctly | Static servers like Live Server cannot run Django backend code. | Used `python manage.py runserver` and opened port `8000`. | Full Django app runs with routes, templates, and database. |

---

## Performance Optimizations

- Uses database ordering with `order_by("-pub_date")` to fetch recent polls efficiently.
- Limits the poll list to five questions to keep the home page lightweight.
- Uses Django's ORM instead of manual SQL for safer and maintainable database access.
- Uses redirect-after-POST to prevent accidental duplicate vote submissions on browser refresh.
- Keeps templates simple and fast to render.

---

## Screenshots

Add screenshots inside a `screenshots/` folder and update the paths below.

### Home Page

![Home Page]<img width="371" height="109" alt="Screenshot 2026-06-06 183255" src="https://github.com/user-attachments/assets/768bbe41-db13-49aa-b0bf-0aae7d29008b" />


### Poll Detail Page

![Poll Detail Page]<img width="211" height="106" alt="Screenshot 2026-06-06 173505" src="https://github.com/user-attachments/assets/f1f366f4-e69b-49a9-afa8-aeccff48d2dd" />
<img width="111" height="59" alt="Screenshot 2026-06-06 173534" src="https://github.com/user-attachments/assets/fd295540-ec14-460f-9963-1014b77eefb2" />
<img width="283" height="355" alt="Screenshot 2026-06-06 172932" src="https://github.com/user-attachments/assets/fd470acb-d0de-46c6-9c16-ad72b1f23627" />



### Admin Login Page

![Admin Login Page]<img width="857" height="427" alt="Screenshot 2026-06-06 172256" src="https://github.com/user-attachments/assets/f6a9d724-5c9c-48c2-bbf4-5122e1abbc76" />


### Admin Dashboard<img width="604" height="235" alt="Screenshot 2026-06-06 172327" src="https://github.com/user-attachments/assets/0a307f01-5cb3-401a-8372-db0f04e2443d" />


![Admin Dashboard]<img width="922" height="421" alt="Screenshot 2026-06-06 172514" src="https://github.com/user-attachments/assets/3206343b-b7af-4fcc-9b53-aa1bfe2522fb" />
<img width="922" height="421" alt="Screenshot 2026-06-06 172514" src="https://github.com/user-attachments/assets/721e33ad-c377-4f1e-9f74-ea5f76a82032" />


### Results Page

![Results Page]<img width="111" height="59" alt="Screenshot 2026-06-06 173534" src="https://github.com/user-attachments/assets/8b88505f-22f6-427d-af83-9c106d5b3c0b" />


### Architecture Diagram

![Architecture Diagram]<img width="1637" height="960" alt="poll app architecture" src="https://github.com/user-attachments/assets/9fa7f34c-1a4d-4130-8fc0-e4a80a356c20" />


---

## Deployment

This project currently runs as a local Django development app. For production deployment, consider:

- Set `DEBUG=False`.
- Move `SECRET_KEY` to environment variables.
- Configure `ALLOWED_HOSTS`.
- Use PostgreSQL or another production-ready database.
- Configure static file hosting with WhiteNoise, Nginx, or cloud storage.
- Run the app with Gunicorn or uWSGI.
- Deploy to Render, Railway, PythonAnywhere, Fly.io, or a VPS.

Example production preparation:

```bash
python manage.py collectstatic
python manage.py migrate
```

---
