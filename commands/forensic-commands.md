# Forensic Commands

This document records the command-line and database-analysis commands used as part of the investigation methodology.

Machine-specific information, personal identifiers, local usernames, and evidence-specific paths have been removed or replaced with placeholders for public repository use.

---

# 1. Volatility 3 — Memory Analysis

Volatility 3 was used to analyse authorised Windows memory images acquired during the investigation.

## 1.1 Identify the Operating System

```powershell
python vol.py -f <MEMORY_IMAGE> windows.info
```

Replace `<MEMORY_IMAGE>` with the path to the authorised memory image.

This command was used to obtain information about the operating system represented in the memory image.

---

## 1.2 List Running Processes

```powershell
python vol.py -f <MEMORY_IMAGE> windows.pslist
```

This command was used to identify processes represented in memory.

Process information was particularly relevant to the investigation of cloud-storage applications and encrypted-storage software.

---

## 1.3 Examine Network Information

```powershell
python vol.py -f <MEMORY_IMAGE> windows.netstat
```

This command was used to examine network-related information available within the memory image.

The output can provide additional context when investigating network activity associated with applications running on the endpoint.

---

## 1.4 Examine Process Command Lines

```powershell
python vol.py -f <MEMORY_IMAGE> windows.cmdline
```

This command was used to examine command-line information associated with processes recovered from memory.

---

## 1.5 Examine Loaded Modules

```powershell
python vol.py -f <MEMORY_IMAGE> windows.modules
```

This command was used to examine loaded modules represented within the memory image.

This was particularly relevant to the encrypted-storage scenario.

---

# 2. RECmd — Windows Registry Analysis

RECmd was used to examine exported Windows Registry hives.

The analysis focused on Registry artefacts associated with Windows users and cloud-storage applications.

## 2.1 Process a Registry Hive

A representative RECmd command is:

```powershell
RECmd.exe -f <REGISTRY_HIVE> --bn <BATCH_FILE> --csv <OUTPUT_DIRECTORY>
```

Replace `<REGISTRY_HIVE>` with the exported Registry hive.

Replace `<BATCH_FILE>` with the appropriate RECmd batch file.

Replace `<OUTPUT_DIRECTORY>` with the authorised analysis output directory.

---

## 2.2 OneDrive Registry Location

The investigation examined the following OneDrive Registry location:

```text
Software\Microsoft\OneDrive\Accounts\Personal
```

This location was examined for information relating to the OneDrive account and application configuration.

---

# 3. PECmd — Windows Prefetch Analysis

PECmd was used to process Windows Prefetch files.

## 3.1 Process Prefetch Files

```powershell
PECmd.exe -d <PREFETCH_DIRECTORY> --csv <OUTPUT_DIRECTORY>
```

Replace `<PREFETCH_DIRECTORY>` with the directory containing the exported Prefetch files.

Replace `<OUTPUT_DIRECTORY>` with the desired analysis output directory.

---

## 3.2 Applications Examined

Prefetch analysis considered application execution evidence associated with:

```text
OneDrive
Google Drive
VeraCrypt
```

The resulting output was used as part of the wider cross-source investigation.

---

# 4. EvtxECmd — Windows Event Log Analysis

EvtxECmd was used to process Windows Event Log files.

## 4.1 Process Event Logs

```powershell
EvtxECmd.exe -d <EVTX_DIRECTORY> --csv <OUTPUT_DIRECTORY>
```

Replace `<EVTX_DIRECTORY>` with the directory containing the exported Event Log files.

Replace `<OUTPUT_DIRECTORY>` with the desired output directory.

---

## 4.2 Event Categories Examined

The investigation considered Event Log information associated with:

```text
4624 — Successful logon
4688 — Process creation
7045 — Service installation
```

These events were considered as supporting evidence for establishing system and temporal context.

---

# 5. SQLite Database Analysis

Cloud-client databases were examined using DB Browser for SQLite.

The investigation examined application databases associated with OneDrive and Google Drive.

## 5.1 OneDrive Database Structures

The following OneDrive database structures were examined:

```text
od_ClientFile_Records
od_ScopeInfo_Records
od_ServiceOperationHistory
od_ClientFolder_Records
```

These structures were examined for information relating to synchronisation and file activity.

---

## 5.2 Google Drive Database Structures

The following Google Drive database structures were examined:

```text
item_properties
mirror_sqlite
metrics_store_sqlite
```

The structures were examined for information associated with cloud-storage activity and metadata.

---

# 6. Registry Analysis Workflow

The Registry investigation followed the general process:

```text
Export Registry hive
        ↓
Preserve exported evidence
        ↓
Process using RECmd
        ↓
Identify relevant Registry locations
        ↓
Examine account and application information
        ↓
Correlate with other evidence sources
```

---

# 7. Prefetch Analysis Workflow

The Prefetch investigation followed the general process:

```text
Preserve Prefetch files
        ↓
Process using PECmd
        ↓
Identify relevant applications
        ↓
Examine execution information
        ↓
Compare with other forensic evidence
```

---

# 8. Event Log Analysis Workflow

The Event Log investigation followed the general process:

```text
Preserve Event Logs
        ↓
Process using EvtxECmd
        ↓
Identify relevant events
        ↓
Establish temporal context
        ↓
Correlate with other artefacts
```

---

# 9. Memory Analysis Workflow

The memory investigation followed the general process:

```text
Acquire RAM
        ↓
Preserve memory image
        ↓
Identify operating system
        ↓
Analyse processes
        ↓
Analyse network information
        ↓
Analyse command lines
        ↓
Analyse loaded modules
        ↓
Correlate findings
```

---

# 10. SQLite Analysis Workflow

The cloud-client database investigation followed the general process:

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
Compare with other evidence
        ↓
Document findings
```

---

# 11. Evidence Correlation

The command-line and database outputs were not interpreted independently.

Results were correlated across:

- Windows Registry
- Prefetch
- Windows Event Logs
- OneDrive databases
- Google Drive databases
- Memory

The purpose of correlation was to establish relationships between application activity, system activity and cloud-storage activity.

---

# 12. Public Repository Safety

The following evidence must not be committed to the public repository:

- Memory dumps
- Full forensic disk images
- Virtual-machine disk images
- Personal cloud-storage files
- Passwords
- Authentication tokens
- Cookies
- Private keys
- Student records
- University credentials
- Personal or unnecessary usernames
- Unredacted forensic exports
- Other confidential investigation material

Only sanitised commands, documentation and appropriately redacted screenshots should be published.

---

# 13. Reproducibility

The commands documented in this file are intended to describe the investigation methodology used in the project.

Exact output may differ according to:

- Windows version
- Application version
- User profile
- System configuration
- Evidence state
- Forensic tool version

The commands should therefore be treated as part of a reproducible investigative methodology rather than as a guarantee of identical results on another system.
