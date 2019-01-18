本项目为springboot集成admin管控台。具体的搭建步骤如下<br>
主项目 spring-boot-admin<br>
子项目server：admin-server<br>
子项目client：admin-client<br>
#主项目
对应的jar
~~~xml
     <dependency>
                    <groupId>org.springframework.boot</groupId>
                    <artifactId>spring-boot-dependencies</artifactId>
                    <version>${spring-boot.version}</version>
                    <type>pom</type>
                    <scope>import</scope>
                </dependency>
~~~
##admin-server
导入admin-server的jar包
~~~xml
      <dependency>
                <groupId>de.codecentric</groupId>
                <artifactId>spring-boot-admin-starter-server</artifactId>
                <version>2.1.0</version>
            </dependency>
~~~
yml的配置
~~~yml
    server:
      port: 8080
    spring:
      application:
        name: admin-server
~~~
主启动类添加@EnableAdminServer
~~~java
    @SpringBootApplication
    @EnableAdminServer //开启AdminServer的功能
    public class AdminServerApplication {
    
        public static void main(String[] args) {
            SpringApplication.run(AdminServerApplication.class, args);
        }
    
    }
~~~
##admin-client
pom内容 导入admin-client客户端jar
~~~xml
     <dependency>
                <groupId>de.codecentric</groupId>
                <artifactId>spring-boot-admin-starter-client</artifactId>
                <version>2.1.0</version>
            </dependency>
~~~
yml配置信息
~~~yml
    server:
      port: 8081
    spring:
      application:
        name:  admin-client
      boot:
        admin:
          client:
            url:  http://127.0.0.1:8080 #指定该client在那个服务端的地址中
    management:
      endpoints:
        web:
          exposure:
            include: '*' #显示健康节点（* 表示所有）
      endpoint:
        health:
          # never:细节永远不会显示
          # always;详细信息显示给所有用户
          # when_authorized:仅向授权用户显示详细信息。可以使用management.endpoint.health.roles配置授权角色。
          show-details: always
~~~
###测试
1、同时开启项目admin-server和admin-client<br>
2、在浏览器输入http://127.0.0.1:8080/会出现如图<br>
application.png(该项目下projectPhoto下)<br>
3、然后点击wallboard会出现<br>
walllboard.png(该项目下projectPhoto下)<br>
4、然后点击<br>
clientDetail(该项目下projectPhoto下)<br>