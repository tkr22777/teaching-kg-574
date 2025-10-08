# Option A: Networked Software Proposal Guide (Implementation)

## Template (1–2 pages)

**1. Title & Team**: Project title, names, majors, emails
**2. Problem Statement**: What you’re building and why (2-3 sentences)
**3. Architecture Diagram**: Components and data flows (client(s), server, storage if any)
**4. Key Features (3–5)**: User-visible capabilities and constraints
**5. Technologies**: Language, libraries, protocols, tools
**6. Success Criteria**: Functional correctness; N clients connect concurrently; target latency/throughput; resilient error handling; end-to-end demo scenario completes

## Scope Guidance

**Good Scope:** Chat app, file transfer, simple HTTP server, DNS resolver, network monitor, port scanner
**Too Simple:** Single HTTP request, ping wrapper
**Too Complex:** Video streaming platform, distributed database

## Required Stack (Python)

Python 3.x; `socket` plus `threading` or `asyncio`; optionally `socketserver` or `asyncio.start_server`; client connects via hostname and port; serialization using `json` or `struct`.

## Coding Guidance (Required Checklist)

- Server uses Python networking APIs: `socket` (required) with `threading` or `asyncio` (e.g., `asyncio.start_server`), or `socketserver` built on `socket`.
- Client is a Python program that accepts `--host/--port` (or equivalent) and connects to the server using `socket` or `asyncio.open_connection`.
- Messages are serialized using `json` or `struct`; include fields to identify sender and message type.
- Server maintains a registry of connected clients and supports: list online clients; broadcast; direct message routing.
- Provide run commands in README, e.g.:`python server.py --host 0.0.0.0 --port 5000python client.py --host <server-host> --port 5000`
- Include a short demo scenario in the README (steps to connect two clients and exchange messages).

## Evaluation (Implementation)

Major weighting on:
- **Functionality:** Features work end-to-end; correct protocol usage; robustness and error handling
- **Readability & Organization of Code:** Clear structure/layering, modular design, descriptive naming, small focused functions

Also considered: documentation (README/run steps), demo clarity, and basic performance targets.

## Tips (Implementation)

- Use layered design (e.g., networking I/O layer, domain/service layer, CLI/UI layer) and modular packages
- Keep functions small and focused (aim for ≤ 30 lines per function) and single-responsibility
- Write clean code: descriptive names, clear error handling
- Start with a minimal viable path (connect → auth/identify → features)
- Separate networking I/O from business logic for easier testing
- Prefer asyncio or threading, not both; keep concurrency simple
- Define a small message schema early (type, from, to, payload)
- Log connections and errors; add timeouts to avoid hangs
- Test locally with multiple clients (different terminals)
