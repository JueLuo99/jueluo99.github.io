---
layout: post
title: 在树莓派上安装 Nginx + PHP
date: 2018-06-10 20:04
category: 树莓派
tags: [nginx, php, linux, raspberry-pi]
---

网上找到的大部分教程均已过时，自己总结了当前（2018年6月）在树莓派上可行的 Nginx + PHP 的安装方法

<!-- more -->

1. 安装 Nginx

    ```sudo apt install nginx```

    至此静态网页已经支持，可以尝试进行访问，正常将会出现“Welcome to nginx!”页面

2. 安装 PHP-FPM

    ```sudo apt install php-fpm```

    网上找到的很多教程这里还是 php5-fpm，现在的 php 早已更新至 7.0

3. 修改 Nginx 的配置文件

    找到如下内容
    ```
    # Add index.php to the list if you are using PHP
    index index.html index.htm index.nginx-debian.html;
    ```

    根据注释的说明，加上 ```index.php``` 来更好地支持 php

    修改后
    ```
     # Add index.php to the list if you are using PHP
    index index.html index.htm index.nginx-debian.html index.php;
    ``` 

    接下来找到如下内容
    ```
    # pass PHP scripts to FastCGI server
        #
        #location ~ \.php$ {
        #       include snippets/fastcgi-php.conf;
        #
        #       # With php-fpm (or other unix sockets):
        #       fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass 127.0.0.1:9000;
        #}
    ```

    这部分的内容是选择当遇到 php 脚本时应该如何处理

    由于刚刚安装的是 ```php-fpm``` ，所以去掉部分注释即可

    修改后（注意整块内容的完整，不要缺少了大括号）
    ```
    # pass PHP scripts to FastCGI server
        #
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
        #
        #       # With php-fpm (or other unix sockets):
                fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        #       # With php-cgi (or other tcp sockets):
        #       fastcgi_pass 127.0.0.1:9000;
        }
    ```

    也可以选择删除多余内容，只保留如下内容
    ```
        location ~ \.php$ {
                include snippets/fastcgi-php.conf;
                fastcgi_pass unix:/var/run/php/php7.0-fpm.sock;
        }
    ```

    修改完毕，重启 Nginx 服务

    ```
    systemctl restart nginx
    ```

4. 测试

    向 Nginx 的网页存放位置（默认是```/var/www/html```）新建一个```index.php```，内容如下
    
    ```
    <?php echo phpinfo(); ?>
    ```

    正常情况访问网站将出现 PHP 的信息页面