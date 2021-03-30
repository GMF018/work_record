## Spring boot

### 配置

+ 动态设置配置是否启动或者在某个环境下生效

  > ```java
  > ## dev /test 环境下生效
  > @Profile({"dev","test"})
  > ## 在配置文件（.yml）中控制是否生效-- true 生效 false  失效
  > //@ConditionalOnProperty(name = "swagger-ui-open", havingValue = "true")
  > ```

### 注解

#### @Configuration

1. @Configuration标注在类上，相当于把该类作为spring的xml配置文件中的<beans>，作用为：配置spring容器(应用上下文)