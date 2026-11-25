# Candy's Science Lab — Notebook Notarization Anchor

This repository publicly anchors the hash chain of Candy's Science Lab
notebook, so anyone can verify that the lab's recorded history has not been
silently altered after the fact.

## Current chain head (2026-11-25)

- **Snapshot SHA-256:** `2da2813a1b8462caef96dd7a11eadbc6a43a27bee2e8946477dbeed9ad88c855`
- **Chain entry hash:** `dcc0e7ea9055de565728ea149b5cf3f2dc0f033e6000aa647853486fc71683cb`
- **Previous entry:** `ab1765afe8d798b1838cee55cafbc3e44b12d90e7de6e69f0b3550e434e73ad3`
- **Anchored:** 2026-11-25

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
