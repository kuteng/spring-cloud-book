.. spring-cloud-config documentation master file, created by
   sphinx-quickstart on Tue Mar 13 00:01:39 2018.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

欢迎来到，文档'spring-cloud-config'！
===============================================
版本：2.0.0.M8
Spring Cloud Config为分布式系统中的外部化配置提供服务器和客户端支持。通过Config Server，您可以在所有环境中管理应用程序的外部属性。客户端和服务器上的概念与Spring Environment和PropertySource抽象一致，所以它们非常适合Spring应用程序，但可以与任何运行在任何语言中的应用程序一起使用。随着应用程序从开发到测试转移到部署管道中，您可以管理这些环境之间的配置，并确保应用程序具有在迁移时所需运行的所有内容。服务器存储后端的默认实现使用git，因此它很容易支持配置环境的标签版本，并且可以通过各种工具来访问内容管理。使用Spring配置很容易添加替代实现并将其插入。

.. toctree::
    :maxdepth: 2

    quick-start/index
    spring-cloud-coufig-server/index
    serving-alternative-formats/index


Indices and tables
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`
