# MEDNOVA · Personal Health Intelligence

## Problem Statement

To develop **MEDNOVA**, an AI-powered, interactive healthcare application that creates a digital health profile of an individual by integrating biological information, medical reports, AI-assisted health insights, wearable-device tracking, and epidemic simulation.

---

## Project Description & Motivation

Modern healthcare systems generate enormous amounts of biological and medical data, yet individuals often lack the tools to understand, connect, and interpret this information meaningfully. As a result:
- Medical reports remain cryptic and difficult to comprehend without clinical training.
- Early health risks and warning signs frequently go unnoticed.
- Natural biological rhythms and circadian variations are poorly understood.
- Disease transmission dynamics during outbreaks are hard for individuals and communities to visualize.

**MEDNOVA** brings together artificial intelligence, biotechnology, medical data analytics, and wearable telemetry into a unified platform. By integrating human biology education, AI-assisted report analysis, circadian rhythm monitoring, and transparent epidemic simulation, MEDNOVA encourages a critical shift from **reactive treatment towards informed and preventive healthcare**.

---

## Core Pillars & System Architecture

MEDNOVA is engineered as a responsive single-page web platform structured across six integrated modules:

### 1. Health Overview & Wellness Index
- **Contextual Health Synthesis**: Adapts greeting and daily context dynamically based on live temporal data.
- **Composite Wellness Index**: Dynamic circular donut visualization scoring overall recovery, sleep, and physical baseline.
- **Autonomic Recovery Tracking**: 7-day sparkline visualizing recovery trends (+12% baseline improvement).
- **AI Health Lens**: Connects personal context flags (such as allergies or seasonal rhinitis) to high-leverage preventive actions for the day.

### 2. Digital Health Profile
- **Comprehensive Digital Biomarker Profile**: Captures critical clinical context including age, pronouns, blood type, known allergies (e.g., Penicillin), and active context/chronic condition flags.
- **Context Synchronization**: Automatically updates global AI reasoning throughout the interface as profile variables change.
- **Persistent Storage**: Retains digital profile state locally across browser sessions using `localStorage`.
- **Profile Readiness Metric**: Real-time progress bar reflecting health profile completeness.

### 3. AI-Assisted Medical Report Analysis
- **Multimodal Report Ingestion**: Drag-and-drop file uploader supporting lab diagnostics in PDF, JPG, and PNG formats.
- **Biomarker Signal Map**: Converts unstructured lab metrics into a clear signal table with clinical reference intervals (e.g., Vitamin D 25-OH, hs-CRP, LDL Cholesterol, HbA1c).
- **Clinician Conversation Builder**: Translates ambiguous numerical findings into actionable, structured questions to empower patients during doctor consultations.

### 4. Biological Clock & Circadian Rhythm Monitoring
- **Circadian Wave Modeling**: Visualizes diurnal fluctuation curves for **Cortisol** (morning awakening response) and **Melatonin** (overnight restorative wave).
- **Interactive 24-Hour Scrubber**: Real-time slider allowing users to scrub across the day to understand hormonal transitions.
- **Time-Bound Actionable Cues**: Practical guidance for morning light exposure, peak cognitive/metabolic focus hours, evening wind-down, and cellular repair windows.

### 5. Epidemic Simulation (SIR Dynamics)
- **Transparent Mathematical Modeling**: Implements a client-side Susceptible–Infected–Recovered (SIR) epidemiological model to educate users on transmission dynamics.
- **Interactive Multi-Variable Controls**: Adjust Basic Reproduction Number ($R_0$), Community Immunity percentage, and Contact Density to observe changes in transmission trajectory.
- **Projection Analytics**: Visualizes 30-day epidemic curves while calculating and pinpointing peak infection percentage and peak day.

### 6. Wearable Device Integration & Telemetry
- **Continuous Vital Signs Stream**: Simulated live stream for smart rings and health wearables.
- **Key Health Telemetry**: Live tracking of Heart Rate Variability (HRV balance in ms), Resting Heart Rate (RHR in bpm), Sleep Quality Score, and Overnight Blood Oxygen ($\text{SpO}_2$).
- **Sleep Architecture Breakdown**: Categorizes nocturnal sleep stages into REM, Deep, and Light restorative phases.
- **Simulated Device Sync**: Interactive trigger to simulate real-time sensor updates, syncing data directly into the holistic Wellness Index.

---

## Tech Stack & Implementation Details

- **Frontend Core**: Vanilla HTML5, CSS3 (CSS Variables, Flexbox, Grid), JavaScript (ES6+).
- **Visualization Library**: [Chart.js](https://www.chartjs.org/) for hardware-accelerated canvas charts (doughnuts, trend lines, multi-dataset curves, and customized scrubber markers).
- **Local Storage API**: Offline-ready data persistence without external database overhead.
- **Vector Assets**: Inlined SVG symbol sprite system for low payload size and crisp rendering.
- **Accessibility**: Built with semantic structure, explicit ARIA roles/labels, live status toasts, and `prefers-reduced-motion` fallbacks.

---


## Team & Competition Info

- **Team Name**: Team Prison
- **Project**: MEDNOVA (AI-Powered Personal Health Intelligence Platform)
- **Event**: Vibeathon Hackathon
