# Repository Dispatch Receiver

This repository listens for incoming `repository_dispatch` events from other repositories (such as `repo-dispatch-sender`) and runs a workflow when they occur.

---

## Workflow File

**Location:** `.github/workflows/on-dispatch.yaml`

```yaml
name: Handle Test Dispatch

on:
  repository_dispatch:
    types: [test-dispatch]
  workflow_dispatch:  # Optional for manual testing

jobs:
  log:
    runs-on: ubuntu-latest
    steps:
      - name: Print payload info
        run: |
          echo "Received dispatch from: ${{ github.event.client_payload.repo }}"
          echo "Version: ${{ github.event.client_payload.version }}"
```

---

## What Triggers This?

This workflow runs when it receives a `repository_dispatch` event with the `event-type: test-dispatch`.

It will also show up in the Actions UI if manually triggered.

---

## Requirements

No secrets or tokens are needed in this repository.

But  **external workflows are allowed** should be ensured:

### GitHub Actions Settings

1. Go to `Settings → Actions → General`
2. Ensure the following are enabled:
   - ✅ “Allow all actions and reusable workflows”
   - ✅ “Allow workflows from outside collaborators/repositories”

---

## Manual Testing

It is possibel to trigger the workflow manually from the Actions tab:

1. Go to **Actions → Handle Test Dispatch**
2. Click **Run workflow**
3. It will print:
   ```
   Received dispatch from: ...
   Version: ...
   ```

---

## Expected Output

When triggered by a dispatch, the log will show:

```
Received dispatch from: <gitub-username>/repo-dispatch-sender
Version: v1.2.3
```


