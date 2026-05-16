# Multimodal AI System for Crop Disease and Insect Prediction

A unified multimodal artificial intelligence framework designed to simultaneously detect crop diseases and insect infestations using both computer vision and tabular intelligence pipelines.

The system combines image-based deep learning models with structured agricultural field metrics to generate robust and fail-safe crop health predictions through a rule-based fusion mechanism.

Developed by Team SPROUT STACK for AgriThon 2.0, a 48-hour national hackathon on AI for Sugarcane Diseases and Pest Management organized by VIT Vellore and sponsored by the Department of Biotechnology, Government of India.

## Team SPROUT STACK

- VK Shridharan, Team Leader
- M Akilan
- S M Makesh Kaarthik
- V Pratyush Kumar

## Hackathon Details

AgriThon 2.0 - AI for Sugarcane Diseases and Pest Management

- Organized by: VIT Vellore
- Sponsored by: Department of Biotechnology, Govt. of India
- Duration: 48 Hours
- Theme: AI-driven Crop Disease and Pest Prediction

Hackathon Certificate:

https://drive.google.com/file/d/1caG4CiGlMT52DEqOpAg6ndTmhJEnuVHN/view?usp=sharing

## Key Features

- Dual YOLOv8 pipelines for independent disease and insect detection
- TabNet-based prediction engine for structured agricultural data
- Multimodal fusion combining image and tabular intelligence
- Offline annotation setup using CVAT and Docker
- Rule-based fail-safe decision logic
- Parallel AI processing architecture
- Real-time inference-ready workflow
- Modular and scalable research pipeline

## System Architecture

The framework processes multi-source agricultural inputs through parallel AI pipelines before merging outputs into a unified prediction layer.

```text
              ┌───────────────┐
              │  Crop Image   │
              └───────┬───────┘
                      ▼
        ┌───────────────────────────┐
        │   Image Streaming Layer   │
        └──────┬─────────────┬──────┘
               │             │
               ▼             ▼
         ┌───────────┐ ┌───────────┐
         │  YOLOv8   │ │  YOLOv8   │
         │ (Disease) │ │ (Insects) │
         └─────┬─────┘ └─────┬─────┘
               │             │
               ▼             ▼
         [Output-1]    [Output-2]
               │             │
               └──────┬──────┘
                      ▼
         ┌───────────────────────────┐
         │    Rule-Based Fusion      │
         │      Logic Engine         │
         └────────────┬──────────────┘
                      ▲
                      │
         ┌───────────────────────────┐
         │ TabNet (Tabular Features) │
         │   [Output-3 & Output-4]   │
         └─────────────▲─────────────┘
                       │
             ┌─────────┴─────────┐
             │ Environmental CSV │
             └───────────────────┘
```

## Core Components

### 1. Disease Detection Pipeline

A dedicated YOLOv8 computer vision model trained to identify crop diseases from field images.

Capabilities:

- Disease localization
- Bounding-box predictions
- Pathology identification
- Confidence scoring

Example diseases:

- Yellow Leaf
- Rust
- Blight
- Leaf Spot

### 2. Insect Detection Pipeline

A separate YOLOv8 model optimized for pest and insect identification.

Capabilities:

- Pest localization
- Insect classification
- Multi-object detection
- Field image analysis

Example pests:

- Aphids
- Caterpillars
- Leaf Borers

### 3. Tabular Intelligence Pipeline

A TabNet classifier processes structured agricultural datasets and environmental metrics.

Input features:

- Soil conditions
- Crop parameters
- Binary field survey responses
- Environmental conditions

Output:

- Disease probability
- Pest probability
- Severity estimation

### 4. Fusion Logic Engine

A deterministic rule-based fusion system combines all intermediate outputs.

Objective:

Ensure fail-safe agricultural prediction by capturing anomalies from either image or tabular streams.

## Decision Fusion Logic

