FROM python:3.10-slim-bookworm
ENV FLASK_RUN_HOST=0.0.0.0

WORKDIR /
RUN adduser --uid 1000 --disabled-password app

RUN apt-get update && apt-get install -y gcc build-essential libpcre3-dev && pip install --no-cache-dir pipenv && rm -rf /var/lib/apt/lists/*

COPY Pipfile* /app/
RUN cd /app && pipenv install --system --deploy

COPY . /app

CMD uwsgi --http :5000 --master --enable-threads --htto :5000 --manage-script-name --mount /=app:app
