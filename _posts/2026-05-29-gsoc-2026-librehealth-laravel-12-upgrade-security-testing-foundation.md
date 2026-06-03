---
title: "GSoC 2026 Week 1: Laravel 12 Upgrade and Security Testing Foundation"
date: 2026-05-29 23:24:00 +0530
categories: [GSoC 2026, LibreHealth]
tags: [gsoc, librehealth, laravel, php, security, testing]
image:
  path: /assets/img/posts/gsoc-laravel12-security-banner.svg
  alt: GSoC Week 1 - Laravel 12 upgrade and security testing foundation update
---

This week, I focused on two important areas of the LibreHealth EHR Laravel project. First is upgrading the application to a modern Laravel and PHP stack, and second is building the foundation for MU security testing.

I raised two merge requests this week.

- [MR !25: Laravel 12 upgrade](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/25) - merged
- [MR !26: Security testing foundation](https://gitlab.com/librehealth/ehr/lh-ehr-laravel/-/merge_requests/26) - pending review

## Laravel 12 Upgrade

Before starting the actual project the first essential thing that was needed to be done was migrating from Laravel 9 to Laravel 12 and aligning it together with PHP 8.3.

The best part was I upgraded it to Laravel 12 with almost no changes in the main code. I actually went deep removed the deprecated packages and I ran the artisan commands to check for any cascading effects on the codebase. If I encountered any issues I resolved it by debugging majorly into it. 

Some packages were deprecated and I removed it's traces and dependencies and since PHP 8.3 is stricter about method signatures. Some framework-related methods needed explicit return types, so we added `: void` wherever required.

And I finally tested the application's all the main workflows by running the every artisan command needed to run the server with prod flag.


### Building Security Testing Foundation

The second major task I did this week was to build the foundation for security testing. Since it was difficult to use the actual seeded database because seeded database was not design for the security testing hence, I wrote the complete seeder for security test. The above MR is in the same context it was create for laying the foundation that will make the MU security testing easier later.

The security testing architecture was built on three main components:

![Security Testing Architecture](/assets/img/posts/security-test-foundation.png)


## SecurityTestSeeder

`SecurityTestSeeder` creates the fake data in the db for role-based security testing.

It prepares users such as clinicians, receptionists, admins, and patients with realistic permissions. This will help us in future tests check whether each type of user can access only the routes that they are allowed to use.

## SecurityTestCase

`SecurityTestCase` this is the abstract class which have all implementation of the security testing. It will be later inherited by the MU workflow security testing.

It handles the common setup work, such as preparing the test database, running the security seeder, logging in test users, managing encrypted Laravel cookies, and creating helper test functions that is required by the MU workflow security testing.


## SecurityTestFoundation

`SecurityTestFoundation` is there for the context of SecurityTestCase to work properly.

It checks that the database is configured correctly, and seeded users can log in, and basic role-based access works at a basic level. 

We have not completed the MU workflow test cases, yet we layed the foundation for them.

## Next Week

Next week, I will continue by working on the MU workflow tests after clarifications from the Mua Rachmann and Robby O'Connor on top of the above foundation I built.

We will also start working on CVSS vectors so that the security findings can be described and prioritized in a more structured way and it would eventually help us for the main goal of our CI/CD pipeline ready.

## Acknowledgement

Thank You Mua Rachmann and Robby O'Connor for your guidance, support.

Thanks for following my GSoC journey.
