# Mac下开发环境搭建

## 1. 必要的第三方支持
### 1.1. VirtualBox
访问[VirtualBox官网](https://www.virtualbox.org/wiki/Downloads)下载最新的VirtualBox版本并安装
### 1.2. Boot2Docker
#### 1.2.1. 访问[Boot2Docker官网](http://boot2docker.io)下载最新的Boot2Docker Mac版本并安装.
#### 1.2.2 配置默认环境
```bash
echo '[ $(boot2docker status 2>/dev/null) == "running" ] && export DOCKER_HOST=tcp://$(/usr/local/bin/boot2docker ip 2>/dev/null):2375' >> ~/.profile
```
#### 可参考文档:
1. [Installing Docker on Mac OS X](http://docs.docker.com/installation/mac/)

### 1.3. Hostile
用于在Mac方便地配置/etc/hosts

1. 访问[Node.js官网](http://nodejs.org/download/)下载最新的node.js安装或者使用`homebrew`安装
2. npm安装

```bash
npm i -g hostile
```

## 2. 安装我们自己的环境

```bash
curl -sL https://raw.githubusercontent.com/iamfat/boot2docker-gini/master/setup | sh
```

## 3. 配置你的专门应用
```bash

# 配置一个本地域名: e.g. app.local => 192.168.59.103
export DOCKER_IP=$(/usr/local/bin/boot2docker ip 2>/dev/null)
hostile set $DOCKER_IP app.local

export BASE_DIR=/mnt/sda1/data
curl -L https://raw.githubusercontent.com/iamfat/boot2docker-gini/master/nginx-site.conf | boot2docker ssh "sudo cat > $BASE_DIR/etc/nginx/sites-enabled/abc"

```