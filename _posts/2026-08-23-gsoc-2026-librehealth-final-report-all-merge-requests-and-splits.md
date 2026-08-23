---
title: "GSoC 2026 Final Report: Final Work Done"
date: 2026-08-23 20:00:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, security, ci-cd, phpstan, final-report]
image:
  path: /assets/img/posts/gsoc-final-report-banner.svg
  alt: GSoC 2026 Final Report - Final Work Done
---

This is the final blog of my Google Summer of Code 2026 journey with LibreHealth. We are finally wrapping up. Over the last twelve weeks I worked on upgrading the LibreHealth EHR Laravel stack, building a security testing foundation, setting up the CI/CD security pipeline, writing Meaningful Use workflow tests, fixing vulnerabilities, and cleaning up the PHPStan baseline.

Since the work got split into a lot of small topic branches, I wanted this final post to act as a single place to reference all the final merge requests (MRs) and their GitLab links. I also wanted to summarize the work done in each MR so you can get a quick overview of the project.

<div class="acknowledgement">
  "I would like to thanks <strong>Robby O'Connor</strong> and <strong>Mua Rachmann</strong> for guiding me through the entire project, Special thanks to <strong>Robby O'Connor</strong> for his quick replies on the Rocket Chat channel and <strong>Mua Rachmann</strong> for his behaviour and guidance during the every meeting.I would also like to thank <strong>LibreHealth</strong> for giving me this opportunity to work on this project and <strong>Google Summer of Code</strong> for providing me this platform to learn and grow." 
</div>

---

## Project Links

- GSoC project page: [https://summerofcode.withgoogle.com/programs/2026/projects/B0KA82Dk](https://summerofcode.withgoogle.com/programs/2026/projects/B0KA82Dk)
- LibreHealth EHR Laravel repo: [https://gitlab.com/librehealth/ehr/lh-ehr-laravel](https://gitlab.com/librehealth/ehr/lh-ehr-laravel)
- Previous weekly blogs: [Week 0](/posts/gsoc-2026-librehealth-proposal-and-journey), [Week 1](/posts/gsoc-2026-librehealth-laravel-12-upgrade-security-testing-foundation), [Week 2](/posts/gsoc-2026-librehealth-week-2-ci-cd), [Week 3](/posts/gsoc-2026-librehealth-week-3-mu-workflows-static-layer-and-dynamic-blocker), [Week 4](/posts/gsoc-2026-librehealth-week-4-test-suite-and-dynamic-layer), [Week 5](/posts/gsoc-2026-librehealth-week-5-cvss-scoring-engine-and-phi-tier), [Week 6](/posts/gsoc-2026-librehealth-week-6-security-scoring-assessment-engine), [Week 7](/posts/gsoc-2026-librehealth-week-7-dependency-upgrades-and-security-pipeline-orchestrator), [Week 8](/posts/gsoc-2026-librehealth-week-8-critical-vulnerabilities-fix-and-contribution-guidelines), [Week 9](/posts/gsoc-2026-librehealth-week-9-mua-meeting-mu-workflow-tests), [Week 10](/posts/gsoc-2026-librehealth-week-10-phpstan-baseline-cleanup), [Week 11](/posts/gsoc-2026-librehealth-week-11-phpstan-level5-and-topic-branch-split), [Week 12](/posts/gsoc-2026-librehealth-week-12-phpstan-level-6-30-percent)

---

## Quick Reference: All Final Merge Requests

Here is the clean list of MRs that represent the final work of this project. Each one has a direct GitLab link so you can check the diff or leave a review.

| MR | Title | GitLab Link |
|---|---|---|
| !30 | left over migration of Laratrust v7 → v8 traits and seeder methods | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/30) |
| !31 | Set deterministic foreign-key defaults in Address and PatientContact factories. | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/31) |
| !32 | add role-based security test foundation with safe payloads for MU Tests | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/32) |
| !33 | Composer dependency upgraded | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/33) |
| !34 | Implemented route pattern constraints and some patient redirect endpoints. | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/34) |
| !35 | Integrated PHPStan static analysis for the CI/CD Pipeline | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/35) |
| !36 | Intro to an OWASP ZAP for DAST. | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/36) |
| !37 | Added GitLab CI/CD pipeline with build, static scan, dynamic scan and scoring gate. | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/37) |
| !38 | Implemented security scoring engine with CVSS, CWE mapping, and HTML reporting | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/38) |
| !39 | Meaningful Workflows Test Cases Covered | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/39) |
| !42 | Security findings from the CI/CD pipeline first run fixed. | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/42) |
| !43 | Fixed the phpstan level 5 issues. | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/43) |
| !44 | Fixed the phpstan level 6 issues. | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/44) |
| !45 | Fixed the phpstan level 7 issues. | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/45) |
| !46 | docs: add CI/CD pipeline and MR guide | [Link](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/46) |

