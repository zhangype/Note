# 基础知识
## Spring Cloud简介
&nbsp;&nbsp;Spring Cloud 是一个基于 Spring Boot 实现的微服务架构开发工具。它为微服务架构中涉及配置管理、服务治理、断路器、智能路由、微代理、全局锁、决策竞选、分布式会话和集群状态管理等操作提供了一种简单的开发方式。  
&nbsp;&nbsp;微服务强调各服务之间进行“无事务”的调用，而对于数据一致性，只要求数据在最后的处理状态是一致的即可。若在过程中发现错误，通过补偿机制来进行处理，使得错误数据能够达到最终的一致性。  
&nbsp;&nbsp;Spring Cloud 包含了多个子项目：  
&nbsp;&nbsp;●**Spring Cloud Config**：配置管理工具，支持使用 Git 存储配置内容，可以使用它实现应用配置的外部化存储，并支持客户端配置信息刷新、加密/解密配置内容等。  
&nbsp;&nbsp;●**Spring Cloud Netflix**：核心组件，对多个Netflix OSS 开源套件进行整合。  
&nbsp;&nbsp;&nbsp;&nbsp;●**Eureka**：服务治理组件，包含服务注册中心、服务注册与发现机制的实现。  
&nbsp;&nbsp;&nbsp;&nbsp;●**Hystrix**：容错管理组件，实现短路器模式，帮助服务依赖中出现的延迟和故障提供强大的容错能力。  
&nbsp;&nbsp;&nbsp;&nbsp;●**Ribbon**：客户端负载均衡的服务调用组件。  
&nbsp;&nbsp;&nbsp;&nbsp;●**Feign**：基于 Ribbon 和 Hystrix 的声明式服务调用组件。  
&nbsp;&nbsp;&nbsp;&nbsp;●**Zuul**：网关组件，提供智能路由、访问过滤等功能。  
&nbsp;&nbsp;&nbsp;&nbsp;●**Archaius**：外部化配置组件。  
&nbsp;&nbsp;●**Spring Cloud Bus**：事件、消息总线用于传播集群中的状态变化或事件，以出发后续的处理，比如用来动态刷新配置等。  
&nbsp;&nbsp;●**Spring Cloud Cluster**：针对 Zookeeper、Redis、Hazelcast、Consul 的选举算法和通用状态模式的实现。  
&nbsp;&nbsp;●**Spring Cloud Cloudfoundry**：与 Pivotal Cloudfoundry 的整合支持。  
&nbsp;&nbsp;●**Spring Cloud Consul**：服务发现与配置管理工具。  
&nbsp;&nbsp;●**Spring Cloud Stream**：通过 Redis、Rabbit 或者 Kafka 实现的消费微服务，可以通过简单的声明式模型来发送和接收信息。  
&nbsp;&nbsp;●**Spring Cloud AWS**：用于简化整合 Amazon Web Service 的组件。  
&nbsp;&nbsp;●**Spring Cloud Security**：安全工具包，提供 Zuul 代理中对 OAuth2 客户端请求中继器。  
&nbsp;&nbsp;●**Spring Cloud Sleuth**：Spring Cloud 应用的分布式跟踪实现，可以完美整合 Zipkin。  
&nbsp;&nbsp;●**Spring Cloud ZooKeeper**：基于 ZooKeeper 的服务发现与配置管理组件。  
&nbsp;&nbsp;●**Spring Cloud Starters**：Spring Cloud 的基础组件，它是基于Spring Boot 风格项目的基础依赖模块。  
&nbsp;&nbsp;●**Spring Cloud CLI**：用于在 Groovy 中快速创建 Spring Cloud 应用的 Spring Boot CLI 插件。  
&nbsp;&nbsp;●... ...  
# 微服务构建：Spring Boot
## 加载顺序
&nbsp;&nbsp;1、在命令行中传入的参数。  
&nbsp;&nbsp;2、SPRING_APPLICATION_JSON 中的属性。SPRING_APPLICATION_JSON 是以JSON 格式配置在系统环境变量中的的内容。  
&nbsp;&nbsp;3、java:comp/env 中的 JNDI 属性。  
&nbsp;&nbsp;4、Java 的系统属性，可以通过System.getProperties()获取的内容。  
&nbsp;&nbsp;5、操作系统的环境变量。  
&nbsp;&nbsp;6、通过random.*配置的随机属性。  
&nbsp;&nbsp;7、位于当前应用 jar 包之外，针对不同{profile}环境的配置文件内容，例如application-{profile}.properties 或是 YAML 定义的配置文件。  
&nbsp;&nbsp;8、位于当前应用 jar 包之内，针对不同{profile}环境的配置文件内容，例如application-{profile}.properties 或是 YAML 定义的配置文件。  
&nbsp;&nbsp;9、位于当前应用jar包之外的 application.properties 和 YAML 配置内容。  
&nbsp;&nbsp;10、位于当前应用jar包之内的 application.properties 和 YAML 配置内容。  
&nbsp;&nbsp;11、在@Configuration注解修改的类中，通过 @PropertySource 注解定义的属性。  
&nbsp;&nbsp;12、应用默认属性，使用 SpringApplication.setDefaultProperties 定义的内容。  
&nbsp;&nbsp;优先级按上面的顺序由高到低，数字越小优先级越高。  
## 监控与管理
&nbsp;&nbsp;spring-boot-starter-actuator 模块的实现对于实施微服务的中小团队来说，可以有效地省去或大大减少监控系统在采集指标时的开发量。  
### 原生端点
&nbsp;&nbsp;**应用配置类**：获取应用程序中加载的应用配置、环境变量、自动化配置报告等与Spring Boot 应用密切相关的配置类信息。  
&nbsp;&nbsp;**度量指标类**：获取应用程序运行过程中用于监控的度量指标，比如内存信息、线程池信息、HTTP 请求统计等。  
&nbsp;&nbsp;**操作控制类**：提供了对应用的关闭等操作类功能。  
#### 应用配置类
&nbsp;&nbsp;●/**autoconfig**：该端点用来获取应用的自动化配置报告，其中包括所有自动化配置的候选项。同时还列出了每个候选项是否满足自动化配置的各个先决条件。该端点可以方便地找到一些自动化配置为什么没有生效的具体原因。该报告内容将自动化配置内容分为以下两各部分：  
&nbsp;&nbsp;&nbsp;&nbsp;●/positiveMatches 中返回的是条件匹配成功的自动化配置。  
&nbsp;&nbsp;&nbsp;&nbsp;●/negativeMatches 中返回的是条件匹配不成功的自动化配置。
