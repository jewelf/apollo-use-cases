# Purpose

演示[Spring Cloud Zuul](https://cloud.spring.io/spring-cloud-netflix/single/spring-cloud-netflix.html#netflix-zuul-reverse-proxy)如何通过Apollo配置中心实现动态路由

# Instructions

1. 在Apollo配置中心创建AppId为`spring-cloud-zuul`的项目
2. 在默认的`application`下做如下配置（可以通过文本模式直接复制、粘贴下面的内容）：

    ```properties
    server.port = 9090
    zuul.routes.test.path = /**
    zuul.routes.test.url = https://github.com
    #zuul.routes.test.url = https://github.com/ctripcorp/apollo
    ```
3. 运行`com.ctrip.framework.apollo.use.cases.spring.cloud.zuul.Application`启动Demo
4. 程序会自动打开`http://localhost:9090`，显式内容为GitHub首页 
5. 在Apollo配置中心修改配置，把`zuul.routes.test.url`的值改为`https://github.com/ctripcorp/apollo`并发布配置
  * 可以以文本模式在原来生效的`zuul.routes.test.url`前面加上`#`注释掉，同时把原来注释掉的指向`https://github.com/ctripcorp/apollo`的配置反注释掉来快速修改
6. 刷新`http://localhost:9090`页面，显式的内容会变成Apollo配置中心的GitHub首页，说明动态路由生效了
