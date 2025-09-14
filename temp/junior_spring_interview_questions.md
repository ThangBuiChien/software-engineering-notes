# Junior Spring Developer Interview Questions
*Tailored for 1 Year Experience Level*

## Section 1: Spring Basics & IoC Container

### Easy Questions (Must Know):
1. **What is Spring Framework and why do we use it?**
2. **What is Dependency Injection? Explain with a simple example.**
3. **What is Inversion of Control (IoC)?**
4. **What is a Spring Bean?**
5. **What is the Spring ApplicationContext?**
6. **How do you create a Spring application?**

### Medium Questions:
7. **What's the difference between ApplicationContext and BeanFactory?**
8. **What are the benefits of using Dependency Injection?**
9. **How does Spring manage object lifecycle?**
10. **What happens when Spring application starts up?**

---

## Section 2: Dependency Injection & Annotations

### Easy Questions (Must Know):
11. **What is @Autowired annotation?**
12. **What are the different types of dependency injection in Spring?**
13. **Explain constructor injection vs setter injection vs field injection.**
14. **Which injection type do you prefer and why?**
15. **What is @Component annotation?**
16. **What are @Service, @Repository, @Controller annotations?**

### Medium Questions:
17. **What happens if Spring finds multiple beans of the same type during @Autowired?**
18. **What is @Qualifier and when do you use it?**
19. **Can you inject a dependency without @Autowired? How?**
20. **What is @Primary annotation?**
21. **What's the difference between @Component and @Bean?**

---

## Section 3: Bean Configuration & Scopes

### Easy Questions (Must Know):
22. **What are Spring Bean scopes? Name the common ones.**
23. **What is the default scope of a Spring bean?**
24. **When would you use prototype scope?**
25. **How do you configure bean scope?**
26. **What is @Configuration annotation?**

### Medium Questions:
27. **What's the difference between singleton and prototype scope in practice?**
28. **What happens if you inject a prototype bean into a singleton bean?**
29. **How do you create beans using Java configuration?**
30. **What is @ComponentScan and what does it do?**
31. **Can you mix XML and annotation-based configuration?**

---

## Section 4: Bean Lifecycle & Advanced Features

### Easy Questions:
32. **What are @PostConstruct and @PreDestroy?**
33. **When are these lifecycle methods called?**
34. **What is bean initialization and destruction?**

### Medium Questions:
35. **Explain the complete Spring bean lifecycle.**
36. **What are circular dependencies in Spring?**
37. **How does Spring resolve circular dependencies?**
38. **Can circular dependencies cause problems? When?**
39. **What is @Lazy annotation and when would you use it?**

---

## Section 5: Property Management & Configuration

### Easy Questions:
40. **How do you inject properties/values from application.properties?**
41. **What is @Value annotation?**
42. **How do you externalize configuration in Spring?**

### Medium Questions:
43. **What is @PropertySource?**
44. **How do you handle different environments (dev, prod) in Spring?**
45. **What is SpEL (Spring Expression Language)?**

---

## Section 6: Spring AOP Basics

### Easy Questions (Awareness Level):
46. **What is AOP (Aspect-Oriented Programming)?**
47. **What is an Aspect in Spring?**
48. **What is an Advice? What types of advice do you know?**
49. **What is a Joinpoint?**
50. **Give an example where you might use AOP.**

### Medium Questions:
51. **How do you enable AOP in Spring?**
52. **What's the difference between @Before and @After advice?**
53. **What is a Pointcut?**

---

## Section 7: Spring Events (If mentioned in your experience)

### Easy Questions:
54. **What are Spring Events?**
55. **How do you publish an event in Spring?**
56. **How do you listen to events?**

### Medium Questions:
57. **What is @EventListener?**
58. **Can events be asynchronous? How?**

---

## Section 8: Practical/Scenario Questions

### Common Scenarios:
59. **You have a service that needs a repository. How would you wire them together?**
60. **Your application is throwing "No qualifying bean" error. What could be the reasons?**
61. **You want to use different database configurations for dev and prod. How would you handle this?**
62. **How do you test Spring components? What annotations do you use?**
63. **You need to execute some code after the application starts. How would you do it?**
64. **Explain how you would create a simple REST controller with a service layer.**

### Code Examples (Be ready to write simple code):
65. **Create a simple Service class with dependency injection.**
66. **Show how to configure a bean using @Configuration.**
67. **Write a simple @RestController that uses a @Service.**
68. **Create a bean with custom initialization logic.**

---

## Section 9: Spring Boot (If you've used it)

### Easy Questions:
69. **What is Spring Boot?**
70. **What is @SpringBootApplication?**
71. **What are Spring Boot starters?**
72. **What is application.properties/application.yml?**
73. **How do you run a Spring Boot application?**

### Medium Questions:
74. **What is auto-configuration in Spring Boot?**
75. **How do you exclude certain auto-configurations?**
76. **What is the difference between @Component and @SpringBootApplication?**

---

## Section 10: Testing (Basic Level)

### Easy Questions:
77. **How do you test Spring components?**
78. **What is @SpringBootTest?**
79. **What is @MockBean?**

---

## Bonus: Experience-Based Questions

### Behavioral Questions:
80. **Describe a challenging problem you solved using Spring.**
81. **What Spring features have you used in your current/previous project?**
82. **How has Spring made your development easier?**
83. **What was the most difficult Spring concept to understand initially?**
84. **How do you stay updated with Spring framework changes?**

---

## Quick Answer Tips for Each Section:

### **Spring Basics:**
- Always mention "loose coupling" and "easier testing" as DI benefits
- Know that ApplicationContext is the main Spring container

### **Dependency Injection:**
- Prefer constructor injection, explain why (immutability, required dependencies)
- @Qualifier solves multiple bean conflicts

### **Bean Scopes:**
- Singleton = one instance per container (default)
- Prototype = new instance every time requested

### **Lifecycle:**
- @PostConstruct = after dependency injection
- @PreDestroy = before bean destruction

### **AOP:**
- Cross-cutting concerns like logging, security
- Don't go too deep - awareness level is fine

### **Practical Questions:**
- Always think about real project examples
- Show understanding of layered architecture (Controller → Service → Repository)

---

## Interview Day Strategy:

1. **Start simple** - Give basic answer first, then elaborate if asked
2. **Use examples** - Reference your actual project experience
3. **Be honest** - If you don't know something, say so but show willingness to learn
4. **Ask questions** - Show interest in their Spring usage

**Remember:** For junior level, they want to see you understand the concepts and can work with them, not that you're a Spring expert! 🚀