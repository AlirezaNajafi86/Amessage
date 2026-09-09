\# 💬 Amessage



A modern real-time messaging platform built with \*\*Django\*\*, \*\*Django Channels\*\*, and \*\*WebSockets\*\*, featuring secure authentication, face recognition, one-to-one conversations, and a clean modern interface.



> 🚧 \*\*Project Status:\*\* Active Development



\---


\## ✨ Overview



\*\*Amessage\*\* is a full-stack real-time messaging application designed for instant communication between users.



The project combines \*\*Django REST Framework\*\* for API-based communication with \*\*Django Channels and WebSockets\*\* for real-time messaging and live conversation updates.



The goal of Amessage is to provide a modern messaging experience while keeping the architecture simple, scalable, and easy to extend.



\---



\## 🚀 Features



\### 🔐 Authentication



\* Username \& password authentication

\* Session-based authentication

\* Face recognition authentication

\* Face enrollment



\### 💬 Messaging



\* One-to-one conversations

\* Real-time message delivery

\* WebSocket-based communication

\* Persistent message storage

\* Message read status



\### 📋 Conversations



\* Real-time conversation list updates

\* Conversation search

\* Create new conversations

\* Delete conversations

\* Automatic latest-message previews



\### 🎨 Interface



\* Modern dark UI

\* Liquid-glass inspired design

\* Responsive layout

\* Clean conversation interface

\* Real-time UI updates



\---



\## ⚡ Real-Time Communication



Amessage uses \*\*Django Channels\*\* and \*\*WebSockets\*\* to provide real-time communication.



Instead of repeatedly refreshing the page, WebSockets maintain an active connection between the client and server.



```text

&#x20;                   Amessage

&#x20;                      │

&#x20;         ┌────────────┴────────────┐

&#x20;         │                         │

&#x20;      REST API                 WebSocket

&#x20;         │                         │

&#x20;         ▼                         ▼

&#x20;  Django / DRF             Django Channels

&#x20;         │                         │

&#x20;         ▼                         ▼

&#x20;     Database              Real-Time Events

&#x20;                                   │

&#x20;                                   ▼

&#x20;                             Frontend UI

```



This architecture allows the application to handle:



\* Instant message delivery

\* Live conversation updates

\* Message read states

\* Real-time conversation previews

\* WebSocket-based communication without page refreshes



\---



\## 🏗️ Architecture



Amessage follows a full-stack architecture built around Django.



```text

┌─────────────────────────────┐

│          Frontend           │

│       HTML / CSS / JS       │

└──────────────┬──────────────┘

&#x20;              │

&#x20;       HTTP / REST API

&#x20;              │

&#x20;              ▼

┌─────────────────────────────┐

│        Django / DRF         │

│        REST Backend         │

└──────────────┬──────────────┘

&#x20;              │

&#x20;              ▼

┌─────────────────────────────┐

│          SQLite             │

│          Database           │

└─────────────────────────────┘



&#x20;              +

&#x20;              

┌─────────────────────────────┐

│       Django Channels       │

│         WebSockets          │

└──────────────┬──────────────┘

&#x20;              │

&#x20;              ▼

┌─────────────────────────────┐

│      Real-Time Events       │

│ Messages / Conversations    │

└─────────────────────────────┘

```



\---



\## 🛠️ Tech Stack



\### Backend



\* \*\*Python\*\*

\* \*\*Django\*\*

\* \*\*Django REST Framework\*\*

\* \*\*Django Channels\*\*

\* \*\*WebSockets\*\*

\* \*\*Uvicorn\*\*

\* \*\*SQLite\*\*



\### Authentication \& Computer Vision



\* Django Authentication

\* OpenCV

\* Face Recognition

\* YuNet Face Detection

\* SFace Face Recognition



\### Frontend



\* HTML5

\* CSS3

\* JavaScript

\* Responsive Design



\---



\## 🔌 WebSocket Architecture



The application uses separate WebSocket responsibilities for chat communication and conversation updates.



\### Chat WebSocket



```text

/ws/chat/<conversation\_id>/

```



Used for:



\* Sending messages

\* Receiving messages

\* Broadcasting messages to conversation participants



\### Conversation WebSocket



```text

/ws/conversations/

```



Used for:



\* Real-time conversation list updates

\* Latest message updates

\* Live sidebar synchronization



This separation keeps the real-time architecture modular and easier to extend.



\---



\## 🤳 Face Recognition Authentication



Amessage includes a face recognition-based authentication system that allows users to authenticate using their face in addition to the traditional username and password method.



The system is built using \*\*OpenCV\*\* and modern face analysis models, with a pipeline designed to detect, extract, and compare facial features.



\### 🔍 Recognition Pipeline



The authentication process follows these main stages:



