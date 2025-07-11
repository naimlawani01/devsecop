FROM python:3.9-alpine

# Install system dependencies
RUN apk add --no-cache gcc musl-dev libffi-dev

# set environment variables
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

# Create app directory
WORKDIR /app

# Copy requirements first for better caching
COPY requirements.txt .

# Install python dependencies
RUN pip install --no-cache-dir --upgrade pip && \
    pip install --no-cache-dir -r requirements.txt && \
    # Clean up
    apk del gcc musl-dev libffi-dev && \
    rm -rf /var/cache/apk/*

# Copy application code
COPY . .

EXPOSE 5000

CMD ["python", "run.py"] 