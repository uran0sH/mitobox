# MitoBox Agent Instructions

MitoBox is a versioned sandbox runtime for AI agents.

## Project Status

MitoBox is in the MVP stage. The MVP should be built directly on Firecracker snapshots.

## Core Concepts

- Snapshot: immutable full VM state, including memory, disk, CPU, and device state.
- Branch: version line for sandbox evolution, with a mutable head Snapshot.
- Sandbox: running Firecracker microVM restored from a Snapshot.
- restore: create a Sandbox from a Snapshot.
- commit: append a new Snapshot to a Branch from a running Sandbox, then advance the Branch head.
- checkout: create a Sandbox from the head Snapshot of a Branch.

A Branch does not contain runtime state. Runtime state lives in Sandboxes; durable state lives in Snapshots.

## MVP Constraints

- Use Firecracker as the VMM backend.
- Keep the first implementation local and single-node.
- Prefer full snapshots before diff snapshots.
- Allow short pause windows for `commit`.
- Keep metadata explicit and inspectable.
- Do not claim live fork, cross-node restore, or production isolation semantics beyond Firecracker.
- Do not replace Firecracker with a directory-copy model.

## Engineering Rules

- Keep implementation small and direct.
- Prefer Rust standard library until a dependency clearly pays for itself.
- Isolate Firecracker-specific code behind a narrow backend boundary.
- Do not refactor unrelated code.
- Update README only for user-facing behavior or positioning changes.

## Verification

Run these after code changes:

```bash
cargo fmt
cargo check
cargo test
```
