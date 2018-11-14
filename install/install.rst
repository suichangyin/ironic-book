====================
1.1 安装 ironic 环境
====================

本文以 packstack 来安装 openstack 测试环境。

环境准备
--------

这里我们以CentOS7.5为例，安装openstack rocky版本，
其它版本安装方法类似。packstack目前对NetworkManager
还不支持，我们修改下配置：

.. code-block:: shell

    systemctl disable firewalld
    systemctl stop firewalld
    systemctl disable NetworkManager
    systemctl stop NetworkManager
    systemctl enable network
    systemctl start network

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
