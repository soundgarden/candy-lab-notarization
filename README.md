# Candy's Science Lab — Notebook Notarization Anchor

This repository publicly anchors the hash chain of Candy's Science Lab
notebook, so anyone can verify that the lab's recorded history has not been
silently altered after the fact.

## Current chain head (2026-11-21)

- **Snapshot SHA-256:** `6efcd1d82490a0f89bfd93fe1597b6332ed95a5e2dbff381c3e9611989520410`
- **Chain entry hash:** `359173c56e27342a8fc1ee730d1fc98c31b7366adc36175fc85b547f2378384e`
- **Previous entry:** `58b4b55ca6c0528ac4ded2b6e5e83790d5ffdbf4868b21e73542b6857b7dc517`
- **Anchored:** 2026-11-21

Machine-readable copy: [ANCHOR.json](ANCHOR.json)

## How verification works

Each day, the lab exports a full snapshot of its records (experiments,
journal, peer reviews, pre-registrations, run ledger, and the rest). The
snapshot is canonicalised — the volatile `exported_at` field removed, the
rest serialised with sorted keys and compact separators — and hashed with
SHA-256. That is the **snapshot hash**: it changes if and only if a stored
lab record changed.

Each chain entry then hashes `{date, snapshot_sha256, prev_hash}` into an
**entry hash**. Because every entry embeds the previous entry's hash,
rewriting any past entry or snapshot breaks the chain and is caught by
verification.

Publishing the head here means the lab's history is anchored outside the
lab itself: a quietly edited notebook would no longer match the hashes the
world can see.

## Honest limits

The chain proves records were not altered *after* notarization. It does not
prove the science is right — that is what the lab's pre-registration,
peer-review gate, and second-seed law are for.
