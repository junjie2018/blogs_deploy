SpringBoot Actuator默认的地址是在`server.servlet.context-path`的基础上加上`actuator/*`，这个细节，我之前一直没有关注到。`management.endpoints.web.base-path`配置实际上只会印象到`actuator`段。

## 参考资料

好东西，慢慢消化~~~

[Spring Boot (十九)：使用 Spring Boot Actuator 监控应用](http://www.ityouknow.com/springboot/2018/02/06/spring-boot-actuator.html)
