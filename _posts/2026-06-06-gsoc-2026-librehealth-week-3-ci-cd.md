---
title: "GSoC 2026 Week 3: CI/CD Pipeline Configuration"
date: 2026-06-06 09:02:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, ci-cd, gitlab]
image:
  path: /assets/img/posts/gsoc-week3-banner.svg
  alt: GSoC Week 3 - CI/CD Pipeline Configuration
---

This week, I wasn't able to code much due to my re-exam but still I laid the foundation for the CI/CD pipeline. The whole setup for the pipeline is done for now, since the project was already on the gitlab so it was easy for the initial setup.

Since we are not sure about the additional runners, we are running the pipeline on gitlab shared runners with docker executor. In future, if we find a need of additional runners we will be adding it later.

## Pipeline Overview

The current pipeline has only two stages:
1. **`build`**
2. **`static-scanning`**

### Stage 1: Build

The `build_job` job is there for setting up the environment by pulling up all PHP dependencies via Composer.

### Stage 2: Static Scanning

This stage includes the `static-scanning-lint` job, it is there to have the same lint and formats accross the whole codebase. It performs a PHP syntax check and file formatting accross the entire application ensuring no unformatted code is merged into the repository. 

## Next Week

After the current CI/CD pipeline foundation is reviewed and approved by Robby O'Connor, the next week I will do all is to make the static layer completed with addition of phpstan ,larastan and composer audit.

## Acknowledgement

Thank You Robby O'Connor for helping me out for the initial setup of pipeline.

Thanks for following my GSoC journey.
