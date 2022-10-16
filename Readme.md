# SpringBoot 2.7.x源码fork分析
## 工程结构
### 构建工具
由之前的maven转为gradle了

### 父子工程
父工程和子工程

### 源码位置
spring-boot-project即为springboot源码位置
- spring-boot：springboot入口模块
- spring-boot-autoconfigure：springboot自动装配功能模块
- spring-boot-actuator：springboot驱动器
- spring-boot-actuator-autoconfigure：springboot自动装配驱动器
- spring-boot-parent：springboot父项目，只定义了很多构建插件，并依赖了springboot-dependencies
- spring-boot-dependencies：springboot依赖模块，定义了springboot可依赖的模块的版本，如jdbc、mysql等
- spring-boot-starters：springboot启动器，会被springboot项目依赖，其中定义了各种默认配置，启动器被依赖即该场景功能基本配置完成，开箱使用
- spring-boot-tools
- spring-boot-devtools
- spring-boot-test
- spring-boot-autoconfigure
- spring-boot-docs

### 主要概念
- 入口
```groovy
    // 依赖了spring-core和spring-context
    api("org.springframework:spring-core")
	api("org.springframework:spring-context")
```

- 自动装配
```groovy
    // 依赖了spring-boot
    api(project(":spring-boot-project:spring-boot"))
```

- 依赖
定义了springboot当前版本默认集成的三方依赖的版本信息

- 驱动器（actuator）
**spring-boot-actuator**
```markdown
Spring Boot Actuator includes a number of additional features to help you monitor and
manage your application when it's pushed to production. You can choose to manage and
monitor your application using HTTP or JMX endpoints. Auditing, health and metrics
gathering can be automatically applied to your application. The
https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#production-ready[user guide]
covers the features in more detail.

== Enabling the Actuator
The recommended way to enable the features is to add a dependency to the
`spring-boot-starter-actuator` '`Starter`'. To add the actuator to a Maven-based project,
add the following '`Starter`' dependency:
```
```groovy
    // 依赖了spring-boot
    api(project(":spring-boot-project:spring-boot"))
```

**spring-boot-actuator-autoconfigure**
```groovy
api(project(":spring-boot-project:spring-boot-actuator"))

	api(project(":spring-boot-project:spring-boot"))
	api(project(":spring-boot-project:spring-boot-autoconfigure"))

	implementation("com.fasterxml.jackson.core:jackson-databind")
	implementation("com.fasterxml.jackson.datatype:jackson-datatype-jsr310")
```

- 启动器
常见starter，如spring-boot-starters-web就是springboot web应用的启动器，依赖了这个就可以开箱即用
```markdown
Spring Boot Starters are a set of convenient dependency descriptors that you can include
in your application. You get a one-stop-shop for all the Spring and related technology
that you need without having to hunt through sample code and copy paste loads of
dependency descriptors. For example, if you want to get started using Spring and
JPA for database access include the `spring-boot-starter-data-jpa` dependency in
your project, and you are good to go.
```
```groovy
plugins {
    id "org.springframework.boot.starter"
}
description = "Starter for building web, including RESTful, applications using Spring MVC. Uses Tomcat as the default embedded container"
dependencies {
  api(project(":spring-boot-project:spring-boot-starters:spring-boot-starter"))
  api(project(":spring-boot-project:spring-boot-starters:spring-boot-starter-json"))
  api(project(":spring-boot-project:spring-boot-starters:spring-boot-starter-tomcat"))
  api("org.springframework:spring-web")
  api("org.springframework:spring-webmvc")
}
```

- 工具
- 开发工具
- 父项目
定义了基础依赖
- 文档
- 测试
