# Task Management System

## Quick Start

```bash
git clone <repo>
cd task-management-system
cp .env.sample .env
docker-compose up
```

## Overview

This project is a task management API built with Django and Django REST Framework. It is a containerized application using Docker and PostgreSQL as the database.

After running the "Quick Start" commands, the application will be available at `http://localhost:8000`.

## Admin Interface

The only available endpoint is the Django admin interface:

-   `http://localhost:8000/admin/`

To access the admin interface, you will first need to create a superuser:

```bash
docker-compose exec django-backend python manage.py createsuperuser
```
