# 🚨 Cyber Guard Pro - IDPS using Agentic AI and ML

An intelligent **Intrusion Detection and Prevention System (IDPS)** powered by machine learning that detects network attacks, analyzes file threats, and validates URL safety in real-time.

## 📋 Table of Contents
- [Overview](#overview)
- [Features](#features)
- [Requirements](#requirements)
- [Installation](#installation)
- [Usage](#usage)
- [Project Structure](#project-structure)
- [How It Works](#how-it-works)
- [Dataset](#dataset)
- [Troubleshooting](#troubleshooting)

---

## 🎯 Overview

**Cyber Guard Pro** is a comprehensive security analysis platform that combines:
- **Machine Learning** for network intrusion detection using the KDD Cup 99 dataset
- **File Analysis** to scan documents (PDF, Word, CSV, TXT) for threats
- **URL Security** assessment using entropy analysis and DNS validation
- **Streamlit UI** for easy-to-use web interface

Perfect for cybersecurity professionals, system administrators, and security researchers.

---

## ✨ Features

### 📁 File Safety Scan
- **Multi-format support**: CSV, PDF, Word (.docx), and TXT files
- **ML-powered detection**: Identifies network attacks in CSV data using trained Random Forest classifier
- **Phishing keyword detection**: Scans text for suspicious keywords (password, login, bank, verify, urgent, bitcoin, etc.)
- **Content preview**: Displays file content for manual review

### 🔍 URL Security Check
- **Entropy analysis**: Detects suspicious domain randomness
- **DNS validation**: Verifies if domain is active
- **Verdict system**: Safe or Suspicious classification
- **Real-time scoring**: Instant URL safety assessment

### 🧠 Machine Learning Model
- **Random Forest Classifier**: 100 estimators trained on KDD Cup 99 dataset
- **42 network features**: Protocol type, service, flags, bytes transferred, and more
- **Binary classification**: Normal traffic vs. Attack traffic
- **Automatic preprocessing**: One-hot encoding for categorical features

---

## 📦 Requirements

- Python 3.7+
- Streamlit
- Pandas
- Scikit-learn
- Joblib
- Python-docx
- Python-pptx
- PyPDF2
- Standard-imghdr

---

## 🚀 Installation

### 1. Clone or Download Repository
```bash
cd IDPS-using-agentic-AI-and-ML
```

### 2. Install Dependencies
```bash
pip install -r requirements.txt
```

### 3. Train the ML Model
Before running the app, train the intrusion detection model:
```bash
python train_model.py
```

**Expected output:**
```
🚀 [1/3] Script started! Loading data...
🧠 [2/3] Training model... This takes 1-2 minutes. Please wait.
✅ [3/3] SUCCESS: intrusion_pipeline.pkl created!
```

This creates `intrusion_pipeline.pkl` which the app uses for predictions.

### 4. Run the Application
```bash
streamlit run app.py
```

The app will open in your browser at `http://localhost:8501`

---

## 💡 Usage

### File Safety Scan

1. Go to the **📁 File Safety Scan** tab
2. Upload a file (CSV, PDF, Word, or TXT)
3. The system will:
   - Display file preview
   - If CSV: Run ML model to detect attacks in network traffic
   - If text-based: Scan for phishing keywords
4. Review results and warnings

### URL Security Check

1. Go to the **🔍 URL Scanner** tab
2. Paste a URL (with or without http://)
3. Click **Scan URL**
4. View results:
   - **Verdict**: Safe or Suspicious
   - **Randomness (Entropy)**: Domain name entropy score
   - **DNS Status**: Whether domain is active

---

## 📁 Project Structure

```
IDPS-using-agentic-AI-and-ML/
├── app.py                      # Main Streamlit application
├── train_model.py              # ML model training script
├── KDDTrain+.txt              # Training dataset (KDD Cup 99)
├── KDDTest+.txt               # Test dataset (KDD Cup 99)
├── requirements.txt            # Python dependencies
├── intrusion_pipeline.pkl      # Trained ML model (generated after training)
└── README.md                   # This file
```

---

## 🔬 How It Works

### Network Intrusion Detection (ML Model)

1. **Data**: KDD Cup 99 dataset with 42 network features
2. **Preprocessing**: 
   - Categorical features (protocol_type, service, flag) → One-hot encoded
   - Numerical features → Passthrough
3. **Model**: Random Forest Classifier with 100 estimators
4. **Output**: Binary prediction (0 = Normal, 1 = Attack)

**Key features analyzed:**
- Duration, protocol type, service type
- Bytes transferred (source & destination)
- Failed login attempts
- Root shell access attempts
- Connection counts and error rates

### Phishing Text Scan

Looks for common phishing/social engineering keywords:
- "password", "login", "bank", "verify", "urgent", "bitcoin", "click here"

### URL Security Scoring

1. **Entropy Calculation**: Measures domain randomness (0-8 scale)
   - High entropy (>4) = Suspicious
2. **DNS Check**: Validates if domain resolves
   - Failed DNS = Suspicious
3. **Final Verdict**: Safe if both checks pass

---

## 📊 Dataset

### KDD Cup 99
- **Training Set**: `KDDTrain+.txt` - 125,973 records
- **Test Set**: `KDDTest+.txt` - 22,544 records
- **Features**: 42 network connection attributes
- **Classes**: Normal traffic vs. 22 attack types

**Attack Categories:**
- DoS (Denial of Service)
- Probe (Reconnaissance)
- U2R (User to Root)
- R2L (Remote to Local)

---

## 🛠️ Troubleshooting

### Issue: "ML Model file missing. Run train_model.py!"
**Solution**: The `intrusion_pipeline.pkl` doesn't exist.
```bash
python train_model.py
```

### Issue: "ScriptRunContext" warning
**Solution**: This is a harmless Streamlit warning. Can be ignored or run with:
```bash
streamlit run app.py
```

### Issue: "KDDTrain+.txt" not found
**Solution**: Ensure both training files are in the project root directory

### Issue: Model takes too long to train
**Expected behavior**: First training takes 1-2 minutes. Subsequent app runs are instant (model is cached).

---

## 📈 Performance

- **Model Training Time**: ~1-2 minutes (one-time)
- **CSV Prediction Speed**: <1 second per file
- **URL Analysis**: <500ms per URL
- **Memory Usage**: ~100-150 MB

---

## 🔐 Security Disclaimer

This IDPS is designed for:
- ✅ Educational purposes
- ✅ Security research
- ✅ Network monitoring in controlled environments

**Note**: This is a proof-of-concept. For production environments, use enterprise-grade IDPS solutions like Snort, Suricata, or Zeek.

---

## 📝 License

This project uses the KDD Cup 99 dataset for educational purposes.

---

## 🤝 Contributing

Have improvements? Feel free to:
1. Test with different datasets
2. Optimize the ML model
3. Add new threat detection features
4. Improve URL validation logic

---

## 📧 Support

For issues or questions, check:
- Streamlit documentation: https://docs.streamlit.io/
- Scikit-learn ML docs: https://scikit-learn.org/
- KDD Cup 99 Dataset: https://kdd.ics.uci.edu/databases/kddcup99/

---

**Last Updated**: May 2026
**Version**: 1.0.0