FROM ubuntu:jammy

LABEL co.iterate.ubuntu.python="3.11"
LABEL co.iterate.ubuntu.node="18.x"
LABEL co.iterate.ubuntu.nvm="0.40.1"
LABEL co.iterate.ubuntu.poetry="1.8.3"
LABEL co.iterate.ubuntu.yarn="1.22.22"

# Skip interactive prompts
ENV DEBIAN_FRONTEND=noninteractive

# Add poetry to PATH
# https://stackoverflow.com/a/38905161/2426653
# https://python-poetry.org/docs/#installation
ENV PATH="$PATH:~/.local/bin"


# Install python 3.11 layer
RUN apt-get update && \
  apt-get install -y software-properties-common && \
  add-apt-repository ppa:deadsnakes/ppa -y && \
  apt-get update && \
  apt-get install -y python3.11


# Install all other packages layer
# required for building psycopg2: libpq-dev, python3.11-dev
# required for pip: python3.11-distutils
RUN apt-get update && \
  apt-get install -y awscli \
  curl \
  libpq-dev \
  nano \
  pip \
  python3.11-dev \
  python3.11-distutils \
  python3.11-venv \
  unzip \
  wget \
  zip


# Install nodejs 18.x
RUN curl -fsSL https://deb.nodesource.com/setup_18.x | bash - && \
  apt-get install -y nodejs


# Install nvm
# https://stackoverflow.com/a/60137919/2426653
SHELL ["/bin/bash", "--login", "-i", "-c"]
RUN curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.1/install.sh | bash && \
  source ~/.bashrc && nvm install v18.19.0 && nvm use v18.19.0
SHELL ["/bin/bash", "--login", "-c"]


# Install poetry and sorting plugin
RUN curl -sSL https://install.python-poetry.org | python3 - --version 1.8.3 && \
  ~/.local/share/pypoetry/venv/bin/poetry self add poetry-plugin-sort


# install yarn classic
RUN curl -sS https://dl.yarnpkg.com/debian/pubkey.gpg | apt-key add - && \
  echo "deb https://dl.yarnpkg.com/debian/ stable main" | tee /etc/apt/sources.list.d/yarn.list && \
  apt update && \
  apt-get install -y yarn


# Setup locale
# https://stackoverflow.com/a/57158691/2426653
RUN apt-get update && apt-get install -y locales && rm -rf /var/lib/apt/lists/* \
  && locale-gen "en_US.UTF-8"
ENV LANG=en_US.UTF-8 \
  LANGUAGE=en_US:en \
  LC_ALL=en_US.UTF-8

