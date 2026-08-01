---
title: "GSoC 2026 Week 10: Single Cleanup Commit & PHPStan Baseline Reduction"
date: 2026-08-01 12:00:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, phpstan, larastan, refactoring]
image:
  path: /assets/img/posts/gsoc-week10-banner.svg
  alt: GSoC Week 10 - PHPStan Baseline Cleanup & Bug Fixes
---

This week, I focused on clearing the static analysis errors in our PHPStan baseline. By now, our baseline was carrying a large amount of errors. I tried to resolve the repeated PHPStan warnings and the actual runtime bugs in our controllers.
I managed to remove out nearly 60% of our baseline errors.

---

## 1. What We Fixed in One Cleanup Commit

We fixed **30 entries** out of the total 59 baseline issues.


These findings were mostly small errors, missing return types, inaccurate docblocks, dead boolean checks, and redundant collection calls across the codebase:

| PHPStan / Larastan Error Category | Fix Summary |
|---|---|
| `property.phpDocType` | Corrected docblock type annotations to match actual properties. |
| `return.missing` | Added missing explicit return types to methods and closures. |
| `argument.unresolvableType` | Resolved unresolvable argument types in callbacks and helpers. |
| `argument.type` | Aligned passed argument types with strict function signatures. |
| `booleanAnd.alwaysFalse` + `notEqual.alwaysFalse` + `attribute.notFound` | Removed dead condition branches and invalid attribute accesses. |
| `booleanOr.rightAlwaysTrue` | Simplified redundant logical OR conditions that always evaluated to true. |
| `return.type` | Enforced exact return types matching declared method contracts. |
| `ternary.alwaysTrue` + `larastan.noUnnecessaryCollectionCall` | Replaced redundant ternary expressions and unnecessary Laravel collection calls. |

---

## 2. Real Bugs We Fixed in the Same Pass

Another **5 `property.notFound` entries** was typo or mis assignments in the controllers.

* **`CalendarController`**: Fixed `$update_at` typos → `$updated_at`.
* **`PatientController`**: Fixed `$patient->deleted_at` incorrectly assigned to `created_at` / `updated_at` array keys.


---

## 3. Remaining Baseline Entries

The remaining 24 entries in the baseline are mostly `property.notFound` warnings on Eloquent models. 

* **`Patient` / `PatientFaceSheet`**: Add `@property` annotations for `first_name`, `last_name`, `dob`, `age`, `sex`, `billing_note`, etc.
* **`User`**: Add `@property` annotations for `fname` and `lname`.
* **`Facility`**: Add `@property` annotations for `name` and `updated_at`.
* **`Generic Model access`**: Clean up dynamic access in `HandleInertiaRequests`.


---

## Next Week Plan

Next week I will focus on:

1. Finalizing the remaining 10–14 baseline entries and preparing the MR for mentor review.
2. Preparing Meet with Mua to actually merge the MR so to look up for the deployment stage in pipeline and also to discuss the final steps for the project completion.

---

## Acknowledgement

Thank you Mua Rachmann and Robby O'Connor for your continuous guidance and feedback.

Thanks for following my GSoC journey.
