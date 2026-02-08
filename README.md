# 📱 DevConnect - Social Media Platform for Developers

<div align="center">

**A full-stack social media application built for developers to connect, share posts, reels, stories, and collaborate in real-time.**

[Features](#-features) -  [Architecture](#-architecture) -  [Tech Stack](#-technology-stack) -  [Installation](#-installation) -  [API Documentation](#-api-documentation)

</div>

***

## 🎯 Overview

DevConnect is a social networking platform designed specifically for developers to share their work, connect with peers, and engage through posts, reels, and stories. It features real-time messaging, user interactions, and a clean, modern interface.

### Key Highlights

- **JWT Authentication** with stateless session management
- **Real-time Messaging** using WebSocket (STOMP protocol)
- **Social Features** including posts, reels, and stories with image/video support
- **Interactive Engagement** with likes, comments, and save functionality
- **User Connections** with follow/unfollow system
- **Cloudinary Integration** for media storage
- **Responsive UI** with modern design principles

***

## ✨ Features

### 🔐 Authentication
- JWT-based authentication with BCrypt password hashing
- User registration with email and password
- Secure login with token generation
- Profile management with editable details
- Gender field for user profiles

### 📝 Posts & Content
- Create posts with captions, images, and videos
- Like and unlike posts with real-time updates
- Comment on posts with user attribution
- Save posts for later viewing
- Delete own posts
- View all posts feed
- User-specific post filtering

### 🎥 Reels
- Create short video reels with titles
- Browse all reels feed
- View user-specific reels
- Cloudinary video storage

### 📖 Stories
- Share temporary stories with images and captions
- View stories from followed users
- Automatic timestamp tracking
- Story viewing by user ID

### 💬 Real-time Messaging
- One-on-one chat functionality
- WebSocket-based real-time message delivery
- Chat creation between users
- Message history retrieval
- Image sharing in messages
- Timestamp tracking (Asia/Kolkata timezone)

### 👥 Social Connections
- Follow/unfollow users
- Followers and following count
- User search by name or email
- View user profiles
- Popular user suggestions

### 🔍 Search & Discovery
- Search users by first name, last name, or email
- Get all users list
- View user profiles by ID
- Profile picture updates

***

## 🏗️ Architecture

DevConnect follows a **three-tier architecture**:

```
┌─────────────────────────────────────────────────┐
│         Presentation Layer (Frontend)           │
│      React 19 • Material-UI • Vite              │
└───────────────────┬─────────────────────────────┘
                    │ REST API + WebSocket
┌───────────────────▼─────────────────────────────┐
│      Business Logic Layer (Backend)             │
│   Spring Boot • Spring Security • JWT           │
│   WebSocket (STOMP) • Spring Data JPA           │
└───────────────────┬─────────────────────────────┘
                    │ JDBC
┌───────────────────▼─────────────────────────────┐
│          Data Access Layer                      │
│             MySQL Database                      │
└─────────────────────────────────────────────────┘
```

### Design Principles

- **Layered Architecture**: Separation of concerns across presentation, business, and data layers
- **RESTful API Design**: Resource-oriented endpoints with proper HTTP methods
- **Real-time Communication**: WebSocket for instant messaging
- **Stateless Authentication**: JWT tokens for scalable authentication
- **Component-Based Frontend**: Reusable React components with modular CSS

***

## 🛠️ Technology Stack

### Backend
- **Framework:** Spring Boot 3.4.4
- **Language:** Java 17
- **Security:** Spring Security + JWT (JJWT 0.12.6)
- **Database:** MySQL 8.0+
- **ORM:** Spring Data JPA (Hibernate)
- **Real-time:** Spring WebSocket + STOMP
- **Build Tool:** Maven

### Frontend
- **Library:** React 19.0.0
- **UI Framework:** Material-UI (MUI) 7.0.2
- **HTTP Client:** Axios 1.9.0
- **Build Tool:** Vite 6.3.1
- **State Management:** Redux 5.0.1 + Redux Thunk
- **WebSocket Client:** SockJS Client + STOMP.js
- **Form Validation:** Formik 2.4.6 + Yup 1.6.1
- **Icons:** MUI Icons Material

### Cloud Services
- **Media Storage:** Cloudinary (Image & Video uploads)

### Development Tools
- **Version Control:** Git & GitHub
- **Backend IDE:** IntelliJ IDEA / Eclipse
- **Frontend Editor:** Visual Studio Code
- **API Client:** Postman
- **Package Manager:** Maven (Backend), npm (Frontend)

***

## 📦 Installation

### Prerequisites

Ensure you have the following installed:
- **Java JDK 17+** - [Download](https://www.oracle.com/java/technologies/downloads/)
- **Node.js 18+** and **npm** - [Download](https://nodejs.org/)
- **MySQL 8.0+** - [Download](https://dev.mysql.com/downloads/)
- **Maven 3.8+** - [Download](https://maven.apache.org/download.cgi)
- **Git** - [Download](https://git-scm.com/)

***

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/rylauq-solutions/DevConnect.git
cd DevConnect
```

### 2. Database Setup

Create a MySQL database:

```sql
CREATE DATABASE devconnect;
```

### 3. Backend Configuration

Navigate to backend and update `application.properties` in `src/main/resources/`:

```properties
# Database Configuration
spring.datasource.url=jdbc:mysql://localhost:3306/devconnect
spring.datasource.username=your_mysql_username
spring.datasource.password=your_mysql_password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

# JPA/Hibernate
spring.jpa.show-sql=false
spring.jpa.hibernate.ddl-auto=update

# Server Port
server.port=8080

# Logging
logging.level.org.hibernate=ERROR
logging.level.com.socialmedia=DEBUG
logging.level.org.springframework.web=DEBUG
```

⚠️ **Important:** Update `JwtConstant.java` with your own secret key:

```java
// devconnect-backend/src/main/java/com/devconnect/config/JwtConstant.java
public static String SECRETKEY = "YourSecureSecretKeyMinimum256BitsForHS256Algorithm";
```

### 4. Run Spring Boot Backend

```bash
cd devconnect-backend
mvn clean install
mvn spring-boot:run
```

**Backend will run on:** `http://localhost:8080`

### 5. Frontend Configuration

Update `api.js` in `devconnect-frontend/src/config/`:

```javascript
export const API_BASE_URL = "http://localhost:8080";
```

### 6. Run React Frontend

Open a new terminal:

```bash
cd devconnect-frontend
npm install
npm run dev
```

**Frontend will run on:** `http://localhost:5173`

### 7. Access the Application

Open your browser and navigate to:
- **Frontend:** `http://localhost:5173`
- **Backend API:** `http://localhost:8080`

***

## 📚 API Documentation

### Base URL
```
http://localhost:8080/api
```

### Authentication Endpoints

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| `POST` | `/auth/signup` | User registration | ❌ |
| `POST` | `/auth/signin` | User login | ❌ |

### User Management

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| `GET` | `/api/users` | Get all users | ✅ |
| `GET` | `/api/users/{userId}` | Get user by ID | ✅ |
| `GET` | `/api/users/profile` | Get current user profile | ✅ |
| `PUT` | `/api/users` | Update user profile | ✅ |
| `PUT` | `/api/users/{userId2}` | Follow/unfollow user | ✅ |
| `GET` | `/api/users/search?query={query}` | Search users | ✅ |
| `DELETE` | `/api/users/{userId}` | Delete user | ✅ |

### Post Management

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| `POST` | `/api/posts` | Create new post | ✅ |
| `GET` | `/api/posts` | Get all posts | ✅ |
| `GET` | `/api/posts/{postId}` | Get post by ID | ✅ |
| `GET` | `/api/posts/user/{userId}` | Get user's posts | ✅ |
| `PUT` | `/api/posts/like/{postId}` | Like/unlike post | ✅ |
| `PUT` | `/api/posts/save/{postId}` | Save/unsave post | ✅ |
| `DELETE` | `/api/posts/{postId}` | Delete post | ✅ |

### Comment Management

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| `POST` | `/api/comments/post/{postId}` | Create comment | ✅ |
| `PUT` | `/api/comments/like/{commentId}` | Like/unlike comment | ✅ |

### Reels Management

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| `POST` | `/api/reels` | Create reel | ✅ |
| `GET` | `/api/reels` | Get all reels | ✅ |
| `GET` | `/api/reels/user/{userId}` | Get user's reels | ✅ |

### Story Management

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| `POST` | `/api/story` | Create story | ✅ |
| `GET` | `/api/story/user/{userId}` | Get user's stories | ✅ |

### Chat & Messaging

| Method | Endpoint | Description | Auth Required |
|--------|----------|-------------|---------------|
| `POST` | `/api/chats` | Create chat | ✅ |
| `GET` | `/api/chats` | Get user's chats | ✅ |
| `POST` | `/api/messages/chat/{chatId}` | Send message | ✅ |
| `GET` | `/api/messages/chat/{chatId}` | Get chat messages | ✅ |

### WebSocket Endpoint

| Protocol | Endpoint | Description |
|----------|----------|-------------|
| `STOMP` | `/ws` | WebSocket connection for real-time messaging |

**Message Mapping:**
- Subscribe: `/user/{groupId}/private`
- Send: `/app/chat/{groupId}`

***

## 🔐 Security Features

- **JWT Authentication**: Stateless token-based authentication with 24-hour expiry
- **Password Hashing**: BCrypt algorithm for secure password storage
- **CORS Configuration**: Configured for localhost and deployed frontend
- **Custom JWT Validator**: Filter-based token validation on each request
- **SQL Injection Prevention**: Parameterized queries via JPA
- **Stateless Sessions**: No server-side session storage

***

## 📂 Project Structure

```
DevConnect/
├── devconnect-backend/              # Spring Boot backend
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/devconnect/
│   │   │   │   ├── bean/            # Entity classes
│   │   │   │   │   ├── User.java
│   │   │   │   │   ├── Post.java
│   │   │   │   │   ├── Comment.java
│   │   │   │   │   ├── Like.java
│   │   │   │   │   ├── Reels.java
│   │   │   │   │   ├── Story.java
│   │   │   │   │   ├── Chat.java
│   │   │   │   │   └── Message.java
│   │   │   │   ├── config/          # Security & WebSocket config
│   │   │   │   │   ├── AppConfig.java
│   │   │   │   │   ├── JwtProvider.java
│   │   │   │   │   ├── JwtValidator.java
│   │   │   │   │   └── WebSocketConfig.java
│   │   │   │   ├── controller/      # REST controllers
│   │   │   │   │   ├── AuthController.java
│   │   │   │   │   ├── UserController.java
│   │   │   │   │   ├── PostController.java
│   │   │   │   │   ├── CommentController.java
│   │   │   │   │   ├── ReelsController.java
│   │   │   │   │   ├── StoryController.java
│   │   │   │   │   ├── ChatController.java
│   │   │   │   │   ├── MessageController.java
│   │   │   │   │   └── RealTimeChatController.java
│   │   │   │   ├── service/         # Business logic
│   │   │   │   │   ├── UserService.java
│   │   │   │   │   ├── PostService.java
│   │   │   │   │   ├── CommentService.java
│   │   │   │   │   ├── ReelsService.java
│   │   │   │   │   ├── StoryService.java
│   │   │   │   │   ├── ChatService.java
│   │   │   │   │   └── MessageService.java
│   │   │   │   ├── repository/      # Data access layer
│   │   │   │   ├── request/         # Request DTOs
│   │   │   │   ├── response/        # Response DTOs
│   │   │   │   └── exceptions/      # Custom exceptions
│   │   │   └── resources/
│   │   │       └── application.properties
│   │   └── test/                    # Tests
│   └── pom.xml
│
├── devconnect-frontend/             # React frontend
│   ├── src/
│   │   ├── components/              # Reusable components
│   │   │   ├── CreatePost/
│   │   │   ├── MiddlePart/
│   │   │   ├── Posts/
│   │   │   ├── Reels/
│   │   │   ├── SearchUser/
│   │   │   ├── SideBar/
│   │   │   └── Suggestions/
│   │   ├── pages/                   # Page components
│   │   │   ├── authentication/
│   │   │   ├── login/
│   │   │   ├── register/
│   │   │   ├── profile/
│   │   │   └── message/
│   │   ├── Redux/                   # State management
│   │   │   ├── Auth/
│   │   │   ├── Post/
│   │   │   └── Message/
│   │   ├── config/                  # API configuration
│   │   │   └── api.js
│   │   ├── utils/                   # Utility functions
│   │   │   └── uploadToCloudinary.js
│   │   └── global.css
│   ├── package.json
│   └── vite.config.js
│
└── README.md
```

***

## 🗺️ Database Schema

### Core Entities

- **users**: User accounts with followers/followings (stored as integer lists)
- **posts**: User posts with caption, image, video, and timestamps
- **postlikes**: Like relationships between users and posts
- **comments**: Comments on posts with user attribution
- **reels**: Short video content with titles
- **stories**: Temporary stories with images and captions
- **chats**: Chat rooms between users
- **messages**: Individual messages within chats

**Relationships:**
- User ↔ Posts (One-to-Many)
- User ↔ Reels (One-to-Many)
- User ↔ Stories (One-to-Many)
- Post ↔ Likes (One-to-Many)
- Post ↔ Comments (One-to-Many)
- Chat ↔ Users (Many-to-Many)
- Chat ↔ Messages (One-to-Many)

***

## 🔧 Troubleshooting

### Backend Issues

**Port Already in Use (8080)**
```bash
# Windows
netstat -ano | findstr :8080
taskkill /PID <PID> /F

# Linux/Mac
lsof -ti:8080 | xargs kill -9
```

**Database Connection Error**
- Verify MySQL is running
- Check credentials in `application.properties`
- Ensure database `devconnect` exists

**JWT Token Error**
- Ensure `SECRETKEY` in `JwtConstant.java` is at least 256 bits (32 characters)

### Frontend Issues

**CORS Error**
- Verify backend `AppConfig.java` includes your frontend URL
- Default allowed origins: `http://localhost:5173`, `https://dev-connect-beige.vercel.app`

**WebSocket Connection Failed**
- Check `WebSocketConfig.java` allowed origins
- Ensure backend is running on port 8080
- Verify STOMP endpoint `/ws` is accessible

**Cloudinary Upload Error**
- Check `cloud_name` and `upload_preset` in `uploadToCloudinary.js`
- Ensure Cloudinary credentials are correct
- Verify internet connectivity

**API Connection Failed**
```bash
# Clear cache and reinstall
rm -rf node_modules package-lock.json
npm install
```

***

## 📞 Support

For issues, questions, or contributions:
- **GitHub Issues**: [Report a bug](https://github.com/rylauq-solutions/DevConnect/issues)

***

<div align="center">

**Made with ❤️ using Spring Boot & React**

⭐ **Star this repository if you find it helpful!** ⭐

</div>
