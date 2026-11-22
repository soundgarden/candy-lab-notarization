# Candy's Science Lab — Notebook Notarization Anchor

This repository publicly anchors the hash chain of Candy's Science Lab
notebook, so anyone can verify that the lab's recorded history has not been
silently altered after the fact.

## Current chain head (2026-11-22)

- **Snapshot SHA-256:** `228c908e41a2a6694235f0f8238b9bf58f16f81491f403a5ed5696cb95532a7f`
- **Chain entry hash:** `76562aca35150bc4eff60540add1389164d8e7b1abc47441fbd4ae134a4fb83a`
- **Previous entry:** `359173c56e27342a8fc1ee730d1fc98c31b7366adc36175fc85b547f2378384e`
- **Anchored:** 2026-11-22

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
