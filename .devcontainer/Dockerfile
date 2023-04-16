FROM ubuntu:22.04

ENV PYTHON_VERSION 3.8.12
ENV DEBIAN_FRONTEND=noninteractive
#Set of all dependencies needed for pyenv to work on Ubuntu
RUN apt-get update \ 
    && apt-get install -y --no-install-recommends make build-essential libssl-dev libpq-dev zlib1g-dev libbz2-dev libreadline-dev libsqlite3-dev wget ca-certificates curl llvm libncurses5-dev xz-utils tk-dev libxml2-dev libxmlsec1-dev libffi-dev liblzma-dev mecab-ipadic-utf8 git postgresql-client telnet unzip zlib1g-dev

RUN curl https://cli-assets.heroku.com/install.sh | sh
RUN curl -fsSL https://deb.nodesource.com/setup_16.x | bash - && apt-get install -y nodejs

ARG USERNAME=codeany
RUN useradd -ms /bin/bash $USERNAME
USER $USERNAME
WORKDIR /home/$USERNAME

ENV PATH=$PATH:"/home/codeany/.local/bin"

RUN echo 'alias psql="psql mydb"' >>  ~/.bashrc

COPY ./build-assets/heroku_config.sh /home/$USERNAME/.theia/heroku_config.sh
RUN echo 'alias heroku_config=". $HOME/.theia/heroku_config.sh"' >> ~/.bashrc

USER root
RUN chown -R $USERNAME:$USERNAME /home/$USERNAME/.theia

CMD ["tail", "-f", "/dev/null"]
