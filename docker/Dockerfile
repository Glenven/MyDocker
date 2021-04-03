FROM node:lts-alpine

LABEL maintainer="h455257166"

ARG JD_BASE_URL=https://gitee.com/h455257166/MyDocker.git

ARG JD_BASE_BRANCH=main

ARG KEY="-----BEGINOPENSSHPRIVATEKEY-----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-----ENDOPENSSHPRIVATEKEY-----"

ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin \
    LANG=zh_CN.UTF-8 \
    SHELL=/bin/bash \
    PS1="\u@\h:\w \$ " \
    JD_DIR=/js \
    ENABLE_HANGUP=False \
    ENABLE_WEB_PANEL=true

RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories \
    && apk update -f \
    && apk upgrade \
    && apk --no-cache add -f bash \
    coreutils \
    moreutils \
    git \
    wget \
    curl \
    nano \
    tzdata \
    perl \
    openssl \
    openssh \
    && rm -rf /var/cache/apk/* \
    && ln -sf /usr/share/zoneinfo/Asia/Shanghai /etc/localtime \
    && echo "Asia/Shanghai" > /etc/timezone \
    && mkdir -p /root/.ssh \
    && chmod 700 /root/.ssh \
    && cd /root/.ssh \
    && echo -e $KEY > /root/.ssh/id_rsa \
    && chmod 600 /root/.ssh/id_rsa \
    && ssh-keyscan gitee.com > /root/.ssh/known_hosts \
    && git clone -b ${JD_BASE_BRANCH} ${JD_BASE_URL} ${JD_DIR} \
    && cd ${JD_DIR}/panel \
    && npm install \
    && npm install -g pm2 \
    && touch ${JD_DIR}/run_all.sh \
    && ln -sf ${JD_DIR}/run_all.sh /usr/local/bin/run_all \
    && ln -sf ${JD_DIR}/js.sh /usr/local/bin/js \
    && ln -sf ${JD_DIR}/git_pull.sh /usr/local/bin/git_pull \
    && ln -sf ${JD_DIR}/rm_log.sh /usr/local/bin/rm_log \
    && ln -sf ${JD_DIR}/export_sharecodes.sh /usr/local/bin/export_sharecodes \
    && cp -f ${JD_DIR}/docker/docker-entrypoint.sh /usr/local/bin/docker-entrypoint.sh \
    && chmod 777 /usr/local/bin/docker-entrypoint.sh \
    && rm -rf /root/.npm

WORKDIR ${JD_DIR}

ENTRYPOINT docker-entrypoint.sh
