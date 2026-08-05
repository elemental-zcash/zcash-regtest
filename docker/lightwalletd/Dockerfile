FROM golang:1.25 AS lightwalletd_base

RUN git clone https://github.com/zcash/lightwalletd.git \
      /go/src/github.com/zcash/lightwalletd \
    && cd /go/src/github.com/zcash/lightwalletd \
    && git checkout 5ef221e

WORKDIR /go/src/github.com/zcash/lightwalletd

RUN make \
  && /usr/bin/install -c ./lightwalletd /usr/local/bin/ \
  && mkdir -p /var/lib/lightwalletd/db \
  && chown 2002:2002 /var/lib/lightwalletd/db

ARG LWD_USER=lightwalletd
ARG LWD_UID=2002

RUN useradd --home-dir "/srv/$LWD_USER" \
            --shell /bin/bash \
            --create-home \
            --uid "$LWD_UID" \
            "$LWD_USER"

WORKDIR "/srv/$LWD_USER"

ENTRYPOINT ["lightwalletd"]
CMD ["--help"]

