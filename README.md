<p align="center">
  <h1 align="center">🛡️ Egocentric Violence & Harassment Detection V3</h1>
  <p align="center">
    <strong>An AI-powered Android application for real-time egocentric violence and harassment detection using deep learning</strong>
  </p>
  <p align="center">
    <a href="#features">Features</a> •
    <a href="#architecture">Architecture</a> •
    <a href="#tech-stack">Tech Stack</a> •
    <a href="#setup">Setup</a> •
    <a href="#model-training">Model Training</a> •
    <a href="#usage">Usage</a> •
    <a href="#api-reference">API Reference</a>
  </p>
  <p align="center">
    <img src="https://img.shields.io/badge/Android-API%2024%2B-brightgreen?logo=android" alt="API Level">
    <img src="https://img.shields.io/badge/Java-11-orange?logo=openjdk" alt="Java 11">
    <img src="https://img.shields.io/badge/Python-3.9%2B-blue?logo=python" alt="Python">
    <img src="https://img.shields.io/badge/TensorFlow-2.16-FF6F00?logo=tensorflow" alt="TensorFlow">
    <img src="https://img.shields.io/badge/FastAPI-Backend-009688?logo=fastapi" alt="FastAPI">
    <img src="https://img.shields.io/badge/License-MIT-yellow" alt="License">
  </p>
</p>

---

## 📖 Overview

**Egocentric Violence & Harassment Detection V3** is a comprehensive Android-based system that leverages deep learning to detect violent and harassing behavior from a first-person (egocentric) camera perspective in real-time. The app captures video through the device camera, sends frames to a FastAPI backend running a trained violence-detection model, and returns classification results — **Violent** or **Non-Violent** — with confidence scores.

The system is designed for personal safety, law enforcement support, and campus security use cases, featuring **emergency response automation**, **incident history tracking**, **PDF report generation**, and **stealth recording mode**.

---

## ✨ Features

### 🎥 Core Detection
- **Real-Time Analysis** — Live camera feed analysis with frame-by-frame violence classification
- **Video Upload & Batch Processing** — Upload existing videos or batch-process multiple files for analysis
- **Confidence Scoring** — Each prediction includes a confidence percentage for transparency
- **On-Device TFLite Support** — TensorFlow Lite integration for optional edge inference

### 🚨 Emergency Response
- **Automated SMS Alerts** — Sends emergency SMS with GPS location when violence is detected
- **WhatsApp Location Sharing** — One-tap location sharing to emergency contacts via WhatsApp
- **Emergency Contacts Management** — Add, edit, and manage trusted emergency contacts
- **Quick-Dial Emergency Services** — Direct call buttons for Police (100), Ambulance (108), Fire (101), Women Helpline (181), Child Helpline (1098), Anti-Ragging Helpline

### 📊 Reporting & History
- **Incident History** — Full searchable history with filtering by date, type, and severity
- **Incident Details** — Detailed view of each detection event with timestamps and confidence
- **PDF Report Generation** — Generate comprehensive PDF reports with statistical analysis and charts
- **Admin Dashboard** — Aggregated statistics, trend analysis, and system-wide metrics

### 🔒 Stealth & Security
- **Foreground Service Recording** — Background video capture with persistent notification
- **Stealth Mode** — Discreet recording with notification-based alerts
- **Firebase Cloud Messaging** — Push notification support for remote alerts
- **User Authentication** — Login/Register system with profile management

### ⚙️ Configuration
- **Dynamic Server Configuration** — Change backend server IP/port from within the app
- **Server Health Monitoring** — Real-time connection status indicator
- **Notification Preferences** — Customizable alert thresholds and notification types
- **Dark Mode Support** — Full dark theme support

---

## 🏗️ Architecture

