---
title: "Embarking on GSoC 2026: LibreHealth & My Journey"
date: 2026-05-03 23:55:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, security, open-source, devsecops]
image:
  path: /assets/img/unnamed.png
  alt: Kishan Singh Profile Picture
---

<style>
:root {
  --lx-primary: #3b82f6;
  --lx-surface: rgba(255, 255, 255, 0.03);
  --lx-border: rgba(120, 120, 120, 0.2);
  --lx-shadow: 0 10px 40px -10px rgba(0,0,0,0.1);
}

html[data-mode="light"] {
  --lx-surface: rgba(0, 0, 0, 0.02);
  --lx-border: rgba(0, 0, 0, 0.08);
}

.luxury-header {
  text-align: center;
  padding: 3rem 1rem;
  margin-bottom: 3rem;
  background: var(--lx-surface);
  border-radius: 16px;
  border: 1px solid var(--lx-border);
  box-shadow: var(--lx-shadow);
  backdrop-filter: blur(10px);
}

.luxury-header img {
  width: 140px;
  height: 140px;
  border-radius: 50%;
  object-fit: cover;
  margin-bottom: 1.5rem;
  box-shadow: 0 8px 24px rgba(0,0,0,0.15);
  border: 4px solid var(--lx-primary);
}

.luxury-header h1 {
  font-size: 2.2rem;
  margin-bottom: 0.5rem;
  font-weight: 700;
  letter-spacing: -0.5px;
}

.luxury-header p {
  color: var(--text-muted-color);
  font-size: 1.1rem;
  max-width: 600px;
  margin: 0 auto;
}

.acknowledgement {
  font-style: italic;
  font-size: 1.1rem;
  text-align: center;
  color: var(--text-muted-color);
  padding: 2rem;
  background: linear-gradient(90deg, transparent, var(--lx-surface), transparent);
  margin: 3rem 0;
  border-radius: 8px;
}

.luxury-card {
  background: var(--lx-surface);
  border-radius: 12px;
  padding: 2rem;
  margin-bottom: 2rem;
  border: 1px solid var(--lx-border);
  box-shadow: var(--lx-shadow);
  transition: transform 0.3s ease;
}

.luxury-card:hover {
  transform: translateY(-3px);
}

.plan-step {
  border-left: 4px solid var(--lx-primary);
  padding-left: 1.5rem;
  margin-bottom: 2rem;
  position: relative;
}

.plan-step::before {
  content: '';
  position: absolute;
  left: -9px;
  top: 0;
  width: 14px;
  height: 14px;
  border-radius: 50%;
  background: var(--lx-primary);
  border: 3px solid var(--main-bg);
}

.plan-step h4 {
  margin-top: -3px;
  color: var(--text-color);
  font-weight: 600;
  font-size: 1.25rem;
}

.resume-item {
  margin-bottom: 2rem;
  padding-bottom: 1.5rem;
  border-bottom: 1px dashed var(--lx-border);
}

.resume-item:last-child {
  border-bottom: none;
  padding-bottom: 0;
}

.resume-meta {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 1rem;
  flex-wrap: wrap;
  gap: 0.5rem;
}

.resume-meta h5 {
  margin: 0;
  font-size: 1.15rem;
  font-weight: 600;
}

.resume-meta .date-location {
  font-size: 0.9rem;
  color: var(--text-muted-color);
  font-weight: 500;
}

.tag-pill {
  display: inline-block;
  padding: 0.3rem 0.8rem;
  background: rgba(59, 130, 246, 0.1);
  color: var(--lx-primary);
  border-radius: 99px;
  font-size: 0.8rem;
  font-weight: 600;
  margin: 0.2rem;
  border: 1px solid rgba(59, 130, 246, 0.2);
}

.skill-category {
  margin-bottom: 1rem;
}

.skill-category strong {
  display: block;
  margin-bottom: 0.4rem;
  color: var(--text-color);
}
</style>

Welcome to my journey! This is the very first entry of my Google Summer of Code (GSoC) 2026 experience. 

