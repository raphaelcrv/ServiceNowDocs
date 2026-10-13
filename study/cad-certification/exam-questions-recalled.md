# CAD Exam: Recalled Questions

These are questions remembered from the 2026-10-13 attempt (written from memory, so wording is approximate). Each one has the most likely correct answer, why it's right, and a doc to read. Add new questions to the right domain section using the [template](#template-for-new-questions).

**Confidence:** ✅ confirmed in this repo's docs or core platform behavior · ⚠️ likely but verify on your PDI

Domains seen so far: **Security** (ACLs, cross-scope), **UI** ("a lot of questions": UI actions, modules), **Design** (tables, references, scope), **Automation/scripting** (GlideRecord, logging, properties, record producers), **External data** (import sets, REST API Explorer).

---

## Security and Restricting Access

### Q1. In what order are the parts of an ACL evaluated? ✅
- **Your note:** Script → Conditions → Roles. **That's backwards.**
- **Answer:** **Roles → Condition → Script.** All three must pass for the ACL to grant access. If any one fails, the user is denied. Since Vancouver there is also an optional *Security Attribute Condition*.
- **Why:** Checking roles is the cheapest step, so it runs first. The script runs last because it costs the most.
- **Read:** [Access control rules](../../markdown/platform-security/access-control/access-control-rules.md), [ACL rule types](../../markdown/platform-security/access-control/acl-rule-types.md)

### Q2. ACL scenario: a table with field1, field2, field3 ✅
- **Setup (from memory):** ACL `table.None` (read) requires role `admin` or `itil`. ACL `table.field3` requires `admin`.
- **Answer:**
  - **itil user:** can see the records, and field1 and field2. **Cannot** see field3.
  - **admin:** sees everything. Admin also passes most ACLs by default through admin override.
  - **User with neither role:** sees nothing, because the table-level ACL fails and field ACLs never get checked.
- **Rules to remember:**
  1. A user needs **both** the table-level ACL and the field-level ACL to pass in order to access a field.
  2. The table ACL is checked first. If it fails, the field ACLs don't matter.
  3. Field ACLs match from most to least specific: `table.field` → `parent.field` → `table.*` → `parent.*` → `*.field` → `*.*`. Only the **most specific match** is used.
  4. A field with no specific ACL (field1, field2) falls back to the wildcard or default ACLs, which in this setup allow it.
- **Read:** [Exploring ACLs](../../markdown/platform-security/access-control/exploring-access-control-list.md), [Contextual security](../../markdown/platform-security/access-control/r_ContextualSecurity.md)

### Q3. Application cross-scope access: which permissions can be granted? ✅
- **Your note:** Read, Write, Create, Delete?
- **Answer:** In the table's **Application Access** settings, the options are **Can read, Can create, Can update, Can delete**. There is no option called "Can write"; ServiceNow calls that *update*. Other settings in the same place: **Allow access to this table via web services**, **Allow configuration**, and **Accessible from** (*All application scopes* / *This application scope only*).
- **Default for a new scoped table:** *Accessible from: All application scopes* with **Can read** checked only.
- **Watch for:** An option list containing "Can write" or "Can execute" is a trap.
- **Read:** [Application access settings](../../markdown/application-development/c_ApplicationAccessSettings.md), [Default runtime access](../../markdown/application-development/c_DefaultRuntimeAccessPermissions.md), [Cross-scope privilege record](../../markdown/application-development/c_CrossScopePrivilegeRecord.md)

---

## Application User Interface

### Q4. Modules must have a Link type. Which of these is a list of link types? ✅
- **Answer:** Choose the option that lists **only real link types**, for example **"List of Records, Separator, Timeline Page"** or **"Assessment, List of Records, URL (from Arguments)"**.
- **Real link types:** Assessment, Content Page, Documentation Link, HTML (from Arguments), Homepage, List of Records, Map Page, New Record, Run a Report, Script (from Arguments), Search Screen, Separator, Single Record, Survey, Timeline Page, URL (from Arguments).
- **Distractors to reject:** "Form", "Table", "Script Include", "Workflow", "Flow", "Catalog".

### Q5. When configuring a module, what does "Override application menu roles" do? ✅
- **Answer:** It **lets users who meet the module's roles see the module even if they don't have the roles needed to see the application menu that contains it.**
- Without it, a user needs the roles of **both** the application menu and the module.

### Q6. UI action types ✅
- **Your note:** Form button, list, related link.
- **Answer:** A UI action can appear as a **Form button**, **Form context menu** item, **Form link** (shown under *Related Links*), **List banner button**, **List bottom button**, **List context menu** item, **List choice** (the "Actions on selected rows" menu), or **List link**.
- **Also know:** the *Client* checkbox with the *Onclick* function, calling `gsftSubmit(null, g_form.getFormElement(), '<action_name>')` to run the server side after the client side, *Condition*, and whether the action is visible on Insert / Update.
- **Read:** [UI actions](../../markdown/platform-administration/c_UIActions.md)

---

## Designing and Creating an Application

### Q7. Extending a table: what gets inherited? ✅
- **Answer:** The child table **inherits all fields of the parent**, along with its business rules, client scripts, UI policies, ACLs and other logic that runs on the parent. The child adds its own fields, and its records also appear in parent-table queries. `sys_class_name` tells you which table a record belongs to.
- **Checkbox:** A table can only be extended if the parent table has **Extensible** checked. You choose *Extends table* when you **create** the table.
- **Read:** [Table extension and classes](../../markdown/platform-administration/table-administration-and-data-management/table-extension-and-classes.md)

