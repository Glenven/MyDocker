# 关于 Docker 版本的《使用与更新》教程 
#### ## 修订日期：2021 年 4 月
ㅤ
# **创建容器**
## # 在 liunx 下创建容器：
### 1、安装 Docker
#### 在线安装 Docker：  `curl -sSL https://get.daocloud.io/docker | sh` 
##### 查看 Docker 当前版本：`docker version`
##### 启动 Docker 后台服务： `service docker start`
###2、下载镜像并安装
    docker run -dit \
    -v /opt/js/scripts:/js/scripts `# 设置活动脚本的主机挂载目录为/opt/js/scripts` \
    -v /opt/js/config:/js/config `# 设置配置文件的主机挂载目录为/opt/js/config` \
    -v /opt/js/log:/js/log `# 设置日志的主机挂载目录为/opt/js/log` \
    -p 6789:6789 `# 设置端口映射，格式为 "主机端口:容器端口"，主机端口号可自定义` \
    -e ENABLE_WEB_PANEL=true `# 启用控制面板功能` \
    --name js `# 设置容器名为js` \
    --network bridge `# 设置网络为桥接，直连主机` \
    --hostname js `# 设置主机名为js` \
    --restart always `# 设置容器开机自启` \
    h455257166/mydocker_1.0:latest

------------
ㅤ
## # 在 Windows 下创建容器：
### 1、安装 Docker
#### Docker Desktop 下载地址：[https://www.docker.com/products/docker-desktop](https://www.docker.com/products/docker-desktop "https://www.docker.com/products/docker-desktop")

####2、 Windows下进入CMD命令创建容器：
    docker run -dit -p 6789:6789 -v C:/Js/scripts:/js/scripts -v C:/Js/config:/js/config -v C:/Js/log:/js/log -e ENABLE_WEB_PANEL=true --name js --network bridge --hostname js --restart always h455257166/mydocker_1.0:latest

> 提醒：Windows下需在C盘根目录创建“Js”文件夹并在文件夹内分别创建scripts，config，log三个文件夹作为脚本文件、配置文件和日志文件的外部挂载目录

------------
ㅤ
# **使用说明**

####附：[Docker 容器使用教程](https://www.runoob.com/docker/docker-container-usage.html)
## 1. 该容器的进入与退出：
- ####进入容器：
``` 
docker exec -it js /bin/bash
```
- ####退出容器：
``` 
exit
``` 

> ㅤ注意：1. 大部分命令都可在容器外部执行，但部分复杂命令只能在容器内执行，注意区分下面教程的命令执行位置。_\
ㅤㅤㅤㅤ2. 如果您修改了默认的容器名称，当使用下面所有的命令时则需要将 `jd`替换为新的名称。_\
ㅤㅤㅤㅤ3. 下面的命令中如果前面加上了 `docker exec -it jd` 则表示在容器外部运行此命令。_\
ㅤㅤㅤㅤ4. 例如 `docker exec -it newname bash js.sh xxx now` ，也可使用 `容器ID`代替。_

------------

ㅤ
## 2. 手动运行所有脚本：

- ####一键执行所有脚本：
```
docker exec -it js bash run_all.sh
```
> ㅤ注意：1. 此脚本的作用为执行所有活动脚本，共有高达几十个活动脚本，时间较长且与账号数量成正比。_\
ㅤㅤㅤㅤ2. 除手动运行活动脚本外该项目还会通过定时的方式自动执行活动脚本，可通过日志查看运行记录。_\
ㅤㅤㅤㅤ3. 执行此脚本后无需守在电脑旁，会自动在最后无限制运行挂机活动脚本，直到您手动停止运行为止。_

- #### 一键更新脚本： 
``` 
docker exec -it js bash git_pull.sh
```
> 注意：每次使用前请执行此命令，确保使用最新的项目脚本和活动脚本，此脚本也配置了定时任务可自动执行。_

#####常见报错：
- 提示 `Repository more than 5 connections`
 - 是由于 `Gitee` 限制了每秒同时拉取项目的IP不能超过 `5` 个所导致，此报错为正常现象，重新执行更新命令即可。_
 
- 提示 `ssh: connect to host gitee.com port 22: Connection timed out` 
 - 是由于您使用平台的 `22` 端口不可用所导致，自行解决处理。
 
