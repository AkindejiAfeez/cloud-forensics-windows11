# SQLite Database Analysis

## 1. Overview

Local cloud-client SQLite databases were examined to identify evidence of cloud-storage activity, file synchronisation, account activity and metadata.

DB Browser for SQLite was used to inspect the relevant databases and tables.

The databases were analysed together with Registry, Prefetch, Event Log and memory evidence.

## 2. OneDrive SyncEngineDatabase

The investigation examined the OneDrive `SyncEngineDatabase.db` database.

Relevant structures included:

```text
od_ClientFile_Records
od_ScopeInfo_Records
od_ServiceOperationHistory
od_ClientFolder_Records
```

These structures were examined for information relating to synchronised files, OneDrive scope and account information, service operations and synchronised folders.

## 3. Scenario 1 — Active Sync

The Scenario 1 OneDrive database contained records associated with the five test files and synchronisation activity.

The database therefore provided a baseline for comparison with the later deletion and sign-out scenarios.

## 4. Scenario 2 — File Deletion

After the test files had been deleted, OneDrive database records remained available in the tested environment.

The project records file records containing deletion-related information, including `serverDeleted` flags.

Google Drive `mirror_sqlite` also retained MD5 checksum information for deleted test files.

## 5. Scenario 3 — Account Sign-Out

Following OneDrive unlinking and Google Drive account disconnection, the tested cloud-client databases were empty or contained no file-level records.

This contrasted with the continued presence of relevant OneDrive Registry information.

The result demonstrates why database absence should be interpreted together with other endpoint artefacts rather than used as a standalone conclusion.

## 6. Google Drive Databases

Relevant structures included:

```text
item_properties
mirror_sqlite
metrics_store_sqlite
```

These databases were examined for file metadata, timestamps, checksums and application/account activity.

## 7. Google Drive — Scenario 4

Google Drive database analysis identified an entry for the VeraCrypt installer:

```text
VeraCrypt Setup 1.26.29.exe
```

The dissertation records the MD5 value:

```text
1d4b1e8a958ee8354c3e66a17bc2a177
```

and file size:

```text
40,832,408 bytes
```

This database evidence was correlated with the Scenario 4 memory evidence identifying `VeraCrypt.exe` and `veracrypt.sys`.

## 8. Analysis Workflow

```text
Locate cloud-client database
        ↓
Preserve database
        ↓
Open database using DB Browser for SQLite
        ↓
Identify relevant tables
        ↓
Examine records and metadata
        ↓
Compare results across scenarios
        ↓
Correlate with other forensic sources
        ↓
Document findings
```

## 9. Interpretation

The database results demonstrate that local cloud-client databases can preserve useful information about synchronisation and file activity.

However, database contents were not persistent in every scenario. In particular, the tested account sign-out procedure resulted in empty local databases.

The results therefore support a multi-source forensic approach.

## 10. Limitations

SQLite database structures and stored records may vary according to cloud-client version, Windows version, account state, synchronisation state, application configuration and actions performed before acquisition.

The structures documented here should therefore be treated as findings from the tested environment rather than universal database specifications.
