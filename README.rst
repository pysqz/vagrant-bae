VAGRANT-BAE
======================

Overview
--------
vagrant-bae是一个借助虚拟化创建工具vagrant构造的包含 BAE3_ 执行单元本地模拟的Ubuntu (12.04.2 LTS)虚拟机环境，
它用于部署与 BAE3_ 线上同构的执行环境，便于开发者在本地调试、运行代码。

Installation
-------------
1. 安装 virtualbox https://www.virtualbox.org 
2. 安装 vagrant http://www.vagrantup.com 
3. 安装 git http://git-scm.com/downloads 或者(for windows) http://msysgit.github.io/

Launch a virtual server 
-----
::

    git clone https://github.com/pysqz/vagrant-bae.git
    cd vagrant-bae
    vagrant up

Log onto your Ubuntu server
----
::

    ### 使用vagrant子命令
    vagrant ssh

    ### 直接使用ssh (username:root, password:vagrant)
    ssh root@127.0.0.1 -p 10022

Playing with BAE3.0
----
*以php应用为例*
::

    svn co https://svn.duapp.com/${your_appid} /home/app/php-app/

    cd /home/admin/php-runtime

    ./build.sh

    ./run.sh start

    ### BAE3.0的php-web模拟环境已经启动
    ### 使用curl命令，访问应用，调试代码
    curl 127.0.0.1:8080

    ### 使用host机器浏览器访问
    127.0.0.1:10080

.. _BAE3: http://developer.baidu.com/events/bae3
