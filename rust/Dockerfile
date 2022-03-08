FROM ubuntu:20.04

ARG UID=1000
ARG GID=1000

ENV USER rust
ENV HOME /home/$USER
ENV PATH "$HOME/.cargo/bin:$PATH"

WORKDIR /tmp
RUN export DEBIAN_FRONTEND=noninteractive \
    && apt-get -qq update \
    && apt-get install -yq \
      build-essential cmake curl git \
    && curl -o miniconda.sh https://repo.anaconda.com/miniconda/Miniconda3-latest-Linux-x86_64.sh \
    && bash miniconda.sh -b -p $HOME/miniconda \
    && $HOME/miniconda/bin/conda init bash \
    && rm -rf /var/lib/apt/lists/* /tmp/* /var/tmp/*

RUN groupadd -g $GID $USER \
    && useradd -u $UID -g $USER $USER \
    && chown -R $USER:$USER $HOME

USER $USER
WORKDIR $HOME

## rust installer (the instructions below) adds `source ..` line to '.profile'.
COPY --chown=$USER profile $HOME/.profile

## Install rust and rustlings.
RUN . ~/.bashrc \
    && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y \
    && curl -L https://git.io/install-rustlings | bash -s $HOME/rustlings
