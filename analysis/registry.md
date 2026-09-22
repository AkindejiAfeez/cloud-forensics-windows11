# Registry Analysis

## 1. Overview

Windows Registry artefacts were analysed to identify evidence of cloud-storage account usage and application configuration on the Windows 11 endpoint.

The investigation focused particularly on OneDrive-related Registry entries recovered from the `NTUSER.hiv` hive. The Registry was analysed alongside Prefetch, Event Logs, cloud-client databases and memory evidence rather than being interpreted in isolation.

## 2. OneDrive Registry Location

The investigation examined:

```text
Software\Microsoft\OneDrive\Accounts\Personal
```

This location contained account and application information relevant to establishing OneDrive usage on the endpoint.

## 3. Scenario 1 — Active Sync

RECmd analysis of the Scenario 1 `NTUSER.hiv` identified 25 OneDrive-related Registry key hits.

The findings provided a baseline for comparison with the deletion, sign-out and encryption scenarios.

## 4. Scenario 2 — File Deletion

After the test files had been deleted from the local and cloud storage locations, RECmd analysis identified 23 OneDrive-related Registry key hits.

The `Software\Microsoft\OneDrive\Accounts\Personal` location retained information associated with the OneDrive account and local synchronisation configuration.

This demonstrated that Registry evidence of previous cloud-client use remained available after the tested file-deletion procedure.

## 5. Scenario 3 — Account Sign-Out

Following OneDrive unlinking and Google Drive account disconnection, cloud-client database contents were cleared in the tested environment.

However, OneDrive-related Registry information remained available.

This finding demonstrates that the absence of local cloud-client database records should not automatically be interpreted as evidence that the endpoint was never associated with the cloud-storage service.

## 6. Scenario 4 — Encryption

Registry evidence was considered together with memory and Google Drive database evidence during the encryption scenario.

The Registry therefore formed part of the wider evidence-correlation process rather than serving as the sole source for establishing encryption activity.

## 7. Interpretation

The results indicate that OneDrive Registry artefacts can provide persistent evidence of account and application usage across the different endpoint states tested in this project.

The Registry was particularly useful for:

- identifying OneDrive account-related information;
- establishing that the cloud client had been configured on the endpoint;
- comparing evidence before and after file deletion;
- comparing evidence before and after account sign-out; and
- correlating application information with other forensic artefacts.

## 8. Limitations

The Registry findings are specific to the controlled Windows 11 environment used in this investigation.

Registry locations and values may vary according to:

- Windows version;
- OneDrive version;
- account configuration;
- user profile; and
- system state.

The persistence observed in these scenarios should therefore not be treated as a guarantee that identical Registry evidence will exist on every Windows endpoint.