- 提示 `Could not resolve hostname gitee.com: Temporary failure in name resolution lost connection` 
 - 是由于无法解析到 `Gitee` 服务器地址所导致，表明网络环境异常，自行解决处理。

------------


## 3. 执行特定的活动脚本：
    docker exec -it js bash js <sprict name>     # 如果设置了随机延迟并且当时时间不在0-2、30-31、59分内，将随机延迟一定秒数
    docker exec -it js bash js <sprict name> now  # 无论是否设置了随机延迟，均立即运行
> _注意：具体查看活动脚本列表可通过命令 `docker exec -it js bash js.sh` 查看， `<sprict name>` 为脚本名。_

------------
ㅤ

## 4. 使用 Diy 自定义脚本扩展活动脚本数量：
- ####使用需知

      1. 此脚本的用途为收集并添加第三方作者编写的活动脚本
      2. 您可以开启自动同步功能，默认同步本人项目中的脚本
      3. 您也可以使用本项目中的模板文件自定义构建您的专属脚本
      4. 您可以将自制的 Diy 脚本上传至您的仓库并使用自动同步功能
      5. 如果您使用了自制的脚本请更改配置文件里的地址链接
- ####启用该功能

      docker exec -it js sed -i 's/EnableExtraShell=""/EnableExtraShell="true"/g' config/config.sh
- ####启用自动同步功能（选择）

      docker exec -it js sed -i 's/EnableExtraShellUpdate=""/EnableExtraShellUpdate="true"/g' config/config.sh
> ㅤ注意：1. 启用该功能后便可直接下载或同步更新本项目中的 Diy 脚本。
> ㅤㅤㅤㅤ2. 如果您想更换同步的地址链接自行修改配置文件中的相关变量。

 - #####如果您想推荐某位作者的第三方活动脚本并将它加入到本项目自定义脚本中，您可以在 Issues 专题下方留言。

------------

ㅤ
## 5. 常用功能：
- ####获取互助码：
```shell
 docker exec -it js bash js get_share_code now
```
- ####格式化导出互助码：
```shell
 docker exec -it js bash export_sharecodes.sh
```
> 注意：其原理是从各个活动脚本的日志中获取，只有运行完所有活动脚本后才可使用

- ####配置互助码与相互助力
 -  #####填法示例：
> #############  定义东东萌宠互助（选填） #############
> 
> MyPet1="xxxxxxxxxxxxxxxxxxxxxxxxx"
> MyPet2="xxxxxxxxxxxxxxxxxxxxxxxxx"
> MyPet3="xxxxxxxxxxxxxxxxxxxxxxxxx"
> MyPet4="xxxxxxxxxxxxxxxxxxxxxxxxx"
> MyPet5="xxxxxxxxxxxxxxxxxxxxxxxxx"
> MyPet6="xxxxxxxxxxxxxxxxxxxxxxxxx"
> MyPet7="xxxxxxxxxxxxxxxxxxxxxxxxx"
> MyPet8="xxxxxxxxxxxxxxxxxxxxxxxxx"
> MyPetA=""
> MyPetB=""
> 
> ForOtherPet1="${MyPet1}@${MyPet2}@${MyPet3}@${MyPet4}@${MyPet5}@${MyPet6}@${MyPet7}@${MyPet8}"
> ForOtherPet2="${MyPet1}@${MyPet2}@${MyPet3}@${MyPet4}@${MyPet5}@${MyPet6}@${MyPet7}@${MyPet8}"
> ForOtherPet3="${MyPet1}@${MyPet2}@${MyPet3}@${MyPet4}@${MyPet5}@${MyPet6}@${MyPet7}@${MyPet8}"
> ForOtherPet4="${MyPet1}@${MyPet2}@${MyPet3}@${MyPet4}@${MyPet5}@${MyPet6}@${MyPet7}@${MyPet8}"
> ForOtherPet5="${MyPet1}@${MyPet2}@${MyPet3}@${MyPet4}@${MyPet5}@${MyPet6}@${MyPet7}@${MyPet8}"
> ForOtherPet6="${MyPet1}@${MyPet2}@${MyPet3}@${MyPet4}@${MyPet5}@${MyPet6}@${MyPet7}@${MyPet8}"
> ForOtherPet7="${MyPet1}@${MyPet2}@${MyPet3}@${MyPet4}@${MyPet5}@${MyPet6}@${MyPet7}@${MyPet8}"
> ForOtherPet8="${MyPet1}@${MyPet2}@${MyPet3}@${MyPet4}@${MyPet5}@${MyPet6}@${MyPet7}@${MyPet8}"

