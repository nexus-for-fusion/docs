# Getting started: a proof of concept in one to two hours

A proof of concept needs two Oracle Fusion Cloud environments (two development pods, or a development and a test pod), and about one to two hours.

## What you need

- **Two Oracle Fusion Cloud environments** you may write to, for example DEV1 and DEV2. Nexus reads from one and writes to the other.
- **An integration user in each pod** with access to the services you want to move: Setup & Maintenance export/import for configuration, and the supplier or lookup REST services for master data.
- **A machine with Docker** (a laptop or a small VM): 8 GB of RAM, 20 GB of disk, outbound HTTPS access to your pods.
- **A trial licence key**, valid for 30 days from first start, which we send on request.

## Option A: run it locally with Docker (recommended for a PoC)

1. Download the Docker Compose file we send with your licence key. It starts three containers: the database (PostgreSQL), the Nexus service and the Nexus web app. Images are pulled from our registry.
2. Put your licence key in the `.env` file next to it.
3. Start it:

   ```bash
   docker compose up -d
   ```

4. Open `http://localhost:3000`, sign in as `admin` with the password from the welcome mail, and set a new password.
5. Under **Admin → Registry → Environments**, register your two pods: URL, a name, and the integration user's credentials. **Test connection** confirms Nexus can reach each one. Credentials are stored outside the database.
6. Under **Admin → Registry → Modules**, create a module: pick a functional area for configuration, or the supplier or lookup objects for master data.
7. Under **Admin → Registry → Pipeline templates**, activate a route from your source pod to your target pod.
8. Go to the **Workspace**, start a hotfix on that route, pick a few records, review, approve, and watch them land. Validate the stage.

## Option B: hosted by us

We run Nexus for you as a private tenant: your own URL, your own database schema, your credentials in a managed secrets vault, and nothing shared with other clients. You provide the two pods and the integration users; we provide the tenant and the onboarding call.

## Option C: in your own cloud

Nexus ships as two container images and a set of Kubernetes manifests. It runs on PostgreSQL, MySQL or Oracle Autonomous Database, and reads credentials from your secrets manager.

## The onboarding hour

| When | What | Who |
|---|---|---|
| 0 to 15 min | Start the containers, sign in, change the admin password | You |
| 15 to 35 min | Register the two environments and test the connections | You, with the integration user details |
| 35 to 50 min | Create a module and activate a route | You, guided by us on a call if you like |
| 50 to 80 min | First hotfix: pick records, review, approve, deploy, validate | Together |
| After | Schedule discovery, add roles and approvers, try a configuration module | You |


---

---

*Nexus is an independent product and is not affiliated with, endorsed by, or sponsored by Oracle. Oracle and Oracle Fusion Cloud are trademarks of Oracle Corporation and its affiliates.*
