# Используйте базовый образ NiFi
FROM apache/nifi:1.16.2

USER root

RUN apt-get update && \
    apt-get install -y \
    wget \
    build-essential \
    smbclient \
    unixodbc \
    unixodbc-dev \
    zlib1g-dev \
    libncurses5-dev \
    libgdbm-dev \
    libnss3-dev \
    libssl-dev \
    libreadline-dev \
    libffi-dev \
    libsqlite3-dev \
    libbz2-dev \
    vim \
    gcc \
    make && \
    wget https://www.python.org/ftp/python/3.10.0/Python-3.10.0.tgz && \
    tar -xf Python-3.10.0.tgz && \
    cd Python-3.10.0 && \
    ./configure --enable-optimizations && \
    make -j $(nproc) && \
    make altinstall && \
    cd .. && \
    rm -rf Python-3.10.0 Python-3.10.0.tgz && \
    apt-get remove --purge -y \
    wget \
    sudo \
    build-essential && \
    apt-get autoremove -y && \
    rm -rf /var/lib/apt/lists/*

COPY requirements/ /requirements/

RUN /usr/local/bin/python3.10 -m pip install --upgrade pip

# Установите необходимые Python пакеты
RUN pip3.10 install --no-cache-dir -r /requirements/requirements.txt

# Установите точку входа
ENTRYPOINT ["bash", "-c"]
