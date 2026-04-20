# 🐶 Dog Training Visualization with Controlled Diffusion Models

## 🔗 Video Link

https://drive.google.com/file/d/1wSiJVdwwQkaRtWLouT6EmJIwSf4wOCgX/view?usp=sharing

---

## 📌 Overview

This project builds a **controlled image generation system** for animal care and training scenarios using diffusion models.

Given structured input (e.g., animal type, breed, condition, environment), the system:

* Converts structured data into prompts
* Generates images using Stable Diffusion
* Evaluates output quality and consistency
* Compares naive vs structured prompting strategies

---

## 🎯 Objective

The goal is to study:

> How structured prompts improve controllability, consistency, and realism in AI-generated images.

---

## 🔢 Dataset

No dataset is directly used for training in this project.

We leverage a pre-trained diffusion model (Stable Diffusion), which has been trained on large-scale image-text datasets.

Suggested datasets such as Oxford-IIIT Pet and AFHQ are used as conceptual references for evaluating realism and diversity of generated animal images.

---

## 💬 Prompt Design

### Baseline Prompt

Simple and vague:

```
a dog training tutorial
```

---

### Structured Prompts (4 Panels)

Panel 1:

```
A red corgi dog and an adult woman standing together on a sunny grass field outdoors, with a frisbee and a bone treat, preparing for fetch training.
```

Panel 2:

```
An adult woman throwing a frisbee across a sunny grass field outdoors, a red corgi dog watching eagerly in the distance.
```

Panel 3:

```
A red corgi dog running back across a sunny grass field outdoors with a frisbee in its mouth.
```

Panel 4:

```
An adult woman kneeling down giving a bone treat to a red corgi dog on a sunny grass field outdoors.
```

---

👉 All structured prompts explicitly define:

* dog breed (corgi)
* dog color (red)
* environment (grass field)
* action (training steps)

This allows controlled generation across panels.

---

## ⚙️ Pipeline

```
Structured Input
      ↓
Prompt Generation (Template-based)
      ↓
Stable Diffusion (Image Generation)
      ↓
Control Mechanisms
  - Structured prompts
  - Negative prompts
      ↓
Image Outputs (Panels + Grids)
      ↓
Evaluation
  - Single-panel accuracy
  - Cross-panel consistency
      ↓
Statistical Analysis
```

---

## 🛠️ Technologies Used

* Python
* PyTorch
* Stable Diffusion (via Diffusers)
* Pandas (evaluation)
* PIL (image processing)

---

## 🎛️ Control Mechanisms

### ✅ 1. Structured Prompts

Used to enforce:

* Breed consistency
* Color consistency
* Scene control

### ✅ 2. Negative Prompts

Used to suppress generation errors:

```
blurry, deformed, extra limbs, bad anatomy, multiple dogs
```

👉 Helps reduce artifacts and improve visual quality.


---

## 📊 Evaluation Methodology

We designed a **human-interpretable scoring system** with two levels:

---

### 🔸 Part 1: Single-Panel Accuracy (Max = 5)

Each image is evaluated on:

| Metric            | Description             |
| ----------------- | ----------------------- |
| dog_color_correct | Correct color           |
| dog_breed_correct | Matches corgi           |
| scene_correct     | Correct environment     |
| prop_present      | Required object present |
| action_correct    | Correct action          |

---

### 🔸 Part 2: Cross-Panel Consistency (Max = 5)

Each 4-panel sequence is evaluated on:

| Metric                    | Description                   |
| ------------------------- | ----------------------------- |
| dog_color_consistent      | Same color across panels      |
| dog_appearance_consistent | Same dog identity             |
| scene_consistent          | Same environment              |
| story_coherent            | Logical progression           |
| props_continuous          | Objects persist across panels |

---

## 📈 Results

### 🔹 Single-Panel Accuracy

| Method     | Mean Score |
| ---------- | ---------- |
| Baseline   | 1.15       |
| Structured | 3.60       |

👉 **+2.45 improvement**

---

### 🔹 Cross-Panel Consistency

| Method     | Mean Score |
| ---------- | ---------- |
| Baseline   | 0.0        |
| Structured | 2.6        |

👉 Baseline fails completely at maintaining consistency.

---

### 🔍 Key Findings

#### ✅ Strengths of Structured Prompts

* Strong control over **breed (0.9) and color (0.95)**
* High environment consistency (1.0)
* Significant improvement in overall accuracy

#### ⚠️ Limitations of Diffusion Models

* Poor **story coherence (0.0)**
* Weak **object continuity (0.0)**
* Inconsistent identity across panels (0.6)

---

## 🧾 Conclusion

Structured prompts significantly improve:

* Attribute-level control (breed, color)
* Image consistency across runs
* Overall generation quality

However, diffusion models still struggle with:

* Maintaining narrative structure
* Tracking objects across scenes
* Preserving identity over multiple images

> This highlights the trade-off between controllability and generative limitations in diffusion models.
