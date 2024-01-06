# Stage 1: Python 
FROM python:3

ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONUNBUFFERED 1

WORKDIR /app

COPY requirements.txt /app/

RUN pip install --upgrade pip

RUN python -m pip install --no-cache-dir -r requirements.txt

COPY . /app/

# Collect static files
RUN python manage.py collectstatic --noinput

# Run Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8080", "swapna_django_project.wsgi:application"]

# Stage 2: PostgreSQL Database
FROM postgres:14.10

ENV POSTGRES_DB=swapproject
ENV POSTGRES_USER=swapna
ENV POSTGRES_PASSWORD=swapna12

# Stage 3: Nginx
FROM nginx:1.19

WORKDIR /etc/nginx

COPY . .

# Expose port 8080 to the outside world
EXPOSE 8080

# Start Nginx when the container starts
CMD ["/usr/sbin/nginx", "-g", "daemon off;"]















