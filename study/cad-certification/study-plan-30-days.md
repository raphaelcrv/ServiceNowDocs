# 30-Day CAD Study Plan

**Goal:** Pass the ServiceNow Certified Application Developer (CAD) exam on **Day 30 (Thu 2026-11-12)**.
**Starting point:** about 69% overall ([score report](score-report.md)). Weakest domains: Automation 55%, Security 58%.
**Target:** at least 80% in every domain on practice tests by Day 26.

## How the plan is built

1. **Weakest, heaviest domains first.** Automation and Security are each 20% of the exam, and you scored below 60% in both. They get Weeks 1–2, while your energy is highest.
2. **Learn by building.** Every day has a hands-on lab on your Personal Developer Instance (PDI). You build one scoped app, **"Equipment Request" (`x_<you>_equip`)**, over the 30 days. Each lab adds a feature that matches that day's topic.
3. **Test, then review the gaps.** Take a timed practice test at the end of each week. Log the scores in the [score history](score-report.md#score-history). Spend the next review day on whatever you missed.
4. **Daily budget:** about 1.5–2 h on weekdays (30 min reading + 60–90 min lab), about 3 h on weekend days.

### Resources

- **This repo's docs.** The links below point to files in [`markdown/`](../../markdown) for the Brazil release.
- **ServiceNow Developer Program** (developer.servicenow.com). Get a free PDI here ([how to access your PDI](../../markdown/application-development/accessing_your_pdi.md)). Also work through the learning paths *Developer Essentials*, *Application Development Fundamentals*, *Scripting in ServiceNow Fundamentals* and *Flow Designer*.
- **ServiceNow University / Now Learning.** Contains the official *CAD exam blueprint* and the *Scripting in ServiceNow Fundamentals* course.
- **Practice tests.** Use a reputable CAD question bank. Always read the explanation, even for questions you answered correctly.

### Daily routine (weekdays)

| Block | Time | What |
|---|---|---|
| Read | 30 min | The linked docs for the day. Write 3–5 flashcards. |
| Build | 60–90 min | The day's PDI lab. |
| Recall | 10 min | Review yesterday's flashcards, then answer 10 practice questions on the topic. |

---

## Week 1 (Days 1–7): Security and Restricting Access (58% → 85%)

| Day | Date | Topic | Read | PDI lab |
|---|---|---|---|---|
| 1 | Wed 10-14 | ACL fundamentals: what an ACL is, the 3 checks (roles → condition → script), `answer`, default deny | [Exploring ACLs](../../markdown/platform-security/access-control/exploring-access-control-list.md), [Access control rules](../../markdown/platform-security/access-control/access-control-rules.md) | Create the scoped app "Equipment Request" with table `equipment_request`. Create roles `x_..._equip.user` and `x_..._equip.manager`. |
| 2 | Thu 10-15 | ACL types, operations and evaluation order: table `table.None` vs. `table.*` vs. `table.field`, most-specific match first | [ACL rule types](../../markdown/platform-security/access-control/acl-rule-types.md), [Create an ACL](../../markdown/platform-security/access-control/t_CreateAnACLRule.md), [Contextual security](../../markdown/platform-security/access-control/r_ContextualSecurity.md) | Write ACLs: users read/create their own requests; managers update all; only managers can edit the `approval` field. |
| 3 | Fri 10-16 | Debugging ACLs, `security_admin` elevation, impersonation | [Debug ACLs](../../markdown/platform-security/access-control/c_AccessControlRulesDebug.md), [ACL troubleshooting](../../markdown/platform-security/access-control/r_ACLTroubleshoot.md), [Show ACL execution plan](../../markdown/platform-security/access-control/t_ShowACLExecutionPlan.md) | Impersonate a test user and a test manager. Turn on *Debug Security Rules* and explain every green and red line you see. |
| 4 | Sat 10-17 | Application access settings: runtime vs. design-time access, "Accessible from", web services access | [Application access settings](../../markdown/application-development/c_ApplicationAccessSettings.md), [Runtime access](../../markdown/application-development/c_RuntimeAccessToAppTables.md), [Design-time access](../../markdown/application-development/c_DesignTimeAccessToAppTables.md) | Change the table's *Accessible from* to "This application scope only". From a global background script, try to read it and explain the result. |
| 5 | Sun 10-18 | Cross-scope privileges, restricted caller access, script protection policy, protecting files | [Cross-scope privilege record](../../markdown/application-development/c_CrossScopePrivilegeRecord.md), [Script protection policy](../../markdown/application-development/c_ScriptProtectionPolicy.md), [Protecting app files](../../markdown/application-development/c_ProtectingApplicationFiles.md), [Global scope](../../markdown/application-development/c_GlobalScope.md) | Write a script include that calls `GlideRecord('incident')` from your scope. Find the cross-scope privilege that gets created and test it with the status set to *Requested* and then *Denied*. |
| 6 | Mon 10-19 | Data policies vs. UI policies vs. ACLs: which one enforces what, client vs. server | [Data policy](../../markdown/platform-administration/c_DataPolicy.md), [Control field values with BRs + client scripts](../../markdown/build-workflows/business-rules-classic/r_BsnsRlClntScptsCntrlFldVl.md) | Make `justification` mandatory three ways: with a UI policy, a data policy and a business rule. Then test each one through the REST API Explorer. |
| 7 | Tue 10-20 | **Review and practice test #1** | Re-read your flashcards | Take a timed full practice test (60 Q / 90 min). Log the score and review every wrong answer. |

## Week 2 (Days 8–14): Application Automation (55% → 85%)

| Day | Date | Topic | Read | PDI lab |
|---|---|---|---|---|
| 8 | Wed 10-21 | Business rules: before / after / async / display, `current` / `previous`, `setAbortAction`, avoiding `current.update()` | [Business rules](../../markdown/build-workflows/business-rules-classic/c_BusinessRules.md), [BRs in scoped apps](../../markdown/build-workflows/business-rules-classic/c_BusinessRulesInScopedApps.md), [Examples](../../markdown/build-workflows/business-rules-classic/business-rule-examples.md) | Before BR: set `number`/`requested_for`. After BR: create a task. Async BR: write a log entry. Explain why each BR needs that timing. |
| 9 | Thu 10-22 | Display BRs and `g_scratchpad`; client scripts (onLoad / onChange / onSubmit / onCellEdit), `g_form`, `g_user` | [Display BRs](../../markdown/build-workflows/business-rules-classic/c_ScriptingWithDisplayBusinessRules.md), [BR + script include overview](../../markdown/application-development/business-rules-and-script-includes.md) | Pass the manager's name to the form through `g_scratchpad`. Add an onChange client script that shows a message when `cost > 1000`. |
| 10 | Fri 10-23 | Script includes: classless vs. `Class.create()`, *Client callable*, GlideAjax (async `getXMLAnswer`) | [BR + script includes](../../markdown/application-development/business-rules-and-script-includes.md), [Apply ACLs to AJAX GlideRecord](../../markdown/platform-security/access-control/r_ApplyACLsToAJAXGlideRecord.md) | Build a client-callable script include `EquipUtils.getStock(sysId)` and call it from an onChange client script with GlideAjax. |
| 11 | Sat 10-24 | Flow Designer: triggers (record / schedule / application), actions, data pills, flow logic, subflows | [Flow Designer](../../markdown/application-development/flow-designer.md), [Flow triggers](../../markdown/build-workflows/workflow-studio/flow-triggers.md), [Subflows](../../markdown/build-workflows/workflow-studio/subflows.md), [Actions](../../markdown/build-workflows/workflow-studio/actions.md) | Build a flow: when a request is created and cost > 1000, ask for manager approval. If approved, set the state; if rejected, notify the requester. |
| 12 | Sun 10-25 | Flow testing and debugging, error handling, run-as (user vs. system), custom actions with inputs and outputs | [Flow debugger](../../markdown/build-workflows/workflow-studio/flow-debugger.md), [Error handler](../../markdown/build-workflows/workflow-studio/flow-error-handler.md), [Action inputs/outputs](../../markdown/build-workflows/workflow-studio/action-inputs-outputs.md) | Turn the approval logic into a subflow and create a custom action with a script step. Test it and read the execution details. |
| 13 | Mon 10-26 | Events (register, `gs.eventQueue`, `parm1`/`parm2`), script actions, notifications, scheduled script executions | [Event registry](../../markdown/platform-administration/system-events/c_EventRegistry.md), [Register an event](../../markdown/platform-administration/system-events/t_RegisterAnEvent.md), [Script actions](../../markdown/platform-administration/system-events/r_ScriptActions.md), [Notifications](../../markdown/application-development/notifications.md), [Create a notification](../../markdown/platform-administration/create-email-notification.md) | Register `x_..._equip.request.overdue`. Write a scheduled job that fires it every day and a notification that it triggers. Check the result in the Event Log and the Outbox. |
| 14 | Tue 10-27 | **Review and practice test #2** | Flashcards: BR timing table, GlideAjax pattern, flow vs. BR vs. workflow | Timed full practice test. Log it. If Security or Automation is still below 75%, redo the weakest lab. |

## Week 3 (Days 15–21): Designing and Creating Apps (67%) + Managing Apps (67%)

| Day | Date | Topic | Read | PDI lab |
|---|---|---|---|---|
| 15 | Wed 10-28 | Application scope, namespace, global vs. scoped, the parts of an app, application files | [Application scope](../../markdown/application-development/c_ApplicationScope.md), [Parts of an application](../../markdown/application-development/c_PartsOfAnApplication.md), [Application files](../../markdown/application-development/c_ApplicationFiles.md) | List every application file in your app in Studio. Switch scopes with the application picker and see what changes. |
| 16 | Thu 10-29 | Tables: extending (`task`) vs. a new table, `sys_` fields, auto-number, dictionary entries and overrides, reference fields, dot-walking | [Table extension and classes](../../markdown/platform-administration/table-administration-and-data-management/table-extension-and-classes.md), [Dictionary entry form](../../markdown/platform-administration/table-administration-and-data-management/r_DictionaryEntryForm.md), [App data tables](../../markdown/application-development/c_ApplicationDataTables.md), [Dot-walking](../../markdown/platform-user-interface/dot-walking-examples.md) | Make `equipment_request` extend `task`, add a reference to a new `equipment_item` table, and add a dictionary override for `state`. |
| 17 | Fri 10-30 | Modules, application menus, lists and forms in scoped apps, UI actions | [Lists and forms in scoped apps](../../markdown/application-development/c_CreatingListsAndFormsScopedApps.md), [UI actions](../../markdown/platform-administration/c_UIActions.md), [Form design](../../markdown/platform-administration/c_FormDesign.md) | Add an application menu with modules: *My Requests* (filtered), *All Requests* (managers only) and *Items*. Add a UI action called *Cancel request*. |
| 18 | Sat 10-31 | Update sets: capture, preview, commit, merge, back out; what does **not** get captured (data, homepage, schedules…) | [Update sets reference](../../markdown/application-development/system-update-sets/update-sets-reference.md), [Update sets in Studio](../../markdown/application-development/servicenow-studio-classic/working-with-update-sets-in-servicenow-studio.md) | Capture a change in an update set, export it to XML, then import, preview and commit it on the same PDI after deleting the change. |
| 19 | Sun 11-01 | Source control (link to Git, commit, branch, stash, apply remote changes), application repository, versioning, dependencies, sharing | [Source control in Studio](../../markdown/application-development/servicenow-studio-classic/source-control-operations-in-sn-studio.md), [App repo in Studio](../../markdown/application-development/servicenow-studio-classic/working-with-the-app-repo-in-servicenow-studio.md), [Versioning](../../markdown/application-development/c_ApplicationVersioning.md), [Dependencies](../../markdown/application-development/c_ApplicationDependencies.md), [Sharing apps](../../markdown/application-development/c_SharingApplications.md) | Link the app to a private GitHub repo. Commit, create a branch, make a change and switch branches. |
| 20 | Mon 11-02 | ATF (tests, steps, suites, the client test runner), delegated development | [ATF](../../markdown/application-development/automated-test-framework-atf/automated-test-framework.md), [Delegated development](../../markdown/application-development/delegated-development-and-deployment/exploring-delegated-development.md) | Write an ATF test: impersonate a user, open a new request form, set values, submit, and assert the record and ACL behavior. Run it as part of a suite. |
| 21 | Tue 11-03 | **Review and practice test #3** | Flashcards: update set vs. source control vs. app repo, when to use each | Timed full practice test. Log it. |

## Week 4 (Days 22–30): External Data (75%), UI refresh (93%), final prep

| Day | Date | Topic | Read | PDI lab |
|---|---|---|---|---|
| 22 | Wed 11-04 | Import sets, staging tables, transform maps, field maps, coalesce (single, multiple, none) | [Import set key concepts](../../markdown/integrate-applications/system-import-sets/c_ImportSetsKeyConcepts.md), [Create transform maps](../../markdown/integrate-applications/system-import-sets/c_CreatingNewTransformMaps.md), [Coalesce](../../markdown/integrate-applications/system-import-sets/c_ImportSetCoalesce.md) | Import a CSV of 20 equipment items. Coalesce on `serial_number` and re-import with changes to prove that rows update instead of being inserted again. |
| 23 | Thu 11-05 | Transform scripts (`onStart`, `onBefore`, `onAfter`, `onComplete`, `source`, `target`, `ignore`, `error`), data sources, scheduled imports | [Transformation script variables](../../markdown/integrate-applications/system-import-sets/r_TransformationScriptVariables.md), [Explicit transform map scripts](../../markdown/integrate-applications/system-import-sets/c_MapExplicitTransformMapScripts.md), [REST data source](../../markdown/integrate-applications/system-import-sets/create-rest-type-data-source.md) | Add an `onBefore` script that skips rows with an empty serial number. Schedule the import to run every day. |
| 24 | Fri 11-06 | Outbound REST (REST Message, `sn_ws.RESTMessageV2`), inbound REST (Table API, Scripted REST API), REST API Explorer, authentication | [Create an outbound REST message](../../markdown/platform-security/authentication/create-an-outbound-rest-message.md), [Scripted REST (SDK)](../../markdown/application-development/servicenow-sdk/scripted-rest-api-api-now-ts.md) | Call a public API (for example a currency rate) from a script include. Expose `GET /api/x_.../equip/stock/{item}` as a Scripted REST API and test it in the REST API Explorer. |
| 25 | Sat 11-07 | UI domain refresh (keep your 93%): UI policies vs. client scripts, UI policy actions, reverse if false, order; form/list config | [UI policy (catalog example)](../../markdown/servicenow-platform/service-catalog/t_CreatUIPolicyForSvcCalgIt.md), [Form design](../../markdown/platform-administration/c_FormDesign.md) | Quick review only, no new build. Answer 30 UI questions and note any misses. |
| 26 | Sun 11-08 | **Full practice test #4 (timed)** | | Review every miss and rank domains. Write a one-page "cheat sheet" from memory. |
| 27 | Mon 11-09 | Targeted remediation on the 2 weakest domains from test #4 | Re-read the linked docs for those topics | Redo the matching labs from scratch, without notes. |
| 28 | Tue 11-10 | **Full practice test #5 (timed)** | | Book the exam if every domain is at least 80% (or confirm the booking). Review misses. |
| 29 | Wed 11-11 | Light review only: cheat sheet, flashcards, BR timing, ACL order, coalesce, update set limits | | No new material. Sleep early. |
| 30 | Thu 11-12 | 🎯 **Exam day** | | Read each question twice and flag uncertain ones. Watch for "BEST"/"NOT" wording. Use all 90 minutes. |

---

## High-yield facts to memorize

**Security**
- The ACL check order is **roles → condition → script**. All three must pass. If no ACL matches, access is denied (when the default deny property is on).
- Table checks go `table.None` first; then field checks run `table.field` → `parent.field` → `table.*` → `parent.*` → `*.field` → `*.*`. The most specific match wins.
- Both a **table-level and a field-level** ACL must grant access for a field to be read or written.
- **UI policies and client scripts are not security.** Use ACLs or data policies to enforce rules on the server side.
- Application access settings control access from *other scopes* (runtime) and editing by *other apps* (design-time).

**Automation**
- **Before** BR: change `current` (do not call `update()`). **After** BR: change *other* records. **Async** BR: slow work that the user should not wait on. **Display** BR: fill `g_scratchpad`.
- Client-to-server: use **GlideAjax** with a *client-callable* script include. Avoid synchronous `getXMLWait` and client-side `GlideRecord`.
- Flows run as **System User** by default. Subflows can be reused, and actions are the building blocks.
- Event flow: register the event → `gs.eventQueue('name', current, parm1, parm2)` → a notification or script action responds.

**Design and Manage**
- Scoped names use the form `x_<vendor>_<app>_<table>`. You cannot change an application's scope after you create it.
- Extending `task` gives you number, state, assignment, approvals and SLA support.
- Update sets capture *configuration*, not *data*. Use source control or the app repo for whole scoped apps.
- Use ATF to regression-test forms, server scripts and flows before upgrades.

**External data**
- Import flow: data source → import set (staging) table → transform map → target table.
- **Coalesce** fields decide update vs. insert. If no field is coalesced, every row is inserted.
- In transform scripts, `ignore = true` skips the row and `error = true` marks it as an error.

## Progress checklist

- [ ] Week 1: Security (practice test #1 score: ___)
- [ ] Week 2: Automation (practice test #2 score: ___)
- [ ] Week 3: Design + Manage (practice test #3 score: ___)
- [ ] Week 4: External data + final prep (tests #4 / #5: ___ / ___)
- [ ] Exam booked for 2026-11-12
- [ ] 🎓 CAD certified
