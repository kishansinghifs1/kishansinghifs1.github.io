---
title: "GSoC 2026 Week 6: Implementing the Security Scoring Engine"
date: 2026-07-03 21:00:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, ci-cd, security, cvss, testing]
image:
  path: /assets/img/posts/gsoc-week6-banner.svg
  alt: GSoC Week 6 - Security Scoring Engine
---

This week, I focused on implementing and finalizing **Layer 3 (Scoring Engine & PHI classification)** of our automated security pipeline.

Here is a breakdown of the design and architecture implemented this week.

---

## Architecture & Component Overview

The security scoring engine runs as a post-processing stage in our pipeline, executed via a custom Laravel Artisan command:

```
[Layer 1: SAST/DAST Tooling]
   ├── composer-audit-report.json
   ├── phpstan-report.json
   └── zap_report.json
            │
            ▼
[Layer 2: Normalization]
   └── FindingNormalizer
            │
            ▼
[Layer 3: Risk Scoring Engine]
   ├── PhiClassifier (Classify: Critical PHI / Moderate PHI / Non-PHI)
   └── CvssScorer (CVSS Base Score + PHI Adjustment)
```

The updated pipeline features a dedicated `cvss-scoring` stage that runs after static and dynamic scanning jobs are complete:

![CI/CD Pipeline with Layer 3 Scoring](/assets/img/posts/third-layer.png)

---

## MY Implementation

### 1. Data Models & Normalization

#### Standardized Finding DTO
To aggregate vulnerabilities from disparate formats, I created a unified `Finding` DTO. It holds identifiers, source markers, severity levels, target paths (file/line or URL), CWE mappings, base/adjusted scores, and scanner-specific metadata.

#### FindingNormalizer 
This class converts raw scanner outputs into our standardized `Finding` DTOs:
*   **Composer Audit**: Resolves package advisories (CWE-937) and maps abandoned packages (CWE-1104).
*   **PHPStan (Larastan)**: Maps static analysis errors, deduces files and lines, and uses basic text matching for severity heuristics.
*   **OWASP ZAP**: Parses web application alerts, mapped URI endpoints, attack parameters, and solutions.

---

### 2. Risk Assessment & Classification

#### PhiClassifier
Not all vulnerabilities carry the same weight in healthcare environments. A vulnerability exposed on a patient encounter page is infinitely more dangerous than one on a general configuration page. The `PhiClassifier` matches paths and URLs to categorize exposure risks:

*   🔴 **Critical PHI** (e.g., patient, prescription, medicalhistory, diagnosis, encounter, facesheet, billing).
*   🟡 **Moderate PHI** (e.g., user, address, facility, calendar, appointment).
*   🟢 **Non-PHI** (default fallback).

#### CvssScorer
The scorer maps raw findings to standard CWEs and calculates base CVSS scores, then applies a risk-adjusted formula based on PHI exposure:
$$\text{Adjusted Score} = \min(10.0, \text{Base Score} + \text{PHI Adjustment})$$
*   **Critical PHI Exposure**: Base score $+ 2.0$
*   **Moderate PHI Exposure**: Base score $+ 1.0$

---

## Next Week Plan

Next week, I will focus on building the pipeline orchestrator and the last layer that is **Trend Analysis**. 
This will help us to track the security posture of the project over time and identify any regressions or improvements. 
I will also focus on caching the builds and other images and making the pipeline faster.

---

## Acknowledgement

Thanks for following along on my GSoC journey. Stay tuned for more updates!
