FROM rust:1.48.0-alpine3.12

ARG USER_NAME
ARG GROUP_NAME
ARG USER_UID
ARG USER_GID
ARG WORK_DIR

RUN addgroup -g $USER_GID -S $GROUP_NAME \
    && adduser -u $USER_UID -s /bin/sh -S $USER_NAME $GROUP_NAME

RUN apk --update --no-cache add git curl bash openssh-client sudo jq

RUN echo "$USER_NAME ALL=(ALL) NOPASSWD: ALL" >> /etc/sudoers.d/${USER_NAME} \
    && chmod 0440 /etc/sudoers.d/$USER_NAME
RUN mkdir /home/${USER_NAME}/${WORK_DIR} \
    && chown ${GROUP_NAME}:${USER_NAME} /home/${USER_NAME}/${WORK_DIR}

COPY --chown=${GROUP_NAME}:${USER_NAME} ./ssh /home/${USER_NAME}/.ssh

USER vscode
WORKDIR /home/${USER_NAME}/${WORK_DIR}
RUN git clone git@github.com:mori-hisayuki/rust_study.git /home/${USER_NAME}/${WORK_DIR}