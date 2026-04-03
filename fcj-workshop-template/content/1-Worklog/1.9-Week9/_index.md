---
title: "Week 9 Worklog"
date: 2024-01-01
weight: 9
chapter: false
pre: " <b> 1.9. </b> "
---

### Week 9 Objectives:

- Continue testing with a deeper regression cycle on fixed and newly integrated features.
- Focus on edge cases, permission boundaries, and invalid input scenarios.
- Reduce reopen defects by applying root-cause-oriented fixes.

### Tasks to be carried out this week:

| Day | Task                                                                                                 | Start Date | Completion Date | Reference Material                                                         |
| --- | ---------------------------------------------------------------------------------------------------- | ---------- | --------------- | -------------------------------------------------------------------------- |
| 2   | - Execute full regression suite across admin, manager, and line leader workflows                     | 03/02/2026 | 03/02/2026      | <https://www.browserstack.com/guide/regression-testing>                    |
| 3   | - Perform negative and permission-boundary tests (expired token, invalid payload, unauthorized role) | 03/03/2026 | 03/03/2026      | <https://owasp.org/www-project-web-security-testing-guide/>                |
| 4   | - Fix medium/high-priority defects and refactor unstable logic causing recurring failures            | 03/04/2026 | 03/04/2026      | <https://refactoring.guru/refactoring>                                     |
| 5   | - Verify fixes in staging and run smoke tests after each deployment update                           | 03/05/2026 | 03/05/2026      | <https://learn.microsoft.com/en-us/azure/devops/pipelines/test/smoke-test> |
| 6   | - Summarize quality metrics and define Week 10 hardening focus items                                 | 03/06/2026 | 03/06/2026      | <https://cloudjourney.awsstudygroup.com/>                                  |

### Week 9 Achievements:

- Increased regression coverage and significantly reduced reopened defects.
- Fixed authorization and session-handling bugs in role-based flows.
- Improved consistency between backend error responses and frontend handling.
- Stabilized major user journeys in staging after repeated smoke and regression runs.
- Delivered a known-issues list with preventive actions for the next sprint.
