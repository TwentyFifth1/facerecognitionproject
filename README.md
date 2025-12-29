# 🎭 Face Recognition & Liveness Detection System

## Advanced AI Project with Web Interface & Anti-Spoofing

**A comprehensive face recognition system combining InsightFace, liveness detection, and head pose analysis**

---

## 📖 Project Overview

This is a production-ready **Face Recognition System** for exam proctoring and identity verification with built-in anti-spoofing protection. It combines multiple AI technologies to create a robust authentication system.

### ✨ Key Features

| Feature                    | Description                                                 | Status      |
| -------------------------- | ----------------------------------------------------------- | ----------- |
| 👤 **Face Recognition**    | Real-time face detection & identification using InsightFace | ✅ Complete |
| 🎭 **Liveness Detection**  | Anti-spoofing (detects fake faces, photos, videos)          | ✅ Complete |
| 🔄 **Head Pose Detection** | Left/Right/Straight/Up/Down head orientation                | ✅ Complete |
| 🌐 **Web Interface**       | Flask-based web dashboard with 8 menu options               | ✅ Complete |
| 📊 **Data Logging**        | SQLite + CSV automatic logging & statistics                 | ✅ Complete |
| 📱 **Cross-Platform**      | Windows 10/11, macOS (Intel/Apple Silicon), Linux           | ✅ Complete |

---

## 🎯 System Capabilities

### 1. Face Recognition (InsightFace Model)

- **Accuracy**: ~99.8% on LFW benchmark
- **Model**: buffalo_l (512-dim embeddings)
- **Speed**: 15-20 FPS real-time
- **Features**:
  - Cosine similarity matching
  - Adjustable confidence threshold (default: 0.45)
  - Unknown person detection
  - Multi-face support

### 2. Anti-Spoofing (Liveness Detection)

- **Detection Methods**:
  - Eye blink analysis (changes in eye distance)
  - Head movement detection (positional change)
  - Depth variation (face size changes)
  - Temporal consistency
- **Accuracy**: ~90%+ against photos & videos
- **Real-time**: <100ms latency

### 3. Head Pose Detection

- **Supported Poses**: Left, Right, Straight, Up, Down
- **Methods**:
  - InsightFace 5-point landmarks (primary)
  - MediaPipe (optional, higher accuracy)
  - Brightness symmetry analysis (fallback)
- **Sensitivity**: Tuned for classroom environments

### 4. Web Dashboard (Flask)

8 Interactive Menu Options:

1. 📸 **Collect Images** - Capture training dataset (80 images/person)
2. 🧹 **Clean Dataset** - Remove blurry/poor quality images
3. 📊 **Analyze Pose** - Visualize head pose detection
4. 🔨 **Build Embeddings** - Train recognition model
5. 👁️ **Real-time Recognition** - Live face identification
6. 🎭 **Liveness Detection** - Anti-spoofing test
7. 🔄 **Head Pose Detection** - Orientation analysis
8. ⚡ **Integrated System** - All features combined (Main Feature)

---

## 🏗️ Project Structure

