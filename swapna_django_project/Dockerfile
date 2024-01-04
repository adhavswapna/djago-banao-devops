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

EXPOSE 8080

# Run Gunicorn
CMD ["gunicorn", "--bind", "0.0.0.0:8000", "swapna_django_project.wsgi:application"]
