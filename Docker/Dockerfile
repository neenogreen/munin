FROM python:3.8-alpine
RUN apk upgrade --no-cache \
    && apk add --no-cache \
    py3-pip \
    musl \
    build-base \
    python3 \
    python3-dev \
    postgresql-dev \
    bash \
    git 

RUN apk add --no-cache libcurl
ENV PYCURL_SSL_LIBRARY=openssl

RUN cd /usr/bin \
    && ln -sf python3 python \
    && ln -sf pip3 pip


RUN git clone https://github.com/neenogreen/munin.git /opt/munin
RUN pip3 install -r /opt/munin/requirements.txt

RUN apk add --no-cache --virtual .build-deps build-base curl-dev \
    && pip install pycurl \
    && apk del --no-cache --purge .build-deps \
    && rm -rf /var/cache/* \
    && rm -rf /root/.cache/*

WORKDIR /opt/munin
EXPOSE 8088
CMD ["/opt/munin/munin.py", "--web", "-w", "8088"]