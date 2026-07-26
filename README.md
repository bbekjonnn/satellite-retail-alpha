# 🛰️ Satellite Imagery Retail Traffic Proxy

[![Python](https://img.shields.io/badge/Python-3.10-blue.svg)](https://www.python.org/)
[![Colab](https://img.shields.io/badge/Open%20in-Colab-F9AB00?logo=googlecolab)](https://colab.research.google.com)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)
[![Status](https://img.shields.io/badge/Status-Research%20POC-orange.svg)]()

> **Predict quarterly revenue surprises for major retailers by counting vehicles in satellite parking lot imagery.**

An end-to-end alternative data pipeline that combines **computer vision**, **geospatial data acquisition**, and **supervised machine learning** to generate an alpha signal ahead of earnings announcements.

---

## 📌 Table of Contents

- [Overview](#overview)
- [Pipeline Architecture](#pipeline-architecture)
- [Key Results](#key-results)
- [Project Structure](#project-structure)
- [Quick Start](#quick-start)
- [Methodology Deep Dive](#methodology-deep-dive)
- [Production Roadmap](#production-roadmap)
- [Tech Stack](#tech-stack)
- [License](#license)

---

## Overview

**Thesis:** Parking lot traffic is a leading indicator of foot traffic → foot traffic drives same-store sales → sales drive revenue surprises → revenue surprises move stock prices.

This project demonstrates a fully reproducible research pipeline that:
1. Acquires high-resolution satellite imagery of retail parking lots
2. Detects and counts vehicles using classical computer vision
3. Fetches quarterly financial data and computes revenue surprise metrics
4. Engineers predictive features (lags, momentum, seasonality, cross-sectional ranks)
5. Trains gradient-boosted models with time-series cross-validation
6. Backtests a long/short trading strategy based on predicted surprises

> **Note:** The notebook includes a `DEMO_MODE` that synthesizes realistic satellite imagery so the full pipeline runs immediately without API credentials. To use real data, configure Sentinel Hub or Earth Engine credentials.

---

## Pipeline Architecture
┌──────────────────┐     ┌──────────────────┐     ┌──────────────────┐
│  Satellite Data  │────▶│  Computer Vision │────▶│ Feature Engineer │
│ (Sentinel-2 /    │     │ (OpenCV Contours │     │ (Lags, Momentum, │
│  PlanetScope)    │     │  + NMS)          │     │  Seasonality)    │
└──────────────────┘     └──────────────────┘     └──────────────────┘
│
┌──────────────────┐     ┌──────────────────┐            │
│  Strategy Signal │◀────│  Gradient Boost  │◀───────────┘
│  (Long / Short)  │     │  + Time-Series CV│
└──────────────────┘     └──────────────────┘
│
▼
┌──────────────────┐
│  Backtest & Eval │
│  (RMSE, Dir Acc) │
└──────────────────┘
