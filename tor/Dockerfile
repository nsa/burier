# build tor from source code
FROM ubuntu:16.04 as builder
ENV DEBIAN_FRONTEND=noninteractive

RUN apt-get update && \
	apt-get install -y git

WORKDIR /burier

RUN git clone --branch maint-0.4.5 https://github.com/torproject/tor.git --single-branch --depth 1 && \
  apt-get install -y automake autotools-dev build-essential libboost-all-dev cmake libevent-dev libssl-dev && \
  cd tor && ./autogen.sh  && ./configure --disable-asciidoc && make

# generate vanity v3 tor address
FROM alexhaydock/mkp224o as vanity
WORKDIR /tmp
ARG prefix
RUN /usr/bin/mkp224o $prefix -n 1 -z -d /tmp/vanity && \
  mkdir -p /tmp/keys && \
  cd /tmp/vanity/$prefix* && cp -a * /tmp/keys

# run tor
FROM ubuntu:16.04

WORKDIR /burier
RUN apt-get update && \
	apt-get install -y libboost-all-dev libevent-dev libssl-dev obfs4proxy obfsproxy

RUN useradd --system --uid 666 -M --shell /usr/sbin/nologin burier

COPY --from=builder /burier/tor/src/app/tor .
COPY --from=vanity /tmp/keys/. /burier/hidden_service/.

ADD storage/torrc .
ADD storage/torrc /etc/tor/torrc

RUN chown 666:666 -R /burier/hidden_service && \
  chown 666:666 /burier/torrc && \
  chmod 700 -R /burier/hidden_service && \
  chmod 600 /burier/hidden_service/hs_ed25519_secret_key && \
  chmod 600 /burier/hidden_service/hs_ed25519_public_key && \
  echo "\n\n\nHERE IS YOUR TOR ADDRESS:\n" && cat /burier/hidden_service/hostname 

USER burier

ENTRYPOINT [ "./tor","-f", "torrc" ]