- ####启动/重启后台运行挂机活动脚本程序：
```shell
docker exec -it js bash js hangup
```
- ####停止后台运行挂机活动脚本程序：
```shell
docker exec -it js pm2 stop jd_crazy_joy_coin
```
- ####  删除脚本的运行日志：
```
    docker exec -it js bash rm_log.sh 
```
> 注意：默认删除 `7天` 以上的日志文件，可以通过配置文件中的相关变量更改默认时间值。

- ####提交您的互助码到公共库：
    Telegram 机器人： @LvanLamCommitCodeBot  @TuringLabbot
> _注意：此公共库由活动脚本作者开发并维护，用于活动间的相互助力以解决助力机会和被助力次数不足的问题，此库定时清空且名额有限，具体提交教程详见回复信息。_

------------
ㅤ

## 6. 控制面板：
- ####  手动启用控制面板：
```
docker exec -it js pm2 start panel/ecosystem.config.js
```
> 注意：在某些环境下当系统重启导致控制面板无法访问提示拒绝连接时可用此命令恢复使用。

- ####  手动关闭控制面板：
```
docker exec -it js pm2 stop panel/ecosystem.config.js
```
> 注意：`VPS` 平台用户关机前请先执行此命令手动停止控制面板，否则在仪表盘强制关机重启后可能会出现无法保存配置文件的问题。

- ####  重启控制面板：
```
docker exec -it js pm2 restart panel/ecosystem.config.js
```

- ####  重置控制面板的用户名和密码：
```
    docker exec -it js bash js resetpwd
```

- #### 升级控制面板：
```
    docker exec -it js /bin/bash
    cd panel
    yarn install || yarn install --registry=https://registry.npm.taobao.org
    exit
```
> 注意：如果您更改了默认访问端口，那么在执行此命令后需要重新修改。

- #### 重新安装控制面板：
```
    docker exec -it js /bin/bash
    cd panel
    yarn install || yarn install --registry=https://registry.npm.taobao.org
    npm install -g pm2
    pm2 start ecosystem.config.js
    exit
```
> 注意：此命令适用于在容器初始化过程中安装失败时使用。


------------
ㅤ
## 7. 更新教程：
- #### 更新 `一键更新` 脚本：
```
docker exec -it js wget https://gitee.com/h455257166/MyDocker/raw/main/js.sh -O git_pull.sh
```

- ####  更新 `配置文件` ：
 - 备份当前配置文件
```
      docker exec -it js mv config/config.sh config/bak/config.sh
```
 - 替换新版配置文件
```
      docker exec -it js cp -f sample/config.sh.sample config/config.sh
```
> _ㅤ注意：操作为直接替换配置文件，您也可以通过控制面板对比工具自行修改。_

------------
ㅤ
## 8. 查看帮助文档：
```
    docker exec -it js cat course/docker.md
```
> 注意：此文档为《使用与更新》教程，即当前页面内容，跟随项目同步更新。

***

ㅤ
## # 使用需知
#### 1.  `run_all.sh` 为一键执行所有活动脚本， `git_pull.sh` 为一键更新脚本
#### 2. 手动执行 `run_all.sh` 脚本后无需守在电脑旁，会自动在最后运行挂机活动脚本
#### 3. 执行 `run_all.sh` 脚本期间如果卡住，可按回车键尝试或通过命令 `Ctrl + Z` 跳过继续执行剩余活动脚本
#### 4. 由于京东活动一直变化可能会出现无法参加活动、报错等正常现象，可手动更新活动脚本
#### 5. 5. 如果需要更新活动脚本，请执行一键更新脚本，它会同步更新 `run_all.sh` 一键执行所有活动脚本
#### 6. 除手动运行活动脚本外该项目还会通过定时的方式全天候自动运行活动脚本，具体运行记录可通过日志查看
#### 7. 该项目已默认配置好 `Crontab` 定时任务，定时配置文件 `crontab.list` 会通过活动脚本的更新而同步更新
#### 8. 之前填入的 `Cookie部分内容` 具有一定的时效性，若提示失效请根据教程重新获取并手动更新
#### 9. 我不是活动脚本的开发者，但后续使用遇到任何问题都可访问本项目寻求帮助，制作不易，理解万岁
