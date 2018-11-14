====================
1.1 安装 ironic 环境
====================

本文以 packstack 来安装 openstack 测试环境。

环境准备
--------

这里我们以CentOS7.5为例，安装openstack rocky版本，其它版本安装方法类似。

安装 packstack
--------------

.. code-block:: shell
    
    # 更新系统rpm包
    yum update -y

    # 添加packstack yum源
    yum install -y centos-release-openstack-rocky
    
    # 更新系统rpm包
    yum update -y

    # 安装openstack-packstack
    yum install -y openstack-packstack

    # 生成answer-file
    packstack --gen-answer-file=filename

安装 openstack
---------------

接着使用下面的命令安装openstack。

修改 answer-file
----------------

packstack 默认是不安装 ironic 的，需要做如下修改，将CONFIG_IRONIC_INSTALL=y改为CONFIG_IRONIC_INSTALL=y：

.. code-block:: shell

    CONFIG_IRONIC_INSTALL=y

安装 openstack
--------------

.. code-block:: shell

    packstack --answer-file=filename
    
    
修复报错1：提示nova数据库缺部分列，drop掉原有数据库之后，重新进行数据库初始化
--------------

.. code-block:: shell

    [root@host-10-0-40-155 ~]# mysql
    
    MariaDB [mysql]> drop database nova;
    Query OK, 60 rows affected (32.57 sec)

    MariaDB [mysql]> create database nova;
    Query OK, 1 row affected (0.00 sec)


修复报错2：提示Error: Failed to apply catalog: Could not authenticate
--------------

.. code-block:: shell

