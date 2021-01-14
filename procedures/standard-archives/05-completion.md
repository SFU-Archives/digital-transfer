###### [Digital Transfer](../../README.md) > [Standard Transfer: Procedures for Archives](00-introduction.md)
###### [1. Pre-Transfer](01-pre-transfer.md) `|` [2. Transfer](02-transfer.md) `|` [3. Validation](03-validation.md) `|` [4. Ingest](04-ingest.md) `|` 5. Completion

# 5. Completion
<img align="right" width="400" src="../../screenshots/05-transfer-completed-notice.png">

Completion entails notifying the producer contact that the transfer has been processed, filing transfer documentation, and cleaning up (deleting) transitory copies of the transfer package.

## Steps
- [5.1 Send Transfer Completed Notice](#51-send-transfer-completed-notice)
- [5.2 File transfer documentation](#52-file-transfer-documentation)
- [5.3 Delete transitory copies](#53-delete-transitory-copies)

<br clear="all"/>

## 5.1 Send Transfer Completed Notice
Notify the producer contact that the transfer has been completed.
- Find the transfer notice (pdf) and a text template for the covering email in the `~/Desktop/DigitalTransfers/<<accession_number>>` folder.

The `Digital Transfer Completed Notice` includes the full list of files included in the transfer.
- Note that this file list is generated from the Bag `manifest` file; it is not stored or retained in the AIS Accession record.

The covering email instructs the contact to delete their own copies of the files they transferred.
- This is typically appropriate for most transfers of university records.
- It may or may not be appropriate for transfers of privately donated records.
- Use your judgment to customize the email message to circumstances of the transfer as needed.

## 5.2 File transfer documentation
File The `Accession Record Form` (full version) on the fonds collection file (paper).
- Find the pdf copy in the `~/Desktop/DigitalTranfers/<<accession_number>>` folder.

File the analysis reports created by the FileAnalysis utility in [validation step 3.7](03-validation.md##35-create-analysis-reports) on the colleciton file (paper or electronic).
- Alternatively you can upload the reports (e.g. as a zip file) to the AIS Accession record at the **Documentation** tab.
- SFU Archives has not yet settled on where best to maintain this documentation.

File any substantive correspondence with the producer relating to the transfer (e.g. validation issues) on the collection file.

## 5.3 Delete transitory copies
Delete the various copies of the transfer package made during the transfer process:
- The copy the producer uploaded to the SFU Vault deposit folder ([step 2.1](02-transfer.md#21-receive-notice-of-a-deposit)).
- The copy you downloaded from the deposit folder for inspection and analysis ([step 2.3](02-transfer.md#23-download-the-transfer-package)).
- The validated package you made with Bagger following validation ([step 3.7](03-validation.md#37-edit-save-the-transfer-package).
- The copy of the validated package you uploaded to `pine` for Archivematica ingest ([step 4.1](04-ingest#41-upload-transfer-package-to-staging-server)).

On Archivematica delete the job entries from the **Transfer** and **Ingest** tabs.

###### Last updated: Jan 13, 2021
###### [< Previous: 4. Ingest](04-ingest.md)
