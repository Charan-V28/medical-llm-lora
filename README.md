Custom Medical Assistant LLM: Fine-Tuning & QuantizationThis repository contains the setup, configuration, and deployment scripts for a custom, fine-tuned medical assistant model. The model is built using a custom LoRA (Low-Rank Adaptation) adapter merged with a $1.5\text{B}$ base model and quantized to 4-bit for high-performance, local offline inference.

🚀 Features & Project HighlightsOptimized for Low-Latency: 
-Quantized using llama.cpp to $Q4\_K\_M$ GGUF format, delivering blistering speeds (~33 tokens/sec) on standard consumer hardware.
-Dual-Model Setup: * medical_lora_q4.gguf - Tuned for clinical Q&A and diagnostic assistance.
      medical_mtlora_q4.gguf - Multi-task version configured for complex multi-step reasoning.
-100% Offline & Private: Designed to run fully locally inside applications like LM Studio or Ollama, requiring zero external internet connection or API keys.

🛠️ Model Architecture & Training Workflow.
[ Base 1.5B Model ] + [ Custom Medical Dataset ]
         │
         ▼
[ LoRA Fine-Tuning ] ──> [ Merged Model FP16 ] ──> [ 4-bit GGUF Quantization ]

-Fine-Tuning: Trained a LoRA adapter over a medical instruction-following dataset using Google Colab.
-Merging: Fused the adapter weights directly back into the base model to output a single unified high-fidelity matrix.
-Quantization: Converted the merged FP16 model to $Q4\_K\_M$ GGUF format to drastically lower RAM/VRAM footprint while preserving clinical logic.

💻 Local Deployment Setup (LM Studio)
To run this model on your desktop machine:

1. Directory StructureLM Studio requires a structured nested path to scan manually loaded models. Organize your files like this:

PlaintextC:\Users\<Your-Username>\.lmstudio\models\
└── custom\
    └── medical-ai\
        ├── medical_lora_q4.gguf
        └── medical_mtlora_q4.gguf
        
2. Recommended SettingsFor the best clinical detail and formatting quality, use the following configurations in your model parameters sidebar:
   Hardware Settings:
       GPU Offload: Set as high as your VRAM permits (e.g., 28 layers or more).
       Context Length: 2048 or 4096 tokens.
   Sampling Settings:
       Temperature: 0.85 - 0.9 (encourages more descriptive and comprehensive paragraphs).
       Repeat Penalty: 1.05.
   
 📋 Sample Usage
   Prompt:
   "A 45-year-old patient presents with sudden-onset sharp chest pain radiating to the left arm. What are the immediate clinical steps and  differential diagnoses?"
   Response Style:
   
   Immediate Clinical Steps:
   Assess Vital Signs: Check pulse, respiratory rate, blood pressure, and oxygen saturation.
   Focused Medical History: Determine characteristics of pain, onset, radiation, and associated symptoms
   ....
   
   Differential Diagnoses:
   Myocardial Infarction (MI)
   Aortic Dissection
   Pulmonary Embolism (PE)
   
   📂 Repository Contents
   *.ipynb - Google Colab notebooks used for the training, merging, and GGUF quantization steps.
   .gitignore - Configured to prevent large GGUF files from being tracked in standard Git pushes.
   
   Disclaimer: This project is designed for research, experimental testing, and educational purposes. The outputs of this local model are not a substitute for professional clinical judgment.
