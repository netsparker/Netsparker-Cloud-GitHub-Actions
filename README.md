# Netsparker Enterprise Scan

This action requests a scan on [Netsparker Enterprise](https://www.netsparkercloud.com/).

## Inputs

### `website-id`:

**Required** Unique Id for your website on Netsparker Enterprise.

### `scan-type`:

**Required** Requested scan type for scan.

### `profile-id`:

**Optional** Unique profile Id for your requested website scan profile on Netsparker Enterprise.

### `user-id`:

**Required** User Id on Netsparker Enterprise API Credentials. Use GitHub Secrets.

### `api-token`:

**Required** API Token on Netsparker Enterprise API Credentials. Use GitHub Secrets.

### `base-url`:

**Optional** Website URL for Netsparker Enterprise.

### `wait-for-completion`:

**Optional** Fail the build if one of the selected scan severity is detected.

### `fail-on-level`:

**Optional** Severity filter. Options : 

DoNotFail : Do not fail the build

Critical  : Critical

Critical,High : High or above 

Critical,High,Medium : Medium or above

Critical,High,Medium,Low : Low or above

Critical,High,Medium,Low,Best Practice : Best Practices or above

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
      # Starts actions with given inputs
      - name: Start Netsparker Enterprise Scan
        id: netsparker-enterprise-scan-step
        uses: netsparker/Netsparker-Cloud-GitHub-Actions@v0.2.2
        with:
          website-id: '******' # FILL HERE
          scan-type: 'FullWithSelectedProfile'
          profile-id: '******' # FILL HERE
          user-id: ${{ secrets.NETSPARKER_USER_ID }}
          api-token: ${{ secrets.NETSPARKER_API_TOKEN }}
          base-url: 'https://www.netsparkercloud.com'
          wait-for-completion: false
          fail-on-level: 'DoNotFail'
      # Displays output for action
      - name: Display Scan Request Message
        run: echo "${{ steps.netsparker-enterprise-scan-step.outputs.scan-message }}" >> $GITHUB_OUTPUT
```
