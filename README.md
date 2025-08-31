# PySpector: A Machine Learning Tool for Detecting Scrambled Python Code



## 📖 Project Overview

PySpector is a practical cybersecurity tool that uses machine learning to distinguish between normal, human-written Python scripts and those that have been deliberately scrambled or hidden (a technique known as obfuscation). This project demonstrates an end-to-end ML pipeline: from custom dataset creation and feature extraction to model training and real-world prediction on new files.

The core of the project is a `RandomForestClassifier` trained to identify the statistical "fingerprints" of scrambled code, providing a fast and effective way to flag potentially malicious scripts for further analysis.

---

## 🎯 The Problem

In cybersecurity, attackers frequently use code obfuscation to hide malware, making it difficult for antivirus software and security analysts to detect. As Python becomes increasingly popular for both legitimate tools and malicious scripts, the ability to automatically identify these intentionally confusing scripts is a critical first step in malware analysis and threat hunting. Manual inspection is slow and impractical at scale, creating a need for an automated solution.

## ✨ The Solution

This project tackles the problem by treating it as a binary classification task. A machine learning model is trained to learn the difference between the statistical properties of normal and scrambled code.

1.  **Custom Dataset:** A balanced dataset was created using thousands of benign Python scripts and their programmatically scrambled counterparts.
2.  **Static Analysis:** The `radon` library is used to perform static analysis on Python files, extracting key metrics related to code complexity (Cyclomatic Complexity, LOC, Halstead metrics) without ever running the code.
3.  **ML Model:** A Random Forest model is trained on these metrics to classify any given Python script as either **Normal** or **Scrambled**.

---

## 🛠️ Tech Stack

* **Language:** Python
* **Core Libraries:** Pandas, NumPy, Scikit-learn
* **Feature Extraction:** Radon
* **Model Persistence:** Joblib
* **Visualization:** Matplotlib, Seaborn
* **Development Environment:** Google Colab / Jupyter Notebook

---







**Example Output:**
```
--- Analyzing file with a specialist model: my_malicious_script.py ---

Extracted Specialist Metrics:
   loc   v(g)  lOCode  lOComment  lOBlank  uniq_Op  uniq_Opnd  total_Op  total_Opnd  branchCount
0  150   45.0     120          5       25       30         95       250         400         45.0

---> Prediction: SCRAMBLED (Confidence: 97.50%)
```

---

## 📊 Model Performance

The final specialist model performs exceptionally well, achieving over **98% accuracy and F1-score** on the held-out test set. The model's feature importance analysis confirms that complexity metrics are the strongest indicators of scrambled code.

![Feature Importance Chart](images/feature_importance.png)
*Figure 1: The most predictive features for identifying scrambled code. Cyclomatic Complexity (`v(g)`) and Halstead-based metrics are clear indicators.*

---

## 🧠 Key Learnings

One of the most significant takeaways from this project was the critical importance of **data relevancy**. An initial approach using a public dataset for general software defects (NASA CM1) proved ineffective for this specific task, as the patterns learned from legacy C code did not apply to modern Python.

This experience led to a strategic pivot to a new problem (obfuscation detection) and a purpose-built dataset. It underscored that a highly relevant, custom dataset is far superior to a large but mismatched one, and it highlighted that diagnosing *why* a model fails is a crucial step in building a successful real-world tool.

---





Created by [Your Name] - [Your Email or LinkedIn Profile URL]

Project Link: [https://github.com/[YourUsername]/py-scrambled-code-detector](https://github.com/[YourUsername]/py-scrambled-code-detector)
