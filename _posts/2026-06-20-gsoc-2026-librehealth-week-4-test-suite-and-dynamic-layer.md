---
title: "GSoC 2026 Week 4: Test Suite Modularization and Dynamic Layer with ZAP"
date: 2026-06-20 01:31:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, ci-cd, security, owasp, zap]
image:
  path: /assets/img/posts/gsoc-week4-banner.svg
  alt: GSoC Week 4 - Dynamic Layer
---

This week I worked mostly with the integeration of dynamic layer in CI/CD pipeline using OWASP ZAP. So tried multiple stuff and got hit by multiple errors.

Initially, I thought of making a docker image and then executing it in docker, but when the pipeline was running docker-in-docker, it was creating a havoc situation. Everything was getting ruined up, and the execution time was escalating. So after researching, I found out that I can do It by adding the build-assest job in build stage, in which I'll build an asset and then on those base assets my dynamic layer will pull it up and run the OWASP ZAP. After running that layer, we'll be extracting the artifacts and based on our artifacts, we can see the results.

For the OWASP ZAP working plan I tried to follow the basic industry standards. And I tried to start with something small, I just gave only those URLs which are meaninful workflow URLs and useful URLs in a list, so that ZAP will only perform crawling on those URLs.

![Dynamic Layer Setup](/assets/img/posts/dynamic-layer.png)

### Problems faced during integration of the OWASP ZAP in CI/CD pipeline.

When I integerated the OWASP ZAP in the CI/CD pipeline, initially I was not able to generate the completely trustable vulnerability report, since our codebase has the unimplemented routes which are supposed to be active. So, while the ZAP was running over it the pipeline was getting failed on those routes. And hence we were stuck with the 500 Internal Server Error. So, the solution that I derived in the way is write the functions over the PatientController.php that is redirecting the traffic to the main patient profile page and the there was some changes I did in the PatientHistoryController.php ( basically I corrected the lookup logic to query by the `pid` column, safely handled missing patients with a standard `404` error page, and fixed the relation lookup using standard Laravel Eloquent dynamic properties.).

And when I was running the ZAP locally I had to guard some routes that were expecting the /:id parameter and there is no validation for it, and there fore I added the regrex protection pattern ^[0-9]+$ to the routes so that no one can attempt the path traversal,injection patterns and parameter tampering attacks through the URL.

![ZAP Artifact Results](/assets/img/posts/zap-artificat.png)

## Next Week Plan

Next week I would be focusing on Layer 3 of the pipeline that is CVSS scoring engine and PHI tier.

## Acknowledgement

Thanks for following my GSoC journey.
