FROM python:3.12

WORKDIR /app

RUN pip install uv

COPY pyproject.toml uv.lock README.md ./
RUN uv sync --locked --no-dev --no-install-project

COPY src/ ./src/

RUN uv sync --locked --no-dev

EXPOSE 8000

CMD ["uv", "run", "gunicorn", \
     "-k", "uvicorn.workers.UvicornWorker", \
     "-w", "4", \
     "-b", "0.0.0.0:8000", \
     "app.main:app"]