The framework follows a pessimistic fusion approach to maximize crop safety.

```text
if either (YOLOv8_Disease is True) or (TabNet_Disease is True):
    Final_Disease_Status = "PRESENT"
else:
    Final_Disease_Status = "ABSENT"

if either (YOLOv8_Insect is True) or (TabNet_Insect is True):
    Final_Insect_Status = "PRESENT"
else:
    Final_Insect_Status = "ABSENT"
```

## Performance Metrics

| Component | Model | Metric | Score |
| --- | --- | --- | --- |
| Disease Detection | YOLOv8 | mAP50 | 82.3% |
| Insect Detection | YOLOv8 | mAP50 | 79.5% |
| Tabular Prediction | TabNet | Accuracy | 87.6% |
| Fusion Pipeline | Rule-Based Fusion | Consistency | 93.2% |

## Data Annotation and Preparation

Annotation tool:

- CVAT (Computer Vision Annotation Tool)
- Docker Desktop

Annotation workflow:

- Uploaded agricultural image datasets
- Created bounding-box annotations
- Exported labels in YOLO format
- Processed XML annotation files
- Generated training-ready datasets

## Dataset Architecture

```text
datasets/
├── disease/
│   ├── images/
│   ├── labels/
│   ├── annotations.xml
│   └── cvat_xml_to_yolo.py

└── insect/
    ├── images/
    ├── labels/
    ├── annotations.xml
    └── cvat_xml_to_yolo.py
```

## Setup and Installation

### Clone Repository

```bash
git clone https://github.com/VK-SHRIDHARAN/AGRI_HACKATHON
cd AGRI_HACKATHON
```

### Install Dependencies

```bash
pip install -r requirements.txt
```

## Offline CVAT Setup Using Docker

### Clone CVAT

```bash
git clone https://github.com/opencv/cvat.git
cd cvat
```

### Start Docker Containers

```bash
docker-compose build
docker-compose up -d
```

### Local Access

- URL: http://localhost:8080
- Username: admin
- Password: admin

## Execution Pipeline

### Step 1 - Disease Detection

```bash
python yolo_disease_infer.py --image datasets/disease/images/test1.jpg
```

### Step 2 - Insect Detection

```bash
python yolo_insect_infer.py --image datasets/insect/images/test1.jpg
```

### Step 3 - TabNet Inference

```bash
python tabnet_infer.py --csv input_data.csv
```

### Step 4 - Fusion Layer Execution

```bash
python fusion.py --image1 path/to/disease_output.txt \
                 --image2 path/to/insect_output.txt \
                 --csv_output path/to/tabnet_output.txt
```

## Technologies Used

### AI / ML

- YOLOv8
- TabNet
- Deep Learning
- Computer Vision
- Multimodal AI

### Programming

- Python

### Data Processing

- Pandas
- NumPy

### Annotation and Deployment

- CVAT
- Docker

### Research Domains

- Precision Agriculture
- Smart Farming
- Crop Intelligence
- Pest Prediction

## Future Improvements

- Real-time mobile deployment
- Edge AI optimization
- Drone-based crop monitoring
- Federated agricultural intelligence
- IoT sensor integration
- Disease severity forecasting
- Multi-crop support system

## Research Contributions

This project demonstrates:

- Multimodal agricultural intelligence
- Hybrid AI reasoning systems
- AI-assisted crop diagnostics
- Rule-based fusion reliability
- Real-world agricultural AI deployment

## Repository Link

GitHub Repository:

https://github.com/VK-SHRIDHARAN/AGRI_HACKATHON

## Acknowledgements

Special thanks to:

- VIT Vellore
- Department of Biotechnology, Government of India
- AgriThon 2.0 Organizers
- Faculty mentors and research coordinators

## Contact

VK Shridharan

- GitHub: https://github.com/VK-SHRIDHARAN
- LinkedIn: https://www.linkedin.com/in/shridharan-vk-108ab728a/