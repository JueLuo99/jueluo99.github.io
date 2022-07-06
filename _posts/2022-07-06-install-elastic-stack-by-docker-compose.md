---
layout: post
title: 使用 Docker Compose 安装 Elastic Stack
date: 2022-07-06 06:47
category: ElasticStack
tags: [elasticsearch, docker, docker-compose, kibana] 
---

## 一、简介
本文将会使用官方提供的 Elastic Stack with Dockers Compose 的方式进行安装
安装内容包含了一个启用了身份验证和网络加密的、三节点的 Elasticsearch 服务器，和一个 Kibana 服务器

## 二、配置要求

- 一个可以安装和运行 Docker 的操作系统（建议避免使用 ARM 架构）
- 至少 4 GB 的内存

本文中采用的操作系统：Ubuntu Server 22.04 LTS

## 三、准备工作

### 安装 Docker 和 Docker Compose

在 Ubuntu 上，通常可使用如下命令直接安装
```bash
sudo apt install docker.io docker-compose
```
在其他平台上，可参考 Docker 的官方文档：

- [Get Docker | Docker Documentation](https://docs.docker.com/get-docker/)
- [Install Docker Compose | Docker Documentation](https://docs.docker.com/compose/install/)


## 四、配置并启动 Elastic Stack

### 准备 docker-compose 文件

创建一个新的空目录，并放置入`.env` 和 `docker-compose.yml` 这两个文件

#### 方法一：从 GitHub 直接下载

```bash
wget https://raw.githubusercontent.com/elastic/elasticsearch/8.1/docs/reference/setup/install/docker/.env
wget https://raw.githubusercontent.com/elastic/elasticsearch/8.1/docs/reference/setup/install/docker/docker-compose.yml
```

#### 方法二：从此处下载后导入

[](../assets/2022/elastic_stack/.env)
[](../assets/2022/elastic_stack/docker-compose.yml)


### 修改 .env 文件

在第 2 行填入欲使用的 `elastic` 用户的密码，稍后**会在登录时使用**
在第 5 行填入欲使用的 `kibana_system`用户的密码（这个值仅在内部配置 Kibana 时使用）
在第 8 行填入欲使用的版本号，在本例中，使用的版本号为 `8.1.3`
如若不希望将 Elasticsearch HTTP API 绑定到 `0.0.0.0:9200`，可将第 18 行的值修改为诸如 `127.0.0.1:9200`的值
同理，可在第 22 行处修改 Kibana 的相关配置

### 启动 Docker Compose

上述文件编辑完毕后，可以尝试启动这个实例

```bash
docker-compose up -d
```

### 停止并移除部署

如需停止上述配置的服务，可使用如下命令（会暂时卸载卷，故数据不会被直接删除，可于下次启动时继续使用）

```bash
docker-compose down
```

想要同时删除所有数据，可使用如下命令

```bash
docker-compose down -v
```

## 五、故障排除

若在尝试启动 Docker Compose 时，出现以下提示

```bash
ERROR: for kibana  Container "abcdef123456" is unhealthy.
ERROR: Encountered errors while bringing up the project.
```

可以尝试通过如下方式调整最大内存映射计数来解决

```bash
sudo sysctl -w vm.max_map_count=262144
```


## 六、总结

若通过上述步骤配置完毕，均成功启动且无异常，则已开放下述两个端口提供服务：

- 通过 `https://example.com:9200`来访问 Elasticsearch API，该站点使用自签证书
- 通过 `http://example.com:5601`访问 Kibana 界面

账号及密码：

- 账号：`elastic`
- 密码：在本文第四节中配置的密码


## 七、参考资料

1. [Running the Elastic Stack ("ELK") on Docker | Getting Started [8.1] | Elastic](https://www.elastic.co/guide/en/elastic-stack-get-started/current/get-started-stack-docker.html#_prerequisites_2)
1. [elasticsearch/docs/reference/setup/install/docker at 8.1 · elastic/elasticsearch](https://github.com/elastic/elasticsearch/tree/8.1/docs/reference/setup/install/docker/)
1. [Docker - Kibana, APM, Elasticsearch issue - - Stack Overflow](https://stackoverflow.com/questions/59226203/docker-kibana-apm-elasticsearch-issue)
1. [Maximum map count check | Elasticsearch Guide [8.1] | Elastic](https://www.elastic.co/guide/en/elasticsearch/reference/current/_maximum_map_count_check.html)
