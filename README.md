# 🌞 Visual Inspection of Solar Panels

A comprehensive full-stack application for automated inspection and monitoring of solar panel systems using AI-powered fault detection, real-time monitoring, and intelligent diagnostics.

![Solar Panel Inspection](https://img.shields.io/badge/Status-Active-brightgreen)
![Version](https://img.shields.io/badge/Version-1.0.0-blue)
![License](https://img.shields.io/badge/License-ISC-green)

---

## 📋 Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Architecture](#architecture)
- [Installation & Setup](#installation--setup)
- [Project Structure](#project-structure)
- [API Documentation](#api-documentation)
- [Usage Guide](#usage-guide)
- [Future Enhancements](#future-enhancements)
- [Contributing](#contributing)

---

## Overview

The **Visual Inspection of Solar Panels** system is a full-stack IoT and AI solution designed to automatically inspect, diagnose, and monitor solar panel arrays. It combines computer vision, machine learning, and real-time web dashboards to detect faults, predict maintenance needs, and optimize energy output.

### Key Use Cases

- **Automated Defect Detection**: Uses YOLOv8 for real-time fault identification
- **Grid Management**: Visual panel grid builder for organizing large installations
- **Predictive Maintenance**: AI-based fault diagnosis and maintenance scheduling
- **Performance Monitoring**: Track energy output and efficiency metrics
- **Intelligent Support**: AI chatbot for solar panel queries and support

---

## ✨ Features

### 🤖 AI & Computer Vision

- **Real-time Fault Detection**: YOLOv8-based object detection for panel defects
- **Automated Inspection Pipeline**: Python backend processes camera feeds
- **AI Fault Diagnosis**: Machine learning models identify and classify panel faults
- **AI Chatbot Support**: Gemini API integration for intelligent Q&A

### 📊 Dashboard & Monitoring

- **Interactive Solar Grid Builder**: Visual interface to configure panel layouts
- **Real-time Performance Metrics**: Monitor energy output and efficiency
- **Inspection History**: Complete audit trail of all inspections
- **Fault Detection Results**: Visual representation of detected defects

### 🔐 User Management

- **JWT Authentication**: Secure token-based authorization
- **Role-based Access**: User and admin roles with specific permissions
- **User Profiles**: Manage inspection history and preferences

### 📅 Scheduling & Management

- **Automated Schedules**: Create and manage inspection schedules
- **Email Notifications**: Alerts for scheduled inspections
- **Maintenance Tracking**: Monitor maintenance status and history
- **Grid Configuration**: Store and manage multiple grid setups

### 🎨 Frontend Features

- **Responsive UI**: Built with React & Tailwind CSS
- **Virtual Scrolling**: Optimized performance for large panel arrays (1000+ panels)
- **Real-time Updates**: Live data synchronization
- **PDF Reports**: Generate inspection reports with jsPDF

---

## 🛠 Tech Stack

### Frontend

```
Framework: React 18.3.1 with TypeScript
Build Tool: Vite 5.4.2
Styling: Tailwind CSS + PostCSS
UI Components: Lucide Icons, Custom Components
State Management: React Context API
HTTP Client: Axios
Virtualization: React Window + React Virtualized
Routing: React Router v6
Notifications: React Toastify
```

### Backend

```
Runtime: Node.js with Express.js 5.1.0
Database: MongoDB (Mongoose) + MySQL
Authentication: JWT (jsonwebtoken), bcryptjs
Utilities: Cookie Parser, CORS
```

### AI/ML & Computer Vision

```
Detection: YOLOv8
Computer Vision: OpenCV
Language Models: Gemini API (Google)
HTTP: Python Requests
```

### DevOps & Tools

```
Package Manager: npm
Task Runner: Concurrently (dev mode)
Linting: ESLint + TypeScript ESLint
Code Quality: TypeScript strict mode
```

---

## 🏗 Architecture

### System Architecture Diagram

```
┌─────────────────────────────────────────────────────┐
│                   Frontend (React + TS)             │
│  Dashboard | Grid Builder | Inspection | AI Chat   │
└─────────────────────────────────────────────────────┘
                        ↕ (HTTP/REST API)
┌─────────────────────────────────────────────────────┐
│            Backend API (Express + Node.js)          │
│  Auth | User | Schedule | Panel | Camera | Grid    │
└─────────────────────────────────────────────────────┘
          ↕ (Database) ↙↘ (Python Script)
    ┌──────────────────────┐   ┌────────────────────┐
    │ MongoDB + MySQL      │   │ Python AI Engine   │
    │ (Panel Data,         │   │ - YOLOv8           │
    │  Users, Schedules)   │   │ - OpenCV           │
    │                      │   │ - Detection Logic  │
    └──────────────────────┘   └────────────────────┘
                                      ↕ (Camera Input)
                              ┌────────────────────┐
                              │   Camera Stream    │
                              │ (Solar Panel Array)│
                              └────────────────────┘
```

### Component Architecture

**Frontend Components:**

- `Dashboard.tsx` - Main monitoring dashboard
- `GridBuilder.tsx` - Visual grid configuration
- `PanelDetail.tsx` - Individual panel inspection details
- `AIChatbotPage.tsx` - AI-powered Q&A interface
- `AIFaultDiagnosisPage.tsx` - Fault diagnosis interface
- `ScheduleForm.tsx` - Schedule creation and management

**Backend Services:**

- `authController.js` - User authentication & JWT management
- `panelController.js` - Panel CRUD operations
- `cameraController.js` - Camera control and streaming
- `scheduleController.js` - Schedule management
- `gridController.js` - Grid configuration

**Database Models:**

- `Panel.js` - Panel attributes, faults, inspection history
- `User.js` - User credentials and profile
- `Schedule.js` - Inspection schedules
- `GridConfig.js` - Grid layout configuration

---

## 📦 Installation & Setup

### Prerequisites

- **Node.js** (v14+)
- **Python** (v3.8+)
- **MongoDB** (local or cloud)
- **MySQL** (optional)
- **Camera Device** (USB or IP camera)

### Backend Setup

```bash
# Navigate to backend directory
cd Backend

# Install dependencies
npm install

# Create .env file
cat > .env << EOF
PORT=5000
MONGODB_URI=mongodb://localhost:27017/solar_panels
MYSQL_HOST=localhost
MYSQL_USER=root
MYSQL_PASSWORD=your_password
JWT_SECRET=your_jwt_secret
EOF

# Start backend server
npm start
```

### Frontend Setup

```bash
# Navigate to project directory
cd project

# Install dependencies
npm install

# Create environment file
cat > .env << EOF
VITE_API_URL=http://localhost:5000
VITE_GEMINI_API_KEY=your_gemini_api_key
EOF

# Start development server
npm run dev
```

### Python AI Engine Setup

```bash
# Navigate to project directory
cd project

# Install Python dependencies
pip install -r requirements.txt

# Download YOLOv8 models
python -c "from ultralytics import YOLO; YOLO('yolov8s.pt')"

# Start detection server
python server.py
```

### Run All Services Concurrently

```bash
# From project root (frontend directory)
npm run dev   # Starts both frontend (Vite) and backend (Express)

# In another terminal, start Python detection engine
cd project
python server.py
```

---

## 📁 Project Structure

```
Visual-Inspection-of-Solar-Panel/
├── Backend/                          # Express API Server
│   ├── config/
│   │   └── db.js                    # Database configuration
│   ├── controllers/
│   │   ├── authController.js        # Authentication logic
│   │   ├── panelController.js       # Panel operations
│   │   ├── cameraController.js      # Camera control
│   │   ├── gridController.js        # Grid management
│   │   └── scheduleController.js    # Schedule management
│   ├── middleware/
│   │   └── authMiddleware.js        # JWT verification
│   ├── models/
│   │   ├── User.js                  # User schema
│   │   ├── Panel.js                 # Panel schema
│   │   ├── Schedule.js              # Schedule schema
│   │   └── GridConfig.js            # Grid configuration schema
│   ├── routes/
│   │   ├── auth.js                  # Auth endpoints
│   │   ├── userRoutes.js            # User endpoints
│   │   └── scheduleRoute.js         # Schedule endpoints
│   ├── utils/
│   │   └── generateToken.js         # JWT token generation
│   ├── server.js                    # Main server file
│   └── package.json
│
├── project/                          # Full-stack Application
│   ├── src/
│   │   ├── components/
│   │   │   ├── EnhancedVirtualPanelList.tsx   # Optimized panel list
│   │   │   ├── PanelRegistrationForm.tsx      # Panel registration
│   │   │   ├── ScheduleForm.tsx               # Schedule creation
│   │   │   ├── VirtualizedPanelContainer.tsx  # Virtual scrolling
│   │   │   ├── common/                        # Reusable components
│   │   │   ├── layout/                        # Layout components
│   │   │   └── sidebar/                       # Navigation
│   │   ├── pages/
│   │   │   ├── Dashboard.tsx                  # Main dashboard
│   │   │   ├── GridBuilder.tsx                # Grid configuration
│   │   │   ├── PanelDetail.tsx                # Panel details
│   │   │   ├── AIChatbotPage.tsx              # AI chatbot
│   │   │   ├── AIFaultDiagnosisPage.tsx       # Fault diagnosis
│   │   │   ├── LoginPage.tsx                  # Login
│   │   │   ├── RegisterPage.tsx               # Registration
│   │   │   ├── InspectionHistory.tsx          # Inspection logs
│   │   │   └── PanelGrid.tsx                  # Grid view
│   │   ├── context/
│   │   │   ├── AuthContext.tsx                # Auth state management
│   │   │   └── PanelContext.tsx               # Panel state management
│   │   ├── api/
│   │   │   └── panelApi.ts                    # API calls
│   │   ├── types/
│   │   │   ├── index.ts                       # Type definitions
│   │   │   └── panel.ts                       # Panel types
│   │   ├── utils/
│   │   │   ├── panelUtils.ts                  # Panel utilities
│   │   │   ├── reportUtils.ts                 # Report generation
│   │   │   └── storage.ts                     # Local storage
│   │   └── App.tsx                            # Root component
│   ├── data/                         # Configuration files
│   │   ├── gridConfig.json
│   │   └── panels.json
│   ├── detections/                  # Detection results
│   ├── model/                        # YOLOv8 models
│   │   ├── best.pt
│   │   └── num.pt
│   ├── server.py                    # Python Flask/FastAPI server
│   ├── app.py                        # Python AI detection app
│   ├── camera_test.py               # Camera testing script
│   ├── fetch_and_inspect.py         # Inspection pipeline
│   ├── upload.py                    # Image upload handler
│   ├── USB.py                       # Camera USB interface
│   ├── requirements.txt             # Python dependencies
│   ├── package.json                 # Frontend dependencies
│   ├── vite.config.ts              # Vite configuration
│   ├── tsconfig.json               # TypeScript config
│   └── tailwind.config.js          # Tailwind CSS config
│
└── groq-chatbot/                     # Optional Groq API Integration
    ├── server.js
    ├── package.json
    └── public/
```

---

## 🔌 API Documentation

### Authentication Endpoints

```
POST   /api/auth/register      Register new user
POST   /api/auth/login         Login user
GET    /api/auth/logout        Logout user
POST   /api/auth/refresh       Refresh JWT token
```

### Panel Management

```
GET    /api/panels             Get all panels
POST   /api/panels             Create new panel
GET    /api/panels/:id         Get panel details
PUT    /api/panels/:id         Update panel
DELETE /api/panels/:id         Delete panel
POST   /api/panels/detection-update  Update panel from detection
```

### Inspection & Scheduling

```
GET    /api/schedule           Get all schedules
POST   /api/schedule           Create inspection schedule
PUT    /api/schedule/:id       Update schedule
DELETE /api/schedule/:id       Delete schedule
GET    /api/schedule/history   Get inspection history
```

### Camera Control

```
GET    /api/camera/status      Get camera status
POST   /api/camera/start       Start camera stream
POST   /api/camera/stop        Stop camera stream
```

### User Management

```
GET    /api/user/profile       Get user profile
PUT    /api/user/profile       Update profile
GET    /api/user/history       Get inspection history
```

---

## 🎯 Usage Guide

### 1. **User Registration & Authentication**

- Register new account on `/register`
- Login with credentials
- JWT token stored in cookies for secure API access

### 2. **Grid Configuration**

- Navigate to Grid Builder
- Define panel dimensions and layout
- Position panels in rows and columns
- Save configuration for future reference

### 3. **Panel Registration**

- Add solar panels to the system
- Specify panel model, size, and installation details
- Assign panels to grid positions
- Track performance metrics

### 4. **Schedule Inspections**

- Create automated inspection schedules
- Select inspection frequency
- Receive notifications at scheduled times
- System triggers camera and AI detection

### 5. **View Inspection Results**

- Access real-time detection results
- View fault detection visualizations
- Get maintenance recommendations
- Generate PDF reports

### 6. **AI Chatbot Support**

- Ask questions about solar panels
- Get instant answers powered by Gemini AI
- Receive troubleshooting guidance
- Access knowledge base

### 7. **Fault Diagnosis**

- Review detected faults
- Get AI-powered diagnosis
- Receive maintenance suggestions
- Track fault resolution status

---

## 🚀 Future Enhancements

- [ ] Real-time WebSocket updates for live monitoring
- [ ] Mobile app (React Native)
- [ ] Advanced analytics and reporting dashboard
- [ ] Integration with weather APIs for efficiency correlation
- [ ] Automated email/SMS alerts for critical faults
- [ ] Multi-site management system
- [ ] IoT sensor integration (temperature, humidity, irradiance)
- [ ] Cloud deployment (AWS, Azure, GCP)
- [ ] Blockchain-based maintenance record keeping
- [ ] Advanced ML models for predictive maintenance
- [ ] 3D visualization of panel arrays
- [ ] API rate limiting and advanced security features
- [ ] Test suite (Jest, pytest)
- [ ] Docker containerization
- [ ] CI/CD pipeline

---

## 📊 Performance Optimizations

### Frontend Optimizations

- **Virtual Scrolling**: Handle 1000+ panels efficiently with React Window
- **Code Splitting**: Lazy load pages with React.lazy()
- **Image Optimization**: Compress detection results
- **Memoization**: Prevent unnecessary re-renders with React.memo

### Backend Optimizations

- **Database Indexing**: Fast queries on frequently accessed fields
- **Caching**: Redis integration (future enhancement)
- **Rate Limiting**: Protect API endpoints (future enhancement)
- **Pagination**: Efficient data fetching

### AI/ML Optimizations

- **Model Quantization**: Faster inference with YOLOv8s
- **Batch Processing**: Process multiple frames efficiently
- **GPU Acceleration**: CUDA support for faster detection

---

## 🔐 Security Features

✅ **JWT Authentication** - Secure token-based authorization  
✅ **Password Hashing** - bcryptjs for secure password storage  
✅ **CORS Configuration** - Restricted API access  
✅ **Cookie Security** - HttpOnly, Secure flags enabled  
✅ **Input Validation** - Server-side validation on all endpoints  
✅ **Environment Variables** - Sensitive data in .env files

---

## 🧪 Testing

```bash
# Run linter
npm run lint

# Run type checking
npx tsc --noEmit
```

---

## 📝 Environment Variables

### Backend (.env)

```
PORT=5000
MONGODB_URI=mongodb://localhost:27017/solar_panels
MYSQL_HOST=localhost
MYSQL_USER=root
MYSQL_PASSWORD=password
JWT_SECRET=your_secret_key
CORS_ORIGIN=http://localhost:5173
```

### Frontend (.env)

```
VITE_API_URL=http://localhost:5000
VITE_GEMINI_API_KEY=your_gemini_api_key
```

### Python (.env or config)

```
CAMERA_INDEX=0
YOLO_MODEL=best.pt
CONFIDENCE_THRESHOLD=0.5
```

---

## 📚 Dependencies Summary

### Core Dependencies

| Package      | Version | Purpose          |
| ------------ | ------- | ---------------- |
| React        | 18.3.1  | UI Framework     |
| Express      | 5.1.0   | Backend API      |
| Mongoose     | 8.15.0  | MongoDB ODM      |
| YOLOv8       | 8.0.0   | Object Detection |
| Tailwind CSS | 3.4.1   | Styling          |
| React Router | 6.22.3  | Routing          |
| Axios        | -       | HTTP Client      |
| jsonwebtoken | 9.0.2   | Authentication   |

---

## 🤝 Contributing

Contributions are welcome! To contribute:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Development Guidelines

- Follow ESLint configuration
- Use TypeScript for type safety
- Write meaningful commit messages
- Test changes before submitting PR
- Update documentation as needed

---

## 📄 License

This project is licensed under the ISC License - see the LICENSE file for details.

---

## 👨‍💻 Author

**Full-Stack Developer**

- Computer Vision & AI Integration
- Full-stack MERN + Python development
- Real-time monitoring systems
- IoT and embedded systems

---

## 📞 Support & Contact

For questions, issues, or suggestions, please open an issue on GitHub or contact the development team.

---

## 🙏 Acknowledgments

- **YOLOv8** by Ultralytics for object detection
- **Google Gemini API** for AI chatbot
- **React & Vite** communities for excellent tooling
- **MongoDB** for flexible data storage
- **OpenCV** for computer vision capabilities

---

## 📈 Project Statistics

- **Frontend Code**: React 18 + TypeScript with Tailwind CSS
- **Backend Code**: Express API with MongoDB + MySQL
- **AI/ML**: YOLOv8 + OpenCV + Gemini API
- **Performance**: Handles 1000+ panels with virtual scrolling
- **Deployment Ready**: Containerizable architecture
- **Security**: JWT auth + password hashing + CORS

---

**⭐ If you found this project helpful, please consider giving it a star!**
