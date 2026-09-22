# Cross-Scenario Findings

## 1. Overview

The investigation used four controlled scenarios:

1. Active Sync
2. File Deletion
3. Account Sign-Out
4. Encryption Simulation

The scenarios were compared across Registry, cloud-client databases, memory and Prefetch evidence.

## 2. Scenario 1 — Active Sync

Scenario 1 established the baseline condition.

The investigation recovered OneDrive Registry information, OneDrive database records, Google Drive database records and Prefetch evidence.

RECmd identified 25 OneDrive-related Registry key hits.

## 3. Scenario 2 — File Deletion

The principal findings were:

- 23 OneDrive-related Registry key hits remained;
- OneDrive database records remained and included deletion-related information;
- Google Drive `mirror_sqlite` retained MD5 checksum information;
- cloud-client processes were identifiable in memory; and
- Prefetch evidence supported cloud-client execution.

The results demonstrate that deletion of the visible files did not result in complete removal of all tested endpoint artefacts.

## 4. Scenario 3 — Account Sign-Out

The principal findings were:

- OneDrive and Google Drive local databases were empty or contained no file-level records;
- OneDrive Registry information remained; and
- OneDrive.exe and GoogleDriveFS.exe were still identified in the Scenario 3 RAM capture.

This demonstrates that clearing or absence of a cloud-client database does not necessarily remove all evidence of previous cloud-service use.

## 5. Scenario 4 — Encryption Simulation

The principal findings were:

- `VeraCrypt.exe` was identified in memory;
- `veracrypt.sys` was identified in memory;
- Google Drive database records contained information associated with the VeraCrypt installer; and
- cloud-storage artefacts provided evidence of activity preceding the encryption stage.

The combination of memory and database evidence supported reconstruction of the sequence more fully than either source alone.

## 6. Cross-Source Correlation

Evidence was correlated across:

```text
Registry
   +
Prefetch
   +
Windows Event Logs
   +
OneDrive databases
   +
Google Drive databases
   +
Memory
```

This approach enabled application activity, file activity and encryption-related activity to be considered together.

## 7. Main Findings

### 7.1 Registry persistence

OneDrive Registry information remained available across the deletion and sign-out conditions tested.

### 7.2 Database persistence is scenario-dependent

Cloud-client database records were available after deletion in the tested environment but were cleared or empty after account sign-out.

### 7.3 Metadata can survive file deletion

Google Drive `mirror_sqlite` retained MD5 checksum information after the tested file-deletion procedure.

### 7.4 Memory can provide volatile encryption evidence

Scenario 4 demonstrated that memory analysis can identify encryption software after the encrypted container had been dismounted.

### 7.5 Multiple artefact sources improve reconstruction

Registry, database, Prefetch and memory evidence were considered together to reconstruct activity across the scenarios.

## 8. Relationship to the Investigation Framework

The cross-scenario findings informed the thirteen-stage investigation framework developed by the project.

The results support an investigative workflow that prioritises preservation and acquisition before analysis and then combines multiple endpoint artefact sources.

## 9. Scope of Findings

These findings are based on controlled experiments conducted in the Windows 11 environment used for the project.

They should not be interpreted as a guarantee that identical artefacts will be present on every Windows endpoint.
