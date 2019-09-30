FROM luochonglie/alpine-vim:latest

RUN apk add --no-cache curl \
&& curl -fLo ~/.vim/autoload/plug.vim --create-dirs \
   https://raw.githubusercontent.com/junegunn/vim-plug/master/plug.vim

ENTRYPOINT ["/bin/sh"]
