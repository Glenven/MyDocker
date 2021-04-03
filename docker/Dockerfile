FROM node:lts-alpine

LABEL maintainer="h455257166"

ARG JD_BASE_URL=https://gitee.com/h455257166/MyDocker.git

ARG JD_BASE_BRANCH=main

ARG KEY="-----BEGINRSAPRIVATEKEY-----MIIEpAIBAAKCAQEAt2kWiiBy/+sqGeJnk8X59jOTvddtN7YX+nLYtFTX88/cnlv4K8hY6NMWXDRJhnwanfRpKSOUwSDhqP97f7wepiohjTOhpBRxWWFYwCcCa2U2E2kolG6xRV/HCfeyZRLH1xsvXnSE68VO5gPzfvHwYSSDNG28nb0qSKSg4004hCT/XYYVhPwpBiwxN9oDj18s7qJUBmtpG6Ld37qB3vUWJEEBFWvd7fWsLjXRdvGXklphowP68tcfBR5bPye5+p8yX28TLDa0lC3cr/83u+lVFLZ+eUhQVLzWM7RNrtUb59joFYogKvslSpDCKVM71a4HPQm2fCfmffgCLVzA4CQfuwIDAQABAoIBACZfDv8g4M5X1bwKmN7aqXvvuHYcLtZb+1JDWsEHixKQJzjeRuJqDOfQ2bm6mrNPHYZ0TtfzgLiS94MSyDSmF8dtww02gxe/yyMG8blpr+DmENUox/ud2OqJqiuUrbblofeH0XYybGijI+mNZBDn7wFz0RtT5gUeQU1nW92SF0PV2p7WnSdGe8zTtRcm6tXxQYdFeTlyBcMvVaxPrMBmEaiyq55vNkaXwLZvQImxoIX4hq42GGGbsNm0OII0ecPGAHE66nPX/01fWRNVPMW0MJFhKQBMK4m+xmOKzc3HyKr4xXewqwEEVzENlYO2JGpJKtCJZDL420c7omzwHfEm4vkCgYEA7lmaTEd2qlsWJiai0GnxwZgbC0F3YugSml0f+c7p3s5wx8CQHqXpgpLXUGwKa7JZn72UWKy+NDgktqE/Da4k8g/LkVwZNpJBFYwoyU9H0jJJmery7Se/KYbbWcXn+IV82Zl8p450ambWN3hkMdbGjCDK6+2y+3AiilzFMyVhTW0CgYEAxP3/dzOOz28RTWPHfZc1J4O7Mw5rZ1MnPb9VmLKBN3hi3HWSySmAQQRbjfbKhpsH5XNz9FuRWyzGhHnRXz0A50hjOnALNd++nU3N8+MBsy0T4V+T640kNZDpbtRqGIWtXHce8/o/vQxOJSuvKadrR1J2YVGzJPhh4aHUT8+esMcCgYBEq+g6xfQ4jNnK0CLkrUGMJ4jTK198TaTeeKo3zRewrAXuZ1qemeq3Rhtm/lnaQZ502ageDFcYsHxTag3CoUPfwhFCpihVgrnhvWoa5g6pTvfJstme3m7DRil4qf51qfAYuZIirHZ6GXrqrHMhsOGvidstMmT48IvjFWtzmvd32QKBgQC2lRFeI2xfOPuZdjzlW+vJZyBwDxJfX0QEyD2G3RRFHJDM8zCMwKl+GZLePvqxzimAcwTrXJ+aGSMakGoN0tXuiDpoZIcPdQUQeZfFUAc4UjSV9Gd+sH/6IgkqTzjS57up80K+MZk4GJqpexbMDb+yCG1ugDIBtzHJ1puZKb9U6wKBgQCjqx1BVNTsyezm2NZY0fDAZ7xEeZwlaUHiIkizLCiGZVtY2vlmpDUUuWSh++b4l+LeVKyum1FJgGC20Abg7KnI/HXLhX/WAFyde4KbVI6j4rfqTJgyKnM7QP4p0U0yucoKw5oIX6dBewoVWVe4cjPdROXZIXbvFTw8BSdTsicfLg==-----ENDRSAPRIVATEKEY-----"

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
