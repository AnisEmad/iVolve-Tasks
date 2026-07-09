FROM python:3.13

WORKDIR /app

RUN groupadd -r appgroup && useradd -r -g appgroup appuser
COPY . .

RUN pip install -r requirements.txt

EXPOSE 5000

USER appuser

CMD ["python", "app.py"]