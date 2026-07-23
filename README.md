# Cognitive Inference via Visual Analysis

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue)]()
[![Transformers](https://img.shields.io/badge/HuggingFace-Transformers-yellow)]()
[![Status](https://img.shields.io/badge/Status-Development-orange)]()

A Visual Question Answering (VQA) web application that lets a user upload an image, ask a natural-language question about it, and receive an AI-generated answer along with a confidence breakdown across the top predicted answers.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Tech Stack](#tech-stack)
- [Project Structure](#project-structure)
- [Getting Started](#getting-started)
  - [Prerequisites](#prerequisites)
  - [Installation](#installation)
  - [Running the App](#running-the-app)
- [How It Works](#how-it-works)
- [Usage](#usage)
- [Roadmap](#roadmap)
- [License](#license)

## Overview

Cognitive Inference via Visual Analysis explores how deep learning models reason over paired image and text inputs to answer open-ended questions about visual content — a task known as Visual Question Answering (VQA). The application wraps a pretrained VQA model behind a simple Flask interface: users submit an image and a question, and the system returns the most likely answer along with a visualization of confidence across the top candidate answers.

## Features

- **Image + Question Input** — Upload any image and ask a free-form question about its contents
- **Top-K Answer Prediction** — Retrieves the top 5 candidate answers with associated confidence scores
- **Confidence Visualization** — Renders a pie chart (via Matplotlib) showing the relative confidence of each candidate answer
- **In-Browser Image Preview** — Uploaded images are base64-encoded and displayed alongside results, no file storage required
- **Simple Web UI** — Single-page Flask + Jinja templates for quick interaction, no separate frontend build step

## Tech Stack

| Layer          | Technology                          |
| -------------- | ------------------------------------ |
| Backend        | Python, Flask                        |
| ML / Inference | PyTorch, Hugging Face Transformers (VQA pipeline) |
| Image Handling | Pillow (PIL)                         |
| Visualization  | Matplotlib                           |
| Frontend       | HTML, CSS                            |

## Project Structure

```
├── app.py            # Flask app: routes, image handling, pie chart generation
├── model.py           # Model loading / configuration logic
├── VQAmodel.py         # VQA model definition and inference helpers
├── requirements.txt    # Python dependencies
├── templates/          # HTML templates (Jinja2) for the web UI
  ├── index.html
  └── result.html
└── static/            # Static assets (CSS, JS, images)
  └── style.css
```

## Getting Started

### Prerequisites

- Python 3.9+
- pip

### Installation

1. Clone the repository:
```bash
   git clone https://github.com/Shanmukhi-Mudundi/Cognitive-Inference-via-Visual-Analysis.git
   cd Cognitive-Inference-via-Visual-Analysis
```

2. (Recommended) Create and activate a virtual environment:
```bash
   python -m venv venv
   source venv/bin/activate   # On Windows: venv\Scripts\activate
```

3. Install dependencies:
```bash
   pip install -r requirements.txt
```

### Running the App

```bash
python app.py
```

The app will be available at `http://localhost:5000` (Flask's default development server, running with `debug=True`).

## How It Works

1. The user uploads an image and submits a question through the web form.
2. The image is converted to a base64-encoded JPEG for in-browser preview.
3. The image and question are passed to a Hugging Face `visual-question-answering` pipeline, which returns the top 5 predicted answers with confidence scores.
4. The top answer is displayed to the user, along with a Matplotlib-generated pie chart visualizing the confidence distribution across all 5 candidate answers.

## Usage

1. Open the app in your browser.
2. Upload an image (e.g., a photo containing objects, people, or scenes).
3. Type a question about the image (e.g., *"What color is the car?"* or *"How many people are in this photo?"*).
4. Submit and view the predicted answer, the uploaded image, and the confidence pie chart.

## Roadmap

- [ ] Add support for batch/multiple question processing per image
- [ ] Improve answer explainability (e.g., attention/heatmap visualization over the image)
- [ ] Add caching for repeated model inference calls
- [ ] Containerize with Docker for easier deployment

## License

This project was developed for academic and research purposes.
