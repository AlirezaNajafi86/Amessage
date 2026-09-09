# 💬 Amessage

A modern real-time messaging platform built with **Django**, **Django Channels**, and **WebSockets**, featuring authentication, face recognition, one-to-one conversations, and a clean modern interface.

> 🚧 **Project Status:** Active Development

---

## ✨ Overview

**Amessage** is a full-stack real-time messaging application designed for instant communication between users.

The project combines **Django REST Framework** for API-based communication with **Django Channels** and **WebSockets** for real-time messaging and live conversation updates.

The goal of Amessage is to provide a modern messaging experience with a simple, modular, and extensible architecture.

---

## 🚀 Features

### 🔐 Authentication

* Username & password authentication
* Session-based authentication
* Face recognition authentication
* Face enrollment

### 💬 Messaging

* One-to-one conversations
* Real-time message delivery
* WebSocket-based communication
* Persistent message storage
* Message read status

### 📋 Conversations

* Real-time conversation list updates
* Conversation search
* Create new conversations
* Delete conversations
* Automatic latest-message previews

### 🎨 Interface

* Modern dark UI
* Liquid-glass inspired design
* Responsive layout
* Clean conversation interface
* Real-time UI updates

---

## ⚡ Real-Time Communication

Amessage uses **Django Channels** and **WebSockets** to provide real-time communication.

Instead of repeatedly refreshing the page, WebSockets maintain an active connection between the client and server.

```text
                    Amessage
                       │
          ┌────────────┴────────────┐
          │                         │
       REST API                 WebSocket
          │                         │
          ▼                         ▼
   Django / DRF             Django Channels
          │                         │
          ▼                         ▼
      Database              Real-Time Events
                                    │
                                    ▼
                              Frontend UI
```

This architecture enables:

* Instant message delivery
* Live conversation updates
* Message read states
* Real-time conversation previews
* Communication without page refreshes

---

## 🏗️ Architecture

Amessage follows a full-stack architecture built around Django.

```text
┌─────────────────────────────┐
│          Frontend           │
│       HTML / CSS / JS       │
└──────────────┬──────────────┘
               │
          HTTP / REST
               │
               ▼
┌─────────────────────────────┐
│        Django / DRF         │
│        REST Backend         │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│           SQLite            │
│          Database           │
└─────────────────────────────┘

               +

┌─────────────────────────────┐
│       Django Channels       │
│         WebSockets          │
└──────────────┬──────────────┘
               │
               ▼
┌─────────────────────────────┐
│      Real-Time Events       │
│ Messages / Conversations    │
└─────────────────────────────┘
```

---

## 🛠️ Tech Stack

### Backend

* **Python**
* **Django**
* **Django REST Framework**
* **Django Channels**
* **WebSockets**
* **Uvicorn**
* **SQLite**

### Authentication & Computer Vision

* Django Authentication
* OpenCV
* Face Recognition
* YuNet Face Detection
* SFace Face Recognition

### Frontend

* HTML5
* CSS3
* JavaScript
* Responsive Design

---

## 🔌 WebSocket Architecture

The application uses separate WebSocket responsibilities for chat communication and conversation updates.

### Chat WebSocket

```text
/ws/chat/<conversation_id>/
```

Used for:

* Sending messages
* Receiving messages
* Broadcasting messages to conversation participants
* Updating message read status

### Conversation WebSocket

```text
/ws/conversations/
```

Used for:

* Real-time conversation list updates
* Latest message updates
* Live sidebar synchronization

This separation keeps the real-time architecture modular and easier to extend.

---

## 🤳 Face Recognition Authentication

Amessage includes a face recognition authentication system that allows users to authenticate using their face in addition to traditional credentials.

The system is built using **OpenCV** and modern face analysis models.

### 🔍 Recognition Pipeline

