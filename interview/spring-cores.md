# Spring Core Knowledge for Java Developer Interviews

## Table of Contents

- [Core Concepts](#core-concepts)
- [Dependency Injection](#dependency-injection)
- [Spring Beans](#spring-beans)
- [Spring Configuration](#spring-configuration)
- [Bean Lifecycle](#bean-lifecycle)
- [AOP Basics](#aop-basics)
- [Spring Boot Essentials](#spring-boot-essentials)

## Core Concepts

- **IoC (Inversion of Control)**
- **DI (Dependency Injection)**
- **Spring Container/Context**
- **ApplicationContext vs BeanFactory**
- **Component Scanning**

- **IoC (Inversion of Control)**

  - Basic principle where control over object creation and lifecycle is transferred to Spring framework

  ```java
  // Without IoC
  class OrderService {
      private PaymentService paymentService = new PaymentService(); // Direct creation
  }

  // With IoC
  @Service
  class OrderService {
      private final PaymentService paymentService; // Spring manages creation

      public OrderService(PaymentService paymentService) {
          this.paymentService = paymentService;
      }
  }
  ```

- **DI (Dependency Injection)**

  - Three types of injection:

    1. Constructor Injection (Recommended)
    2. Setter Injection
    3. Field Injection

  ```java
  // Constructor Injection
  @Service
  public class UserService {
      private final UserRepository userRepository;

      @Autowired // Optional since Spring 4.3 if only one constructor
      public UserService(UserRepository userRepository) {
          this.userRepository = userRepository;
      }
  }

  // Setter Injection
  @Service
  public class UserService {
      private UserRepository userRepository;

      @Autowired
      public void setUserRepository(UserRepository userRepository) {
          this.userRepository = userRepository;
      }
  }

  // Field Injection (Not Recommended)
  @Service
  public class UserService {
      @Autowired
      private UserRepository userRepository;
  }
  ```

- **Spring Container/Context**
- Manages bean lifecycle
- Basic configuration:

```java
@Configuration
public class AppConfig {
    @Bean
    public UserService userService() {
        return new UserService();
    }
}

// Usage
ApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);
UserService userService = context.getBean(UserService.class);
```

- **ApplicationContext vs BeanFactory**
- **Component Scanning**

```java
@Configuration
@ComponentScan(basePackages = "com.example")
public class AppConfig {
}

// Components that will be scanned
@Component
class BasicService {}

@Repository
class UserRepository {}

@Service
class UserService {}

@Controller
class UserController {}
```

## Dependency Injection

- **Constructor Injection**
- **Setter Injection**
- **Field Injection**
- **@Autowired**
- **@Qualifier**
- **@Primary**

```java
// Interface
public interface MessageService {
    String getMessage();
}

// Multiple implementations
@Service
public class EmailService implements MessageService {
    @Override
    public String getMessage() {
        return "Email message";
    }
}

@Service
@Primary  // Makes this the default implementation
public class SMSService implements MessageService {
    @Override
    public String getMessage() {
        return "SMS message";
    }
}

// 1. Constructor Injection (Recommended)
@Service
public class NotificationService {
    private final MessageService messageService;

    @Autowired // Optional if single constructor
    public NotificationService(MessageService messageService) {
        this.messageService = messageService;
    }
}

// 2. Setter Injection
@Service
public class NotificationService {
    private MessageService messageService;

    @Autowired
    public void setMessageService(MessageService messageService) {
        this.messageService = messageService;
    }
}

// 3. Field Injection (Not Recommended)
@Service
public class NotificationService {
    @Autowired
    private MessageService messageService;
}

// Using @Qualifier
@Service
public class NotificationService {
    private final MessageService messageService;

    @Autowired
    public NotificationService(@Qualifier("emailService") MessageService messageService) {
        this.messageService = messageService;
    }
}

// Multiple dependencies example
@Service
public class CompleteNotificationService {
    private final MessageService messageService;
    private final UserService userService;
    private final LogService logService;

    @Autowired
    public CompleteNotificationService(
        @Qualifier("emailService") MessageService messageService,
        UserService userService,
        LogService logService
    ) {
        this.messageService = messageService;
        this.userService = userService;
        this.logService = logService;
    }
}
```

## Spring Beans

- **Bean Scopes**
  - **Singleton**
  - **Prototype**
  - **Request**
  - **Session**
  - **Global-session**
- **Bean Definition**
- **Bean Lifecycle Annotations**
  - **@Component**
  - **@Service**
  - **@Repository**
  - **@Controller**

## Spring Configuration

- **Java-based (@Configuration)**
- **XML-based Configuration**
- **Annotation-based Configuration**
- **@ComponentScan**
- **@PropertySource**
- **@Value**
- **Properties files**

## Bean Lifecycle

- **Initialization**
- **Destruction**
- **@PostConstruct**
- **@PreDestroy**
- **InitializingBean**
- **DisposableBean**

## AOP Basics

- **Aspect**
- **Pointcut**
- **Advice**
- **JoinPoint**
- **@Before**
- **@After**
- **@Around**

## Spring Boot Essentials

- **Auto-configuration**
- **Starter dependencies**
- **application.properties/yaml**
- **@SpringBootApplication**
- **Embedded servers**
- **Actuator basics**
