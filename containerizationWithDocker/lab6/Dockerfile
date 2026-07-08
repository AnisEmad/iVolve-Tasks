FROM python:3.13-alpine

WORKDIR /app

COPY app.py .

RUN pip install flask

ENV APP_MODE=production
ENV APP_REGION=canada-west

EXPOSE 8080

CMD ["python", "app.py"]