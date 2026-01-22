---
layout: post
title: "Daily Plan - 2026-01-21"
date: 2026-01-21
---

# Daily Plan - Wednesday, January 21, 2026

## Today's Theme
I've got three hot feature sets all touched within the last couple days, and they're all sitting at that same priority level (score 22). Rather than context-switch between all of them, I'm going to focus on **decision-kernel-ui2** and **email-sms-transports** today. Both have strong momentum (11 and 6 commits this week respectively), and the tasks are foundational pieces that will unlock more work. I want to knock out some concrete building blocks while the architecture is fresh in my head.

## The Main Work

**dk-p0-routes: Create API routes file for Decision Kernel**
I touched the decision-kernel-ui2 feature set 2 days ago, and with 11 commits this week, it's clear this is a strategic focus for me right now. This routes file is the p0 task, which tells me it's foundational - everything else in this feature set will need these routes defined. Getting this done first makes sense because it establishes the API contract that the TypeScript types will mirror.

**dk-p1-types-enums: Create TypeScript enum types**
Following directly from the routes work, I need to define the TypeScript enums while the API structure is fresh in my head. The decision-kernel-ui2 feature set has momentum behind it, and these two tasks together will give me a solid foundation for the UI integration work. I like keeping the backend routes and frontend types in sync from the start rather than backfilling later.

**p1-email-transport-skeleton: Create EmailTransportService class skeleton**
The email-sms-transports feature set also got touched 2 days ago (6 commits this week), so I've got recent context here too. This skeleton is one of four related tasks in this feature set, and starting with the email transport makes sense because it's probably the more familiar pattern. Once I have this structure working, the SMS transport will follow the same pattern.

**p1-sms-transport-skeleton: Create SmsTransportService class skeleton**
If the email transport skeleton goes smoothly, I'll tackle the SMS version immediately after. These two skeletons together represent the core architecture for the feature set, and getting both done today would be solid progress. They're parallel structures, so the context transfer between them should be minimal.

## Housekeeping

**Review task-management planning directory**
This one's been sitting in "Needs Research" and contains strategic planning documents for task management and workflow optimization. Since I'm actively working across multiple feature sets today, it might be worth spending 30 minutes here to see if there are any workflow improvements I should be applying. Meta, but potentially valuable.

**Check in on internationalization test coverage**
I've got 38 commits in the internationalization feature set this week - that's massive momentum. The two remaining tasks are both unit tests for locale resolution. I'm not prioritizing them today because I want to focus on the foundational architecture work, but I should at least review where they stand. They might be quick additions tomorrow if I've got spare cycles.

## Parked

The **internationalization** feature set has huge momentum (38 commits this week), but those remaining test tasks feel like cleanup rather than foundational work. I'd rather push forward on the decision kernel and transport architecture while I've got energy for building new structures. The i18n tests can wait a day or two without losing much context.

I'm also not touching **p1-sms-driver-interface** or **p1-provider-update** from the email-sms-transports set today. The driver interface and provider updates are important, but they depend on having the transport skeletons in place first. If I get both skeletons done, I might peek at the driver interface, but I'm not committing to it in the main plan.

---

## Update - 06:03 PM

Wrapped up the waitlist signup feature today - the whole end-to-end flow is now in place. Started with the database foundation (migration for verification columns), then built out the backend pieces systematically: the actions for submitting and verifying signups, both API and web controllers, the necessary tasks for token generation and email sending, plus the notification system. The frontend integration came together nicely too, adding the form directly to the GatewayWelcome component with proper styling and a clean success view for verified users. It's one of those satisfying builds where each piece clicks into place.

Also made solid progress on two other fronts. Continued the internationalization work, adding dashboard widget translations - got the Orders and Email Campaign widgets properly localized. The RTL testing went well too; direction switching works smoothly without page reloads and persists across navigation as expected. On the SDK front, I dove deeper into the capability-driven architecture concept, analyzing how the MCP SDK flows work and documenting the approach in ADR-0115. Created prototype specs for identity.session_whoami and compliance.policy_get to test the pattern. The BaseApiClient analysis revealed some useful integration patterns that'll inform the final design.

## The Numbers
- Additional tasks: 34
- Feature areas: waitlist-signup, internationalization, scaffold-fe-sdk
<!-- Generated by dev-tracker publish_to_jekyll.py (AI mode) -->
<!-- accomplished-date: 2026-01-21 -->
<!-- unit-ids: waitlist-migration-verification-columns,waitlist-action-verify,waitlist-api-controller,waitlist-api-routes,waitlist-model-relocate-enhance,waitlist-action-submit,waitlist-frontend-form,waitlist-service-provider,waitlist-task-create-signup,waitlist-task-generate-token,waitlist-notification,waitlist-task-send-email,waitlist-web-controller,waitlist-web-routes,i18n-p4-dashboards-json,waitlist-task-find-by-token,waitlist-form-request,waitlist-frontend-styles,waitlist-verified-view,i18n-p4-widget-orders,i18n-p4-widget-email-campaign,scaffold-fe-sdk-002,scaffold-fe-sdk-021,scaffold-fe-sdk-022,scaffold-fe-sdk-024,scaffold-fe-sdk-027,scaffold-fe-sdk-001,scaffold-fe-sdk-035,waitlist-cleanup-stubs,i18n-p3-icon-rtl-test,i18n-p3-dir-switch-test,i18n-p3-dir-persist-test,scaffold-fe-sdk-042,scaffold-fe-sdk-036 -->

<!-- unit-ids: i18n-p3-dir-persist-test,i18n-p3-dir-switch-test,i18n-p3-icon-rtl-test,i18n-p4-dashboards-json,i18n-p4-widget-email-campaign,i18n-p4-widget-orders,scaffold-fe-sdk-001,scaffold-fe-sdk-002,scaffold-fe-sdk-021,scaffold-fe-sdk-022,scaffold-fe-sdk-024,scaffold-fe-sdk-027,scaffold-fe-sdk-035,scaffold-fe-sdk-036,scaffold-fe-sdk-042,waitlist-action-submit,waitlist-action-verify,waitlist-api-controller,waitlist-api-routes,waitlist-cleanup-stubs,waitlist-form-request,waitlist-frontend-form,waitlist-frontend-styles,waitlist-migration-verification-columns,waitlist-model-relocate-enhance,waitlist-notification,waitlist-service-provider,waitlist-task-create-signup,waitlist-task-find-by-token,waitlist-task-generate-token,waitlist-task-send-email,waitlist-verified-view,waitlist-web-controller,waitlist-web-routes -->