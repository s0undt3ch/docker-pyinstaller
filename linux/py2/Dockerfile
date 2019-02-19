FROM centos:6
SHELL ["/bin/bash", "-i", "-c"]

# Target python version to build
ARG PYTHON_VERSION=2.7.15
# Target pyinstaller version
ARG PYINSTALLER_VERSION=3.4

# PYPI repository location
ENV PYPI_URL=https://pypi.python.org/
# PYPI index location
ENV PYPI_INDEX_URL=https://pypi.python.org/simple

COPY entrypoint.sh /entrypoint.sh

RUN \
    set -x \
    # update system
    && yum install -y yum && yum update -y \
    && yum install -y \
      git \
      readline-devel \
      zlib-devel \
      gcc \
      sqlite-devel \
      bzip2-devel \
      openssl \
      openssl-devel \
      make \
      patch \
      gcc-c++ \
      readline-devel \
    # install pyenv
    && echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc \
    && echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc \
    && source ~/.bashrc \
    && curl -L https://github.com/pyenv/pyenv-installer/raw/master/bin/pyenv-installer | bash \
    && echo 'eval "$(pyenv init -)"' >> ~/.bashrc \
    && source ~/.bashrc \
    # install python
    && PYTHON_CONFIGURE_OPTS="--enable-shared" pyenv install $PYTHON_VERSION \
    && pyenv global $PYTHON_VERSION \
    && pip install --upgrade pip \
    # install pyinstaller
    && pip install pyinstaller==$PYINSTALLER_VERSION \
    && mkdir /src/ \
    && chmod +x /entrypoint.sh

VOLUME /src/
WORKDIR /src/

ENTRYPOINT ["/entrypoint.sh"]
