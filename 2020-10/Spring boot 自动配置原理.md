### Spring boot 自动配置原理

---

spring boot 启动时通过 **@EnableAutoCofiguration** 注解，加载所有jar包下 META-INFO 文件下的 **spring.factory** 文件，获取键为 **EnableAutoConfiguration** 的所有值，将名称和这些值对应的类加载到IOC容器中，实现自动配置。

### spring.property 配置实现原理

---

spring.property文件的属性通过 注解 **@ConfigurationProperties**

加载到名为 xxxProperty的类中，该类以bean的形式通过注解 **@EnableConfigurationProperties**注入到名为 xxxAutoConfiguration的类中，从而实现通过 xx.property文件覆盖springboot 的自动配置。