Client Side Usage
============================

.. toctree::
    :maxdepth: 3

要在应用程序中使用这些功能，只需将其构建为依赖于spring-cloud-config-client的Spring Boot应用程序（如下：配置客户端的测试用例或示例应用程序）。最方便的添加依赖项的方法就是通过Spring Boot启动器 `org.springframework.cloud:spring-cloud-starter-config` 。对于Maven用户这里有一个参考的pom文件和BOM（spring-cloud-starter-parent）和Gradle、Spring CLI用户的Spring IO版本管理属性文件。例如Maven配置：

pom.xml::

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>{spring-boot-docs-version}</version>
        <relativePath /> <!-- lookup parent from repository -->
    </parent>

    <dependencyManagement>
        <dependencies>
            <dependency>
                <groupId>org.springframework.cloud</groupId>
                <artifactId>spring-cloud-dependencies</artifactId>
                <version>{spring-cloud-version}</version>
                <type>pom</type>
                <scope>import</scope>
            </dependency>
        </dependencies>
    </dependencyManagement>

    <dependencies>
        <dependency>
            <groupId>org.springframework.cloud</groupId>
            <artifactId>spring-cloud-starter-config</artifactId>
        </dependency>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-test</artifactId>
            <scope>test</scope>
        </dependency>
    </dependencies>

    <build>
        <plugins>
               <plugin>
                   <groupId>org.springframework.boot</groupId>
                   <artifactId>spring-boot-maven-plugin</artifactId>
               </plugin>
        </plugins>
    </build>

    <!-- repositories also needed for snapshots and milestones -->

然后你可以创建一个标准的Spring Boot应用程序，就像这个简单的HTTP服务器一样：::

    @SpringBootApplication
    @RestController
    public class Application {

        @RequestMapping("/")
        public String home() {
            return "Hello World!";
        }

        public static void main(String[] args) {
            SpringApplication.run(Application.class, args);
        }

    }

运行时，会从默认的本地服务的8888端口上，接受外部的配置（如果它正在运行）。要修改启动行为，可以使用bootstrap.properties（比如application.properties，但是应用程序上下文的引导阶段）更改配置服务器的位置。::

    spring.cloud.config.uri: http://myconfigserver.com

引导属性将作为高优先级属性源显示在/env端点中，例如:::

    $ curl localhost:8080/env
    {
        "profiles":[],
        "configService:https://github.com/spring-cloud-samples/config-repo/bar.properties":{
            "foo":"bar"
        },
        "servletContextInitParams":{},
        "systemProperties":{...},
        ...
    }

