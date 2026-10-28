# Proven at scale

A whole-population supplier compare was run between the same two pods on 12 and 13 October 2026, with no record limit.

| Measure | Result |
|---|---|
| Suppliers read from the source pod | 43,959 suppliers · 423,170 records · 21 minutes |
| Suppliers read from the target pod | 40,016 suppliers · 391,291 records · 20 minutes |
| Differences found | 32,821 records across 4,016 suppliers (3,943 new, 73 changed) |
| Time to compute the difference | Under two minutes, inside the database |
| Time to compute the deployment diff for the pipeline stage | 28 seconds |
| Deployment | More than 9,000 supplier records written to the target in one approved run, resumed twice after deliberate interruptions without re-sending what had landed; writes paced at eight requests per second to protect the pod; records Oracle refused (for example, a federal tax type Oracle will not accept) were reported individually and did not stop the run |

Reads are paged and paced, so a compare of this size is safe to run against a live development or test pod.

---

---

*Nexus is an independent product and is not affiliated with, endorsed by, or sponsored by Oracle. Oracle and Oracle Fusion Cloud are trademarks of Oracle Corporation and its affiliates.*
