快速入门
=========================

通过如下命令开始服务：::

    $ cd spring-cloud-config-server
    $ ../mvnw spring-boot:run

这个服务是一个Spring Boot的应用程序，所以如果你愿意，可以通过IDE来运行它（Main类是ConfigServerApplication）。你可以这样尝试一个客户端用法：::

    $ curl localhost:8888/foo/development
    {"name":"foo","label":"master","propertySources":[
      {"name":"https://github.com/scratches/config-repo/foo-development.properties","source":{"bar":"spam"}},
      {"name":"https://github.com/scratches/config-repo/foo.properties","source":{"foo":"bar"}}
    ]}

定位属性源的默认策略是克隆一个git仓库（这个配置行在 `spring.cloud.config.server.git.uri` ）同时使用它初始化小型的Spring应用程序 `SpringApplication` 。


.. toctree::
    :maxdepth: 2
    :numbered: 2

    01_client_side_usage