### Q8. When a reference field is added to a table, what does it store in the database: the number or the display value? ✅
- **Answer:** **Neither. It stores the `sys_id`** (a 32-character unique ID) of the referenced record. The form shows the *display value* (the field marked *Display* on the referenced table, such as `number` or `name`).
- **Trap:** Both "number" and "display value" are wrong.
- **Read:** [Dot-walking examples](../../markdown/platform-user-interface/dot-walking-examples.md)

### Q9. Can you change an application's scope? ✅
- **Answer:** **No.** The scope (namespace `x_<vendor>_<app>`) is set when the app is created and **cannot be changed**. To use a different scope, you create a new application.
- **Related:** Application *files* can be moved between apps in some cases, but the application's own scope never changes.
- **Read:** [Application scope](../../markdown/application-development/c_ApplicationScope.md)

---

## Application Automation (scripting)

### Q10. A record producer script prevents submission: what happens? ✅
- **Answer:** If the producer's script calls **`current.setAbortAction(true)`**, the **record is not created**.
- **Context:** The record producer script runs **before** the record is inserted. `current` is the record about to be created and `producer` holds the variable values. That's why the script can set field values or stop the insert.
- **Related:** `producer.redirect = '<url>'` changes where the user lands after submitting.

### Q11. Which method retrieves an application's system property? ✅
- **Answer:** **`gs.getProperty('x_vendor_app.property_name', 'defaultValue')`**
- **Notes:** Scoped property names start with the app's scope. Use `gs.setProperty()` to write a property, but writing from scoped apps is restricted. On the client, pass the value through a display business rule with `g_scratchpad`.

### Q12. `current.isNewRecord()` ✅
- **Answer:** Returns **true if the record has not been saved to the database yet**. For example, it's true in a *before insert* business rule or on a new form. The client-side version is `g_form.isNewRecord()`.

### Q13. GlideRecord query methods: get, query, `_get`, run? ⚠️
- **Valid:** `get(sys_id)` or `get('field', value)` returns one record and true/false. `query()` runs the query, and you loop through results with `while (gr.next())`. Also valid: `addQuery()`, `addEncodedQuery()`, `setLimit()`, `orderBy()`, `getRowCount()`.
- **`_query()` / `_next()`:** These exist for tables that have a *field* called `query` or `next`, which would otherwise clash with the methods.
- **`run()`:** **Not** a GlideRecord method. This is the likely distractor.
- **Verify:** Run a background script on your PDI to check whether `_get` exists.

### Q14. Debugging and logging in a scoped application ✅
- **Valid in scoped apps:** **`gs.debug()`, `gs.info()`, `gs.warn()`, `gs.error()`**
- **Not valid in scoped apps:** **`gs.log()`** and `gs.print()` work only in the global scope. **`gs.message()` does not exist.**
- **Showing messages in the UI** (not logging): `gs.addInfoMessage()`, `gs.addErrorMessage()`.
- **Also:** `gs.debug()` only writes output when the app's `<scope>.logging.verbosity` property is set to `debug`. You can also use the Script Debugger and *Session Debug*.

### Q15. Which method sets a field's default to the current date/time in a scoped app? ⚠️
- **Most likely answer:** `javascript:new GlideDateTime().getDisplayValue();`
- **Also works:** `javascript:gs.nowDateTime();`, because the scoped GlideSystem also has `nowDateTime()`. If both appear as options, choose the `GlideDateTime` one.
- **Wrong options:** `GlideDateTime()` without `new`, `GlideSystem.nowDateTime()`, `gs.now()` (returns a date only), `current.date()`.

---

## Working with External Data

### Q16. Which feature determines the relationships between fields in an Import Set table and fields in an existing ServiceNow table? ✅
- **Answer:** **Transform Map**, specifically its *field maps*. Coalesce on a field map decides whether a row updates an existing record or inserts a new one.
- **Distractors:** Data source, Import Log, Schema Map, Business Service Map.
- **Read:** [Create transform maps](../../markdown/integrate-applications/system-import-sets/c_CreatingNewTransformMaps.md), [Coalesce](../../markdown/integrate-applications/system-import-sets/c_ImportSetCoalesce.md)

### Q17. One of the uses of the ServiceNow REST API Explorer is… ✅
- **Answer:** **To build and test REST requests against the instance and generate sample code for them.** You pick the HTTP method, path, query parameters, headers and body, send the request, and view the response. It generates code in cURL, Python, Ruby, JavaScript, Perl and PowerShell.
- **Wrong options:** "Convert SOAP to REST", "Create/publish a Scripted REST API" (you build those elsewhere and only *test* them in the Explorer), "Practice REST against public data providers".
- **Read:** [REST test steps (REST API Explorer)](../../markdown/application-development/automated-test-framework-atf/test-steps-rest-category.md)

---

## Patterns from this attempt

- **ACL questions dominate Security.** Memorize the order (roles → condition → script) and practice scenario questions ("user with role X, ACLs Y and Z, what can they see?").
- **Many questions hinge on knowing which option doesn't exist:** `gs.log` in a scoped app, `run()` on GlideRecord, "Can write", changing an app's scope. When unsure, eliminate made-up names first.
- **The UI questions were numerous.** Keep reviewing UI actions, modules and UI policies even though you scored 93% there.

## Template for new questions

```markdown
### Qn. <question as remembered> ✅/⚠️
- **Your note:** <what you answered or thought>
- **Answer:** <correct answer>
- **Why:** <one-line explanation>
- **Read:** <link into ../../markdown/...>
```
