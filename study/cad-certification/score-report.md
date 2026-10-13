# CAD Exam: Score Report

**Certification:** ServiceNow Certified Application Developer (CAD)
**Recorded:** 2026-10-13
**Result:** Did not pass. Target retake date: **2026-11-12** (see [1-hour weekday plan](study-plan-1h-weekdays.md))

## Score by domain

| Test domain | Percent correct | Blueprint weight* | Weighted points | Status |
|---|---:|---:|---:|---|
| Designing and Creating an Application | 67% | 20% | 13.4 | 🟠 Needs work |
| Application User Interface | 93% | 20% | 18.6 | 🟢 Strong |
| Security and Restricting Access | 58% | 20% | 11.6 | 🔴 Weak, top priority |
| Application Automation | 55% | 20% | 11.0 | 🔴 Weak, top priority |
| Working with External Data | 75% | 10% | 7.5 | 🟡 OK, needs reinforcement |
| Managing Applications | 67% | 10% | 6.7 | 🟠 Needs work |
| **Estimated overall** | | **100%** | **≈ 68.8%** | |

\* The weights come from the most recently published CAD exam blueprint. ServiceNow updates the blueprint from time to time, so check the current one on [ServiceNow University](https://learning.servicenow.com) before the exam. The exam is about 60 questions in 90 minutes and is scored on a scaled basis. A safe target is **≥ 80% in every domain** on practice tests.

## Analysis

- **What went well:** Application User Interface (93%). Forms, lists, UI policies, client-side behavior and UI actions are already solid. This domain only needs light upkeep.
- **Where the most points are lost:** *Application Automation* (55%) and *Security and Restricting Access* (58%). Each carries 20% of the exam. Raising both to 85% adds about **11 points** to the overall score. That alone would likely be enough to pass.
- **Next lever:** *Designing and Creating an Application* (67%, 20% weight). This covers application scope, tables, the dictionary and Studio. Raising it to 85% adds about **3.6 points**.
- **Lower-weight gaps:** *Managing Applications* (67%) and *Working with External Data* (75%) carry 10% each. These topics are compact and quick to close: update sets, source control, the application repository, ATF, import sets and transform maps.

### Gap → topic map

| Domain | Likely topics behind the missed questions |
|---|---|
| Security | ACL evaluation order (table → field, `*` wildcards), ACL rule types and operations, roles vs. conditions vs. scripts (`answer`), application access settings (runtime vs. design access, "Can read/create/update/delete", "Allow access to this table via web services"), cross-scope privileges, restricted caller access, script protection policy, data policies vs. UI policies |
| Automation | Business rule timing (before / after / async / display) and when to use each, `current` / `previous` / `g_scratchpad`, script includes (classless vs. class, client-callable), GlideAjax, Flow Designer (triggers, actions, subflows, data pills, error handling, run-as), events (registry, `gs.eventQueue`), script actions, notifications, scheduled script executions |
| Design/Create | Global vs. scoped apps, scope namespace (`x_`), tables (extend vs. new, `sys_` fields, table auto-numbering), dictionary entries and overrides, reference fields and dot-walking, application files, modules and application menus, Studio, guided application creator |
| Managing apps | Update sets (capture rules, merging, preview/commit, why some records are not captured), Git source control in Studio (link, commit, branch, stash), application repository publish/install, versioning and dependencies, ATF, delegated development |
| External data | Import sets → staging table → transform map, coalesce rules, transform scripts (`onBefore`, `onAfter`, `source`, `target`, `ignore`), data sources (file/JDBC/REST), scheduled imports, REST Messages, Scripted REST APIs, REST API Explorer |

## Score history

| Date | Attempt | Design | UI | Security | Automation | Ext. data | Managing | Est. overall |
|---|---|---:|---:|---:|---:|---:|---:|---:|
| 2026-10-13 | CAD exam attempt | 67% | 93% | 58% | 55% | 75% | 67% | ≈ 69% |
| 2026-10-23 | Half practice test #1 | | | | | | | |
| 2026-10-30 | Half practice test #2 | | | | | | | |
| 2026-11-09 | Half practice test #3 | | | | | | | |
| 2026-11-12 | **Exam** | | | | | | | |
