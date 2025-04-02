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

SimpleMailMessage

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

HTMLMailMessage

```java
    @Async
    @Override
    public void sendHtmlFormatSuccessPayment(String toEmail, String subject,  String customerName, String amount, String orderId) throws MessagingException, IOException {
        MimeMessage message = mailSender.createMimeMessage();
        MimeMessageHelper helper = new MimeMessageHelper(message, true);

        helper.setFrom(setFrom);
        helper.setTo(toEmail);
        helper.setSubject(subject);

        // Load HTML template
        ClassPathResource resource = new ClassPathResource("static/payment-confirmation-template.html");
        String htmlTemplate = StreamUtils.copyToString(resource.getInputStream(), StandardCharsets.UTF_8);

        // Replace placeholders with actual values
        String htmlContent = htmlTemplate
                .replace("${customerName}", customerName)
                .replace("${amount}", amount)
                .replace("${orderId}", orderId);

        // Set the HTML content
        helper.setText(htmlContent, true);

        mailSender.send(message);
    }
```

```html
<div class="content">
  <p>Dear ${customerName},</p>
  <p>
    Thank you for your payment! Your payment of ${amount} for order ${orderId}
    has been successfully processed.
  </p>
  <p>If you have any questions, please contact us at support@example.com.</p>
</div>
```
