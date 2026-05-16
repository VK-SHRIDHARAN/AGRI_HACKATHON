# 🔍 Multimodal AI System for Crop Disease & Insect Prediction

A unified, multimodal artificial intelligence framework built to concurrently detect sugarcane/crop diseases and pest infestations. This system processes both computer vision feeds (field images) and electronic farm metrics (tabular data), applying a pessimistic fusion decision layer to ensure reliable crop diagnostic mapping.

Developed by **Team Sprout Stack** for **AgriThon 2.0** *(48-Hour Hackathon on 'AI for Sugarcane Diseases and Pest Management' organized by VIT, Vellore and sponsored by the Department of Biotechnology, Govt. of India)*.

---

## 🚀 Key Features
- **Dual CV Pipelines:** Independent YOLOv8 implementations optimized for plant pathology (diseases) and entomology (insect pests).
- **Tabular Intelligence:** Integrates structural, environmental, and questionnaire metrics via a TabNet classifier.
- **Fail-Safe Decision Fusion:** Merges textual predictions and visual outputs via deterministic conditional statements.
- **Offline Annotation Setup:** Local containerized environment configurations to prevent agricultural data sovereignty leaks.

---

## 🏛 System Architecture

The pipeline processes multi-source data through parallel streams before converging into a final evaluation layer:
