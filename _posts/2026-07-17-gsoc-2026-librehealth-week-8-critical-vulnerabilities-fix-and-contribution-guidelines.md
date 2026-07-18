---
title: "GSoC 2026 Week 8: Fixed Critical Vulnerabilities , Updated Contribution Guidelines and Wrote Tests for MU Workflows"
date: 2026-07-17 21:00:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, ci-cd, security, owasp, zap, csp, dependencies]
image:
  path: /assets/img/posts/gsoc-week8-banner.svg
  alt: GSoC Week 8 - Critical Vulnerability Fixes &amp; Contribution Guidelines
---

Since we completed the all the three laeyers of the pipeline last week, this week I mostly focus on fixing the critical vulnerability that I came across during the CI/CD run. Another thing I picked up is updating the contribution guidelines with the addition of the how to read the security reports and how to fix the vulnerabilities. And last I also wrote some tests for the MU workflows that were pending since long.

---

## Findings from the CI/CD 

The CI/CD report flagged the below vulnerabilities:  

*   **PHPStan `env()` calls** in `SecurityScoreCommand` — four high-severity config-in-code findings.
*   **Abandoned composer package** `jamesdordoy/laravelvuedatatable`.
*   **Missing security headers** — CSP, `X-Frame-Options`, `X-Content-Type-Options`, and a leaking `X-Powered-By` header.
*   **XSRF-TOKEN cookie without `HttpOnly`**.
*   **Big redirect responses** carrying page content.
*   **Vulnerable JS libraries** in `public/js/vendor.js`: axios `0.21.4`, lodash `4.17.21`, and Vue `2.7.14`.

---

## Implementation Breakdown

### 1. PHPStan `env()` Findings

I created `config/ci.php` to hold CI environment variables with `env()` fallbacks, then replaced the four `env()` calls in `SecurityScoreCommand::updateHistory()` with `config('ci.*')`. 

### 2. Removed Abandoned Datatable Package

`jamesdordoy/laravelvuedatatable` is abandoned, so I:

*   Removed it from `composer.json`.
*   Removed `LaravelVueDatatableTrait` from `User` and `Patient`.
*   Replaced `DataTableCollectionResource` with a custom resource that returns the same JSON shape the frontend `laravel-vue-datatable` component expects.
*   Updated `PatientController::getPatientData()` to use the custom query builder.

### 3. Security Headers Middleware

I added `app/Http/Middleware/SecurityHeaders.php` and registered it in `app/Http/Kernel.php`. The middleware sets:

| Header | Value |
|---|---|
| `X-Content-Type-Options` | `nosniff` |
| `X-Frame-Options` | `DENY` |
| `Content-Security-Policy` | `default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data:; font-src 'self' data:; connect-src 'self'; frame-ancestors 'self'; base-uri 'self'; form-action 'self'; object-src 'none'` |
| `X-Powered-By` | stripped from responses |

### 4. HttpOnly Cookie Fix

The `XSRF-TOKEN` cookie was missing the `HttpOnly` flag. I overrode `VerifyCsrfToken::addCookieToResponse()` to create the cookie with `httpOnly = true`, and updated `resources/app/app.js` to read the CSRF token from the existing `<meta name="csrf-token">` so axios/Inertia keep working. I also made the `ehr_patient` cookie `HttpOnly` with `SameSite=Lax`.

### 5. Big Redirect Responses

Some redirects were carrying full response bodies. I reproduced the reported redirects with `curl`, then added a small middleware that clears the response body for `3xx` responses so no PHI or page content leaks through a redirect body.

### 6. Vulnerable JS Libraries

The runtime bundle contained known-vulnerable versions of axios, lodash, and Vue. I updated `package.json` and `package-lock.json`:

*   Upgraded direct **axios** to a safe version (`>= 0.32.0`).
*   Used `overrides` to force the same safe axios version for transitive dependencies such as `@inertiajs/inertia`.
*   Upgraded **lodash** to the latest safe `4.x` patch.
*   Upgraded **vue** and **vue-template-compiler** to the latest Vue 2 patch (`2.7.16`).

After `npm ci && npm run prod`, I re-ran `retire.js` on `public/js/vendor.js` until no high or critical runtime findings remained.

---

## Updating the Contribution Guidelines

I added a new `Security Vulnerability Tracking & Resolution` section to the project contribution guidelines:

*   Where findings I explained the respective layer with their artifacts that is `composer-audit-report.json`, `phpstan-report.json`, `zap_report.json`, `findings.json`, `scored_findings.json`, and `security-report.html`.
*   I explained how the `PhiClassifier` and `CvssScorer` turn raw findings into risk-adjusted scores.
*   The triage workflow : how to confirm the vulnerabilites, scope to runtime vs. build-time, open a focused branch, fix, add tests, and re-run `composer audit`, `phpstan`, `npm audit`, and `retire.js` before merging.

---

## Tests for MU Workflows

I basically wrote the test for the PaitentRegistrationSecurity workflow and ClinicalDataExchangeSecurity workflow.

---
## Next Week Plan

Next week I will focus on:

1. Completeling the MU Workflow test suites.
2. Working on the broken logic of the application.

---

## Acknowledgement

Thank you Mua Rachmann and Robby O'Connor for the guidance.

Thanks for following my GSoC journey.