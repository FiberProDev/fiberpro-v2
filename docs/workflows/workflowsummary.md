# FiberPro V2 Workflow Summary

## Purpose
FiberPro V2 is a workflow-driven internal operations platform for telecom traffic control plans, permit package generation, project tracking, and billing support.

This version is a clean rebuild of V1. V1 is reference-only and is not the active build target.

## Product Principles
- The core object in the system is the **project**
- Supabase is the **source of truth**
- The web app is the **human operations interface**
- n8n will handle **long-running automations and external process workflows**
- The UI should reflect workflow status clearly at all times
- V2 uses only the following internal roles:
  - **admin**
  - **designer**
- Review is handled by **admin only**
- There is **no reviewer role** in V2

## User Roles

### Admin
Admin users have full internal visibility and control.
They can:
- view all projects
- manage project statuses
- assign designers
- review projects
- request revisions
- approve work
- trigger package generation
- manage companies, billing, settings, and workflow visibility

### Designer
Designer users work assigned projects.
They can:
- view assigned projects
- review intake/project details
- upload deliverables and supporting files
- respond to revision requests
- mark work ready for admin review

### Client Users
Client-facing users may exist later in the portal, but internal operations in V2 are centered on admin and designer.

## Core Project Lifecycle

Projects should move through a controlled status lifecycle.

Suggested statuses:
- draft
- submitted
- intake_review
- awaiting_client_info
- assigned
- in_progress
- ready_for_review
- revisions_required
- approved
- package_requested
- package_generating
- package_ready
- invoiced
- completed
- archived

## Main Workflows

### 1. Client Intake Workflow
1. A new project is submitted
2. Project record is created in Supabase
3. Intake files are uploaded
4. Intake data is reviewed
5. If information is missing, project moves to `awaiting_client_info`
6. If information is complete, project moves to `intake_review` and then can be assigned

### 2. Assignment Workflow
1. Admin reviews intake
2. Admin assigns a designer
3. Project status moves to `assigned` or `in_progress`

### 3. Rules / Road Data Workflow
1. SLD and related files are attached to the project
2. Road and jurisdiction data are reviewed or extracted
3. Rules output is generated or edited
4. Recommended detail sheets / TCD selections are stored in structured form
5. Admin or designer may override recommendations when needed

### 4. Production Workflow
1. Designer works the assigned project
2. Designer uploads deliverables and supporting files
3. Designer updates project data as needed
4. Designer marks the project `ready_for_review`

### 5. Admin Review Workflow
1. Admin opens the project needing review
2. Admin checks files, metadata, and output
3. Admin either:
   - approves the project, or
   - requests revisions
4. If revisions are requested:
   - project moves to `revisions_required`
   - notes are stored
   - designer updates work and re-submits

### 6. Permit Package Workflow
1. Once approved, admin can request package generation
2. The app creates a `workflow_job`
3. The app triggers an n8n workflow
4. n8n fetches project data, files, and application data
5. n8n generates forms and/or package outputs
6. Generated outputs are uploaded back to storage
7. Workflow job records and events are updated
8. Project status moves to `package_ready` when complete

### 7. Billing Workflow
1. Approved or package-ready projects become invoice-eligible
2. Invoice records are created and linked to projects
3. Billing status is tracked in the system
4. Billing automation may be added later through n8n

## Ownership Boundaries

### The Web App Owns
- authentication
- roles and permissions
- project records
- file metadata
- project status management
- review actions
- assignment
- workflow job visibility
- billing views
- settings and rules configuration
- audit history

### Supabase Owns
- relational data
- auth
- storage
- audit persistence
- workflow job records
- file metadata
- structured project data

### n8n Will Own
- long-running async workflows
- package generation
- form autofill
- external integrations
- notifications
- billing/reporting automation later

## Workflow Jobs

Workflow jobs are a first-class concept in V2.

Suggested job types:
- intake_validation
- rules_preprocess
- application_data_build
- form_autofill
- permit_package_generation
- invoice_generation
- revision_notification
- metrics_rollup

Suggested workflow job statuses:
- queued
- running
- completed
- failed
- cancelled
- retrying

## UI Priorities
The UI should make the following obvious on every important screen:
- what the project is
- what status it is in
- who owns it
- what action is next
- what files or workflows are attached
- what happened previously
- whether anything is blocked

## Design Direction
The V2 interface should follow the Stitch design system:
- white or near-white overall background
- tonal separation instead of heavy borders
- very light gray surfaces/cards
- subtle depth, minimal shadows
- light blue as the primary accent
- clean, Google-like professionalism
- simple, calm, structured, operational