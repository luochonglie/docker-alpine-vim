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

COPY ./vimrc /root/.vimrc

RUN curl -fLo /root/.vim/autoload/plug.vim --create-dirs \
    https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim \ 
 && vim --not-a-term -c "PlugInstall! | qall!" \
 && cd ~/.vim/plugged/YouCompleteMe \
 && python3 install.py


# Build vim from git source
FROM luochonglie/alpine-vim:latest

COPY --from=builder ~/.vimrc ~/.vimrc
COPY --from=builder ~/.vim/ ~/.vim/
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

ENTRYPOINT ["/bin/sh"]
