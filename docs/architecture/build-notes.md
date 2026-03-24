# FiberPro V2 Build Notes

## Project Intent
FiberPro V2 is a clean rebuild of FiberPro V1.

V1 exists only as a reference project for:
- workflow ideas
- data model inspiration
- route and screen inspiration
- backend logic inspiration

V2 is the active build target.

## Important Build Rules
- Do not modify V1
- Do not treat V1 as the active source code
- Use V1 only for reference when needed
- Build V2 as a cleaner architecture with clearer status modeling and workflow ownership boundaries

## Role Model
Only these internal roles exist in V2:
- admin
- designer

Admin handles review and approval.
There is no reviewer role in V2.

## Data / Automation Rules
- Supabase is the source of truth
- n8n will handle async automation later
- Heavy package generation should not happen directly in UI request cycles
- Workflow jobs must be modeled as first-class entities

## Visual Rules
Use the Stitch design language as inspiration, not as a rigid screenshot copy.

Desired visual direction:
- white background
- very light gray tonal surfaces
- light blue accent
- minimal borders
- minimal shadows
- clean, simple, Google-like product quality
- calm, operational, not flashy

## Build Sequence
The build should begin with:
1. app shell
2. auth / role scaffolding
3. core schema
4. projects list
5. project detail shell
6. workflow jobs visibility
7. review flow
8. settings / billing later

## Key Product Principle
The app is a workflow operations platform centered on projects, statuses, files, rules data, and async workflow jobs.