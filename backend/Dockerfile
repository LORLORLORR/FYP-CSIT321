# Use a slim Python image (works well on Railway)
FROM python:3.10-slim

# Install system dependency needed by LightGBM (OpenMP)
RUN apt-get update && apt-get install -y --no-install-recommends \
    libgomp1 \
 && rm -rf /var/lib/apt/lists/*

# Set working directory
WORKDIR /app

# Install Python dependencies
COPY requirements.txt .
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of your backend code
COPY . .

# Railway listens on PORT env var, default to 8080
ENV PORT=8080

# Start your Flask app via gunicorn
CMD ["gunicorn", "-b", "0.0.0.0:8080", "app:app"]