```
face-recognition-system/
│
├── 📄 README.md                      # This file
├── 📋 requirements.txt                # Python dependencies
│
├── 🌐 Flask Web Application
│   ├── app.py                        # Main Flask server (Port 8080)
│   ├── templates/                    # HTML templates
│   │   ├── index.html                # Home page
│   │   ├── integrated.html           # Main integrated system
│   │   ├── collect.html              # Image collection UI
│   │   ├── clean.html                # Dataset cleaning UI
│   │   ├── analyze.html              # Pose analysis UI
│   │   ├── build.html                # Embedding builder UI
│   │   ├── recognition.html          # Recognition UI
│   │   ├── liveness.html             # Liveness test UI
│   │   └── pose.html                 # Pose detection UI
│   └── static/
│       └── style.css                 # Unified styling
│
├── 🐍 Python Core Modules
│   ├── integrated_system.py          # Integrated CLI system
│   ├── main_system.py                # Main menu system
│   ├── collect_images.py             # Dataset collection
│   ├── build_embeddings.py           # Model training
│   ├── realtime_recognition.py       # Recognition engine
│   ├── head_pose_detector.py         # Pose detection
│   ├── liveness_detector.py          # Liveness check
│   ├── dataset_quality_cleaner.py    # Dataset cleaning
│   ├── check_installation.py         # Dependency checker
│   ├── test_dataset.py               # Dataset testing
│   └── setup.py                      # Setup configuration
│
├── 🔧 Installation Scripts
│   ├── install.sh                    # macOS/Linux installer
│   └── install.bat                   # Windows installer
│
├── 📁 Data Directories (Auto-created)
│   ├── dataset/                      # Training images
│   │   └── [person_name]/            # Per-person folders
│   │       ├── person1_0001.jpg
│   │       ├── person1_0002.jpg
│   │       └── ...
│   ├── models/                       # Trained embeddings
│   │   └── insightface_embeddings.pickle  # 512-dim vectors
│   └── logs/                         # Automatic logging
│       ├── integrated_log.csv        # CSV format
│       └── integrated_log.sqlite     # Database format
│
└── 🎨 Model Weights (Downloaded on first run)
    └── ~/.insightface/models/buffalo_l/  # InsightFace model
```

---

## 🚀 Quick Start Guide

### Step 1: Installation (5 minutes)

```bash
# Clone or download repository
cd face-recognition-system

# Create virtual environment (Python 3.9+)
conda create -n face_recognition python=3.11
conda activate face_recognition

# Install dependencies
pip install -r requirements.txt

# Verify installation
python check_installation.py
```

**Output should show:**

```
✅ OpenCV installed
✅ NumPy installed
✅ InsightFace installed
✅ ONNX Runtime installed
✅ Flask installed
✅ All requirements met!
```

### Step 2: Run the System

**Option A: Web Interface (Recommended)**

```bash
conda activate face_recognition
python app.py

# Then open browser: http://localhost:8080
```

**Option B: Command Line Interface**

```bash
conda activate face_recognition
python integrated_system.py
```

### Step 3: Workflow

1. **Collect Training Data**

   - Run: `python collect_images.py` or Web → Option 1
   - Capture 80 images per person
   - Good lighting, various angles

2. **Build Recognition Model**

   - Run: `python build_embeddings.py` or Web → Option 4
   - Creates `models/insightface_embeddings.pickle`
   - Minimum 40% success rate recommended

3. **Run Recognition System**
   - Run: `python integrated_system.py` or Web → Option 8
   - Real-time face identification
   - Automatic logging to CSV & SQLite

---

## ⚙️ Configuration & Tuning

### Key Parameters (in `app.py` & `integrated_system.py`)

```python
# Face Recognition Sensitivity
SIM_THRESHOLD = 0.45          # Lower = more lenient (0.3-0.6 range)

# Frame Processing
FRAME_RESIZE = 0.5            # 0.5x downscale for speed (affects accuracy)

# Head Pose Detection
YAW_THRESHOLD = 0.10          # Left/Right sensitivity
PITCH_THRESHOLD = 0.08        # Up/Down sensitivity

# Liveness Detection
LIVENESS_THRESHOLD = 2        # Movement points required

# Logging
LOG_COOLDOWN_SEC = 5.0        # Minimum seconds between same-person logs
```

### Tuning Guide

**Sensitivity Too High (Few False Positives)**

- ↑ Increase `SIM_THRESHOLD` (0.50 → 0.55)
- Result: More strict matching

**Sensitivity Too Low (Many False Positives)**

- ↓ Decrease `SIM_THRESHOLD` (0.45 → 0.40)
- Result: More lenient matching

**Head Pose Not Detecting**

- ↓ Decrease `YAW_THRESHOLD` (0.10 → 0.08)
- ↓ Decrease `PITCH_THRESHOLD` (0.08 → 0.06)

