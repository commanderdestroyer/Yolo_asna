FROM python:3.12-slim

WORKDIR /app

# Install system dependencies
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
        ffmpeg \
        libgl1 \
        libglib2.0-0 \
    && rm -rf /var/lib/apt/lists/*

# Copy dependency file first for Docker layer caching
COPY requirement.txt .
# chi lay file requirement.txt từ build context tren may host roi
# copy vao thu muc hien tai trrong image/container tuc la WORKDIR
# sau khi copy xong thi /app/ chi co file requirement.txt empty
# chua he co cac dependencies vi may cai nay chua dc cai


# Install CPU-only PyTorch
RUN pip install --no-cache-dir \
    torch \
    torchvision \
    --index-url https://download.pytorch.org/whl/cpu

# Install application dependencies
RUN pip install --no-cache-dir -r requirement.txt
# dependencies se dc cai sau dong nay



# Copy application code and model
COPY . .

# Create a non-root user
RUN useradd --create-home --shell /bin/bash appuser \
    && chown -R appuser:appuser /app

USER appuser

EXPOSE 8000

# Container health check
HEALTHCHECK --interval=30s --timeout=10s --start-period=60s --retries=3 \
    CMD python -c "import urllib.request; urllib.request.urlopen('http://127.0.0.1:8000/health')" || exit 1

CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]

# viet copy requirement truoc khi copy ..
# docker layer caching
# docker co the cache:
#    Layer 1: Python base image
#    Layer 2L requirement
#    Layer 3: pip install dependencies
#    Layer 4: source code 
# neu sau nay sua file main.py ma khong sua requirement, Docker co the 
# dung lai layer 3 thay vi tai lai toan bo dependencies
