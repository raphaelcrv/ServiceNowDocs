# CAD Study Plan: 1 Hour per Weekday

**Goal:** Pass the CAD exam on **Thu 2026-11-12**.
**Budget:** 1 hour per weekday, no weekends. That gives **21 sessions (about 21 h)** from Wed 2026-10-14 to Wed 2026-11-11.
**Starting point:** about 69% overall ([score report](score-report.md)). Weakest domains: Automation 55%, Security 58%.

This is a condensed version of the [30-day study plan](study-plan-30-days.md), which needed about 60 h. Use that plan's links when you want more reading on a topic.

## What changed from the 30-day plan

- **Time goes where the points are.** Security and Automation (20% each, both below 60%) get 10 of the 21 sessions. UI (93%) gets only a short refresh.
- **One app, smaller labs.** You still build the "Equipment Request" scoped app on your PDI, but each lab is about 35 minutes and covers only the core of the topic.
- **Half practice tests.** A full test (60 Q / 90 min) doesn't fit in an hour, so each test day is 30 questions in 45 minutes plus 15 minutes of review.
- **Go/no-go checkpoint on Fri 11-06.** If you're not on track, move the exam then (see [Checkpoint](#go-no-go-checkpoint)).

## Every session (60 min)

| Block | Time | What |
|---|---|---|
| Recall | 5 min | Review yesterday's flashcards. |
| Read | 20 min | The docs linked for the day. Write 3 flashcards. |
| Build | 35 min | The day's PDI lab. |

## Week 1: Security, part 1

| # | Date | Topic | Read | PDI lab (35 min) |
|---|---|---|---|---|
| 1 | Wed 10-14 | ACL basics: roles → condition → script, `answer`, default deny, `table.None` vs. `table.*` vs. `table.field` | [Access control rules](../../markdown/platform-security/access-control/access-control-rules.md), [ACL rule types](../../markdown/platform-security/access-control/acl-rule-types.md) | Create the scoped app "Equipment Request", the table `equipment_request`, and the roles `user` and `manager`. |
| 2 | Thu 10-15 | Writing and debugging ACLs, impersonation, `security_admin` elevation | [Create an ACL](../../markdown/platform-security/access-control/t_CreateAnACLRule.md), [Debug ACLs](../../markdown/platform-security/access-control/c_AccessControlRulesDebug.md) | Users read their own requests; only managers can edit `approval`. Impersonate both roles with *Debug Security Rules* on. |
| 3 | Fri 10-16 | Application access settings (runtime vs. design time), cross-scope privileges | [Application access settings](../../markdown/application-development/c_ApplicationAccessSettings.md), [Cross-scope privilege record](../../markdown/application-development/c_CrossScopePrivilegeRecord.md) | Set *Accessible from* to "This application scope only" and try to read the table from a global background script. |

## Week 2: Security, part 2 + Automation, part 1

| # | Date | Topic | Read | PDI lab (35 min) |
|---|---|---|---|---|
| 4 | Mon 10-19 | Data policy vs. UI policy vs. ACL; restricted caller access, script protection policy | [Data policy](../../markdown/platform-administration/c_DataPolicy.md), [Script protection policy](../../markdown/application-development/c_ScriptProtectionPolicy.md) | Make `justification` mandatory with a UI policy, then with a data policy. Test both through the REST API Explorer. |
| 5 | Tue 10-20 | Business rules: before / after / async / display, `current` / `previous`, `setAbortAction` | [Business rules](../../markdown/build-workflows/business-rules-classic/c_BusinessRules.md), [Examples](../../markdown/build-workflows/business-rules-classic/business-rule-examples.md) | Before BR sets `requested_for`. After BR creates a task. Say out loud why each needs that timing. |
| 6 | Wed 10-21 | Display BRs, `g_scratchpad`, client scripts (onLoad / onChange / onSubmit), `g_form` | [Display BRs](../../markdown/build-workflows/business-rules-classic/c_ScriptingWithDisplayBusinessRules.md) | Pass the manager's name to the form with `g_scratchpad`. Add an onChange script that warns when `cost > 1000`. |
| 7 | Thu 10-22 | Script includes (classless vs. `Class.create()`), *Client callable*, GlideAjax | [BR + script includes](../../markdown/application-development/business-rules-and-script-includes.md) | Build `EquipUtils.getStock()` and call it from a client script with GlideAjax (`getXMLAnswer`). |
| 8 | Fri 10-23 | **Half practice test #1** | | 30 Q / 45 min, then 15 min reviewing every miss. Log the score. |

## Week 3: Automation, part 2 + Design