```text

Camera

&#x20;  │

&#x20;  ▼

Frame Capture

&#x20;  │

&#x20;  ▼

YuNet Face Detection

&#x20;  │

&#x20;  ▼

Face Detection

&#x20;  │

&#x20;  ▼

SFace Feature Extraction

&#x20;  │

&#x20;  ▼

Face Embedding

&#x20;  │

&#x20;  ▼

Feature Comparison

&#x20;  │

&#x20;  ▼

Identity Verification

```



\### 🧠 Face Detection — YuNet



Amessage uses \*\*YuNet\*\* for face detection.



YuNet is responsible for locating faces inside camera frames and determining the position of the detected face before recognition takes place.



The model used by the project is:



```text

face\_detection\_yunet\_2023mar.onnx

```



The detection stage provides the facial region required by the recognition pipeline.



\### 🧬 Face Recognition — SFace



After detecting a face, Amessage uses \*\*SFace\*\* to extract a numerical representation of the detected face.



The model used by the project is:



```text

face\_recognition\_sface\_2021dec.onnx

```



The extracted facial features are stored as part of the user's `FaceProfile`.



```text

Face

&#x20; │

&#x20; ▼

SFace

&#x20; │

&#x20; ▼

Feature Vector

&#x20; │

&#x20; ▼

FaceProfile

```



During authentication, a new face is processed through the same pipeline and its extracted features are compared with the stored features.



\### 🔐 Authentication Flow



```text

User opens Face Login

&#x20;       │

&#x20;       ▼

Camera captures frame

&#x20;       │

&#x20;       ▼

Detect face with YuNet

&#x20;       │

&#x20;       ▼

Extract features with SFace

&#x20;       │

&#x20;       ▼

Compare with stored profile

&#x20;       │

&#x20;       ├── Match ──────► Login

&#x20;       │

&#x20;       └── No Match ───► Authentication Failed

```



\### 🗂️ Face Profile Storage



Each enrolled user can have an associated `FaceProfile`.



The model contains:



\* User relationship

\* Extracted facial features

\* Creation timestamp

\* Last update timestamp



Conceptually:



```text

User

&#x20;│

&#x20;└── FaceProfile

&#x20;      ├── features

&#x20;      ├── created\_at

&#x20;      └── updated\_at

```



\### 🛡️ Design Considerations



The face recognition system is implemented as an additional authentication method rather than replacing traditional credentials.



This allows Amessage to support both:



\* Username \& password authentication

\* Face recognition authentication



The face recognition pipeline is currently designed for local development and experimentation and can be further improved with additional security measures before production deployment.



\---



\## 🗃️ Data Models



The messaging system currently includes the following core models:



```text

User

&#x20;│

&#x20;└── FaceProfile



User

&#x20;│

&#x20;└── Conversation

&#x20;       │

&#x20;       ├── Participants

&#x20;       │

&#x20;       └── Messages

&#x20;              │

&#x20;              ├── Sender

&#x20;              ├── Text

&#x20;              ├── Created At

&#x20;              └── Read Status

```



\### Core Models



\* `User`

\* `FaceProfile`

\* `Conversation`

\* `Message`



\---



\## 📱 Interface



The Messenger interface focuses on a clean and modern user experience.



Current UI elements include:



\* Conversation sidebar

\* Conversation search

\* User avatars

\* Message bubbles

\* Message timestamps

\* New conversation interface

\* Delete conversation controls

\* Real-time message rendering

\* Dark liquid-glass visual design



The desktop experience is currently the primary development focus.



\---



\## 🗺️ Roadmap



The project is actively being developed.



\### 🔜 Planned Improvements



\* \[ ] Unread message counter

\* \[ ] Online / Offline status

\* \[ ] Typing indicator

\* \[ ] Improved message timestamps

\* \[ ] Delivery states

\* \[ ] WebSocket reconnect handling

\* \[ ] Redis channel layer

\* \[ ] Production deployment

\* \[ ] Performance optimization

\* \[ ] Additional messaging features



\---



\## 📸 Screenshots



Screenshots will be added as the interface reaches a more complete stage.



\---



\## 🚀 Future Architecture



The current development environment uses SQLite and an in-memory channel layer for local testing.



The planned production architecture will move toward:



```text

&#x20;             Internet

&#x20;                 │

&#x20;                 ▼

&#x20;            Reverse Proxy

&#x20;                 │

&#x20;                 ▼

&#x20;             Django

&#x20;            /      \\

&#x20;           /        \\

&#x20;      REST API    WebSockets

&#x20;                      │

&#x20;                      ▼

&#x20;                   Redis

&#x20;                      │

&#x20;                      ▼

&#x20;                 PostgreSQL

```



The production architecture is planned to improve scalability, reliability, and real-time communication performance.



\---



\## 📂 Project Status



Amessage is currently under active development.



The core authentication, conversation system, messaging system, and WebSocket infrastructure are implemented.



The real-time conversation synchronization and additional messaging features are currently being developed.



\---



\## 👨‍💻 Author



\*\*Alireza Najafi\*\*



GitHub: \*\*AlirezaNajafi86\*\*



\---



\## 📄 License



License information will be added before the first public source-code release.



