---
title: "GSoC 2026 Week 5: Unified CVSS Scoring Engine and Pipeline Integration"
date: 2026-06-27 12:00:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, ci-cd, security, cvss, testing]
image:
  path: /assets/img/posts/gsoc-week5-banner.svg
  alt: GSoC Week 5 - CVSS Scoring Engine and PHI Tier
---

This week was relatively light on coding. I worked on a small implementation of the CVSS Scoring Engine and spent most of my time researching and planning how to integrate it smoothly into our CI/CD pipeline.

## 1. CVSS Scoring Engine

I figured out that, mapping the vulnerabilities to CWEs is utmost neccessary, so I'll proceed with creating the simple DTO and then perform a normalisation. And then I'll proceed to map it with the CWEs. As we have already find the MU workflows so after mapping the vulnerabilities to CWEs I'll apply the CVSS scoring engine on them, and I'll decide the threshold based on the MU workflows (i.e., how critical the vulnerabilities are based on their impact on the workflows). This is the architecture I build through the week and plan to implement it in upcoming week.

## 2. Security Scoring Console Command 

The best way I found out to automate the result aggregation, vulnerability scoring, PHI classification and the threshold gating is to use the artisan command so I'll be using that. 
After the command would be executed I would generate the findings and scored findings in a json file which would be the artifacts of the job. 
For the security metrics and trends, I'll be storing that in a json file (basically I'm using the JSON file as our database for now). 
I still need to confirm the html reporting structure with my mentor and some of the above architecture but this all I have planned for now.

## Next Week Plan

Next week, I will continue building on this integration and make sure all CI jobs run stably and efficiently.

## Acknowledgement

Thanks for following my GSoC journey.
