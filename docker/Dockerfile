FROM node:latest

# create an app user
ARG USERNAME
ARG DOCKER_UID
ARG DOCKER_GID
RUN groupadd -g $DOCKER_GID $USERNAME
RUN useradd -m -u $DOCKER_UID -g $DOCKER_GID -s /bin/bash $USERNAME

WORKDIR /app

RUN chown -R $DOCKER_UID:$DOCKER_UID /app
RUN chmod -R g+w /app \
    && chown -R $USERNAME:$USERNAME /usr/local/bin/

# sudo power (without password) <- DEVELOPMENT AND PLAYGROUND ONLY
RUN usermod -a -G sudo $USERNAME && \
    echo '$USERNAME ALL=(ALL) NOPASSWD:ALL' >> /etc/sudoers

# starter script
COPY start-container /usr/local/bin/start-container
RUN chmod +x /usr/local/bin/*

CMD ["start-container"]