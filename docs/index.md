# Overview

**Keep your Oracle Fusion Cloud environments in sync without re-keying anything.**

Nexus finds what is different between two Oracle Fusion environments, lets the right people review and approve exactly those records, writes them into the target environment through Oracle's own import and REST interfaces, and then reads the target back to prove the change landed. It covers both **configuration** (Setup & Maintenance tasks) and **master data** (suppliers and lookups today, more objects on the way).

> From "what changed?" to "it is live and verified" in one governed, auditable flow.

---

## The problem it solves

Every Oracle Fusion programme runs several environments: development, test, UAT, pre-production, production. Keeping them aligned is a constant, manual job.

**Configuration.** Setup & Maintenance can export and import a whole task or offering, but it is all-or-nothing. There is no way to ship just the five lookup codes that changed this sprint, so teams either re-key the change by hand in every environment or move far more than they intended. Oracle's compare can show differences, but turning that into a clean, selective import package is many manual steps.

**Master data.** Suppliers, lookups and similar records are usually keyed again in each environment. A supplier with an address, a site, a contact and flexfields is four to six Oracle screens and ten to twenty minutes of careful typing. A hundred suppliers is a week of somebody's time, with typos nobody will find until an invoice bounces.

**Governance.** Change tickets are approved in a ticketing tool where the approver cannot see the actual records. After go-live nobody can say who changed what in production, or why, and environments quietly drift apart.

| Today, by hand | With Nexus |
|---|---|
| Export whole tasks, diff spreadsheets, re-key the rest | Nexus reads both environments and shows the exact records that differ, field by field |
| Approve a ticket title | Approve the records themselves, with the before and after values on screen |
| Key suppliers again in each pod | Pick the suppliers, approve, and Nexus creates or updates them with everything underneath |
| "Did it land?" means logging in and checking | Nexus reads the target back and proves every record matches |
| No record of who moved what | Every discovery, decision, approval and write is kept, per record |

The time figures below are illustrative and depend on your volumes. They reflect what we see in practice.

| Activity | Manual | With Nexus |
|---|---|---|
| Find what changed in a functional area | Half a day of exports and comparison | Minutes |
| Move 100 suppliers with sites and contacts to another pod | Days of keying and checking | One review and one approval |
| Approve a change | Blind sign-off, follow-up questions | Approver sees the diff; one click |
| Recover from a failed import | Hours, usually a full re-run | Resume from the failed records |
| Answer "who deployed this and when?" | Log hunting | One screen |

---

## How Nexus works in five steps

```
 Discover  →  Review  →  Approve  →  Deploy  →  Verify
```

1. **Discover.** Nexus connects to your Oracle environments with a read-only integration user, exports the configuration or reads the master data, and stores a snapshot. It can compare a source environment against a target, or against the baseline it captured last time.
2. **Review.** The differences become a **changeset**: a list of added, changed and removed records, each with its old and new values. Reviewers keep what should move and set aside what should not, with a reason that is kept.
3. **Approve.** The changeset is submitted to a **pipeline route** that fixes the source and target pair. Approvers see the exact records, the current values in the target, and any drift since the review. Who may submit and who may approve is defined per route and per data area.
4. **Deploy.** Nexus writes the approved records into the target: Setup & Maintenance objects through Oracle's CSV import, master data through Oracle's REST services, parents before children, one request per record tree. Every record gets its own outcome and Oracle's own response.
5. **Verify.** After a successful deployment, one click re-reads the target environment and compares it with what was sent. The stage is marked **Validated** only when every record matches.

Everything is kept: the snapshots, the diff, who excluded which record and why, who approved, every request to Oracle and its answer, and the verification result.

---

## Three migration paths

| Path | When you use it | What makes it different |
|---|---|---|
| **Dev Promotion** | The regular flow from development towards production | Nexus pins a **baseline** after each promotion, so the next changeset holds only what changed since. Records a reviewer set aside come back automatically next time with fresh values. |
| **Hotfix** | A targeted change between any two environments, including master data | Two environments are read at once and compared directly. For master data you **pick the records** to move, or let Nexus compare everything that matches a search. Goes straight to the target after approval. |
| **Release** | Shipping tested changes to pre-production and production | Bundles approved changesets into one release with its own approval gates, takes a snapshot of the target before writing, and offers a governed **revert** to that snapshot. |

All three run on the same engine, the same approvals and the same audit trail.

---

---

*Nexus is an independent product and is not affiliated with, endorsed by, or sponsored by Oracle. Oracle and Oracle Fusion Cloud are trademarks of Oracle Corporation and its affiliates.*
