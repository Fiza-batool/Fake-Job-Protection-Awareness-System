
# 🛡️ AI-Based Fake Job Protection & Awareness System

An AI-powered **Fake Job Protection & Awareness System** designed to help users identify potentially fraudulent job opportunities through **text analysis, job-post image analysis, and URL verification**.

The system combines **Machine Learning, OCR, data processing, web technologies, and security-oriented verification techniques** to provide detection results, risk scores, verification history, community reporting, and job-fraud awareness.

---

## 🚀 Live Demo

🔗 **[Try the Live Application](https://job-detection-64hm.vercel.app/)**

---

## 🎯 Project Overview

Online job scams can appear in different forms, including written job descriptions, image-based job advertisements, suspicious websites, and social-media posts.

This project provides multiple ways for users to evaluate a job opportunity:

* 📝 **Text-Based Detection**
* 🖼️ **Image-Based Detection using OCR**
* 🔗 **URL Verification**
* 📊 **Risk Score & Confidence**
* 🛡️ **Job-Fraud Awareness**
* 📢 **Community Reporting**
* 🕒 **Verification History**
* 💬 **User Feedback**

The goal is not only to detect suspicious jobs, but also to help users become more aware of common job-fraud indicators.

---

# ✨ Key Features

## 📝 1. Text-Based Job Detection

Users can submit a job description or provide information such as:

* Job title
* Company profile
* Description
* Requirements
* Benefits

The submitted content is cleaned and transformed using **TF-IDF vectorization**, then analyzed by the trained Machine Learning model.

### Output

The system provides:

* **Real / Fake prediction**
* Fake probability
* Real probability
* Confidence
* Risk score
* Model information

A **30% fake-probability threshold** is used for the final classification.

---

## 🖼️ 2. Image-Based Job Detection

Users can upload an image or screenshot of a job advertisement.

The system uses **Tesseract OCR** to extract text from the uploaded image.

### Image Processing Pipeline

```text
Job Post Image
      ↓
Image Preprocessing
      ↓
Grayscale Conversion
      ↓
Contrast Enhancement
      ↓
Image Sharpening / Resizing
      ↓
Tesseract OCR
      ↓
Extracted Text
      ↓
Text Cleaning
      ↓
TF-IDF Vectorization
      ↓
Random Forest Model
      ↓
Real / Fake + Risk Assessment
```

The system also calculates an **OCR confidence score** to indicate the quality of extracted text.

---

## 🔗 3. URL Verification

Users can submit a job-related website URL for verification.

The system performs multiple checks, including:

* URL format validation
* HTTPS/SSL verification
* WHOIS/domain information
* Domain creation date
* Domain age
* Suspicious keyword detection
* Trust score calculation

The result includes:

* **Safe / Suspicious status**
* Risk score
* Trust score
* SSL status
* Domain age
* Domain information
* Suspicious/blacklisted indicator

---

# 🤖 Machine Learning

## Model Development

The project uses an enhanced job-posting dataset containing **16,060 job records**.

The dataset was developed using job-posting data and additional examples representing modern and Pakistani job-market scenarios.

The enhanced dataset includes:

* Real job descriptions
* Fake job descriptions
* Pakistani fake-job examples
* Modern real-job examples

Additional fake-job examples include patterns such as:

* Registration/payment requests
* WhatsApp-based job scams
* Suspicious fee requirements
* Other common fraudulent-job patterns

---

## 🔬 Models Compared

Five Machine Learning algorithms were trained and compared:

| Model                        | Purpose                 |
| ---------------------------- | ----------------------- |
| Multinomial Naive Bayes      | Text classification     |
| Logistic Regression          | Text classification     |
| Random Forest                | Ensemble classification |
| Support Vector Machine (SVM) | Classification          |
| Decision Tree                | Classification          |

After comparison, **Random Forest was selected as the final model** based on the project's evaluation results.

### Reported Accuracy

**97.43%**

> Accuracy reported from the project's model-training process.

---

## ⚖️ Handling Class Imbalance

The dataset originally contained a significant imbalance between real and fake job examples.

To reduce the impact of class imbalance, the training process uses:

```python
class_weight='balanced'
```

This gives greater importance to the minority class during model training and helps the model detect fraudulent job examples more effectively.

---

# 📊 Model Evaluation

The model-training process evaluates the classifiers using:

* Accuracy
* Precision
* Recall
* F1-Score
* Confusion Matrix
* Classification Report

The training workflow also generates visualizations for model evaluation and comparison.

---

# 🧠 Text Processing Pipeline

The text detection process follows these steps:

```text
Job Information
      ↓
Text Cleaning
      ↓
Remove URLs / HTML / Unwanted Characters
      ↓
Normalize Text
      ↓
TF-IDF Vectorization
      ↓
Trained Random Forest Model
      ↓
Real / Fake Probabilities
      ↓
Risk Assessment
```

---

# 📊 Risk Assessment

The system uses model probabilities to calculate the potential risk of a job listing.

For text and image detection:

```text
Fake Probability ≥ 30%
        ↓
      FAKE
```

Otherwise:

```text
Fake Probability < 30%
        ↓
      REAL
```

The system returns both **real and fake probabilities**, allowing the application to display a more informative risk assessment rather than relying only on a binary result.

---

# 🛡️ Job-Fraud Awareness

Detection is only one part of the system.

The project also focuses on **job-fraud awareness** by helping users recognize common warning signs.

Users can learn to be cautious when a job opportunity contains indicators such as:

* Requests for registration or processing fees
* Unrealistic salary promises
* Requests for sensitive personal information
* Suspicious URLs
* Pressure to communicate through unofficial channels
* "Too good to be true" offers
* Suspicious company or job information

The purpose is to help users make more informed decisions when applying for jobs online.

---

# 📢 Community Reporting

Users can report suspicious job opportunities to help build community awareness.

Supported reporting reasons include:

* Payment Required
* Personal Information Theft
* Fake Company
* Too Good To Be True
* Suspicious URL
* Duplicate Posting
* Other

The system also checks for duplicate reports before storing a new report.

---

# 🕒 Verification History

Detection results are stored in **MongoDB** to maintain verification history.

The system records information such as:

* Detection method
* Input information
* Prediction
* Risk score
* Timestamp

This allows users/system administrators to review previous verification activity.

---

# 💬 User Feedback

Users can provide feedback on detection results using:

* 👍 Thumbs Up
* 👎 Thumbs Down
* Optional comments

Feedback statistics include:

* Total feedback
* Positive ratings
* Negative ratings
* User satisfaction rate

This feedback can be used to identify areas for future model and system improvement.

---

# 🏗️ System Architecture

```text
                         USER
                           │
             ┌─────────────┼─────────────┐
             │             │             │
          Job Text      Job Image      Job URL
             │             │             │
             │          Tesseract        │
             │             │             │
             │       Extracted Text      │
             │             │             │
             └─────────────┼─────────────┘
                           │
                     Processing
                           │
                  ┌────────┴────────┐
                  │                 │
               ML Model        URL Analysis
                  │                 │
                  └────────┬────────┘
                           │
                  Detection / Risk
                           │
              ┌────────────┼────────────┐
              │            │            │
           Result       Risk Score   Awareness
              │
              ↓
          MongoDB
              │
       History / Reports
       / User Feedback
```

---

# 🧰 Tech Stack

### Backend

* Python
* Flask
* REST API

### Machine Learning

* scikit-learn
* Random Forest
* Multinomial Naive Bayes
* Logistic Regression
* Support Vector Machine
* Decision Tree
* TF-IDF

### Data Processing

* Pandas
* NumPy

### OCR & Image Processing

* Tesseract OCR
* pytesseract
* Pillow (PIL)

### URL & Domain Verification

* Requests
* WHOIS
* Python URL parsing

### Database

* MongoDB

### Deployment

* Vercel

---

# 📁 Project Structure

```text
Fake-Job-Detection/
│
├── Backend/
│   ├── routes/
│   ├── models/
│   ├── database/
│   └── ...
│
├── Frontend/
│   └── ...
│
├── .gitignore
└── README.md
```

---

# 🎓 Project Context

This project was developed as a **Final Year Project (FYP)** focused on applying Artificial Intelligence and Machine Learning to a real-world problem: **online job fraud detection and awareness**.

The system combines multiple technologies into a single application to provide users with different ways to evaluate potentially fraudulent job opportunities.

---

# 🔮 Future Improvements

Possible future improvements include:

* Expanding the training dataset
* Adding more diverse Pakistani and international job-scam examples
* Improving model generalization
* More advanced website/domain reputation analysis
* Improved OCR for low-quality and multilingual job advertisements
* Explainable AI for showing why a job was classified as suspicious
* Real-time threat intelligence integration
* Continuous model improvement using validated user feedback

---

# 👩‍💻 Developer

**Fiza Batool**

**Web Developer | AI Applications & Automation**

🔗 **GitHub:** [Fiza-batool](https://github.com/Fiza-batool)

🔗 **LinkedIn:** [Connect with me on LinkedIn](https://www.linkedin.com/in/fiza-batool-69a145408/)

---

## ⚠️ Disclaimer

This application is intended as an **assistive job-fraud detection and awareness tool**.

Detection results should not be considered a definitive guarantee that a job opportunity or website is legitimate or fraudulent. Users should independently verify employers, websites, and job offers before sharing personal information or making payments.