<div class="acknowledgement">
  "I would like to extend my deepest gratitude to <strong>Robby O'Connor</strong> for guiding me through the entire onboarding process, helping me craft my proposal, and extending such a warm welcome. A huge thank you as well to <strong>Mua Rachmann</strong> for continuously answering my queries and providing invaluable support."
</div>

---

## 🛠️ Project Implementation Plan

For my GSoC project with LibreHealth, I am focusing on building an advanced, comprehensive security testing architecture. Below is a detailed look at the roadmap and how the 4-layer system will be constructed.

<div class="luxury-card">
  <div class="plan-step">
    <h4>1. MU Workflow Security Test Suite</h4>
    <p>I will build a complete security test suite for all seven Meaningful Use (MU) workflows, testing each end-to-end. The flow for each test will be:</p>
    <ul>
      <li>Seed the database with different types of users.</li>
      <li>Simulate requests and attempt to modify the database.</li>
      <li>Verify whether the system correctly allows or blocks the simulated requests based on authorization logic.</li>
    </ul>
  </div>

  <div class="plan-step">
    <h4>2. Static Layer (PHPStan + Enlightn + Composer Audit)</h4>
    <p>We will set up a static security analysis stage in our CI pipeline that runs on every Merge Request or push to the main branch. The code will pass through three tools:</p>
    <ul>
      <li><strong>PHPStan:</strong> Scans for type and logical issues.</li>
      <li><strong>Enlightn:</strong> Scans for framework-level security vulnerabilities.</li>
      <li><strong>Composer Audit:</strong> Scans for outdated or vulnerable dependencies.</li>
    </ul>
    <p>Each tool will generate a JSON report, which will be merged into a single structured file to notify the user.</p>
  </div>

  <div class="plan-step">
    <h4>3. Dynamic Layer (OWASP ZAP)</h4>
    <p>Dynamic security testing will be integrated using OWASP ZAP. After seeding the database with test users to provide authenticated access, OWASP ZAP will:</p>
    <ul>
      <li>Crawl the application to discover all available endpoints.</li>
      <li>Perform active scans to simulate real-world attacks (e.g., SQL Injection, Cross-Site Scripting).</li>
    </ul>
    <p>All results will be exported in a JSON report for further risk scoring.</p>
  </div>

  <div class="plan-step">
    <h4>4. CVSS Scoring & PHI Classification</h4>
    <p>A custom scoring engine will be built to calculate the risk level of each discovered vulnerability. Findings from the static and dynamic layers will be passed to a CVSS scorer, mapped to a CWE (Common Weakness Enumeration). A PHI (Protected Health Information) classification system will then adjust the score based on whether the vulnerability affects critical patient data (categorized as critical, moderate, or non-PHI).</p>
  </div>

  <div class="plan-step">
    <h4>5. Security Gate</h4>
    <p>This will act as the final gate in the CI/CD pipeline. The computed risk score will determine the fate of the Merge Request. If the CVSS score is less than 7, the request will pass; otherwise, it will be automatically blocked to ensure repository safety.</p>
  </div>

  <div class="plan-step">
    <h4>6. HTML, JSON Reports & Trend Tracking</h4>
    <p>A comprehensive reporting system will generate three types of output after every CI run:</p>
    <ul>
      <li><strong>HTML Report:</strong> A human-readable summary of the test results.</li>
      <li><strong>JSON Report:</strong> A machine-readable format for integration.</li>
      <li><strong>CSV File:</strong> Used specifically for tracking security trends across multiple builds.</li>
    </ul>
  </div>

  <div class="plan-step">
    <h4>7. Documentation</h4>
    <p>I will create a complete documentation guide for future contributors. This document will comprehensively explain how the 4-layer security system works and provide instructions on how to add new security tests to the pipeline.</p>
  </div>
</div>


---

Thank you for reading my first GSoC 2026 update! I am incredibly excited to begin executing this implementation plan and working closely with the LibreHealth community to build a robust security testing framework. Stay tuned for weekly updates as development officially kicks off.
