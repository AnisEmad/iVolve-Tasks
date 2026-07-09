FROM python:3.13-alpine

WORKDIR /app

RUN addgroup -S appgroup && adduser -S appuser -G appgroup

COPY . .

RUN pip install -r requirements.txt

EXPOSE 5000

USER appuser

CMD ["python", "app.py"]