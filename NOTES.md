# Patch Notes

## Summary

I reviewed the application across the controller, repository, and database interaction layers and fixed three high-value issues.

1. Fixed a SQL operator-precedence bug in `TaskRepository` by grouping the title/description search conditions. This ensures archived and status filters are applied correctly.
2. Removed an artificial `Thread.sleep()` delay from `TaskController` that unnecessarily increased API response time.
3. Added validation for `page` and `pageSize` so invalid pagination requests return `400 Bad Request` instead of causing server errors.

## What I Did Not Change

I did not make unrelated refactors, dependency upgrades, frontend redesigns, or changes to lower-priority logging/code-quality issues. The goal was to keep the patch focused on correctness, performance, and API robustness.

## Biggest Remaining Risk

The application still loads all matching tasks from the database before performing pagination in Java. With a much larger dataset, this could increase memory usage and response time. A production implementation should move pagination into the database using SQL/JPA pagination.

## Tools / AI Used

I used VS Code, PowerShell, Git/GitHub, and the application's existing Maven/Node tooling. I also used AI assistance to understand the code, identify potential issues, reason about their impact, and validate fixes. I manually reviewed, tested, and understood each change before applying it.