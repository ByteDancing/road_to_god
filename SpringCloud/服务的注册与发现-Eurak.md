Eureka:
    微服务注册中心，基于REST服务，包含Server和Client；
    
    
    
版本升级到Finchley后，Eureka的依赖也因此改变：
```
pom文件：
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-dependencies</artifactId>
    <version>Finchley.SR2</version>
    <type>pom</type>
    <scope>import</scope>
</dependency>

```

####    编写一个Euraka服务的注册中心服务


- 加新的依赖：
```
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-netflix-eureka-server</artifactId>
</dependency>

```
 - 加注解
 
``` 
@SpringBootApplication
@EnableEurekaServer
public class EurekaApplication {
    private static final Logger logger = LoggerFactory.getLogger(EurekaApplication.class);

    public static void main(String[] args) {
        SpringApplication.run(EurekaApplication.class, args);
        logger.info("eureka server start success");
    }
}

```
- 写配置
``` 
server:
  port: 8761

eureka:
  client:
    register-with-eureka: false #不向其他EureakServer注册（包含自己）
    fetch-registry: false       #不从其他Eurake服务获取数据
    service-url:
      defaultZone: http://localhost:8761/eureka/

```
 
####    Eureka的加密访问
- 加依赖
```
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-security</artifactId>
    </dependency>
```
- 加注解
```

@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.csrf().ignoringAntMatchers("/eureka/**");
        super.configure(http);
    }

    @Bean
    @Override
    protected UserDetailsService userDetailsService() {
        /*System.out.println("**********");
        InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
        manager.createUser(User.withUsername("apple").password("hello").roles("USER").build());
        return manager;*/
        User.UserBuilder users = User.withDefaultPasswordEncoder();
        InMemoryUserDetailsManager manager = new InMemoryUserDetailsManager();
        manager.createUser(users.username("user").password("password").roles("USER").build());
        manager.createUser(users.username("admin").password("password").roles("USER", "ADMIN").build());
        return manager;
    }
}


```