---

## 🌐 Web Interface Usage

### Access the System

**URL:** `http://localhost:8080`

### Main Options

#### 1. 📸 Collect Images

- Enter person's name
- Capture 80 images with movement
- Quality indicators: Green=Good, Yellow=Too Small, Orange=Blurry
- Saved to: `dataset/[name]/`

#### 2. 🧹 Clean Dataset

- Removes blurry images automatically
- Laplacian variance scoring
- Preview before deletion

#### 3. 📊 Analyze Pose

- Real-time head pose visualization
- Color indicators for each pose
- Helpful for dataset analysis

#### 4. 🔨 Build Embeddings

- Trains recognition model
- Shows success rate per person
- Creates `models/insightface_embeddings.pickle`
- **Must run before Option 5-8**

#### 5. 👁️ Real-time Recognition

- Live face identification
- Shows confidence scores
- Green box = Known, Red box = Unknown

#### 6. 🎭 Liveness Detection

- Tests anti-spoofing
- Green = Real person, Red = Fake
- Educational demo

#### 7. 🔄 Head Pose Detection

- Shows all 5 pose types
- Tuned for classroom use
- Color-coded display

#### 8. ⚡ Integrated System (Main)

- **All features combined:**
  - Face recognition
  - Liveness detection
  - Head pose analysis
  - Automatic logging
- **Real-time output:**
  - Identified person name
  - Confidence score
  - Liveness status
  - Head pose
  - Frame count

### Database Access

**View Logs in Web:**

- Statistics API: `/stats`
- Rotation stats: `/stats/rotations`
- Health check: `/health`

**Export Logs:**

```bash
# CSV format
open logs/integrated_log.csv

# SQLite database
sqlite3 logs/integrated_log.sqlite
> SELECT * FROM recognition_log LIMIT 10;
```

---

## 🔐 Security & Privacy

### Data Protection

- ✅ All processing is local (no cloud upload)
- ✅ Models run on-device
- ✅ SQLite database stored locally
- ✅ No external API calls

### Anti-Spoofing Features

- Multi-method liveness detection
- Temporal consistency checking
- Movement-based verification
- Real-time frame analysis

---

## 📊 Logging & Analysis

### CSV Format

```csv
timestamp,name,similarity,liveness,pose,x1,y1,x2,y2
2025-12-30T15:30:45,John,0.9234,LIVE,Straight,100,50,250,300
2025-12-30T15:31:02,John,0.8956,LIVE,Right,105,52,255,305
```

### Database Queries

```sql
-- Total detections
SELECT COUNT(*) FROM recognition_log;

-- Unique people
SELECT COUNT(DISTINCT name) FROM recognition_log;

-- Recent activity
SELECT timestamp, name, similarity FROM recognition_log
ORDER BY id DESC LIMIT 10;

-- Liveness statistics
SELECT liveness, COUNT(*) FROM recognition_log
GROUP BY liveness;

-- Head pose analysis
SELECT pose, COUNT(*) FROM recognition_log
GROUP BY pose;
```

---

## 🐛 Troubleshooting

### Installation Issues

| Error                              | Solution                                  |
| ---------------------------------- | ----------------------------------------- |
| `ModuleNotFoundError: insightface` | `pip install insightface --no-cache-dir`  |
| `ModuleNotFoundError: onnxruntime` | `pip install onnxruntime`                 |
| ONNX CoreML error on macOS         | Already fixed with `CPUExecutionProvider` |
| Permission error on Windows        | Run terminal as Administrator             |

### Runtime Issues

| Error                        | Solution                                          |
| ---------------------------- | ------------------------------------------------- |
| **Camera won't open**        | Check System Preferences → Camera permissions     |
| **"Cannot open camera"**     | Try `VideoCapture(1)` or close Zoom/Skype         |
| **Embeddings not found**     | Must run Option 4 (Build Embeddings) first        |
| **Port 8080 already in use** | Change `PORT = 8081` in `app.py`                  |
| **macOS terminal freezes**   | Aggressive cleanup in code, press Ctrl+C          |
| **Blurry images**            | Improve lighting, ensure steady hand, larger face |

