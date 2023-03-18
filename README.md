# x-ui

Support multi-protocol multi-user xray panel

# Features

- System Status Monitoring
- Support multi-user and multi-protocol, web page visualization operation
- Supported protocols:vmessvlesstrojanshadowsocksdokodemo-doorsockshttp
- Support for configuring more transport configurations
- Traffic statistics, limit traffic, limit expiration time
- customizable xray configuration template
- support https Access panel (bring your own domain name + ssl Certificate)
- Support one keySSLCertificate application and automatic renewal
- For more advanced configuration items, see Panel

# Install&upgrade

```
bash <(curl -Ls https://raw.githubusercontent.com/vaxilu/x-ui/master/install.sh)
```

## manual installation&upgrade

1. first from https://github.com/vaxilu/x-ui/releases Download the latest compressed package, generally choose `amd64`architecture
2. Then upload this compressed package to the server's `/root/`directory, and use `root`user login server

> if your server cpu architecture is not `amd64`, the command in the `amd64`Replace with another schema

```
cd /root/
rm x-ui/ /usr/local/x-ui/ /usr/bin/x-ui -rf
tar zxvf x-ui-linux-amd64.tar.gz
chmod +x x-ui/x-ui x-ui/bin/xray-linux-* x-ui/x-ui.sh
cp x-ui/x-ui.sh /usr/bin/x-ui
cp -f x-ui/x-ui.service /etc/systemd/system/
mv x-ui/ /usr/local/
systemctl daemon-reload
systemctl enable x-ui
systemctl restart x-ui
```

## usedockerInstall

> this docker tutorial with docker mirrored by[Chasing66](https://github.com/Chasing66)supply

1. Installdocker

```shell
curl -fsSL https://get.docker.com | sh
```

2. Installx-ui

```shell
mkdir x-ui && cd x-ui
docker run -itd --network=host \
    -v $PWD/db/:/etc/x-ui/ \
    -v $PWD/cert/:/root/cert/ \
    --name x-ui --restart=unless-stopped \
    enwaiax/x-ui:latest
```

> Build own mirror image

```shell
docker build -t x-ui .
```

## SSLcertificate application

> This feature and tutorial are provided by[FranzKafkaYu](https://github.com/FranzKafkaYu)supply

script built-inSSLCertificate application function, use this script to apply for a certificate, the following conditions must be met:

- knowCloudflare register e-mail
- knowCloudflare Global API Key
- The domain name has passedcloudflareParse to the current server

ObtainCloudflare Global API KeyMethods:
    ![](media/bda84fbc2ede834deaba1c173a932223.png)
    ![](media/d13ffd6a73f938d1037d0708e31433bf.png)

To use just type `domain name`, `Mail`, `API KEY`That’s it, the diagram is as follows:
        ![](media/2022-04-04_141259.png)

Precautions:

- The script usesDNS APIApply for a certificate
- use by defaultLet'sEncryptasCAdirection
- The certificate installation directory is/root/certTable of contents
- The certificates applied for by this script are all wild domain name certificates

## TgRobot use (under development, temporarily unavailable)

> This feature and tutorial are provided by[FranzKafkaYu](https://github.com/FranzKafkaYu)supply

X-UIsupport byTgThe robot implements functions such as daily traffic notification, panel login reminder, etc., usingTgRobot, need to apply by yourself
Please refer to the specific application tutorial[blog link](https://coderfan.net/how-to-use-telegram-bot-to-alarm-you-when-someone-login-into-your-vps.html)
Instructions for use:Set robot-related parameters in the background of the panel, including

- TgrobotToken
- TgrobotChatId
- TgRobot cycle time, usingcrontabgrammar  

Reference syntax:
- 30 * * * * * //every point30sto notify
- @hourly      //hourly notification
- @daily       //Daily notification (0:00 am sharp)
- @every 8h    //Every8hour notice  

TGNotification content:
- Node traffic usage
- Panel Login Reminder
- Node expiration reminder
- Traffic warning reminder  

More functions are planned...
## suggestion system

- CentOS 7+
- Ubuntu 16+
- Debian 8+

# common problem

## from v2-ui migrate

First installed the v2-ui Install the latest version on the server x-ui, and then use the following command to migrate, the native will be migrated v2-ui of `all inbound account data`to x-ui`Panel settings and username and password are not migrated`

> After successful migration please `closure v2-ui`and `reboot x-ui`,otherwise v2-ui of inbound will be with x-ui of inbound Will produce `port conflict`

```
x-ui v2-ui
```

## issue closure

All kinds of white problems see high blood pressure

## Stargazers over time

[![Stargazers over time](https://starchart.cc/vaxilu/x-ui.svg)](https://starchart.cc/vaxilu/x-ui)
