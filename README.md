# IACP Generic Worker Portal

Public GitHub Pages front-end for the **Iran Azadi AgentOps Control Plane — Generalized Worker Bridge (LAB)**.

## Current version

Generic Worker Portal v0.1.0

## Design

The portal contains no task-specific or role-specific workflow logic.

A worker session is supplied through the URL fragment:

`#token=<worker-session-token>`

The portal removes the fragment from the visible URL and reads the authoritative session from the Generic Gateway. The Gateway provides:

- Project ID
- Task ID
- Task type and title
- Role and role type
- Worker ID
- Revision
- Task instruction
- Expected output type/count
- Current state
- Lock ID
- Registered artifacts
- `allowedActions`

The portal renders mutation controls only from `allowedActions`.

## Supported worker actions

- `CLAIM`
- `SUBMIT_RESULT`
- `QA_APPROVE`
- `QA_NEEDS_REVISION`
- Heartbeat while an active lock exists

## Mutation safety

- Mutation POSTs are single-attempt only.
- A mutation transport response is not treated as authoritative.
- After every mutation attempt, the portal performs authoritative `get_session` readback.
- If authoritative readback fails, mutations are blocked rather than blindly retried.

## Environment

LAB only. Production changes remain frozen.
