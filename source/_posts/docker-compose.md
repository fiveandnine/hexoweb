---
title: docker-compose
date: 2020-03-27 21:18:21
tags:
 - node
 - docker
---



```aidl
# docker-compose.yml
# 语法版本( 3 和 2 区别有点大, 比如 3 取消了 volume_from 的相关语法)
version: "3"

networks:
  frontend:
    driver: ${NETWORKS_DRIVER}
  backend:
    driver: ${NETWORKS_DRIVER}
docker network create -d bridge network_swarm

volumes:
  mysql_volume:
    driver: ${VOLUMES_DRIVER}
  redis_volume:
    driver: ${VOLUMES_DRIVER}
  rabbitmq_volume:
    driver: ${VOLUMES_DRIVER}
# 服务编排
services:
  # workspace:
  #   image: tianon/true
  #   container_name: dnmp-www
  #   volumes:
  #     - ./www:/usr/share/nginx/html

# NGINX #############################################
  nginx:
    container_name: dnmp-nginx
    build: 
      context: ./nginx
      args:
          - PHP_UPSTREAM_CONTAINER=${NGINX_PHP_UPSTREAM_CONTAINER}
          - PHP_UPSTREAM_PORT=${NGINX_PHP_UPSTREAM_PORT}
    depends_on:
      - php-fpm
    ports:
      - "${NGINX_HOST_HTTP_PORT}:80"
      - "${NGINX_HOST_HTTPS_PORT}:443"
    volumes:
      # 没必要把配置文件用卷来挂载, 不然就算配置更新了 nginx 也是要重启的

      # 挂载运行代码目录
      - ${APP_CODE_PATH_HOST}:/var/www
      # 挂载日志目录
      - ${NGINX_HOST_LOG_PATH}:/var/log/nginx
    # 使用 networks 取代 links 在同一个网络模式下的服务是互通的
    # 在service 中使用其他的 service 就直接调用 service 名就行, 不用管 ip 地址, docker 会自己维护一套
    networks:
      - frontend
      - backend


# PHP-FPM #############################################
  php-fpm:
    container_name: dnmp-php-fpm
    # 这里的args 是属于 build 下面的,用于构建./php-fpm/Dockerfile 文件中 ARG 参数指定 php 版本
    build: 
      context: ./php-fpm
      args:
        - PHP_VERSION=${PHP_VERSION}
    volumes:
      - ${APP_CODE_PATH_HOST}:/var/www
      - ./php-fpm/php${PHP_VERSION}.ini:/usr/local/etc/php/php.ini
    expose:
      - "9000"
    networks:
      - backend
    
  redis:
    container_name: dnmp-redis
    build:
      context: ./redis
      args:
        - REDIS_SET_PASSWORD=${REDIS_SET_PASSWORD}
    ports:
      - ${REDIS_HOST_PORT}:6379
    volumes:
      # 这里卷挂载的是本地文件
      # - ${DATA_PATH_HOST}/redis:/data
      # 这里创建一个 redis_volume来存放数据
      - redis_volume:/data

# Mysql #############################################
  mysql:
    container_name: dnmp-mysql
    # 镜像来源: https://github.com/docker-library/mysql/blob/fc3e856313423dc2d6a8d74cfd6b678582090fc7/5.7/Dockerfile
    image: mysql:${MYSQL_VERSION}
    volumes:
      # - ${DATA_PATH_HOST}/mysql:/var/lib/mysql
      - mysql_volume:/var/lib/mysql
    # 容器只要停止就会重启
    restart: always
    environment: 
      MYSQL_ROOT_PASSWORD: ${MYSQL_ROOT_PASSWORD}
      MYSQL_DATABASE: ${MYSQL_DATABASE}
      MYSQL_USER: ${MYSQL_USER}
      MYSQL_PASSWORD: ${MYSQL_PASSWORD}
    ports:
      - ${MYSQL_HOST_PORT}:3306
```

