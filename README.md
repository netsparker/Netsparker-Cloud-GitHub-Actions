# Netsparker Enterprise Scan

This action requests a scan on [Netsparker Enterprise](https://www.netsparkercloud.com/).

## Inputs

### `website-id`:

**Required** Unique id for your website on Netsparker Enterprise.

### `scan-type`:

**Required** Requested scan type for scan.

### `profile-id`:

**Optional** Unique profile id for your requested website scan profile on Netsparker Enterprise.

### `user-id`:

**Required** User Id on Netsparker Enterprise API Credentials. Use GitHub Secrets.

### `api-token`:

**Required** API Token on Netsparker Enterprise API Credentials. Use GitHub Secrets.

## Outputs

### `scan-message`:

Scan message for requested scan.

## Example Scan Workflow

```yaml
name: Netspaker Enterprise Scan Sample Workflow

on:
  push:
    branches: [ main ]

jobs:
  netspaker_scan_job:
    runs-on: ubuntu-20.04
    steps:
      # Clones action repository
      - name: Checkout action repository
        id: netsparker-enterprise-scan-action
        uses: actions/checkout@v2
        with:
          repository: netsparker/Netsparker-Cloud-GitHub-Actions
          ref: v0.0.1
          path: .
      # Starts actions with given inputs
      - name: Start Netsparker Enterprise Scan
        id: netsparker-enterprise-scan-step
        uses: ./
        with:
          website-id: '******' # FILL HERE
          scan-type: 'FullWithSelectedProfile'
          profile-id: '******' # FILL HERE
          user-id: ${{ secrets.NETSPARKER_USER_ID }}
          api-token: ${{ secrets.NETSPARKER_API_TOKEN }}
      # Displays output for action
      - name: Display Scan Request Message
        run: echo "${{ steps.netsparker-enterprise-scan-step.outputs.scan-message }}"
```