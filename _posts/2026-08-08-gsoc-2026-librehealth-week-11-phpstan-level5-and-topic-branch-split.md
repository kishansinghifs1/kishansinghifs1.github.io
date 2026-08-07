---
title: "GSoC 2026 Week 11: PHPStan Level 5 Completed & Focused Topic Branch Split"
date: 2026-07-08 21:00:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, phpstan, larastan, ci-cd, security, refactoring]
image:
  path: /assets/img/posts/gsoc-week11-banner.svg
  alt: GSoC Week 11 - PHPStan Level 5 Complete &amp; Topic Branch Split
---

This week was all about two things: cleaning up the remaining PHPStan baseline errors up to level 5 and splitting our three large feature branches into focused, reviewable topic branches. I am happy to say that we have finally cleared all the PHPStan level 5 issues, and the baseline is now clean for level 5. 

---

## 1. PHPStan Level 5 — Baseline Clear

Last week we had 24 remaining baseline entries. This week I resolved all of them with that, the PHPStan level 5 baseline is now empty and we will move to level 6 next week.

---

## 2. Splitting the Monolithic Branches Into Focused Topic Branches

The bigger chunk of this week was restructuring our three parent branches into small topic branches.

Here is how the split looks:

### From `mr-26` (3 branches)

| # | Branch | What It Does |
|---|--- |---|
| 1 | `chore/laratrust-v8-migration` | Migrates Laratrust v7 traits and methods to v8 |
| 2 | `fix/factory-test-defaults` | Replaces random `country_id`/`city_id` values in `AddressFactory` and `PatientContactFactory` with deterministic defaults (156 / 1) to eliminate flaky foreign-key failures during seeding |
| 3 | `test/security-test-suite` | Adds `SecurityTestSeeder`, `SecurityTestCase`, `SecurityTestFoundationTest` for the MU workflows |

### From `composer-updated-end-to-end` (2 branches)

| # | Branch |  What It Does |
|---|---|---|
| 4 | `chore/composer-dependency-upgrades` | upgraded `composer.json` and `composer.lock` to Laravel 12 / Laratrust v8 compatible versions |
| 5 | `fix/route-constraints-and-patient-redirects` | Adds route pattern constraints and patient redirect endpoints |

### From `CI-CD-Pipeline-Setup` (4 branches)

| # | Branch | What It Does |
|---|---|---|
| 6 | `phpstan` | Adds `phpstan.neon.dist` (level 5) and `phpstan-baseline.neon` |
| 7 | `zap` | OWASP ZAP DAST configuration (`zap-plan.yaml`) and dedicated `ZapSeeder` for testing |
| 8 | `ci` | `.gitlab-ci.yml`, `Dockerfile.ci`, and `.env.ci` with build, static-scan, dynamic-scan, and scoring stages |
| 9 | `scoring` | Full security scoring engine: `app/Security/*`, `SecurityScoreCommand`, CVSS calculator, CWE mapper, PHI classifier, gate logic, and HTML report generator |

---

## Next Week Plan

Next week I will focus on:

1. Work on the PHPStan level 6 baseline and start reducing it.
2. Get these topic branches reviewed and merged.

---

## Acknowledgement

Thank you Mua Rachmann and Robby O'Connor for your continuous guidance and feedback.

Thanks for following my GSoC journey.
