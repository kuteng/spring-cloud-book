快速入门
=========================

通过如下命令开始服务：::

    $ cd spring-cloud-config-server
    $ ../mvnw spring-boot:run

这个服务是一个Spring Boot的应用程序，所以如果你愿意，可以通过IDE来运行它（Main类是ConfigServerApplication）。你可以这样尝试一个客户端用法：::

    $ curl localhost:8888/foo/development
    {
        "name":"foo",
        "label":"master",
        "propertySources":[
            {
                "name":"https://github.com/scratches/config-repo/foo-development.properties",
                "source":{
                    "bar":"spam"
                }
            },
            {
                "name":"https://github.com/scratches/config-repo/foo.properties",
                "source":{
                    "foo":"bar"
                }
            }
        ]
    }

定位属性源的默认策略是克隆一个git仓库（这个配置行在 `spring.cloud.config.server.git.uri` ）同时使用它初始化一个小型的Spring应用程序 `SpringApplication` 。这个小型应用程序的 `Environment` 是用于列举出属性源，同时通过 `JSON` 格式发布他们。

这个HTTP服务具有的资源表单如下：::

    /{application}/{profile}[/{label}]
    /{application}-{profile}.yml
    /{label}/{application}-{profile}.yml
    /{application}-{profile}.properties
    /{label}/{application}-{profile}.properties

在Spring应用 `SpringApplication` 中，我们将"application"注入到配置 `spring.config.name` 中；"profile"是一个自由的配置（可以作为一个属性列表，使用逗号个开）；"label"是git的分支/标签（默认为 `master` ），同时它是可选的。

.. toctree::
    :maxdepth: 2
    :numbered: 2

    01_client_side_usage
    02_spring_cloud_config_server
