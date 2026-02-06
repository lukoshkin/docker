FROM ubuntu:20.04

ARG UID=1000
ARG GID=1000

ENV USER=rust
ENV HOME=/home/$USER
ENV PATH="$HOME/.cargo/bin:$PATH"

RUN apt-get -qq update && DEBIAN_FRONTEND=noninteractive \
## git and curl are required by the installation instructions at the bottom.
    apt-get install -yq build-essential curl git cmake \
    && rm -rf /var/lib/apt/lists/* \
    && groupadd -g $GID $USER \
    && useradd -m -u $UID -g $USER $USER \
    && chown -R $USER:$USER $HOME \
    && curl --proto '=https' --tlsv1.2 -sSf https://sh.rustup.rs | sh -s -- -y

USER $USER
WORKDIR $HOME
