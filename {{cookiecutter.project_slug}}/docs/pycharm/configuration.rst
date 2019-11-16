远程Docker调试
=======================

想在docker中调用远程python，首先得要确定pycharm中配置docker信息。

从 *【Settings > Build, Execution, Deployment > Docker】* 。 

* 如果使用linux，可以直接通过使用socket `unix:///var/run/docker.sock` ；
* 如果使用Windows或者MacOS，请确定docker-machine已经安装，然后通过 *【Import credentials from Docker Machine】* 配置docker-machine。


.. image:: images/1.png

配置远程python解释器
-----------------------------------

项目将通过"Run/Debug Configurations"来启动调试。

.. image:: images/2.png

但是正如您所示，刚开始的时候将会在django图标前看到红色的‘X’。此时需要通过配置 *【Settings > Build, Execution, Deployment】* 添加python远程解释器。

然后，从 *【Settings > Project > Project Interpreter】* ，选择  *【Add Remote】* 添加远程解释器。

.. image:: images/3.png

切换至 *【Docker Compose】* 选项，选择项目中的`local.yml`。然后填写 *【Service name】* 。

.. image:: images/4.png

点击 *【OK】*，关闭 *【Settings】* 页，坐等程序自动关闭...

.. image:: images/7.png

过几秒后，重新点击 *【Run/Debug Configurations】* 可以查看到之前django前的红色X已经消失。

.. image:: images/8.png

**通过上述配置，可以执行一下操作**:

* 运行或者调试程序
.. image:: images/f1.png
* 运行或调试测试用力
.. image:: images/f2.png
.. image:: images/f3.png
* 运行或调试django相关命令
.. image:: images/f4.png
* 其他操作..

常见问题
------------

* Pycharm在"Connecting to Debugger"的时候被夯住

.. image:: images/issue1.png

连接失败，查看防火墙信息。可以简单查看 - https://youtrack.jetbrains.com/issue/PY-18913

* .idea目录下文件被修改

  `.idea/` 目录下的大部分文件已经被添加在 `.gitignore`。因为该部分配置会根据机器上的目录进行配置，故可以将该部分文件添加在git的忽略文件列表中:

.. image:: images/issue2.png


理论上可以直接从代码仓库中删除。但是这样操作的话，其他开发者可能需要重新参考本页进行项目配置。如果不想查看该部分改动，可以在项目中运行以下命令：

    $ git update-index --assume-unchanged cmdb.iml
