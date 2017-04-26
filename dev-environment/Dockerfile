# Base image
FROM ubuntu:14.04

# Put my hand up as maintainer
MAINTAINER chishui<chishui2@gmail.com>

# Suppress debian frontend warnings from Ubuntu base image
RUN DEBIAN_FRONTEND=noninteractive

# Install OS tools we'll need
RUN \
    apt-get update && \
    apt-get -y install \
        build-essential \
        tmux \
        curl \
        vim \
        git \
        autojump \
        zsh \
        # Python libraries
        python \
        python-dev \
        python-setuptools \
        # 
        cmake

# Install OH-MY-ZSH to see pretty terminal and ditch the bash
RUN curl -L https://github.com/robbyrussell/oh-my-zsh/raw/master/tools/install.sh | bash

RUN \
    git clone https://github.com/chishui/dotfile.git /root/dotfile && \
    cp /root/dotfile/.vimrc /root && \
    cp /root/dotfile/robbyrussell.zsh-theme /root/.oh-my-zsh/themes && \
    cp /root/dotfile/.zshrc /root

RUN git clone https://github.com/VundleVim/Vundle.vim.git ~/.vim/bundle/Vundle.vim
RUN git clone https://github.com/flazz/vim-colorschemes.git ~/.vim/bundle/vim-colorschemes
RUN vim +PluginInstall  +qall
#RUN vim -c 'PluginInstall' -c 'qa!'
RUN cd /root/.vim/bundle/YouCompleteMe/ && \
    ./install.py --clang-completer

# Set environment variables
ENV HOME /root

# Define working directory
WORKDIR /root

# Define default command
CMD ["/bin/zsh"]
