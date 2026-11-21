# 🚀 Agile Sprint Retrospective Web Application with AI Sentiment Analysis

[![Angular](https://img.shields.io/badge/Angular-18-DD0031?style=for-the-badge&logo=angular&logoColor=white)](https://angular.io/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.x-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)](https://spring.io/projects/spring-boot)
[![PostgreSQL](https://img.shields.io/badge/PostgreSQL-16-4169E1?style=for-the-badge&logo=postgresql&logoColor=white)](https://www.postgresql.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110+-009688?style=for-the-badge&logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![PyTorch](https://img.shields.io/badge/PyTorch-CUDA-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white)](https://pytorch.org/)
[![Hugging Face](https://img.shields.io/badge/🤗%20Hugging%20Face-Twitter--RoBERTa-FFD21E?style=for-the-badge)](https://huggingface.co/cardiffnlp/twitter-roberta-base-sentiment)

> **Bachelor's Final Year Project (PFE) — Computer Science: Big Data & Data Analysis**  
> Developed during an end-of-studies internship at **TELNET INC** (Sfax, Tunisia) | **Higher Institute of Computer Science and Multimedia of Sfax (ISIMS)** — Academic Year 2024–2025[cite: 1, 4, 19].

---

## 📋 Table of Contents
- [Overview](#-overview)
- [Demo Video](#-demo-video)
- [Key Features & Role-Based Access](#-key-features--role-based-access)
- [System Architecture](#-system-architecture)
- [AI & NLP Sentiment Analysis Pipeline](#-ai--nlp-sentiment-analysis-pipeline)
- [Repository Structure](#-repository-structure)
- [Tech Stack](#-tech-stack)
- [Getting Started & Installation](#-getting-started--installation)
- [API Endpoints Overview](#-api-endpoints-overview)
- [Author & Acknowledgments](#-author--acknowledgments)

---

## 🎯 Overview

In Agile/Scrum environments, sprint retrospectives are critical ceremonies for continuous improvement, team alignment, and bottleneck resolution[cite: 15]. However, managing feedback manually across scattered tools often leads to poor action-item follow-up, lack of prioritization, and difficulty assessing underlying team morale[cite: 15, 19, 20].

This full-stack web platform provides a **centralized, collaborative, and intelligent workspace** tailored for Agile teams[cite: 15, 25]. Beyond standard retrospective boards, interactive voting, and Kanban task tracking, the platform integrates a **fine-tuned Transformer NLP model (`Twitter-RoBERTa`)** exposed via **FastAPI** to automatically classify team feedback into **Positive**, **Negative**, or **Neutral** sentiments in real time[cite: 15, 111, 115].

---

## 🎥 Demo Video

<!-- 
  INSTRUCTIONS TO EMBED YOUR VIDEO ON GITHUB:
  1. Edit this README directly on GitHub.com.
  2. Drag and drop your .mp4 demo video file right below this comment block.
  3. GitHub will automatically upload it and replace it with a native playable video link!
  (Alternatively, paste your YouTube/Drive link below)
-->

https://github.com/user-attachments/assets/YOUR-VIDEO-ASSET-ID

*(If the embedded player does not load, [watch the full walkthrough here](#))*

---

## ✨ Key Features & Role-Based Access

The application enforces Role-Based Access Control (RBAC) across **four distinct user roles**[cite: 30]:

### 🔐 Common Features (All Authenticated Users)
* **Secure Authentication & Onboarding:** Email/password authentication secured with Spring Security[cite: 31, 40]. Newly created accounts automatically receive a temporary password via email[cite: 49, 56].
* **Personal User Dashboard:** Visual overview of ongoing and completed retrospectives presented as interactive cards[cite: 31, 69].
* **Real-Time AI Sentiment Analysis:** One-click sentiment evaluation (`Positive`, `Negative`, `Neutral`) on any retrospective comment powered by the NLP microservice[cite: 31, 115, 116].
* **Profile Management:** Update personal details, avatar, skills, bio, and password[cite: 36, 53, 93].

### 👔 Project Manager
* **User Management:** Create, update, search, and delete user accounts and assign roles[cite: 31, 56].
* **Project Lifecycle Management:** Create and manage projects (timeline, category, progress percentage, sprint count, and team member assignments)[cite: 31, 58, 59].
* **Executive & Admin Analytics Dashboard:** Monitor global KPIs, sprint burndown charts, task completion rates, task distribution by status/priority, and team velocity[cite: 31, 94].

### 🧭 Scrum Master
* **Retrospective Facilitation:** Launch retrospectives linked to specific projects and sprints, invite participants (with automated email invitations), and set report availability windows[cite: 32, 70, 82].
* **Custom Retrospective Templates:** Use built-in frameworks (*Start-Stop-Continue*, *Mad-Sad-Glad*) or create/customize multi-column templates with estimated durations[cite: 32, 91, 92].
* **Action Item & Kanban Tracking:** Convert retrospective insights into actionable tasks with priorities, due dates, tags, attachments, and assignees[cite: 32, 80, 81]. Toggle seamlessly between **Kanban Board** (`To Do`, `In Progress`, `Completed`) and **Table View**[cite: 79, 80].

### 👥 Team Member
* **Collaborative Kanban Feedback:** Post, edit, and categorize comments under retrospective columns with priority levels, tags, and optional image attachments[cite: 32, 77, 78].
* **Interactive Heart-Voting System:** Upvote high-priority comments with live vote counters to democratically surface the most critical team topics[cite: 32, 78].

### 🛡️ Administrator
* Full system-wide privileges inheriting all capabilities of Project Managers, Scrum Masters, and Team Members[cite: 32].

---

## 🏗️ System Architecture

The solution follows a clean separation of concerns across three decoupled modules[cite: 44, 115]:

1. **Frontend (`frontend/` — Angular 18):** Component-based Single-Page Application (SPA) handling UI views, reactive forms, data binding, interactive Kanban boards, and analytics dashboards[cite: 40, 44, 45]. Communicates with both backend services via RESTful HTTP/JSON requests[cite: 44, 115].
2. **Backend (`backend/` — Spring Boot 3.x):** Monolithic layered architecture organized into `Controller`, `Service`, `Repository`, and `Model/DTO` packages[cite: 44]. Handles business logic, authentication/authorization via Spring Security, automated SMTP email notifications, and data persistence via Spring Data JPA / Hibernate[cite: 40, 41, 44, 45].
3. **Database (`PostgreSQL`):** Relational database storing users, roles, projects, retrospectives, custom templates, comments, heart-votes, action tasks, and tags[cite: 39, 45, 72, 91].
4. **AI Microservice (`ai/` — FastAPI + PyTorch):** Dedicated Python REST service hosting the fine-tuned `Twitter-RoBERTa` model for low-latency real-time sentiment inference on retrospective comments.

---

## 🧠 AI & NLP Sentiment Analysis Pipeline

To automatically interpret qualitative sprint feedback, three pre-trained Transformer architectures were benchmarked on real Agile retrospective comments[cite: 105, 106]:

### 1. Pre-Trained Model Benchmarking
| Model | Base Architecture | Language Support | Accuracy | Weighted F1-Score | Inference Time | Avg. Confidence |
| :--- | :--- | :--- | :---: | :---: | :---: | :---: |
| `bert-base-multilingual-uncased-sentiment`[cite: 105] | BERT[cite: 106] | Multilingual (6 langs)[cite: 106] | 62.5%[cite: 109] | 0.57[cite: 109] | 0.749s[cite: 109] | 0.44[cite: 109] |
| `twitter-xlm-roberta-base-sentiment`[cite: 105] | XLM-RoBERTa[cite: 106] | Multilingual (8 langs)[cite: 106] | 62.5%[cite: 109] | 0.57[cite: 109] | 0.124s[cite: 109] | 0.78[cite: 109] |
| **`cardiffnlp/twitter-roberta-base-sentiment`**[cite: 105, 110] | **RoBERTa**[cite: 106] | **English**[cite: 106] | **87.5%**[cite: 109] | **0.88**[cite: 109] | **0.287s**[cite: 109] | **0.79**[cite: 109] |

### 2. Domain-Specific Dataset Generation & Fine-Tuning
* **Synthetic Agile Corpus (`2,100` samples):** Generated via a domain-contextualized Python pipeline (`generate_agile_dataset.py`) covering Scrum ceremonies, roles, and engineering workflows, balanced equally across **700 Positive**, **700 Negative**, and **700 Neutral** comments (80% Train / 10% Validation / 10% Test)[cite: 112].
* **Training Configuration:** Fine-tuned using PyTorch with NVIDIA CUDA GPU acceleration (`max_length=128`, `batch_size=8` with gradient accumulation `2`, `lr=2e-5`, linear scheduler, weight decay `0.01`, optimizing for best validation F1-score)[cite: 110, 111].
* **Post-Fine-Tuning Evaluation (Test Set — 210 samples):**
  * **Negative:** Precision `1.00` | Recall `0.99` | F1-Score `0.99`[cite: 114]
  * **Neutral:** Precision `1.00` | Recall `1.00` | F1-Score `1.00`[cite: 114]
  * **Positive:** Precision `0.99` | Recall `1.00` | F1-Score `0.99`[cite: 114]
  * **Overall Test Accuracy:** **`100%` (Macro F1: `1.00`)**[cite: 114]

---

## 📁 Repository Structure

* **`backend/`** — Spring Boot REST API & Business Logic[cite: 40, 44]
  * `src/main/java/.../controller/` — REST Controllers (`Auth`, `User`, `Project`, `Retrospective`, `Comment`, `Vote`, `Task`, `Template`)[cite: 44, 51, 70, 71, 90]
  * `src/main/java/.../service/` — Core business logic & automated SMTP email notification services[cite: 44, 51, 70]
  * `src/main/java/.../repository/` — Spring Data JPA / Hibernate database repositories[cite: 44, 45]
  * `src/main/java/.../model/` — JPA Entities, Enums (`UserRole`, `ProjectStatus`, `RetroStatus`, `TaskStatus`, `TaskPriority`, `CommentPriority`), and DTOs[cite: 44, 52, 72]
  * `src/main/resources/application.properties` — Database & mail server configuration
  * `pom.xml` — Maven dependencies

* **`frontend/`** — Angular 18 Single-Page Application[cite: 40, 44]
  * `src/app/components/` — Landing page, Login, User & Admin Dashboards, Kanban boards, Retrospective & Task modals[cite: 45, 54, 55, 77, 79, 94]
  * `src/app/services/` — Angular HTTP services communicating with Spring Boot and FastAPI[cite: 44, 45]
  * `src/app/models/` — TypeScript interfaces & data models
  * `angular.json` & `package.json` — Angular workspace configuration & npm dependencies

* **`ai/`** — NLP Sentiment Analysis Microservice & Training Scripts[cite: 112, 115]
  * `sentiment_analyzer.py` — FastAPI application serving the fine-tuned sentiment classifier
  * `generate_agile_dataset.py` — Domain-specific Agile comment dataset generator (`agile_retrospective_comments_large.csv`)[cite: 112, 113]
  * `twitter_roberta_finetuned/` — Fine-tuned Transformer model weights & tokenizer configuration[cite: 111]
  * `requirements.txt` — Python dependencies

---

## 🛠️ Tech Stack

* **Frontend:** Angular 18, TypeScript, HTML5, CSS3[cite: 39, 40]
* **Backend:** Java, Spring Boot, Spring Security, Spring Data JPA / Hibernate, JavaMail Sender[cite: 40, 41, 45]
* **Database:** PostgreSQL[cite: 39]
* **AI & Machine Learning:** Python, PyTorch, CUDA, Hugging Face `transformers`, `scikit-learn`, `pandas`, FastAPI, Uvicorn[cite: 104, 105, 115]
* **Tools & Methodology:** Agile Scrum (4 Sprints), UML (Draw.io), Postman, DataGrip, IntelliJ IDEA, WebStorm, PyCharm, Git/GitHub[cite: 27, 38, 39, 40, 42, 103]

---

## 🚀 Getting Started & Installation

### Prerequisites
* **Java JDK 17+** & **Maven**
* **Node.js (v18+)** & **Angular CLI (`npm install -g @angular/cli`)**
* **PostgreSQL 14+**[cite: 39]
* **Python 3.10+** (Conda environment recommended; NVIDIA GPU with CUDA optional for faster inference)[cite: 104]

### 1. Database Setup
Create a PostgreSQL database[cite: 39]:
```sql
CREATE DATABASE retrospective_db;
