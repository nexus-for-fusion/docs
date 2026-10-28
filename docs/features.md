# Feature tour

## Registry: everything that can move, in one place

- **Environments.** Register each Oracle pod once with its URL and an integration user. Credentials go into a secrets vault, never into the application database. Renaming an environment is safe; re-pointing it to a different pod is detected and guarded.
- **Oracle catalogue, pre-loaded.** 35 offerings, 32 functional areas, 742 Setup & Maintenance tasks and about 800 configuration business objects ship with the product. Switch on what applies to you.
- **Master data objects.** Suppliers (the full tree: addresses, sites, site assignments, contacts, flexfields and more) and lookups are registered from Oracle's own service descriptions. Suppliers are only the example: any other master data object can be registered the same way, and a client's registry settings travel between instances as an export/import package.
- **Modules.** Group the functional areas or master data objects a team owns into a module, and run discovery, review and approvals per module.
- **Routes.** A pipeline template is a route: it pins the source and target pair, the stages, and whether a stage needs approval.

## Auto-discovery and baselines

- Run discovery on demand or on a schedule. For configuration, Nexus submits Oracle's export jobs, waits for them, downloads the result and parses it. For master data it reads Oracle's REST services in pages, several at a time, with a request pace that protects your pod.
- The first run quietly establishes the baseline so you only ever see real changes.
- Records are identified by their business keys (a lookup code, a supplier number), never by Oracle's internal numeric ids, so the same record is recognised across pods. Where Oracle assigns a per-pod identifier, Nexus learns it and maps it to the target's value on deployment.

## Field-level diff

- Added, changed and removed records, with the fields that differ highlighted and the current target value next to the value that will be deployed.
- Renamed child records (an address whose name changed) are recognised as one change rather than a delete and an add.
- Fields you mark as sensitive can be masked: sent on create only, never compared, never shown.

## Changeset review

- Keep or exclude per record, or in bulk: "keep only these", with the reason stored on every excluded record.
- Give a changeset a name your team will recognise; the system label stays as its permanent identity.
- On the promotion path, records set aside in one cycle come back automatically in the next, with fresh values, until they are deployed or deliberately dropped.
- Tags, presence ("who else is reviewing"), and a per-object view of what is in and what is out.

## Approval gating and access control

- A role is a function (migration, registry, security) at read or write level, combined with a data scope: which modules, and on which routes the holder may **submit** or **approve**.
- A user can hold several roles; each role is evaluated as a whole, so a template approver for one route cannot approve on another.
- Approvers see the records, the target's current values and any drift since the diff was computed. Stage 1 of a promotion can be auto-approved; a hotfix route can require a named approver who is not the submitter.
- A refusal tells the user why: which permission the closest role lacks.

## Pipeline and execution

- Ordered stages per environment with a queue, so two changes never write to the same environment at once.
- The diff is recomputed against the live target when a stage reaches the front of the queue. If another change already landed the same records, the stage skips them.
- Configuration goes in through Oracle's CSV import with parent records included automatically in the right order. Master data goes in through REST, one request per record tree (a supplier and everything under it), parents first, new records created and changed records updated.
- A record Oracle refuses never stops the run; it is marked failed with Oracle's message and its dependants are skipped. Only systemic failures (authentication, outages) stop a run.
- Resume picks up where a run stopped and never re-sends what already landed.

## Verification and traceability

- **Validate** re-reads the target after a deployment and compares every record with what was sent. The result is a per-record verdict: matched, different, or missing.
- A traceability view answers "when was this record last deployed to this environment, by which change, approved by whom?" in one query.

## Security and operations

- Sign-in with per-user accounts, a 24-hour session, lockout after repeated failures and a login history.
- Oracle credentials and the masking key live in a secrets manager (Google Secret Manager today, environment-based for local use); the application database never holds a password.
- Runs on PostgreSQL, MySQL or Oracle Autonomous Database. Multi-tenant hosting isolates each client in its own namespace and schema.

---

## What is covered today

**Configuration.** Any Setup & Maintenance task Oracle can export and import, driven by the pre-loaded catalogue, with natural keys learned from Oracle's own export signals and dependency ordering on import.

**Master data.** Suppliers are the worked example in these pages, with their full tree of addresses, sites, site assignments, contacts, contact addresses, business classifications and flexfields, alongside standard and common lookups. Any master data object Oracle exposes through its services can be handled the same way; adding one is a registration step, not a code change.

**Not yet.** Deleting records in the target, attachments and file content, and BI Publisher reports.

---

---

*Nexus is an independent product and is not affiliated with, endorsed by, or sponsored by Oracle. Oracle and Oracle Fusion Cloud are trademarks of Oracle Corporation and its affiliates.*