---

## Foundational Work

### MR !25 — Laravel 12 Upgrade

[MR !25](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/25) was the first MR of the project. It upgraded the project from Laravel 10 to Laravel 12 and aligned everything with PHP 8.3. I had to remove some deprecated packages and add explicit return types where PHP 8.3 was stricter. This was the base on which every other MR was built. I wrote more about this in the [Week 1 blog](/posts/gsoc-2026-librehealth-laravel-12-upgrade-security-testing-foundation).

---

## Part 1 of the Split

The original big branch that had Laravel 12 leftovers, security test foundation, dependency upgrades, and factory fixes was split into four focused branches so each piece could be reviewed on its own.

### MR !33 — Composer Dependency Upgrades

[MR !33](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/33) carries the `chore/composer-dependency-upgrades` branch. It updates `composer.json` and `composer.lock` to versions that work with Laravel 12 and Laratrust v8, and it resolves a bunch of CVEs reported by `composer audit`.

### MR !32 — Security Test Foundation

[MR !32](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/32) carries the `test/security-test-suite` branch. It adds `SecurityTestSeeder`, the abstract `SecurityTestCase`, and `SecurityTestFoundationTest`. These create realistic users like clinicians, receptionists, admins, and patients so the MU workflow security tests have proper data to run against.

### MR !31 — Factory Foreign-Key Defaults

[MR !31](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/31) carries the `fix/factory-test-defaults` branch. The `AddressFactory` and `PatientContactFactory` were using random `country_id` and `city_id` values, which made the tests flaky. I replaced them with deterministic defaults (`156` / `1`) so seeding stops failing randomly.

### MR !30 — Laratrust v7 → v8 Migration

[MR !30](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/30) carries the `chore/laratrust-v8-migration` branch. It migrates the remaining Laratrust v7 traits, seeder methods, and helper calls to their Laratrust v8 equivalents. This is the example link format you asked for, and every other MR in this post follows the same pattern.

---

## Part 2 of the Split — Route Constraints and Patient Redirects

### MR !34 — Application Stability Fixes

[MR !34](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/34) combines five related production fixes that were blocking the OWASP ZAP dynamic scan:

1. **Broken patient menu links** — Some controller methods were missing and causing 500 errors.
2. **Wrong patient lookup** — `PatientHistoryController` was using `id` instead of `pid`, so I fixed the lookup and added a proper 404 for missing patients.
3. **Debug code in production** — Removed stray `dd()` calls that were breaking AJAX responses.
4. **Broken session redirect** — Fixed the invalid `guest.index` route after session expiration.
5. **Unsafe route parameters** — Added regex constraints (`^[0-9]+$`) to user, facility, and patient ID routes to stop path traversal and parameter tampering.

---

## Part 3 of the Split — CI/CD Security Pipeline

The original `CI-CD-Pipeline-Setup` branch was huge, so we split it into four focused topic branches. There is also [MR !29](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/29) which holds the full automated security scanning engine and pipeline in one place, but the same contents are broken down into the four MRs below for easier review.

### MR !35 — PHPStan Static Analysis

[MR !35](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/35) adds `phpstan.neon.dist` at level 5, the initial `phpstan-baseline.neon`, and the `static-scanning-larastan` CI job. This is the static analysis layer of the pipeline.

### MR !36 — OWASP ZAP for DAST

[MR !36](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/36) introduces OWASP ZAP for dynamic scanning. It includes the `zap-plan.yaml`, a `ZapSeeder` for test data, and the `dynamic-scanning-zap` CI job that runs against a built application image.

