FROM resin/rpi-raspbian:wheezy

RUN apt-get update && apt-get install -y --no-install-recommends \
    curl \
    g++ \
    gcc \
    libc6-dev \
    make \
    pkg-config \
	&& rm -rf /var/lib/apt/lists/*

ENV GOLANG_VERSION 1.7.3
ENV GOLANG_DOWNLOAD_URL https://golang.org/dl/go$GOLANG_VERSION.linux-armv6l.tar.gz
ENV GOLANG_DOWNLOAD_SHA256 d02912d121e1455e775a5aa4ecdb2a04f8483ba846e6d2341e1f35b8e507d7b5

RUN curl -fsSL "$GOLANG_DOWNLOAD_URL" -o golang.tar.gz \
	&& echo "$GOLANG_DOWNLOAD_SHA256  golang.tar.gz" | sha256sum -c - \
	&& tar -C /usr/local -xzf golang.tar.gz \
	&& rm golang.tar.gz

ENV GOPATH /go
ENV PATH $GOPATH/bin:/usr/local/go/bin:$PATH

RUN mkdir -p "$GOPATH/src" "$GOPATH/bin" && chmod -R 777 "$GOPATH"
WORKDIR $GOPATH

COPY go-wrapper /usr/local/bin/
