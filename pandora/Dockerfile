FROM python:2.7-slim-buster

ENV DEBIAN_FRONTEND=noninteractive

RUN printf 'deb http://archive.debian.org/debian buster main\n' > /etc/apt/sources.list \
    && printf 'deb http://archive.debian.org/debian-security buster/updates main\n' >> /etc/apt/sources.list \
    && printf 'Acquire::Check-Valid-Until "false";\n' > /etc/apt/apt.conf.d/99archive \
    && apt-get update -o Acquire::Check-Valid-Until=false \
    && apt-get install -y --no-install-recommends \
        build-essential \
        ca-certificates \
        git \
        libffi-dev \
    && rm -rf /var/lib/apt/lists/*

WORKDIR /opt/pdf

COPY ./pdfscan.py /tmp/pdfscan.py

RUN git clone --depth 1 https://github.com/malice-plugins/pdf.git /opt/pdf \
    && cp /tmp/pdfscan.py /opt/pdf/pdfscan.py \
    && pip install --no-cache-dir --upgrade pip wheel \
    && pip install --no-cache-dir -r requirements.txt \
    && mkdir -p /malware/dump

EXPOSE 3993

ENTRYPOINT ["python", "/opt/pdf/pdfscan.py"]
CMD ["web"]
