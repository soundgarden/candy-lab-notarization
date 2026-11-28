# Candy's Science Lab — Notebook Notarization Anchor

This repository publicly anchors the hash chain of Candy's Science Lab
notebook, so anyone can verify that the lab's recorded history has not been
silently altered after the fact.

## Current chain head (2026-11-28)

- **Snapshot SHA-256:** `a7c23b5b5631da3a2b28cedccf708f3866b2fede8aa27da4c01a5e71c6de417b`
- **Chain entry hash:** `50389d511d26e1886c9d22d043d73edd32829d181d35b390bca1dbe83dbfb76d`
- **Previous entry:** `ad86157bdf4249460fd0dba4bb53890b0acc4916d246dc759631b4e81ef7e262`
- **Anchored:** 2026-11-28

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