```
┌──────────────────────────────────────────────────────────────────┐
│                      ANDROID APPLICATION                         │
│                                                                  │
│  ┌─────────┐  ┌───────────┐  ┌──────────┐  ┌─────────────────┐ │
│  │ Activities│  │ Fragments  │  │ Adapters │  │ ViewModels      │ │
│  │ (14 UI   │  │            │  │ (3)      │  │ (8 + Factory)   │ │
│  │ screens) │  │            │  │          │  │                 │ │
│  └────┬─────┘  └─────┬──────┘  └────┬─────┘  └───────┬─────────┘ │
│       │              │              │                │           │
│       └──────────────┴──────────────┴────────────────┘           │
│                              │                                   │
│  ┌───────────────────────────┴───────────────────────────────┐   │
│  │                     BUSINESS LOGIC                         │   │
│  │  ┌──────────────┐  ┌───────────────┐  ┌────────────────┐  │   │
│  │  │ Repository    │  │ Managers       │  │ Services       │  │   │
│  │  │ (CrimeRepo)  │  │ (Emergency,   │  │ (Recording,   │  │   │
│  │  │              │  │  Location,     │  │  Upload,      │  │   │
│  │  │              │  │  Alert)        │  │  FCM)         │  │   │
│  │  └──────┬───────┘  └───────────────┘  └────────────────┘  │   │
│  └─────────┼─────────────────────────────────────────────────┘   │
│            │                                                     │
│  ┌─────────┴──────────────────────────────────────────────────┐  │
│  │                      DATA LAYER                             │  │
│  │  ┌──────────────┐  ┌─────────────────┐  ┌──────────────┐  │  │
│  │  │ Room Database │  │ Retrofit/OkHttp │  │ SharedPrefs  │  │  │
│  │  │ (SQLite)      │  │ (REST Client)   │  │              │  │  │
│  │  └──────────────┘  └────────┬────────┘  └──────────────┘  │  │
│  └─────────────────────────────┼──────────────────────────────┘  │
│                                │                                 │
└────────────────────────────────┼─────────────────────────────────┘
                                 │ HTTP/REST
                                 ▼
┌────────────────────────────────────────────────────────────────┐
│                     FASTAPI BACKEND SERVER                      │
│                                                                │
│  ┌──────────────┐  ┌──────────────────┐  ┌──────────────────┐ │
│  │ REST API      │  │ Violence Detection│  │ Video Processing │ │
│  │ Endpoints     │  │ ML Model          │  │ Pipeline         │ │
│  │ (FastAPI)     │  │ (TensorFlow)      │  │ (OpenCV)         │ │
│  └──────────────┘  └──────────────────┘  └──────────────────┘ │
└────────────────────────────────────────────────────────────────┘
```

---

## 🛠️ Tech Stack

### Android Application
| Component | Technology | Version |
|-----------|-----------|---------|
| **Language** | Java (+ Kotlin extensions) | Java 11 |
| **Camera** | CameraX | 1.3.4 |
| **Networking** | Retrofit 2 + OkHttp | 2.11.0 / 4.12.0 |
| **Database** | Room (SQLite) | 2.6.1 |
| **Architecture** | ViewModel + LiveData (MVVM) | 2.7.0 |
| **Video Playback** | ExoPlayer | 2.19.1 |
| **Charts** | MPAndroidChart | 3.1.0 |
| **PDF** | iTextPDF | 7.2.3 |
| **ML (On-Device)** | TensorFlow Lite | 2.16.1 |
| **Push Notifications** | Firebase Cloud Messaging | 23.2.1 |
| **Location** | Google Play Services Location | 21.2.0 |
| **UI** | Material Design Components | 1.12.0 |

### Backend Server
| Component | Technology |
|-----------|-----------|
| **Framework** | FastAPI |
| **Server** | Uvicorn |
| **ML Framework** | TensorFlow / Keras |
| **Video Processing** | OpenCV |
| **Language** | Python 3.9+ |

### Model Training
| Component | Technology |
|-----------|-----------|
| **Platform** | Kaggle Notebooks |
| **Framework** | TensorFlow / Keras |
| **Task** | Binary Classification (Violent / Non-Violent) |

---

## 📂 Project Structure

