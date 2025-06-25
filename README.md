# Real-Time Collaborative Whiteboard Application

A feature-rich, real-time collaborative whiteboard application built with modern web technologies that allows multiple users to draw, collaborate, and share ideas simultaneously through WebSocket connections.

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Architecture](#architecture)
- [Installation](#installation)
  - [Prerequisites](#prerequisites)
  - [Backend Setup](#backend-setup)
  - [Frontend Setup](#frontend-setup)
  - [Environment Variables](#environment-variables)
- [Usage](#usage)
- [API Documentation](#api-documentation)
- [Security Implementation](#security-implementation)
- [Deployment](#deployment)
- [Contributing](#contributing)
- [License](#license)

## 🔍 Overview

This Real-Time Collaborative Whiteboard application enables multiple users to join a shared canvas and draw/collaborate in real-time. Built using the MERN stack (MongoDB, Express.js, React.js, Node.js) with WebSocket integration, it offers a seamless drawing experience with JWT authentication to ensure secure access to shared whiteboards.

## ✨ Features

- **Real-time Collaboration**: Multiple users can draw on the same whiteboard simultaneously
- **User Authentication**: Secure JWT-based authentication system
- **Persistent Whiteboards**: Save and load whiteboard sessions from MongoDB
- **Drawing Tools**:
  - Pen with adjustable thickness and colors
  - Shapes (rectangles, circles, lines)
  - Text input capabilities
  - Selection and manipulation of drawn elements
- **Session Management**: Create, join, and manage whiteboard sessions
- **Canvas Operations**: Undo/redo functionality, clear canvas, save as image
- **User Presence**: See who is currently active on the whiteboard
- **Responsive Design**: Works across desktop and mobile devices

## 🛠️ Technology Stack

### Frontend
- **React.js**: UI library for building the user interface
- **Socket.io-client**: Client-side WebSocket implementation for real-time updates
- **rough.js**: Library for creating hand-drawn, sketchy graphics
- **perfect-freehand**: For smooth, natural drawing experience
- **Tailwind CSS**: Utility-first CSS framework for styling
- **React Router**: For navigation between different views
- **Axios**: For HTTP requests to the backend API

### Backend
- **Node.js**: JavaScript runtime environment
- **Express**: Web application framework
- **Socket.io**: Server-side WebSocket implementation
- **MongoDB**: NoSQL database for storing whiteboard data
- **Mongoose**: MongoDB object modeling tool
- **JWT (jsonwebtoken)**: For secure authentication
- **bcrypt**: For password hashing
- **cors**: For Cross-Origin Resource Sharing
- **dotenv**: For environment variables management

## 🏗️ Architecture

The application follows a client-server architecture:

### Backend Architecture
- **Server**: Express.js server handling HTTP requests and WebSocket connections
- **Authentication**: JWT-based authentication middleware for API endpoints and WebSocket connections
- **Database**: MongoDB for storing user data, whiteboard sessions, and drawing elements
- **WebSocket Server**: Real-time communication between clients using Socket.io
- **Routes**: RESTful API endpoints for user management and whiteboard operations

### Frontend Architecture
- **Components**: Reusable React components for UI elements
- **State Management**: React context API for application state
- **WebSocket Client**: Socket.io client for real-time updates
- **Canvas Rendering**: HTML5 Canvas for rendering drawings
- **Routing**: React Router for navigation between pages

## 🚀 Installation

### Prerequisites
- Node.js (v14 or later)
- MongoDB (local instance or MongoDB Atlas)
- npm or yarn

### Backend Setup
```bash
# Clone the repository
git clone https://github.com/navyarejeti10/collaborative-whiteboard.git
cd collaborative-whiteboard/whiteboard_az/backend

# Install dependencies
npm install

# Start the backend server
node server.js
```

### Frontend Setup
```bash
# Navigate to the frontend directory
cd ../whiteboard

# Install dependencies
npm install

# Start the development server
npm start
```

### Environment Variables

Create a `.env` file in the backend directory with the following variables:

```
# Server configuration
PORT=5001

# MongoDB connection string
MONGODB_URI=mongodb://localhost:27017/whiteboard_app
# Or use MongoDB Atlas
# MONGODB_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/whiteboard_app

# JWT Secret Key
JWT_SECRET=your_secret_key

# CORS Origins
CORS_ORIGIN=http://localhost:3000
```

## 🖌️ Usage

1. Register a new account or login with existing credentials
2. Create a new whiteboard or join an existing one
3. Use the drawing tools to collaborate in real-time
4. Share the whiteboard ID with others to invite them to collaborate
5. Save your work and access it later

## 📝 API Documentation

### Authentication Endpoints

| Endpoint | Method | Description | Request Body | Response |
|----------|--------|-------------|--------------|----------|
| `/api/users/register` | POST | Register a new user | `{ username, email, password }` | `{ user, token }` |
| `/api/users/login` | POST | Login a user | `{ email, password }` | `{ user, token }` |

### Canvas Endpoints

| Endpoint | Method | Description | Request Body | Response |
|----------|--------|-------------|--------------|----------|
| `/api/canvas` | GET | Get all canvases for a user | - | `{ canvases }` |
| `/api/canvas/:id` | GET | Get a specific canvas | - | `{ canvas }` |
| `/api/canvas` | POST | Create a new canvas | `{ name, elements }` | `{ canvas }` |
| `/api/canvas/:id` | PUT | Update a canvas | `{ elements }` | `{ canvas }` |
| `/api/canvas/:id/share` | PUT | Share a canvas with another user | `{ userId }` | `{ canvas }` |

## 🔒 Security Implementation

### JWT Authentication
JSON Web Tokens (JWT) are used for authentication. After a successful login, the server generates a JWT that includes the user's identity and expiration time. This token is sent to the client and stored locally. For every subsequent request, the client sends the JWT in the Authorization header. The backend verifies the token's validity before granting access.

### WebSocket Security
To prevent unauthorized WebSocket connections, JWT authentication is implemented. When a user connects to the WebSocket server, their token is sent in the connection request. The backend verifies the token using a middleware before allowing the connection. If the token is invalid or missing, the connection is rejected.

### API Security Measures
- **CORS**: Cross-Origin Resource Sharing is configured to prevent unauthorized domains from accessing the API
- **HTTPS**: Communication is encrypted to protect sensitive information
- **Input Validation**: All user inputs are validated to prevent malicious data
- **Password Encryption**: User passwords are hashed using bcrypt before storing in the database
- **Rate Limiting**: Protection against DDoS attacks and brute-force attacks

## 🌐 Deployment

### Backend Deployment (Render)
1. Create a new Web Service on Render
2. Connect your GitHub repository
3. Set build command: `npm install`
4. Set start command: `node server.js`
5. Add environment variables from the `.env` file
6. Deploy

### Frontend Deployment (Vercel)
1. Import your project from GitHub
2. Configure build settings:
   - Build command: `npm run build`
   - Output directory: `build`
3. Add environment variables
4. Deploy