| # | Date | Topic | Read | PDI lab (35 min) |
|---|---|---|---|---|
| 9 | Mon 10-26 | Flow Designer: triggers, actions, data pills, flow logic, approvals | [Flow Designer](../../markdown/application-development/flow-designer.md), [Flow triggers](../../markdown/build-workflows/workflow-studio/flow-triggers.md) | Flow: when a request with cost > 1000 is created, ask the manager to approve, then set the state. |
| 10 | Tue 10-27 | Subflows, custom actions, error handling, run-as, flow debugger | [Subflows](../../markdown/build-workflows/workflow-studio/subflows.md), [Error handler](../../markdown/build-workflows/workflow-studio/flow-error-handler.md) | Move the approval into a subflow. Run it and read the execution details. |
| 11 | Wed 10-28 | Events (`gs.eventQueue`, `parm1`/`parm2`), script actions, notifications, scheduled jobs | [Event registry](../../markdown/platform-administration/system-events/c_EventRegistry.md), [Script actions](../../markdown/platform-administration/system-events/r_ScriptActions.md) | Register an "overdue" event, fire it from a scheduled job, and send a notification. Check the Event Log. |
| 12 | Thu 10-29 | App scope and namespace, app files, extending `task`, dictionary overrides, reference fields, dot-walking | [Application scope](../../markdown/application-development/c_ApplicationScope.md), [Table extension](../../markdown/platform-administration/table-administration-and-data-management/table-extension-and-classes.md) | Make `equipment_request` extend `task`, add a reference to a new `equipment_item` table, and add a dictionary override. |
| 13 | Fri 10-30 | **Half practice test #2** | | 30 Q / 45 min + review. Log the score. |

## Week 4: Design, Managing apps, External data

| # | Date | Topic | Read | PDI lab (35 min) |
|---|---|---|---|---|
| 14 | Mon 11-02 | Modules, application menus, UI actions; quick UI policy refresh | [Lists and forms in scoped apps](../../markdown/application-development/c_CreatingListsAndFormsScopedApps.md), [UI actions](../../markdown/platform-administration/c_UIActions.md) | Add *My Requests* and *All Requests* (managers only) modules and a *Cancel request* UI action. |
| 15 | Tue 11-03 | Update sets: capture, preview, commit, merge; what is **not** captured | [Update sets reference](../../markdown/application-development/system-update-sets/update-sets-reference.md) | Capture a change, export it to XML, delete the change, then import, preview and commit it. |
| 16 | Wed 11-04 | Source control, app repository, versioning, ATF basics | [Source control in Studio](../../markdown/application-development/servicenow-studio-classic/source-control-operations-in-sn-studio.md), [ATF](../../markdown/application-development/automated-test-framework-atf/automated-test-framework.md) | Write one ATF test that opens a new request form, submits it and checks the record. (Git linking: read only.) |
| 17 | Thu 11-05 | Import sets, transform maps, coalesce, transform scripts (`ignore`, `error`, `source`, `target`) | [Import set key concepts](../../markdown/integrate-applications/system-import-sets/c_ImportSetsKeyConcepts.md), [Coalesce](../../markdown/integrate-applications/system-import-sets/c_ImportSetCoalesce.md) | Import a 10-row CSV coalescing on `serial_number`, then re-import with changes to prove rows update. |
| 18 | Fri 11-06 | REST: REST Message / `RESTMessageV2`, Table API, Scripted REST API, REST API Explorer | [Outbound REST message](../../markdown/platform-security/authentication/create-an-outbound-rest-message.md) | Read one record of your table with the REST API Explorer. **Then do the [go/no-go checkpoint](#go-no-go-checkpoint).** |

## Week 5: Final prep

| # | Date | Topic | What to do |
|---|---|---|---|
| 19 | Mon 11-09 | **Half practice test #3** | 30 Q / 45 min + review. Rank the domains from weakest to strongest. |
| 20 | Tue 11-10 | Fix the 2 weakest domains | Re-read their docs and redo one lab from memory. Go through the [recalled exam questions](exam-questions-recalled.md). |
| 21 | Wed 11-11 | Light review only | [High-yield facts](study-plan-30-days.md#high-yield-facts-to-memorize), flashcards, recalled questions. No new material. Sleep early. |
| 🎯 | Thu 11-12 | **Exam** | Read each question twice. Watch for "BEST" and "NOT". Use all 90 minutes. |

## Go/no-go checkpoint

On **Fri 11-06**, look at practice tests #1 and #2:

- **Go:** Security and Automation are both at least 75% → keep the 11-12 date.
- **No-go:** either one is below 75% → move the exam about 2 weeks (around 11-26) and repeat Weeks 2–3 at the same pace. Check your exam provider's reschedule deadline before you decide.

If you can find one extra hour on a weekend, use it for a full timed practice test (60 Q / 90 min). It's the best way to practice your pacing.

## Progress checklist

- [ ] Week 1: Security part 1
- [ ] Week 2: Security part 2 + Automation part 1 (test #1: ___)
- [ ] Week 3: Automation part 2 + Design (test #2: ___)
- [ ] Week 4: Design, Managing, External data. Go/no-go: ___
- [ ] Week 5: Final prep (test #3: ___)
- [ ] 🎓 CAD certified
