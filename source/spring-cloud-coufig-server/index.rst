Spring的云配置服务
==============================
这个服务为外部配置（键值对或者类似的YAML内容）提供HTTP形式的资源型的API。通过 ``@EnableConfigServer`` 批注，这个服务可以很轻松的嵌入到一个Spring Boot的应用中。So this app is a config server:

ConfigServer.java. ::

    @SpringBootApplication
    @EnableConfigServer
    public class ConfigServer {
      public static void main(String[] args) {
        SpringApplication.run(ConfigServer.class, args);
      }
    }

与所有Spring Boot应用程序一样，它默认在端口8080上运行，但您可以通过各种方式将其切换到常规端口8888。最简单的方式，就是通过 ``spring.config.name=configserver`` （就是在Config Server的jar文件中的configserver.yml文件）启动他，这里也设置了一个默认的配置库。另一个方法就是使用您自己的application.properties。例如：

application.properties.::

    server.port: 8888
    spring.cloud.config.server.git.uri: file://${user.home}/config-repo

``${user.home}/config-repo`` 是一个git仓库，其中包含了YAML和properties文件。

| 在Windows中，如果是绝对路径，你需要在URL中增加一个额外的 ``/`` 作为驱动前缀。例如 ``file:///${user.home}/config-repo`` 。
|
| 如果你在“配置”仓库中只保存文本文件，那么初始克隆这个仓库会很快。但是如果你在仓库中存放二进制文件特别是大型文件，你可能在第一次请求配置的时候遭遇延迟甚至服务器的内存溢出。