### MR !37 — GitLab CI/CD Pipeline Orchestration

[MR !37](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/37) adds the main `.gitlab-ci.yml`, the `Dockerfile.ci`, `.env.ci`, and the pipeline stages: `build`, `static-scan`, `dynamic-scan`, and `scoring`. It also makes the pipeline run only on merge requests.

### MR !38 — Security Scoring Engine

[MR !38](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/38) is the full scoring engine under `app/Security/`. It has the `Finding` DTO, `FindingNormalizer`, `CweMapper`, `PhiClassifier`, `CvssScorer`, `SecurityGate`, `SecurityScoreCommand`, and the HTML report generator. It normalizes findings from Composer Audit, PHPStan, and ZAP, maps them to CWEs, calculates CVSS v3.1 base scores, applies PHI-tier adjustments, and fails the pipeline when the score crosses the threshold.

---

## Part 4 of the Split — MU Workflow Tests

### MR !39 — Meaningful Use Workflow Tests

[MR !39](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/39) adds the complete Meaningful Use workflow security tests on top of the foundation from MR !32. It covers role-based access validation for the six main MU workflows Mua and I agreed on. I wrote more about this in the [Week 9 blog](/posts/gsoc-2026-librehealth-week-9-mua-meeting-mu-workflow-tests).

---

## Part 5 of the Split — First-Run Security Findings

### MR !42 — Security Findings Fixed

[MR !42](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/42) fixes the vulnerabilities that showed up the first time the complete pipeline ran:

- Moved PHPStan `env()` calls in `SecurityScoreCommand` to `config/ci.php`.
- Removed the abandoned `jamesdordoy/laravelvuedatatable` package.
- Added `SecurityHeaders` middleware for CSP, `X-Frame-Options`, `X-Content-Type-Options`, and stripped `X-Powered-By`.
- Added `HttpOnly` to `XSRF-TOKEN` and `ehr_patient` cookies.
- Added middleware to clear response bodies for 3xx redirects.
- Upgraded vulnerable JS libraries (`axios`, `lodash`, Vue 2 patch).

I covered the details in the [Week 8 blog](/posts/gsoc-2026-librehealth-week-8-critical-vulnerabilities-fix-and-contribution-guidelines).

---

## Part 6 of the Split — PHPStan Level-by-Level Cleanup

After setting up the baseline in MR !35, I split the cleanup into three levels so it would not be one giant MR.

### MR !43 — PHPStan Level 5

[MR !43](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/43) resolves all PHPStan level 5 baseline entries. It includes docblock corrections, missing return types, dead boolean branches, and a couple of real bugs like typos in `CalendarController` and wrong date assignments in `PatientController`.

### MR !44 — PHPStan Level 6

[MR !44](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/44) targets PHPStan level 6, mostly missing generic type annotations on Eloquent relationships (`HasMany`, `BelongsTo`, `HasOne`, `MorphMany`, `HasFactory`) and missing iterable value types in models and controllers.

### MR !45 — PHPStan Level 7

[MR !45](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/45) resolves PHPStan level 7 issues, like casting `env('APP_NAME')` before `Str::slug()`, resolving the currency manager properly, adding PHPDoc to the `Currency` model, using `JSON_THROW_ON_ERROR` in `EHRInstaller`, and safe `preg_match` offset access in `RequirementsChecker`.

---

## Part 7 — Documentation

### MR !46 — CI/CD Pipeline and MR Guide

[MR !46](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/46) adds the contributor documentation. It covers the CI/CD layout, contribution model, GitLab pipeline stages, MU workflow security tests, code quality gates, local development setup, troubleshooting for blocked MRs, and best practices.

---

## Final Thoughts

This project touched almost every part of the LibreHealth EHR Laravel application the framework upgrade, dependency hygiene, role-based security testing, static and dynamic analysis, risk scoring, vulnerability fixes, and contributor docs. Splitting everything into focused topic branches to make the review process easy.

The coolest outcome for me is that the project now has a working automated security pipeline that can be extended later. New vulnerabilities can be caught by Composer Audit, PHPStan/Larastan, and OWASP ZAP; normalized and scored by the security engine; and blocked at the MR gate when they cross the risk threshold.

Thanks for following my GSoC 2026 journey.