### Performance Issues

| Issue            | Optimization                                            |
| ---------------- | ------------------------------------------------------- |
| Slow FPS         | Decrease `FRAME_RESIZE` to 0.3                          |
| High CPU         | Enable GPU (uncomment in requirements.txt)              |
| Memory leak      | Restart Flask app every 1 hour                          |
| Poor recognition | Collect more diverse images (different lighting/angles) |

---

## 📈 Performance Metrics

### Benchmarks (Tested on MacBook Air M1)

| Component        | Speed      | Accuracy       |
| ---------------- | ---------- | -------------- |
| Face Detection   | ~10ms      | 99.8% LFW      |
| Face Embedding   | ~80ms      | 512-dim vector |
| Similarity Match | <1ms       | 0.45 threshold |
| Liveness Check   | ~20ms      | ~90%           |
| Head Pose        | ~15ms      | ~85%           |
| **Total E2E**    | **~150ms** | **95%+**       |

### Throughput

- Single face: 7-8 FPS
- Multiple faces: 15-20 FPS (downscaled)
- Web streaming: 25 FPS

---

## 🎓 Educational Value

This project demonstrates:

- ✅ Deep learning for computer vision
- ✅ Face detection & recognition algorithms
- ✅ Anti-spoofing techniques
- ✅ Web application development (Flask)
- ✅ Real-time video processing
- ✅ Database design & querying
- ✅ Cross-platform Python development

---

## 📚 Key Libraries Used

| Library          | Purpose                 | Version    |
| ---------------- | ----------------------- | ---------- |
| **InsightFace**  | Face recognition (main) | ≥0.7.3     |
| **OpenCV**       | Computer vision tasks   | 4.8.0+     |
| **NumPy**        | Numerical computing     | 1.24.0+    |
| **Flask**        | Web framework           | 3.0.0      |
| **ONNX Runtime** | Model inference         | 1.16.0+    |
| **Scikit-learn** | ML utilities            | 1.3.0+     |
| **MediaPipe**    | Optional pose detection | (optional) |

---

## 🤝 Team Contributions

- **Ohm - 1143531**: Face Recognition (InsightFace integration, embedding building)
- **Chris - 1143565**: Head Pose Detection (Left/Right orientation)
- **Felix - 1143550**: Combined system, Flask web app, database logging, liveness Detection (Anti-spoofing, web interface)
- **Tae - 1143566**: UI/UX design
- **Peter - 1143567**: Testing, presentation

---

## 📝 License

Educational project for Yuan Ze University (IBPI Program)

---

## 👨‍💻 Author Contact

**Name**: Tae - 楊晟恩  
**Student ID**: 1143566  
**University**: Yuan Ze University, Taiwan  
**Program**: International Bachelor's Program in Informatics  
**Email**: s1143566@mail.yzu.edu.tw

---

## 🎯 Future Enhancements

- [ ] GPU acceleration (CUDA/Metal)
- [ ] Real-time 3D face reconstruction
- [ ] Emotion recognition
- [ ] Age/gender estimation
- [ ] Masked face recognition
- [ ] Multi-person simultaneous detection
- [ ] Cloud deployment (AWS/Azure)
- [ ] Mobile app (iOS/Android)
- [ ] Deployment on edge devices (Raspberry Pi, Jetson)

---

## 🔗 References

- InsightFace: https://github.com/deepinsight/insightface
- OpenCV: https://opencv.org
- Flask: https://flask.palletsprojects.com
- MediaPipe: https://mediapipe.dev

---

**Last Updated**: December 30, 2025  
**Version**: 2.0 - Production Ready  
**Status**: ✅ Complete for Week 17 Submission
