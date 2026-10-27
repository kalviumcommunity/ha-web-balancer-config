# CloudNotes Web Balancer Brief

CloudNotes runs behind one global HTTP(S) load balancer. The load balancer sends traffic to a managed instance group named `cloudnotes-mig`. Each VM runs the CloudNotes app on port 8080.

## Intended design

1. **Health checks.** The health check calls the app's health endpoint, `/health`, on port 8080. The app returns HTTP 200 there. A VM that fails the check is taken out of rotation.
2. **High availability.** The backend group is regional in `us-central1` and spreads its VMs across three zones: `us-central1-a`, `us-central1-b`, and `us-central1-c`. A zone failure must not take CloudNotes down.
3. **HTTPS only.** Port 80 is a redirect-only front door. Every HTTP request gets a `301` redirect to HTTPS. No user is served plain HTTP.

## Files

| File | What it holds |
|---|---|
| `health-check.txt` | Health check for the CloudNotes backend |
| `backend-group.txt` | Backend service and its instance group |
| `http-redirect.txt` | URL map and redirect for port 80 |

## Rules for students

- Edit only the three files above. Do not edit this README.
- Keep every name, port, and region unchanged, except where a fix needs a change.
- No paid tool, no cloud account, no install. Edit the text files in the browser.
