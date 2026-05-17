# 💬 SpringBoot WebSocket Chat Application

A real-time group chat application built with **Spring Boot** and **WebSocket (STOMP)**, featuring a clean browser-based UI powered by **Thymeleaf**. Users can join a shared chat room, send messages instantly, and receive live join/leave notifications — all without page reloads.

---

## 🚀 Features

- ✅ Real-time bidirectional messaging via WebSocket
- ✅ STOMP messaging protocol over WebSocket
- ✅ Join/Leave event notifications broadcast to all users
- ✅ Browser-based UI (no frontend framework required)
- ✅ Thymeleaf template rendering
- ✅ Lombok for clean, boilerplate-free Java models
- ✅ Built on Spring Boot 3.3.5 with Java 17

---

## 🛠️ Tech Stack

| Layer        | Technology                          |
|--------------|--------------------------------------|
| Backend      | Spring Boot 3.3.5, Java 17           |
| WebSocket    | Spring WebSocket + STOMP protocol    |
| Templating   | Thymeleaf                            |
| Build Tool   | Maven (via Maven Wrapper)            |
| Utility      | Lombok                               |
| Frontend     | HTML, CSS, JavaScript (SockJS + STOMP.js) |

---

## 📁 Project Structure

```
SpringBoot-WebSocket-Chat-Application/
├── src/
│   ├── main/
│   │   ├── java/com/chat/app/
│   │   │   ├── config/          # WebSocket configuration (STOMP endpoints, message broker)
│   │   │   ├── controller/      # Chat controller (message handling)
│   │   │   └── model/           # ChatMessage model (sender, content, type)
│   │   └── resources/
│   │       ├── static/          # CSS, JavaScript (SockJS, STOMP.js)
│   │       └── templates/       # Thymeleaf HTML templates (chat UI)
│   └── test/
├── .mvn/wrapper/                # Maven wrapper files
├── pom.xml
├── mvnw / mvnw.cmd              # Maven wrapper scripts
└── README.md
```

---

## ⚙️ Prerequisites

Make sure you have the following installed:

- **Java 17+** — [Download here](https://adoptium.net/)
- **Maven 3.6+** *(or use the included Maven Wrapper — no separate install needed)*
- A modern web browser

---

## 🏃 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/camelia0011/SpringBoot-WebSocket-Chat-Application.git
cd SpringBoot-WebSocket-Chat-Application
```

### 2. Build the Project

Using the Maven Wrapper (no Maven installation required):

```bash
# Linux / macOS
./mvnw clean install

# Windows
mvnw.cmd clean install
```

### 3. Run the Application

```bash
# Linux / macOS
./mvnw spring-boot:run

# Windows
mvnw.cmd spring-boot:run
```

### 4. Open the Chat

Navigate to:

```
http://localhost:8080
```

Open multiple browser tabs or windows to simulate multiple users chatting in real time.

---

## 📡 How It Works

```
Browser                    Spring Boot Server
  │                               │
  │──── HTTP GET /  ─────────────>│  (Thymeleaf renders chat page)
  │<─── HTML page ────────────────│
  │                               │
  │──── WS Connect /ws ──────────>│  (WebSocket handshake via SockJS)
  │                               │
  │──── STOMP SUBSCRIBE ─────────>│  /topic/public
  │                               │
  │──── STOMP SEND ──────────────>│  /app/chat.sendMessage
  │                               │
  │<─── STOMP BROADCAST ──────────│  /topic/public  (to all subscribers)
  │                               │
```

- **SockJS** provides a fallback for browsers that don't support native WebSocket.
- **STOMP** (Simple Text Oriented Messaging Protocol) is layered on top to handle pub/sub routing.
- The server broadcasts messages to all connected clients via the `/topic/public` destination.
- Join and leave events are sent as special message types so the UI can display notifications.

---

## 🔌 WebSocket Endpoints

| Endpoint               | Description                              |
|------------------------|------------------------------------------|
| `/ws`                  | WebSocket connection endpoint (SockJS)   |
| `/app/chat.sendMessage`| Send a chat message                      |
| `/app/chat.addUser`    | Register a new user joining the chat     |
| `/topic/public`        | Subscribe to receive broadcasted messages|

---

## 📦 Key Dependencies (pom.xml)

```xml
<!-- Web MVC -->
<dependency>spring-boot-starter-web</dependency>

<!-- WebSocket support (STOMP) -->
<dependency>spring-boot-starter-websocket</dependency>

<!-- Server-side HTML templating -->
<dependency>spring-boot-starter-thymeleaf</dependency>

<!-- Reduce Java boilerplate -->
<dependency>lombok</dependency>
```

---

## 🖥️ Usage

1. Open `http://localhost:8080` in your browser.
2. Enter your **username** and click **Join**.
3. A join notification is broadcast to all connected users.
4. Type a message in the input box and press **Send** (or hit Enter).
5. Messages appear instantly for all connected users.
6. Closing the tab triggers a leave notification.

---

## 🧪 Running Tests

```bash
./mvnw test
```

---

## 🔧 Configuration

The application runs on **port 8080** by default. To change it, add the following to `src/main/resources/application.properties`:

```properties
server.port=9090
```

---

## 📌 Notes

- This is a **group chat** application — all users share a single chat room.
- There is **no authentication** or **message persistence** — messages exist only for the duration of the session.
- Designed as a learning project demonstrating Spring Boot WebSocket + STOMP integration.

---

## 🤝 Contributing

Contributions are welcome! Feel free to open issues or submit pull requests.

1. Fork the repository
2. Create your feature branch: `git checkout -b feature/your-feature`
3. Commit your changes: `git commit -m 'Add your feature'`
4. Push to the branch: `git push origin feature/your-feature`
5. Open a Pull Request

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 🙏 Acknowledgements

- Inspired by the [EmbarkXOfficial](https://github.com/EmbarkXOfficial/sb-websocket-chat-app) WebSocket chat tutorial
- [Spring WebSocket Documentation](https://docs.spring.io/spring-framework/docs/current/reference/html/web.html#websocket)
- [SockJS](https://github.com/sockjs/sockjs-client) & [STOMP.js](https://github.com/stomp-js/stompjs)
