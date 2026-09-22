# Artefact Matrix

## 1. Purpose

This matrix summarises the principal artefact sources examined during the four controlled scenarios.

## 2. Comparative Artefact Matrix

| Artefact source | Scenario 1 — Active Sync | Scenario 2 — File Deletion | Scenario 3 — Account Sign-Out | Scenario 4 — Encryption |
|---|---|---|---|---|
| OneDrive Registry account keys | Recovered — 25 key hits | Recovered — 23 key hits | Recovered | Recovered — 25 key hits |
| OneDrive database records | Recovered | Recovered, including deletion-related information | Empty in tested environment | Recovered |
| Google Drive database records | Recovered | Recovered, including MD5 information | Empty in tested environment | Recovered, including VeraCrypt installer information |
| Memory — cloud processes | N/A — Scenario 1 RAM could not be analysed | Recovered | Recovered | Recovered |
| Memory — encryption software | N/A | N/A | N/A | `VeraCrypt.exe` and `veracrypt.sys` recovered |
| Prefetch — cloud-client execution | Recovered | Recovered | Recovered | Recovered; VeraCrypt execution also considered |
| Windows Event Logs | Processed | Processed | Processed | Processed |
| Primary evidential contribution | Baseline cloud activity | Persistence after deletion | Persistence after sign-out | Encryption activity and cross-source correlation |

## 3. Interpretation

Different scenarios produced different combinations of recoverable evidence.

Registry evidence was particularly persistent across the tested conditions, whereas local cloud-client database evidence was dependent on account state.

Memory provided important additional evidence in the encryption scenario.

## 4. Investigative Implication

The results support a multi-source forensic methodology.

Where one artefact source is unavailable or has been cleared, investigators can examine other endpoint sources such as Registry, Prefetch, Event Logs, memory and remaining cloud-client metadata.

## 5. Scope

The matrix summarises observations from the controlled experiments performed for this project. It should not be treated as a universal artefact-presence matrix for all Windows systems or all versions of OneDrive and Google Drive.