```
Egocentric-Violence-and-Harassment-Detection-V3/
├── app/
│   └── src/main/
│       ├── java/com/krishna/crimedetection/
│       │   ├── activities/          # 14 Activity screens (UI Controllers)
│       │   │   ├── MainActivity.java            # Primary camera + upload interface
│       │   │   ├── RealtimeActivity.java         # Live real-time detection
│       │   │   ├── DashboardActivity.java        # User dashboard
│       │   │   ├── AdminDashboardActivity.java   # Admin statistics view
│       │   │   ├── IncidentHistoryActivity.java  # Incident history browser
│       │   │   ├── IncidentDetailsActivity.java  # Single incident detail view
│       │   │   ├── EmergencyActivity.java        # Emergency services panel
│       │   │   ├── EmergencyContactsActivity.java # Manage emergency contacts
│       │   │   ├── BatchUploadActivity.java      # Multi-video batch upload
│       │   │   ├── ReportGeneratorActivity.java  # PDF report generation
│       │   │   ├── SettingsActivity.java         # App settings
│       │   │   ├── NotificationsActivity.java    # Notification center
│       │   │   ├── PermissionsActivity.java      # Runtime permissions
│       │   │   └── SplashActivity.java           # Launch screen
│       │   │
│       │   ├── adapters/            # RecyclerView adapters
│       │   │   ├── IncidentAdapter.java
│       │   │   ├── EmergencyContactAdapter.java
│       │   │   └── NotificationsAdapter.java
│       │   │
│       │   ├── auth/                # Authentication module
│       │   │   ├── LoginActivity.java
│       │   │   ├── RegisterActivity.java
│       │   │   └── ProfileActivity.java
│       │   │
│       │   ├── fragments/           # Dialog fragments
│       │   │   └── EmergencyResponseDialog.java
│       │   │
│       │   ├── managers/            # System managers
│       │   │   └── EmergencyResponseManager.java
│       │   │
│       │   ├── models/              # Data models & Room entities
│       │   │   ├── AppDatabase.java             # Room database definition
│       │   │   ├── CrimeRecord.java             # Primary entity
│       │   │   ├── CrimeDao.java                # Data Access Object
│       │   │   ├── EmergencyContact.java        # Contact entity
│       │   │   ├── EmergencyContactDao.java
│       │   │   ├── VideoUploadRecord.java       # Upload tracking entity
│       │   │   ├── VideoUploadDao.java
│       │   │   ├── CrimeSceneEvidence.java      # Evidence entity
│       │   │   ├── CrimeSceneEvidenceDao.java
│       │   │   ├── FilterState.java             # UI filter state
│       │   │   ├── PaginationState.java         # Pagination state
│       │   │   ├── Prediction.java              # ML prediction model
│       │   │   └── UploadStatus.java            # Upload status enum
│       │   │
│       │   ├── network/             # Networking layer
│       │   │   ├── ApiClient.java               # API client configuration
│       │   │   ├── ApiService.java              # Retrofit API interface
│       │   │   ├── RetrofitClient.java          # Retrofit builder
│       │   │   ├── NetworkStateManager.java     # Connection monitoring
│       │   │   ├── ViolenceDetectionManager.java # Core detection logic
│       │   │   ├── VideoUploadHelper.java       # Upload utilities
│       │   │   ├── ProgressRequestBody.java     # Upload progress tracking
│       │   │   ├── PredictionResponse.java      # API response model
│       │   │   ├── HealthCheckResponse.java     # Server health model
│       │   │   ├── StatsResponse.java           # Statistics model
│       │   │   └── models/                      # Additional network models
│       │   │
│       │   ├── realtime/            # Real-time detection pipeline
│       │   │   ├── RealtimeCameraManager.java   # Camera control
│       │   │   ├── RealtimePredictionManager.java # Prediction pipeline
│       │   │   ├── FrameAnalyzer.java           # Frame extraction
│       │   │   ├── FramePreprocessor.java       # Frame preprocessing
│       │   │   ├── FrameBuffer.java             # Frame buffering
│       │   │   ├── FrameCaptureListener.java    # Capture callbacks
│       │   │   ├── AlertManager.java            # Real-time alert system
│       │   │   └── RealtimeAlertBottomSheet.java # Alert UI
│       │   │
│       │   ├── repository/          # Data repository (MVVM)
│       │   │   └── CrimeRepository.java
│       │   │
│       │   ├── services/            # Background services
│       │   │   ├── RecordingForegroundService.java  # Background recording
│       │   │   ├── VideoUploadService.java          # Background upload
│       │   │   └── MyFirebaseMessagingService.java   # FCM handler
│       │   │
│       │   ├── utils/               # Utility classes
│       │   │   ├── PreferenceUtils.java         # SharedPreferences wrapper
│       │   │   ├── NotificationUtils.java       # Notification builder
│       │   │   ├── NotificationHandler.java     # Notification logic
│       │   │   ├── NotificationPreferences.java # Notification settings
│       │   │   ├── PdfReportGenerator.java      # PDF generation
│       │   │   ├── FileUtils.java               # File operations
│       │   │   ├── WhatsAppManager.java         # WhatsApp integration
│       │   │   ├── SmsUtils.java                # SMS utilities
│       │   │   ├── LocationManager.java         # GPS location
│       │   │   ├── TokenManager.java            # Auth token management
│       │   │   ├── NetworkUtils.java            # Network helpers
│       │   │   ├── TimeUtils.java               # Time formatting
│       │   │   ├── VideoUploadHelper.java       # Upload helpers
│       │   │   ├── Constants.java               # App constants
│       │   │   └── AppExecutors.java            # Thread pool
│       │   │
│       │   └── viewmodel/           # MVVM ViewModels
│       │       ├── CrimeViewModel.java
│       │       ├── CrimeViewModelFactory.java
│       │       ├── RealtimeViewModel.java
│       │       ├── ReportViewModel.java
│       │       ├── VideoUploadViewModel.java
│       │       ├── UploadServiceViewModel.java
│       │       ├── EmergencyContactViewModel.java
│       │       ├── LiveDataObserver.java
│       │       └── ViewModelExt.kt
│       │
│       ├── res/                     # Android resources
│       │   ├── layout/              # 27 XML layout files
│       │   ├── drawable/            # Icons and shape drawables
│       │   ├── values/              # Colors, strings, themes
│       │   ├── values-night/        # Dark mode overrides
│       │   ├── menu/                # Menu definitions
│       │   ├── raw/                 # Raw assets
│       │   └── xml/                 # Backup rules, file paths
│       │
│       └── AndroidManifest.xml      # App permissions & components
│
├── Kaggle_Notebook_Code/            # Model training notebook
│   └── egocentric-violence-and-harassment-detection.ipynb
│
├── gradle/                          # Gradle wrapper
├── build.gradle                     # Root build config
├── settings.gradle                  # Project settings
├── gradle.properties                # Gradle properties
└── README.md                        # This file
```

