```pom.xml
    <dependency>
			<groupId>org.springframework.boot</groupId>
			<artifactId>spring-boot-starter-mail</artifactId>
	</dependency>
```

```app.properties
spring.mail.host=smtp.gmail.com
spring.mail.port=587
spring.mail.username=
spring.mail.password=
#login with App Passwords
spring.mail.properties.mail.smtp.auth=true
spring.mail.properties.mail.smtp.starttls.enable=true
spring.mail.properties.mail.smtp.starttls.required=true
```

```java
@Service
@RequiredArgsConstructor
public class EmailServiceImpl implements EmailService {

   private final JavaMailSender mailSender;

   @Value("${spring.mail.username}")
   private String setFrom;

   @Async  //Enable async, remember to add @EnableAsync in the main class
   @Override
   public void sendSimpleEmail(String toEmail, String subject, String body) {
       SimpleMailMessage message = new SimpleMailMessage();
       message.setFrom(setFrom);
       message.setTo(toEmail);
       message.setSubject(subject);
       message.setText(body);

       mailSender.send(message);

   }
}
```
