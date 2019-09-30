# Multistage builds to reduce image size to ~37MB
# by tuanhtrng
FROM alpine:latest as builder

MAINTAINER JAremko <w3techplaygound@gmail.com>

WORKDIR /tmp

# Install dependencies
RUN apk add --no-cache \
    build-base \
    ctags \
    git \
    libx11-dev \
    libxpm-dev \
    libxt-dev \
    make \
    ncurses-dev \
    python \
    python-dev \
    python3

# Build vim from git source
RUN git clone https://github.com/vim/vim \
 && cd vim \
 && ./configure \
		--disable-gui \
		--disable-netbeans \
		--with-features=big \
		--enable-multibyte \
		--enable-pythoninterp \
		--with-python-config-dir=/usr/lib/python2.7/config \
		--enable-python3interp \
		--with-python-config-dir=/usr/lib/python3.7/config-3.7m-x86_64-linux-gnu \
 && make install
 
FROM alpine:latest
 
COPY --from=builder /usr/local/bin/ /usr/local/bin
COPY --from=builder /usr/local/share/vim/ /usr/local/share/vim/
# NOTE: man page is ignored

RUN apk add --no-cache \
   diffutils \
   libice \
   libsm \
   libx11 \
   libxt \
   ncurses \
   python \
   python3 

ENTRYPOINT ["vim"]
