FROM cgr.dev/chainguard/python:latest-dev AS builder
WORKDIR /app
ADD https://github.com/badtuxx/giropops-senhas.git /app
RUN python -m venv venv
ENV PATH=/app/venv/bin:$PATH
RUN pip install --upgrade pip && pip install -r requirements.txt && pip install requests

FROM cgr.dev/chainguard/python:latest
WORKDIR /app 
COPY --from=builder /app /app
ENV PATH=/app/venv/bin:$PATH
EXPOSE 5000
ENTRYPOINT [ "flask" ,"run", "--host=0.0.0.0"]
HEALTHCHECK --interval=30s --timeout=10s --start-period=10s --retries=3 CMD ["python", "-c", "import requests; exit(0) if requests.get('http://127.0.0.1:5000').status_code == 200 else exit(1)"]