---

## 📋 Prerequisites

| Requirement | Details |
|------------|---------|
| **Android Studio** | Jellyfish (2024.1) or newer |
| **JDK** | Java 11+ |
| **Android Device** | Physical device recommended (API 24+ / Android 7.0+) |
| **Python** | 3.9+ (for backend server) |
| **pip packages** | `fastapi`, `uvicorn`, `opencv-python`, `tensorflow` |
| **Network** | Phone and computer on the same Wi-Fi network |

---

## ⚙️ Setup

### 1. Clone the Repository

```bash
git clone https://github.com/rohan-chand-m-01/Egocentric-Violence-and-Harassment-Detection-V3.git
cd Egocentric-Violence-and-Harassment-Detection-V3
```

### 2. Backend Server Setup

Before running the Android app, start your FastAPI violence-detection backend:

```bash
# Install Python dependencies
pip install fastapi uvicorn opencv-python tensorflow numpy pillow

# Start the server (use 0.0.0.0 to allow connections from your phone)
uvicorn main:app --host 0.0.0.0 --port 8000
```

Find your computer's local IP address:

| OS | Command | Example Output |
|----|---------|----------------|
| **Windows** | `ipconfig` → look for `IPv4 Address` | `192.168.1.15` |
| **macOS** | `ifconfig en0` → look for `inet` | `192.168.1.15` |
| **Linux** | `hostname -I` | `192.168.1.15` |

### 3. Android App Setup

1. Open the project in **Android Studio**
2. Wait for Gradle sync to complete
3. Connect your Android device via USB (enable **USB Debugging** in Developer Options)
4. Click **Run ▶️** to build and deploy

### 4. Connect App to Backend

1. Ensure your phone and computer are on the **same Wi-Fi network**
2. Open the app → Go to **Settings** (top-right menu)
3. Enter your server URL: `http://<YOUR_IP>:8000`
4. Click **Save** — the status bar should show `✅ Server Connected`

---

## 🧠 Model Training

The deep learning model is trained using a **Kaggle Notebook** included in this repository at:

```
Kaggle_Notebook_Code/egocentric-violence-and-harassment-detection.ipynb
```

### Training Pipeline
1. **Dataset**: Egocentric violence/harassment video dataset
2. **Preprocessing**: Frame extraction, resizing, and normalization using OpenCV
3. **Model Architecture**: CNN-based binary classifier (Violent vs. Non-Violent)
4. **Framework**: TensorFlow / Keras
5. **Output**: Trained model exported for FastAPI backend serving & TFLite conversion for on-device inference

