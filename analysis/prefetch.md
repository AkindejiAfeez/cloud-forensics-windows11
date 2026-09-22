# Windows Registry Analysis

## 1. Overview

The Windows Registry was examined as a persistent source of forensic evidence during the investigation.

The analysis focused on identifying artefacts associated with cloud-storage applications, user accounts and application configuration.

RECmd was used to process and examine exported Registry hives.

---

## 2. OneDrive Registry Artefacts

The investigation examined the following OneDrive Registry location:

```text
Software\Microsoft\OneDrive\Accounts\Personal
This location contained information associated with the OneDrive account and application configuration.

The Registry was therefore considered an important evidence source for establishing the presence and configuration of OneDrive on the Windows endpoint.

**3. Registry Persistence** 

OneDrive-related Registry artefacts remained identifiable following the tested file-deletion and account-sign-out activities.

This finding was significant because the state of cloud-client databases changed following account disconnection, while Registry evidence associated with OneDrive remained available.

4. Account Information

The Registry examination identified information associated with the OneDrive account.

The project also examined information relating to OneDrive sign-in activity, including account-related values.

These artefacts provided persistent endpoint evidence that could be correlated with other sources.

5. Investigative Value

Registry artefacts can contribute evidence relating to:

Cloud-account configuration
Application configuration
Account information
Sign-in activity
Persistence of application traces

Registry evidence can therefore remain useful when cloud-client database information has changed or become unavailable.

6. Correlation

Registry findings were compared with:

Prefetch
Windows Event Logs
OneDrive databases
Google Drive databases
Memory

This cross-source approach reduced reliance on any single artefact.

7. Interpretation

A Registry artefact should not automatically be interpreted as proof that a specific user action occurred.

Interpretation should consider:

The operating-system version
Cloud-client version
User profile
Configuration
Timeline
Supporting evidence

The findings in this repository relate specifically to the controlled environment used during the project.

8. Limitations

Registry artefacts can vary between Windows versions, application versions and configurations.

Future investigations should therefore validate the observed artefacts against the specific endpoint under examination.