```text
Camera
  │
  ▼
Frame Capture
  │
  ▼
YuNet Face Detection
  │
  ▼
Face Detection
  │
  ▼
SFace Feature Extraction
  │
  ▼
Face Embedding
  │
  ▼
Feature Comparison
  │
  ▼
Identity Verification
```

### 🧠 Face Detection — YuNet

Amessage uses **YuNet** for face detection.

YuNet locates faces inside camera frames and provides the facial region required by the recognition pipeline.

Model:

```text
face_detection_yunet_2023mar.onnx
```

### 🧬 Face Recognition — SFace

After detecting a face, Amessage uses **SFace** to extract a numerical representation of the detected face.

Model:

```text
face_recognition_sface_2021dec.onnx
```

The extracted features are stored in the user's `FaceProfile`.

```text
Face
 │
 ▼
SFace
 │
 ▼
Feature Vector
 │
 ▼
FaceProfile
```

During authentication, a new face is processed through the same pipeline and compared with the stored features.

### 🔐 Authentication Flow

```text
User opens Face Login
        │
        ▼
Camera captures frame
        │
        ▼
Detect face with YuNet
        │
        ▼
Extract features with SFace
        │
        ▼
Compare with stored profile
        │
        ├── Match ──────► Login
        │
        └── No Match ───► Authentication Failed
```

### 🗂️ Face Profile Storage

Each enrolled user can have an associated `FaceProfile`.

The profile contains:

* User relationship
* Extracted facial features
* Creation timestamp
* Last update timestamp

Conceptually:

```text
User
 │
 └── FaceProfile
      ├── features
      ├── created_at
      └── updated_at
```

### 🛡️ Design Considerations

Face recognition is implemented as an additional authentication method rather than replacing traditional credentials.

Amessage currently supports:

* Username & password authentication
* Face recognition authentication

The face recognition system is currently intended for local development and experimentation and can be further improved with additional security measures before production deployment.

---

## 🗃️ Data Models

The messaging system currently includes the following core models:

```text
User
 │
 └── FaceProfile

User
 │
 └── Conversation
      │
      ├── Participants
      │
      └── Messages
           │
           ├── Sender
           ├── Text
           ├── Created At
           └── Read Status
```

### Core Models

* `User`
* `FaceProfile`
* `Conversation`
* `Message`

---

## 📱 Interface

The Messenger interface focuses on a clean and modern user experience.

Current UI elements include:

* Conversation sidebar
* Conversation search
* User avatars
* Message bubbles
* Message timestamps
* New conversation interface
* Delete conversation controls
* Real-time message rendering
* Dark liquid-glass visual design

The desktop experience is currently the primary development focus.

---

## 📸 Screenshots

Screenshots will be added as the interface reaches a more complete stage.

<!-- Screenshots will be added here -->

---

## 🗺️ Roadmap

The project is actively being developed.

### 🔜 Planned Improvements

* [ ] Unread message counter
* [ ] Online / Offline status
* [ ] Typing indicator
* [ ] Improved message timestamps
* [ ] Delivery states
* [ ] WebSocket reconnect handling
* [ ] Redis channel layer
* [ ] Production deployment
* [ ] Performance optimization
* [ ] Additional messaging features

---

## 🚀 Future Architecture

The current development environment uses SQLite and an in-memory channel layer for local testing.

The planned production architecture will move toward:

```text
             Internet
                 │
                 ▼
            Reverse Proxy
                 │
                 ▼
              Django
             /      \
            /        \
       REST API    WebSockets
                       │
                       ▼
                    Redis
                       │
                       ▼
                  PostgreSQL
```

The production architecture is planned to improve scalability, reliability, and real-time communication performance.

---

## 📂 Project Status

Amessage is currently under active development.

The core authentication, conversation system, messaging system, and WebSocket infrastructure are implemented.

Additional real-time and messaging features are currently being developed.

---

## 👨‍💻 Author

**Alireza Najafi**

GitHub: **AlirezaNajafi86**

---

## 📄 License

License information will be added before the first public source-code release.