> 💡 **Tip**: Open the notebook directly on [Kaggle](https://www.kaggle.com/) for GPU-accelerated training.

---

## 📱 Usage

### Real-Time Detection
1. Launch the app and navigate to **Real-Time Detection**
2. Point the camera at the scene
3. The app continuously captures frames and sends them for analysis
4. Results appear as overlay badges: 🟢 **Non-Violent** or 🔴 **Violent** with confidence %

### Video Upload
1. From the main screen, tap **Upload Video**
2. Select a video from your gallery
3. The video is sent to the backend for frame-by-frame analysis
4. View results in the **Incident History**

### Batch Upload
1. Navigate to **Batch Upload**
2. Select multiple videos
3. All videos are queued and processed sequentially with progress tracking

### Emergency Response
1. When violence is detected, the app can automatically:
   - Send SMS alerts with GPS coordinates to emergency contacts
   - Share live location via WhatsApp
2. Use the **Emergency** screen for quick-dial to:
   - 🚔 Police (100)
   - 🚑 Ambulance (108)
   - 🚒 Fire (101)
   - 👩 Women Helpline (181)
   - 👶 Child Helpline (1098)

### Report Generation
1. Go to **Report Generator**
2. Select date range and filters
3. Generate a **PDF report** with:
   - Incident summary
   - Statistical analysis
   - Charts and visualizations

---

## 🔌 API Reference

The app communicates with the FastAPI backend via REST endpoints:

| Method | Endpoint | Description |
|--------|----------|-------------|
| `GET` | `/health` | Server health check |
| `POST` | `/predict` | Analyze video/frames for violence |
| `GET` | `/stats` | Get detection statistics |
| `POST` | `/upload` | Upload video file for processing |

### Sample Request

```bash
curl -X POST "http://192.168.1.15:8000/predict" \
  -F "file=@video.mp4" \
  -H "Content-Type: multipart/form-data"
```

### Sample Response

```json
{
  "prediction": "Violent",
  "confidence": 0.94,
  "timestamp": "2026-10-02T14:00:00",
  "frames_analyzed": 30
}
```

---

## 🔧 Troubleshooting

| Issue | Solution |
|-------|----------|
| **App can't connect to server** | Ensure both devices are on the same Wi-Fi. Don't use `127.0.0.1` on a physical device — use your actual IP. |
| **Firewall blocking** | Add an inbound rule for port `8000` or temporarily disable the firewall. |
| **Camera not working** | Grant Camera and Microphone permissions in Android Settings → Apps → CrimeDetection. |
| **SMS not sending** | Grant SMS permission and ensure a default SMS app is configured. |
| **Video upload fails** | Check file size. Ensure the backend server has enough storage and the connection is stable. |
| **Gradle sync fails** | File → Invalidate Caches → Restart Android Studio. Ensure JDK 11+ is configured. |

---

## 🔐 Permissions

The app requires the following Android permissions:

| Permission | Purpose |
|-----------|---------|
| `CAMERA` | Video capture for analysis |
| `RECORD_AUDIO` | Audio recording during video capture |
| `INTERNET` | Communication with backend server |
| `ACCESS_FINE_LOCATION` | GPS coordinates for emergency alerts |
| `SEND_SMS` | Automated emergency SMS alerts |
| `CALL_PHONE` | Quick-dial emergency services |
| `READ_CONTACTS` | Emergency contact selection |
| `POST_NOTIFICATIONS` | Detection result notifications |
| `FOREGROUND_SERVICE` | Background recording capability |
| `WAKE_LOCK` | Keep device active during recording |

---

## 🤝 Contributing

Contributions are welcome! Here's how to get started:

1. **Fork** this repository
2. **Create** a feature branch: `git checkout -b feature/your-feature`
3. **Commit** your changes: `git commit -m "Add your feature"`
4. **Push** to the branch: `git push origin feature/your-feature`
5. **Open** a Pull Request

---

## 📄 License

This project is licensed under the MIT License — see the [LICENSE](LICENSE) file for details.

---

## 👤 Authors

- **Krishna S** — *Android Application Development & System Design*
- **Rohan Chand M** — *Project Lead & Repository Maintainer*

---

<p align="center">
  <sub>Built with ❤️ for a safer world</sub>
</p>
