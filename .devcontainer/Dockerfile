# See here for image contents: https://github.com/microsoft/vscode-dev-containers/tree/v0.150.0/containers/python-3/.devcontainer/base.Dockerfile

# [Choice] Python version: 3, 3.9, 3.8, 3.7, 3.6
ARG VARIANT="3.8"
FROM mcr.microsoft.com/vscode/devcontainers/python:0-${VARIANT}

ADD .devcontainer/sources.list /etc/apt/sources.list

ENV DEBIAN_FRONTEND noninteractive
ENV PYPI=https://mirrors.aliyun.com/pypi/simple/

RUN apt-get update -y && \
    apt-get install -y tzdata default-libmysqlclient-dev

RUN rm -rf /etc/localtime && ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime

RUN echo 'export GPG_TTY=$(tty)' >> ~/.zshrc

RUN pipx install -i ${PYPI} poetry



# [Optional] If your pip requirements rarely change, uncomment this section to add them to the image.
# COPY requirements.txt /tmp/pip-tmp/
# RUN pip3 --disable-pip-version-check --no-cache-dir install -r /tmp/pip-tmp/requirements.txt \
#    && rm -rf /tmp/pip-tmp

WORKDIR /app/
COPY poetry.lock .
COPY pyproject.toml .
RUN poetry export -f requirements.txt --without-hashes --dev > requirements.txt
RUN pip3 --disable-pip-version-check --no-cache-dir install -r requirements.txt




