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
         ┌───────────────────────────┐     ┌───────────────────────────┐
         │    Rule-Based Fusion      │ ◄── │ TabNet (Tabular Features) │
         │      Logic Engine         │     │   [Output-3 & Output-4]   │
         └────────────┬──────────────┘     └─────────────▲─────────────┘
                      │                                  │
                      ▼                         ┌────────┴──────────┐
           ┌──────────────────────┐             │ Environmental CSV │
           │ Final Prediction Map │             └───────────────────┘
           └──────────────────────┘

---

## 🛠 Setup & Installation

### 1. Repository & Main Environment
```bash
# Clone the project repository
git clone [https://github.com/your-username/crop-disease-multimodal.git](https://github.com/your-username/crop-disease-multimodal.git)
cd crop-disease-multimodal

# Install core system dependencies
pip install -r requirements.txt
2. Offline Data Annotation (CVAT Setup via Docker)To maintain local security over field images, annotations are structured offline:Bash# Clone and open the official CVAT toolkit
git clone [https://github.com/opencv/cvat.git](https://github.com/opencv/cvat.git)
cd cvat

# Spin up local Docker containers
docker-compose build
docker-compose up -d
Local Web Access: Open your browser and navigate to http://localhost:8080Default Credentials: Username: admin | Password: admin📂 Dataset ArchitectureThe architecture relies on split multi-modal feeds configured locally as follows:datasets/
├── disease/
│   ├── images/              # Field imagery containing leaf pathologies
│   ├── labels/              # Bounding box targets (Blight, Rust, etc.)
│   ├── annotations.xml
│   └── cvat_xml_to_yolo.py  # Map extraction parsing tool
└── insect/
    ├── images/              # Pest infestation photography
    ├── labels/              # Target box definitions (Aphid, Caterpillar, etc.)
    ├── annotations.xml
    └── cvat_xml_to_yolo.py
📊 Evaluation & Metrics SummaryComponent StreamModel EnginePrimary MetricScore EvaluatedPathology EngineYOLOv8mAP5082.3%Entomology EngineYOLOv8mAP5079.5%Agronomic MatrixTabNet ClassifierAccuracy87.6%Combined PipelineRule-Based CombinerSystem Consistency93.2%💻 Execution PipelineRun inference through the serial terminal execution structure using the commands below:Step 1: Detect Pathology from Image StreamBashpython yolo_disease_infer.py --image datasets/disease/images/test1.jpg
Step 2: Detect Insects from Image StreamBashpython yolo_insect_infer.py --image datasets/insect/images/test1.jpg
Step 3: Run TabNet Predictive Processing on Environmental DataBashpython tabnet_infer.py --csv input_data.csv
Step 4: Run Decision Fusion ExecutionBashpython fusion.py --image1 path/to/disease_output.txt \
                 --image2 path/to/insect_output.txt \
                 --csv_output path/to/tabnet_output.txt
⚙️ Decision Fusion Logic MatrixTo maximize crop security, the model relies on a pessimistic conditional logic schema:Pythonif either (YOLOv8_Disease is True) or (TabNet_Disease is True):
    Final_Disease_Status = "PRESENT"
else:
    Final_Disease_Status = "ABSENT"

if either (YOLOv8_Insect is True) or (TabNet_Insect is True):
    Final_Insect_Status = "PRESENT"
else:
    Final_Insect_Status = "ABSENT"
👥 Hackathon Team (SPROUT STACK)VK Shridharan (Team Leader)M AkilanS M Makesh KaarthikV Pratyush Kumar
