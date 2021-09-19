# Getting Started

### Reference Documentation

For further reference, please consider the following sections:

* [Official Apache Maven documentation](https://maven.apache.org/guides/index.html)
* [Spring Boot Maven Plugin Reference Guide](https://docs.spring.io/spring-boot/docs/2.5.4/maven-plugin/reference/html/)
* [Create an OCI image](https://docs.spring.io/spring-boot/docs/2.5.4/maven-plugin/reference/html/#build-image)

# 尚医通

## 1. 项目环境搭建

hostipal-manage:医院接口模拟端，已开发，直接使用

syt_parent:项目根目录，管理子模块

- common:公共模块父节点
  - common_util：工具类模块，所有模块都可以依赖于它
  - rabbit_util：rabbitmq业务封装
  - service_util：service 服务的工具包，包含service服务的公共配置类，所有service模块依赖于它
- server_gateway：服务网关
- model：实体类模块
- service：api接口服务父节点
  - service_hosp：医院api接口服务
  - service_cmn：公共api接口服务
  - service_user：用户api接口服务
  - service_order：订单api接口服务
  - service_oss：文件api接口服务



>1. 新建syt_parent  springboot项目
>
>   - packing改为pom，表明是父工程
>
>   - ```xml
>     <?xml version="1.0" encoding="UTF-8"?>
>     <project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>              xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 https://maven.apache.org/xsd/maven-4.0.0.xsd">
>         <modelVersion>4.0.0</modelVersion>
>         <modules>
>             <module>common</module>
>             <module>model</module>
>         </modules>
>         <parent>
>             <groupId>org.springframework.boot</groupId>
>             <artifactId>spring-boot-starter-parent</artifactId>
>             <version>2.5.4</version>
>             <relativePath/> <!-- lookup parent from repository -->
>         </parent>
>         <groupId>com.flywinter</groupId>
>         <artifactId>syt_parent</artifactId>
>         <version>0.0.1-SNAPSHOT</version>
>         <name>syt_parent</name>
>     <!--    作为父工程创建-->
>         <packaging>pom</packaging>
>         <description>syt_parent</description>
>         <properties>
>             <java.version>11</java.version>
>             <cloud.version></cloud.version>
>             <alibaba.version></alibaba.version>
>             <mybatis-plus.version></mybatis-plus.version>
>             <mysql.version></mysql.version>
>             <swagger.version>3.0.0</swagger.version>
>             <jwt.version></jwt.version>
>             <fastjson.version></fastjson.version>
>             <httpclient.version></httpclient.version>
>             <easyexcel.version></easyexcel.version>
>             <aliyun.version></aliyun.version>
>             <oss.version></oss.version>
>     
>         </properties>
>         <dependencyManagement>
>             <dependencies>
>                 <!--        springcloud依赖-->
>                 <dependency>
>                     <groupId>org.springframework.cloud</groupId>
>                     <artifactId>spring-cloud-dependencies</artifactId>
>                     <version>2020.0.3</version>
>                     <type>pom</type>
>                     <scope>import</scope>
>                 </dependency>
>                 <dependency>
>                     <groupId>com.alibaba.cloud</groupId>
>                     <artifactId>spring-cloud-alibaba-dependencies</artifactId>
>                     <version>2021.1</version>
>                     <type>pom</type>
>                     <scope>import</scope>
>                 </dependency>
>                 <!--        mybatis plus持久层-->
>                 <dependency>
>                     <groupId>com.baomidou</groupId>
>                     <artifactId>mybatis-plus-boot-starter</artifactId>
>                     <version>3.4.3.3</version>
>                 </dependency>
>                 <!--        mysql驱动-->
>                 <dependency>
>                     <groupId>mysql</groupId>
>                     <artifactId>mysql-connector-java</artifactId>
>                     <version>8.0.25</version>
>                 </dependency>
>                 <!--        swagger2-->
>                 <dependency>
>                     <groupId>io.springfox</groupId>
>                     <artifactId>springfox-swagger2</artifactId>
>                     <version>${swagger.version}</version>
>                 </dependency>
>                 <!--        swagger ui-->
>                 <dependency>
>                     <groupId>io.springfox</groupId>
>                     <artifactId>springfox-swagger-ui</artifactId>
>                     <version>${swagger.version}</version>
>                 </dependency>
>                 <!--        jjwt-->
>                 <dependency>
>                     <groupId>io.jsonwebtoken</groupId>
>                     <artifactId>jjwt</artifactId>
>                     <version>0.9.1</version>
>                 </dependency>
>                 <dependency>
>                     <groupId>org.apache.httpcomponents</groupId>
>                     <artifactId>httpclient</artifactId>
>                     <version>4.5.13</version>
>                 </dependency>
>                 <dependency>
>                     <groupId>com.alibaba</groupId>
>                     <artifactId>fastjson</artifactId>
>                     <version>1.2.78</version>
>                 </dependency>
>     
>                 <dependency>
>                     <groupId>com.aliyun</groupId>
>                     <artifactId>aliyun-java-sdk-core</artifactId>
>                     <version>4.5.25</version>
>                 </dependency>
>                 <dependency>
>                     <groupId>com.aliyun.oss</groupId>
>                     <artifactId>aliyun-sdk-oss</artifactId>
>                     <version>3.13.1</version>
>                 </dependency>
>                 <!--        日期时间工具-->
>                 <dependency>
>                     <groupId>joda-time</groupId>
>                     <artifactId>joda-time</artifactId>
>                     <version>2.10.10</version>
>                 </dependency>
>     
>                 <dependency>
>                     <groupId>com.alibaba</groupId>
>                     <artifactId>easyexcel</artifactId>
>                     <version>2.2.11</version>
>                 </dependency>
>     
>                 <dependency>
>                     <groupId>org.springframework.boot</groupId>
>                     <artifactId>spring-boot-starter-test</artifactId>
>                     <scope>test</scope>
>                 </dependency>
>             </dependencies>
>     
>         </dependencyManagement>
>     
>         <build>
>             <plugins>
>                 <plugin>
>                     <groupId>org.springframework.boot</groupId>
>                     <artifactId>spring-boot-maven-plugin</artifactId>
>                 </plugin>
>             </plugins>
>         </build>
>     
>     </project>
>     ```
>
>2. 搭建common父模块
>
>   - 打包方式改为pom
>
>   - ```xml
>     <packaging>pom</packaging>
>     ```
>
>   - 在common里面创建子模块common_util和子模块service_util
>
>   - common的pom配置
>
>   - ```xml
>     <?xml version="1.0" encoding="UTF-8"?>
>     <project xmlns="http://maven.apache.org/POM/4.0.0"
>              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>              xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
>         <parent>
>             <artifactId>syt_parent</artifactId>
>             <groupId>com.flywinter</groupId>
>             <version>0.0.1-SNAPSHOT</version>
>         </parent>
>         <modelVersion>4.0.0</modelVersion>
>         <artifactId>common</artifactId>
>         <packaging>pom</packaging>
>         <modules>
>             <module>common_util</module>
>             <module>service_util</module>
>         </modules>
>         <dependencies>
>             <!--        常用web加监控-->
>             <dependency>
>                 <groupId>org.springframework.boot</groupId>
>                 <artifactId>spring-boot-starter-web</artifactId>
>                 <scope>provided</scope>
>             </dependency>
>             <dependency>
>                 <groupId>org.springframework.boot</groupId>
>                 <artifactId>spring-boot-starter-actuator</artifactId>
>                 <scope>provided</scope>
>             </dependency>
>             <!--        mybatis plus持久层-->
>             <dependency>
>                 <groupId>com.baomidou</groupId>
>                 <artifactId>mybatis-plus-boot-starter</artifactId>
>                 <scope>provided</scope>
>             </dependency>
>     <!--        lombok-->
>             <dependency>
>                 <groupId>org.projectlombok</groupId>
>                 <artifactId>lombok</artifactId>
>             </dependency>
>             <!--        swagger2-->
>             <dependency>
>                 <groupId>io.springfox</groupId>
>                 <artifactId>springfox-swagger2</artifactId>
>             </dependency>
>             <!--        swagger ui-->
>             <dependency>
>                 <groupId>io.springfox</groupId>
>                 <artifactId>springfox-swagger-ui</artifactId>
>             </dependency>
>         </dependencies>
>     
>     </project>
>     ```
>
>3. 创建子模块model
>
>   - pom
>
>   - ```xml
>     <?xml version="1.0" encoding="UTF-8"?>
>     <project xmlns="http://maven.apache.org/POM/4.0.0"
>              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>              xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
>         <parent>
>             <artifactId>syt_parent</artifactId>
>             <groupId>com.flywinter</groupId>
>             <version>0.0.1-SNAPSHOT</version>
>         </parent>
>         <modelVersion>4.0.0</modelVersion>
>     
>         <artifactId>model</artifactId>
>     
>         <properties>
>             <maven.compiler.source>11</maven.compiler.source>
>             <maven.compiler.target>11</maven.compiler.target>
>         </properties>
>         <dependencies>
>             <dependency>
>                 <groupId>org.projectlombok</groupId>
>                 <artifactId>lombok</artifactId>
>             </dependency>
>             <dependency>
>                 <groupId>com.baomidou</groupId>
>                 <artifactId>mybatis-plus-boot-starter</artifactId>
>                 <scope>provided</scope>
>             </dependency>
>             <!--        swagger2-->
>             <dependency>
>                 <groupId>io.springfox</groupId>
>                 <artifactId>springfox-swagger2</artifactId>
>                 <scope>provided</scope>
>             </dependency>
>             <!--        swagger ui-->
>             <dependency>
>                 <groupId>io.springfox</groupId>
>                 <artifactId>springfox-swagger-ui</artifactId>
>                 <scope>provided</scope>
>             </dependency>
>             <dependency>
>                 <groupId>com.alibaba</groupId>
>                 <artifactId>easyexcel</artifactId>
>                 <scope>provided</scope>
>             </dependency>
>             <dependency>
>                 <groupId>org.springframework.boot</groupId>
>                 <artifactId>spring-boot-starter-data-mongodb</artifactId>
>                 <scope>provided</scope>
>             </dependency>
>             <dependency>
>                 <groupId>com.alibaba</groupId>
>                 <artifactId>fastjson</artifactId>
>                 <scope>provided</scope>
>             </dependency>
>         </dependencies>
>     
>     </project>
>     ```
>
>4. 创建service
>
>   - ```xml
>     <?xml version="1.0" encoding="UTF-8"?>
>     <project xmlns="http://maven.apache.org/POM/4.0.0"
>              xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
>              xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
>         <parent>
>             <artifactId>syt_parent</artifactId>
>             <groupId>com.flywinter</groupId>
>             <version>0.0.1-SNAPSHOT</version>
>         </parent>
>         <modelVersion>4.0.0</modelVersion>
>         <packaging>pom</packaging>
>         <artifactId>service</artifactId>
>     
>         <properties>
>             <maven.compiler.source>11</maven.compiler.source>
>             <maven.compiler.target>11</maven.compiler.target>
>         </properties>
>         <dependencies>
>             <dependency>
>                 <groupId>com.flywinter</groupId>
>                 <artifactId>service_util</artifactId>
>                 <version>0.0.1-SNAPSHOT</version>
>             </dependency>
>             <dependency>
>                 <groupId>com.flywinter</groupId>
>                 <artifactId>model</artifactId>
>                 <version>0.0.1-SNAPSHOT</version>
>             </dependency>
>     <!--        web-->
>             <dependency>
>                 <groupId>org.springframework.boot</groupId>
>                 <artifactId>spring-boot-starter-web</artifactId>
>             </dependency>
>             <dependency>
>                 <groupId>org.springframework.boot</groupId>
>                 <artifactId>spring-boot-starter-actuator</artifactId>
>             </dependency>
>             <!--        mybatis plus持久层-->
>             <dependency>
>                 <groupId>com.baomidou</groupId>
>                 <artifactId>mybatis-plus-boot-starter</artifactId>
>             </dependency>
>             <!--        mysql驱动-->
>             <dependency>
>                 <groupId>mysql</groupId>
>                 <artifactId>mysql-connector-java</artifactId>
>             </dependency>
>             <!--        开发者工具-->
>             <dependency>
>                 <groupId>org.springframework.boot</groupId>
>                 <artifactId>spring-boot-devtools</artifactId>
>                 <optional>true</optional>
>             </dependency>
>             <!--        服务调用openfeign-->
>             <dependency>
>                 <groupId>org.springframework.cloud</groupId>
>                 <artifactId>spring-cloud-starter-openfeign</artifactId>
>             </dependency>
>     <!--        服务注册-->
>             <dependency>
>                 <groupId>com.alibaba.cloud</groupId>
>                 <artifactId>spring-cloud-starter-alibaba-nacos-discovery</artifactId>
>             </dependency>
>     <!--        流量控制-->
>             <dependency>
>                 <groupId>com.alibaba.cloud</groupId>
>                 <artifactId>spring-cloud-starter-alibaba-sentinel</artifactId>
>             </dependency>
>         </dependencies>
>         <build>
>             <plugins>
>                 <plugin>
>                     <groupId>org.springframework.boot</groupId>
>                     <artifactId>spring-boot-maven-plugin</artifactId>
>                 </plugin>
>             </plugins>
>             <resources>
>                 <resource>
>                     <directory>src/main/java</directory>
>                     <includes>
>                         <include>**/*.yml</include>
>                         <include>**/*.properties</include>
>                         <include>**/*.xml</include>
>                     </includes>
>                     <filtering>false</filtering>
>                 </resource>
>                 <resource>
>                     <directory>src/main/resources</directory>
>                     <includes>
>                         <include>**/*.yml</include>
>                         <include>**/*.properties</include>
>                         <include>**/*.xml</include>
>                     </includes>
>                     <filtering>false</filtering>
>                 </resource>
>             </resources>
>         </build>
>     
>     </project>
>     ```
>

service里面新建service_user模块



提交git仓库

