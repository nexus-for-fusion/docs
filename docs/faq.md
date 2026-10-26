# Frequently asked questions

**Does Nexus write to production?**
Only through an approved pipeline stage on a route you activated, by an approver you named. Nothing writes without an approval, and every write is recorded with Oracle's response.

**Where are my Oracle credentials kept?**
In a secrets manager (Google Secret Manager for hosted tenants, your own vault or environment for self-hosted), never in the Nexus database, never in a log.

**What happens when Oracle refuses a record?**
The record is marked failed with Oracle's own message, anything that depends on it is skipped, and the rest of the run continues. Fix the data and resume; records that already landed are not sent again.

**Can I undo a deployment?**
On the release path, Nexus snapshots the target before it writes and offers a governed revert to that snapshot. On every path you can see exactly which records were written, with their previous values.

**Does it change anything in my Oracle environments to install?**
No. Nexus uses Oracle's standard export, import and REST services with an integration user you create. There is nothing to install in the pod.

**Which databases does Nexus itself run on?**
PostgreSQL, MySQL 8 or Oracle Autonomous Database. The Docker PoC uses PostgreSQL.

**How is access controlled?**
Per-user sign-in; roles that combine a function (migration, registry, security) with a data scope (modules, and routes at submitter or approver level); a superuser account as the safety net; lockout and login history.

---

*Nexus is an independent product and is not affiliated with, endorsed by, or sponsored by Oracle. Oracle and Oracle Fusion Cloud are trademarks of Oracle Corporation and its affiliates.*
