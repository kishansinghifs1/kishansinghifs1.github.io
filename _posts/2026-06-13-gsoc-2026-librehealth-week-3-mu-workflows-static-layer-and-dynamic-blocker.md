---
title: "GSoC 2026 Week 3: MU Workflows, Static Layer Completion, and Dynamic Layer Blocker"
date: 2026-06-13 21:30:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, ci-cd, security, owasp, zap]
image:
  path: /assets/img/posts/gsoc-week3-banner.svg
  alt: GSoC Week 3 - MU workflows and CI/CD security progress
---

This week was actually good, I had my first ever meeting with my mentor Mua Rachmann, there was actually big dilemma with the decision on MU workflows, which was about deciding which routes should I consider for which MU workflow and how to map them. We conluded that for now we would be maintaining the 6 main MU workflows.
After finalizing the MU workflows, I completed the static layer of the pipeline.

## Week 3 Pipeline Progress

This week, I completed the static layer of the pipeline.

The pipeline now includes these stages:
    
1. **`build`**
2. **`static-scanning`**

### Build Stage

No changes were made in it.

### Static Scanning Stage

I completed static scanning with three jobs:

1. **`static-scanning-lint`**
- Runs PHP lint checks across app/config/routes/database/tests/bootstrap
- Excludes `vendor` and `node_modules`

2. **`static-scanning-composer-audit`**
- Runs `composer audit --locked --format=json`
- Exports `composer-audit-report.json` as an artifact
- Keeps report available for one week

3. **`static-scanning-larastan`**
- Sets up extensions required for analysis
- Uses CI environment file
- Runs PHPStan/Larastan with project configuration
- Uses controlled memory limit for stable execution

I also created the baseline so we can focus first on project completion first and then we will be back to fix the base line issues later that is my bonus milestone for the project.

## Meaningful Use Workflow Mapping

Along with CI work, you can find the below image for the finalized MU workflow mapping, which is based on the routes and their functionalities I and mua have in depth talking about it and since we already have the initial setup of the security test seeder and security test foundation interface we can inherit and make the MU workflows done and dusted.

![Meaningful Use Workflow Mapping](/assets/img/posts/gsoc-week4-mu-workflow.svg)

## Current Blocker: Dynamic Layer

Since OWASP ZAP is bit tricky to integrate it in pipeline, whatever tutorials I found were bit old and not much helpful, Since for SPA applications, the authentication is bit different and in our case we are using the sanctum for authentication, the csfr token management for the spider ajax scanning is pain in the ass, I am still trying to find a way to manage the CSRF token for the spidering and ajax scanning in ZAP, I will be seeking help from Robby O'Connor for this issue.

## Next Week Plan

Next week, I will focus on:
1. Implementing the finalized Meaningful Use workflow test suites.
2. Integrating OWASP ZAP in CI/CD dynamic layer after the guidance.

## Acknowledgement

Thank You Mua Rachmann for the wonderful meeting, guidance, and clarity on MU workflow direction.

Thank You Robby O'Connor for continuous support on CI/CD pipeline implementation.

Thanks for following my GSoC journey.
