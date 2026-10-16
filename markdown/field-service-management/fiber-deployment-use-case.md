---
title: Field Service fiber deployment workflow example
description: This Field Service fiber deployment workflow example shows how a telecom infrastructure services provider such as Congruex coordinates its own crews and contractor teams to connect a customer to a new fiber network.
locale: en-US
topic_type: concept
breadcrumb: [Example workflows, Explore, Field Service Management]
---

# Field Service fiber deployment workflow example

This Field Service fiber deployment workflow example shows how a telecom infrastructure services provider such as Congruex coordinates its own crews and contractor teams to connect a customer to a new fiber network.

**Note:** The company, people, and figures in this example are illustrative. They are not taken from a real customer implementation.

Daniel, a regional operations manager at a fiber broadband operator, needs a new fiber build in a residential area activated before a service-launch date. The operator outsources engineering, construction, and customer installation to Congruex. Previously, the operator and its service provider tracked each address in separate spreadsheets and email threads. Work was handed between crews by phone, permits and splice records were hard to find, and nobody could say how many homes were ready to connect.

After Congruex adopted ServiceNow, the build is tracked end to end in Field Service Management. The operator opens a build request, FSM breaks it into work orders and tasks, and the work is routed to Congruex crews or to partner contractors based on skills, territory, and capacity. Each customer address moves from survey to activation in a single record, and Daniel sees progress in real time.

## Field Service fiber deployment workflow diagram

\[Image: Field Service Management fiber deployment workflow. For text description, refer to the following table.\]

## Field Service fiber deployment workflow steps

The following table provides the steps for the Field Service fiber deployment workflow.

|Steps|Description|
|-----|-----------|
|1. Open build request|The operator submits a build request for a service area, or a customer orders service through the operator's portal. A Customer Service Management \(CSM\) case or order is created with the service address and the preferred install window.|
|2. Auto-generate work orders|Work order templates create a work order for each address or build segment. Each work order contains the tasks needed to deliver service, such as site survey, permit check, underground or aerial construction, fiber splicing, drop installation, and customer activation. Required skills, certifications, and parts are populated from the template.|
|3. Plan by territory and capacity|Using Territory Planning and Capacity and Reservations Management, planners confirm that each geographic region has enough qualified crews and materials for the target dates before work is promised to the customer.|
|4. Route to crews or contractors|Tasks that Congruex crews can perform are assigned with dynamic scheduling based on location, skills, and availability. Work that exceeds internal capacity, or that requires a local specialty, is offered to contractor teams through the Field Service Marketplace. Contractor teams respond and are evaluated against service level agreements \(SLAs\).|
|5. Bundle and coordinate|Task bundling groups nearby tasks, such as several drop installations on the same street, so a crew completes them in one trip. For jobs that need more than one person, such as pole work or trenching, crew operations schedules the whole crew together.|
|6. Execute with the mobile app|The technician receives the task in the Mobile Agent app, which also works offline in areas with weak coverage. The app provides the address, work instructions, required parts, and related knowledge articles. The customer receives a text with the technician's estimated arrival time.|
|7. Capture quality data|Questionnaires guide the technician through required checks, such as signal-level readings, splice documentation, and safety confirmations. Photos and notes are attached to the task. A task cannot be closed until the required answers are recorded.|
|8. Confirm and activate|After the drop is installed and tested, the customer signs the work order on the technician's device. A summary PDF of the tasks, parts used, and time spent is attached to the work order. The service is activated and the originating case or order is updated.|
|9. Report and improve|Managers review progress by region and by crew or contractor in the Field Service Performance Analytics dashboards. Metrics such as homes passed versus homes connected, first-time completion, and SLA compliance support billing validation, audits, and planning for the next build phase.|

## Why this matters

-   Operators and service providers work from one shared record instead of separate spreadsheets and emails.
-   Internal crews and contractors are managed under the same process, with the same quality checks and SLA tracking.
-   Customers get arrival updates and a confirmed installation, which reduces missed appointments and repeat calls.
-   Complete work order data supports accurate billing and audits.

**Parent Topic:**[Field Service Management workflow examples](https://raw.githubusercontent.com/ServiceNow/ServiceNowDocs/brazil/markdown/field-service-management/fsm-use-cases.md)
