---
title: "GSoC 2026 Week 12: PHPStan Level 6 Progress and Error Cleanup"
date: 2026-08-14 12:00:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, phpstan, larastan]
image:
  path: /assets/img/posts/gsoc-week12-banner.svg
  alt: GSoC Week 12 - PHPStan Level 6 Progress and Error Cleanup
---

This week, I moved on to PHPStan Level 6 and started reducing the remaining issues in the baseline. I have completed 30 percent of the Level 6 PHPStan issues so far, and the next step is to keep clearing the rest in a structured way.

---

## 1. Level 6 Error Summary

While working on PHPStan Level 6, I came across a total of 78 issues. Most of the issues were related to missing type information and Laravel Eloquent relationships.

1. 35 issues - Missing generic types: Added proper type information to Eloquent relationships such as `HasMany`, `BelongsTo`, `HasOne`, `MorphMany`, and `HasFactory`.
2. 28 issues - Missing iterable value types: Added types for arrays so PHPStan knows what kind of values they contain.
3. 5 issues - Missing parameter types: Added proper type hints to method parameters where they were missing.
4. 3 issues - Missing return types: Added return type declarations to a few methods.
5. 4 issues - Unresolvable return types: Fixed cases where PHPStan could not determine the return type of `Collection::transform()` callbacks.
6. 2 issues - Unreachable code: Removed code that could never be executed after `dd()` / `exit()` in `PatientAppointmentController`.
7. 1 issue - Template type: Fixed a type-related issue with the `morphMany()` relationship in the `User` model.

---

## 2. What I Resolved So Far

The main work this week was to start cleaning up the highest-volume issues first, especially the generic type annotations on Eloquent relationships and the missing iterable value types.

These are the areas that matter most right now:

* `missingType.generics` on model relationships and factory traits.
* `missingType.iterableValue` on arrays used in models, helpers, and controller methods.
* `method.unresolvableReturnType` where callback type information needs to be made explicit.
* `missingType.parameter` and `missingType.return` in smaller methods that still need proper signatures.

---

## 3. Next Week Plan

Next week I will continue to work on the remaining PHPStan Level 6 issues.

---

## Acknowledgement

Thank you Mua Rachmann and Robby O'Connor for your continuous guidance and feedback.

Thanks for following my GSoC journey.