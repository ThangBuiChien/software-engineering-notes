# Real Time Chat Application using Spring WebSocket

## Function requirements

    - Real time chat application
    - User could join multi chat rooms and chat rooms could have multi users
    - User could send message to chat room
    - User coud see the history chat of chat room

## Class design

## Code

```pom.xml
<dependency>
	<groupId>org.springframework.boot</groupId>
	<artifactId>spring-boot-starter-websocket</artifactId>
</dependency>
```

```java

@Configuration
@EnableWebSocketMessageBroker
public class WebSocketConfig implements WebSocketMessageBrokerConfigurer {
    @Override
    public void registerStompEndpoints(StompEndpointRegistry registry) {
        registry.addEndpoint("/websocket").withSockJS();
    }

    @Override
    public void configureMessageBroker(MessageBrokerRegistry registry) {
        registry.setApplicationDestinationPrefixes("/app");
        registry.enableSimpleBroker("/topic");
    }

}
```

The logic is very simple, we have 2 main methods: + registerStompEndpoints: register the endpoint for websocket + configureMessageBroker: configure the message broker

=> Use js to connect to websocket, then just send message to topic and their ID. Handle the message when receive message from topic

```js
var socket = new SockJS("/websocket");
stompClient = Stomp.over(socket);
stompClient.connect({}, onConnected, onError);
```

```js
function onConnected() {
  // subscribe to topic based on room id
  stompClient.subscribe("/topic/room/" + room, onMessageReceived);
}
```

```js
function onMessageReceived(payload) {
    var message = JSON.parse(payload.body);
    // handle message on frontend, get content using message.content

```

```js
//Handle send message
function send(event) {
  var messageContent = messageInput.value.trim();

  if (messageContent && stompClient) {
    var chatMessage = {
      sender: username,
      content: messageInput.value,
      type: "CHAT",
    };

    // Send the message to the selected room
    stompClient.send("/app/chat.send/" + room, {}, JSON.stringify(chatMessage));
    messageInput.value = "";
  }
  event.preventDefault();
}
```

Message controller handle

```java
@Controller
@RequiredArgsConstructor
public class ChatController {

  @MessageMapping("/chat.register/{roomId}")
    @SendTo("/topic/room/{roomId}") // Use room ID dynamically
    public ChatMessage register(
            @DestinationVariable Long roomId,
            @Payload ChatMessage chatMessage,
            SimpMessageHeaderAccessor headerAccessor) {
              // code to store in db if needed

              return chatMessage; // Notify other users in the room about the new user
    }
  @MessageMapping("/chat.send/{roomId}")
    @SendTo("/topic/room/{roomId}") // Send message to a specific room
    public ChatMessage sendMessage(@DestinationVariable Long roomId, @Payload ChatMessage chatMessage) {
      // code to store in db if needed

      return chatMessage; // Broadcast the message to the room
    }
}
```
