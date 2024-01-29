# 需要在根目录下执行docker build
# docker build -t python3.10-gunicorn-basic -f Dockerfile .

ARG PYTHON_VERSION="3.10"
FROM python:${PYTHON_VERSION} as runtime

ADD sources.list /etc/apt/

# hadolint ignore=DL3008
RUN apt-get update \
    && apt-get install -y --no-install-recommends \
    #netcat \
    libpq-dev \
    libgl1 \
    unixodbc-dev \
    g++ \
    libssl-dev \
    curl \
    net-tools \
    vim \
    && apt-get clean \
    && rm -rf /var/lib/apt/lists/*

# Install dependencies
RUN pip install -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com -U --no-cache-dir pip==23.0.1 \
    && export PATH="/root/.local/bin:$PATH" \
    && pip config set global.index-url https://mirrors.aliyun.com/pypi/simple/ \
    && pip install gunicorn==21.2.0