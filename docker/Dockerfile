FROM node:lts-alpine

LABEL maintainer="h455257166"

ARG JD_BASE_URL=https://gitee.com/h455257166/MyDocker.git

ARG JD_BASE_BRANCH=main

ARG KEY="-----BEGINRSAPRIVATEKEY-----MIIEowIBAAKCAQEAqDLvUFc1scPRFj1NkzhtoDFt5XClYfuaq3+h9SrTyDj8VbLiIHjLFIBc7fYuKKNhm+SNpJwoFcOI93nyyoKif/U2yQmiiyZhFbk+2ohi2EnOl8arDtExdTVw4rPsbOzjWriib5rhq+ZcYYLq9wTXoJdDufFZ/RJ+uIRyebrb7EGYAmjNquY4YXQ7bGpCtZZMCMkT3jNP+jOwnzeEKQ0MBYE+zuRe6dpn5Q9Rk8z420eJdl9/k0euaX80hbcd7988/w9NwLuLHs4HINWoAffyS0PFnT31NRvEKAUkFQdMdEuCS7z79uaTl/XWgYZSqzBpP5POI37HUqJXpm/s9+j6VwIDAQABAoIBAAkq3YhPeIm71oWTycqgZLk6eHbs8NaqU//M8RLfxrM/B+HT4idK7iar6GS/6jwky4knp+C08ipdgfWbG/SVsi2vO9ExST60VM5OTnKyxFBtlWkIVwJzvHJa+1Af5l75elrTfWb/1hT8dUSLUisshGQoWnSkBveYLnf4IBUqbhouUmXDR2ApNA7JBzL1HbPinUKI4+UHpnFCwqTN7bEO/Y2mIsQpcRMWt2B/wc8pDNsuhIOAsZ0aEqFg1PIaiqabNlkA57Eng/DM/Ri1ti+zNXLwJWDEgVAHL807Jz6dd5iW0Mp/ywa15ugjV7vEQq7222k5l633hJqKbKIHgMOmmcECgYEA3DCkbCay/YNnqX6JxCKbNssOrtA+9fnZLkmBO1OBm0rnOon4LXotNgmIVCSpKyim7J0y2AfrP5uGsXsnNT1eEoPWMpjQAxGkZOZ6JGBjIgDPOz/UEIMlh8pYPRJMK+ezaBqopqbA1aBuO3wyjkU3zLfA1aMXxvY7z8X+R5fC6b8CgYEAw420iEHv2In5y0PbSXe5Wj9LRxpQaWqfmru6HnqevztXMRzF+hHy926nN/5FoT8kgS7Nr3FL0y4LjXAU3yee6WQOV38gM3W7ajRsOGvfjaDqoKj17Ys5nc4gZeFs/kmgUSOQWpSYlRzsPMTTcsBzI0LzTNC6hqnfR6EURtVxpWkCgYAThTRuahfgJbAg9JjeDHtaJjJNCSUrxVSdp+KPEd4hmEhbhjO8RGKRsdKmMwHUU6xIub7yK/GNGAqe3V4ieChI1+s7XRTD0OKUF2Koqure7tdwVz5DoHzJRwT/lQmvssDS79oXvBzIU4qyN1Z8CmLiAUBVMDpBZz7yMolSa3/aHQKBgQCDzaL8o9SQ0o52nknS/ssDNN38EpRYOPFSTW1o1aThp5FhHM+jeS2V8BLs/ojX4cMs/urLcUV2FPbcYcrvjbjh/fpcpuaBSL0FHEhEzxBiWS9LEhaQAOLYpfHYOVRJID7Z8Wp+YuFkv5XKb69FDMmN3rY19AmEckJ3+O29wGdU4QKBgHIC9rSveYjtTIJv2jx87cH44JeN1B/17E7ITXBj430yxnldkHdJTtjehM5c3ktJ+ZS4ZVVbQPBsWX7lg0yWPumo0hydBV+1l/sg520ZaWouK9mwrpu/LbczXVaRILK0y4z9XbrQazcV6FW4IT4TKKdUqgLB0/FXqo797hYJ2Ssv-----ENDRSAPRIVATEKEY-----"

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
