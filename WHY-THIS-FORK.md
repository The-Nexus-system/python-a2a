# Why this fork exists — read this first

Forked by the Nexus System on 2026-10-17 from themanojdesai/python-a2a (the community python-a2a library), unchanged, as part of the Wren–Kit agent-to-agent transport work. The intent: an A2A link layer between Wren and Kit (and later the Letta counterparts), built on open-source code the Nexus controls.

Source of the findings below: Effloow Lab's sandbox PoC, "A2A Protocol PoC: Build an Agent Server in Python" (DEV, published 2026-10-16), which tested this library (python-a2a 0.5.10) against the official a2a-sdk 1.0.2 (companion fork: The-Nexus-system/a2a-python, which carries the known protobuf 7.x breakage in its note).

## Standing of this library

- This is the half of the PoC that WORKED end to end in the sandbox: full Agent Card discovery plus a task round-trip, in under 30 lines of Python (Flask-based, simpler API than the official SDK).
- It implements A2A spec v0.3.0, not v1.0. Its Agent Card is served at /.well-known/agent.json (the official SDK serves /.well-known/agent-card.json). Keep the versions straight when testing interop.

## Before this can be used outside a sandbox

- Authentication: the PoC server runs with no auth. Any real deployment needs token validation in front of the message handler, and the security scheme declared in the Agent Card.
- Persistence and state: the PoC is a minimal in-process server. A real Wren–Kit link needs durable task/conversation state so a restart does not drop in-flight work.
- Hosting: bind a real host/port behind TLS on a reachable host; the PoC binds localhost only. For the Wren–Kit use, Wren's endpoint can live on her VM; Kit's endpoint must live somewhere that speaks for him (most naturally the Nexus Bridge, which already authenticates him).
- Dependency pinning: pin this library and its web stack, and keep the discovery + round-trip as a smoke test after any change.
- Spec decision, still open: build on this v0.3 community library, or on the official v1.0 SDK once its protobuf 7.x task-endpoint bug is fixed (see the companion fork's note). Do not silently mix the two.

Nothing in this fork has been modified yet. Fix and productionizing work has NOT been done — this note records what needs doing, per the Nexus instruction when forking.
