FROM python:3.11-slim

WORKDIR /app

# Install dependencies including bsdtar
RUN apt-get update && \
    apt-get install -y \
    git \
    libarchive-tools \
    curl && \
    rm -rf /var/lib/apt/lists/*

# Copy codebase (will be checked out to correct commit by CI)
COPY codebase/ .

# Install requirements
RUN pip install --upgrade pip && \
    sed -i 's/protobuf==3.20/protobuf>=3.20/' requirements.txt && \
    sed -i 's/^pyautogen$/pyautogen==0.2.35/' requirements.txt && \
    sed -i 's/^anthropic>=0.18.1$/anthropic==0.18.1/' requirements.txt && \
    pip install --no-cache-dir -r requirements.txt && \
    pip install --no-cache-dir py7zr

CMD ["python", "main.py"]