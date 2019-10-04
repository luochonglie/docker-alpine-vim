# Multistage builds to reduce image size to ~37MB
# by luochonglie
FROM luochonglie/alpine-vim:latest as builder

MAINTAINER luochonglie <luochonglie@gmail.com>

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
    python3 \
    python3-dev \
    cmake \
    curl

ADD vimrc /root/.vimrc
RUN cat ~/.vimrc

RUN curl -fLo /root/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim \
 && vim --not-a-term -c "PlugInstall! | qall!" \
 && cd ~/.vim/plugged/YouCompleteMe \
 && python3 install.py 

RUN mkdir -p /files   
RUN cp /root/.vimrc /files/vimrc 
RUN cp -r /root/.vim/ /files/vim/

# Build vim from git source
FROM luochonglie/alpine-vim:latest

COPY --from=builder /files/vimrc /root/.vimrc
COPY --from=builder /files/vim/ /root/.vim/
# NOTE: man page is ignored

RUN apk add --no-cache \
   diffutils \
   libice \
   libsm \
   libx11 \
   libxt \
   ncurses \
   python \
   python3 \
   git \
   libstdc++

ENTRYPOINT ["/bin/sh"]
