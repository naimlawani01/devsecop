# Build stage
FROM node:18-alpine AS build

WORKDIR /app

# Copy package files
COPY package*.json ./

# Install dependencies including webpack-cli
RUN npm install

# Copy source code
COPY . .

# Build assets
RUN npm run build

# Production stage
FROM python:3.11.5-alpine

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

# Copy built assets from build stage
COPY --from=build /app/static/dist ./static/dist

# Manage Assets & DB 
RUN python manage.py collectstatic --no-input && python manage.py makemigrations && python manage.py migrate

# gunicorn
CMD ["gunicorn", "--config", "gunicorn-cfg.py", "core.wsgi"]
