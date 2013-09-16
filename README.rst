VAGRANT-BAE
======================

Overview
--------
vagrant-bae是一个借助虚拟化创建工具vagrant构造的包含 BAE3_ 执行单元本地模拟的Ubuntu (12.04.2 LTS)虚拟机环境，
它用于部署与 BAE3_ 线上同构的执行环境，便于开发者在本地调试、运行代码。

Installation
-------------
1. 安装 virtualbox https://www.virtualbox.org，详细过程参见官网文档
2. 安装 vagrant http://www.vagrantup.com，详细过程参见官网文档，推荐版本>=1.2.2
3. 安装 git http://git-scm.com/downloads 或者(for windows) http://msysgit.github.io/ 


Usage
-----
Launch a virtual server 
+++++++++++++++++++++++
::

    git clone https://github.com/pysqz/vagrant-bae.git
    cd vagrant-bae
    vagrant up

Log onto your Ubuntu server
+++++++++++++++++++++++++++
::
 
    ### 使用vagrant子命令，默认用户为vagrant，建议开发者切换到root操作
    vagrant ssh

    ### 或者直接使用ssh (username:root, password:vagrant)
    ssh root@127.0.0.1 -p 10022

Playing with BAE3.0
+++++++++++++++++++
本地开发环境中集成了BAE3.0客户端工具 cli_ ，开发者可以借助cli对应命令进行本地部署及调试。 

*以php应用为例*
::
    ### 开发者信息初始化
    bae login

    ### 获取BAE应用，其中ID中在管理控制台应的"基本信息"中获取
    bae app setup -I <ID> 

    ### 发布代码都本地环境
    bae app publish --local

    ### 上述操作后，你可以通过如下方式访问应用。进而修改代码，调试运行

    ### 1.虚拟机中使用curl命令访问
    ###### php或python应用可指定应用域名，同时处理多个应用，域名可以通过bae app list获取
    curl 127.0.0.1:8080 -H "Host: $app_domain"
    ###### java应用直接指定对应的war包名(root.war直接通过/访问)
    curl 127.0.0.1:8080/$war_name/

    ### 2.宿主机中使用浏览器访问
    ###### php或python可修改系统hosts文件，将127.0.0.1配为指定的应用域名
    app_domain:10080
    ###### java应用同样指定对应的war包名(root.war直接通过/访问)
    127.0.0.1:10080/$war_name/

    ### 另开发者可执行对本地环境后端server的控制
    bae instance restart --local
    bae instance start --local
    bae instance stop --local

    ### 上述cli命令详细介绍请参看 http://godbae.duapp.com/?p=338

Note
----
1. 因创建64bit虚拟机，故需开启计算机中VT属性。一般操作为BIOS > Security > OS Security > Intel Virtualization Technology(ENABLE)
2. 确保你的环境中ssh可使用，详见 http://www.openssh.org/
3. 确保你的环境中系统盘或根目录有2G空闲，若virtualbox使用的虚拟介质也存储在系统盘或根目录，则至少需要4G空闲
4. 执行"vagrant up"后在提示"Waiting for VM to boot. This can take a few minutes."处卡住的情况，可参看https://github.com/mitchellh/vagrant/issues/455，强力处理方法为在virtualbox中手动重启虚拟机。

.. _BAE3: http://developer.baidu.com/events/bae3
.. _cli: http://godbae.duapp.com/?p=338