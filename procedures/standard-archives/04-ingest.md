###### [Digital Transfer](../../README.md) > [Standard Transfer: Procedures for Archives](00-introduction.md)
###### [1. Pre-Transfer](01-pre-transfer.md) `|` [2. Transfer](02-transfer.md) `|` [3. Validation](03-validation.md) `|` 4. Ingest `|` [5. Completion](05-completion.md)

# 4. Ingest
###### Status: draft
<img align="right" width="350" src="../../screenshots/04-ingest.png">

Ingest is the process of putting validated transfer packages into the Archives' repository using Archivematica. You also run AIS scripts to import metadata from the transfer's `bag-info` file to populate the Accession record and generate accession forms and notices.

## Steps
- [4.1 Upload transfer package to staging server](#41-upload-transfer-package-to-staging-server)
- [4.2 Ingest to Archivematica backlog](#42-ingest-to-archivematica-backlog)
- [4.3 Import Bag data to AIS Accession record](#43-import-bag-data-to-ais-accession-record)
- [4.4 Output AIS forms and notices](#44-output-ais-forms-and-notices)

<br clear="all"/>

## 4.1 Upload transfer package to staging server
Upload the validated transfer package to the Archives' `pine` VM at `/var/transfersoure`. This directory can be accessed by Archivematica for ingest.

You can upload the package by various methods, but whichever you choose **must be able to preserve the original timestamps of the files**, i.e. timestamps must not be overwritten with the date / time of copying.
- The most reliable method to ensure this is the command-line utility [rsync](https://github.com/SFU-Archives/digital-repository-utilities/blob/master/utilities/rsync.md), described below.
- You can, however, use an FTP client if you set its preferences to preserve timestamps.
- In Cyberduck, go to Preferences > Transfers > Timestamps > Uploads; check `Preserve modification dates`.
- You can also specify that Cyberduck verifies checksums on upload, though it is not clear that this in fact works.

By whatever method, you must have permissions to access the Archives' VMs, i.e. your email address must be included on the mail-list that controls access.
- Consult with RD to be added to the access list.

To run rsync via command line in Terminal:

```
$ rsync -vhrlt --progress <<file_path_to_package>> <<user>>@pine.archives.sfu.ca:/var/transfersource`.
```

Note that you will be prompted to enter your SFU computing password.

Flags:
- -v = verbose.
- -h = human-readable output.
- -r = recursive (copies all sub-folders and their contents).
- -l = symlinks.
- -t = timestamps.
- --progress (shows progress in Terminal window).

After copying is complete, connect to `pine` via Cyberduck to confirm that upload was successful and timestamps preserved.

## 4.2 Ingest to Archivematica backlog
<img align="right" width="400" src="../../screenshots/04-archivematica.png">

Log on to Archivematica and ingest the transfer package to backlog.
- Use the `aspen` pipeline for most standard transfers of textual records and related materials.
- Reserve the `alder` pipeline for transfers of large files, e.g. typically video and audio materials.

On the `Transfer` tab:
- Select `Transfer type` = "Unzipped bag".
- Enter the `Transfer name` using the naming convention `ACNYYYY-NNN_Creator_Descriptor`, "ACN2021-100_SFUGeography_CommitteeFiles" (should be the same as the name of the validated transfer package created in [step 3.7](03-validation.md#37-edit-save-the-transfer-package)) above).
- Enter the `Accession number` without the `ACN` prefix, e.g. "2021-100".
- Leave `Access system ID` blank.
- Check `Automatically approve`.
- Use the `Browse` button to navigate to and select the transfer package you uploaded to `pine` at [step 4.1 above](#41-upload-transfer-package-to-staging-server); click the `Add` button.
- Click the `Start transfer` button.

As Archivematica processes the transfer, you will be prompted at three decision-points to select an option:
- `Perform file format identification (Transfer)` = "Yes – Siegfried".
- `Examine contents` = "Yes".
- `Create SIP` = "Send to backlog".

At the end of the process, go to the Archivematica `Backlog` tab to verify completion.

Archivematica will sometimes encounter errors (and throw error messages) during processing.
- "Non-fatal" errors can stand, e.g. failure to identify the file format of a particular file; but these should be noted in the Accession record (see section 5.2 below).
- "Fatal" errors will cause Archivematica to quit the ingest process; consult with other staff and Artefactual support as needed to resolve these on a case-by-case basis.

<br clear="all"/>

## 4.3 Import Bag data to AIS Accession record
<img align="right" width="400" src="../../screenshots/04-import-confirm.png">

Use the `bag-info.txt` file from the validated transfer package to populate the AIS Accession record that you created previously when generating an `Accession number` in [step 2.2](02-transfer.md#22-create-an-accession-record).

Before importing the bag data, make sure that a fonds and authority record for the creator already exist in the AIS.

Launch the import script from the AIS:
- Open the AIS Archives module.
- On the **Home > Accessions > Actions** tab, click the `Import Bag metadata` link.
- You will be prompted to select a folder: **always select the top-level folder of the bag** (e.g. `ACN2021-100_SFUGeography_CommitteeFiles`).
- You can also run the script by navigating to the Accession record > **Reports** tab; click the `Image SFU MoveIt bag` link.

The AIS will prompt you to confirm that the `Accession number` entered in the `bag-info` file matches an Accession record in the AIS.
- Values will mis-match if you launched the import script from the wrong Accession record in the AIS or if you entered the wrong number in Bagger when adding validation metadata to the bag.
- Confirm, or enter the correct `Accession number` as required.

The AIS imports the bag data and routes you to a **Data Entry** screen to review / verify the data and add other descriptive information as required.
- All fields that have a red arrow next to them should be completed; the rest are optional.
- Other optional note fields can be accessed by buttons (e.g. `+ Add note on provenance`).
- See the [AIS documentation site](https://github.com/SFU-Archives/ais-database) for guidance on all fields in [AIS Accession records](https://github.com/SFU-Arhives/ais-database/blob/master/modules/archives/accession.md); the following notes highlight specifics relevant to the accessioning of digital transfers.

<br clear="all"/>

### Transfer tab
<img align="right" width="400" src="../../screenshots/04-import-edit.png">

Update the default `Accession title` ("SFU MoveIt transfer") with something more descriptive.
- To use the transfer name supplied by the contact (displayed immediately above), click the `Use bag database` button.

The shaded `Records creator` field shows the value that was supplied by the contact in the bag.
- Link the accession to the `Creator's AIS authority record` by selecting their name from the drop-down list.
- Link the accession to the creator's AIS fonds record by selecting / entering the `Fonds reference code`.
- The authority and fonds records must already exist; if you need to create them, click the `Cancel` button, create the records, then re-run the bag import script.

### Contact tab
The contact's information as supplied in the bag is displayed in the shaded fields.
- Select the contact's name from the `Contact ID` field to link the transfer to the contact's existing AIS authority record.
- If the contact's supplied information (e.g. `Position / Job title`) or `Email address`) differs from the information on the authority record, you can update the authority record by clicking the `Use bag info` button on any given field; but if the authority record information is more accurate, leave as is.

If the contact's name does not appear in the drop-down list in the `Contact ID` field, create a new AIS authority record for the contact.
- Link the contact to a department / organization.
- Click the `Add new` button next to the contact's name to create an authority record.

### Description tab
The `Date range` field is based on the data the contact submitted with the bag.
- If you know it is not accurate, enter the correct information here.

The `Bag size` field is calculated from the actual size of the transfer.

### Scope and content tab
The `Scope and content` note field combines the descriptive information supplied by the contact in the bag and that added by the archivist during validation (displayed in shaded fields here).
- Edit as required for the Accession record.

### Dates tab
These fields record dates of events in the workflow: bagging and transfer (by the contact) and ingest (by the archivist).
- The `Bagging date` is generated by SFU MoveIt on package creation.
- To set the `Transfer date` to the `Bagging date` click the `Use same` button; or enter it manually if these are known to be different.
- The `Ingest date` and `Staff responsible` values default to the current date and staff name; correct if needed.

### Management tab
Flag any known privacy, copyright, or long-term preservation issues.

### AIP tab
Assuming you have already ingested the transfer to Archivematica backlog ([step 4.2 above](#42-ingest-to-archivematica-backlog), click the `Create AIP` button to register the backlog package in the AIS.
- The AIS `AIP` table tracks both fully processed AIPs as well as packages stored in backlog.

### Submit data
Click the `Submit` button to complete data entry



<br clear="all"/>

## 4.4 Output AIS forms and notices
<img align="right" width="400" src="../../screenshots/04-forms-notices.png">

<br clear="all"/>

###### Last updated: Jan 11, 2021
###### [< Previous: 4. Ingest](04-ingest.md) `|` [Next: 5. Completion >](#05-completion.md)
