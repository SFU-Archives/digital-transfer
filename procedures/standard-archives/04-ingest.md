###### [Digital Transfer](../../README.md) > [Standard Transfer: Procedures for Archives](00-introduction.md)
###### [1. Pre-Transfer](01-pre-transfer.md) `|` [2. Transfer](02-transfer.md) `|` [3. Validation](03-validation.md) `|` 4. Ingest `|` [5. Completion](05-completion.md)

# 4. Ingest
###### Status: draft
<img align="right" width="350" src="../../screenshots/04-ingest.png">

Ingest is the process of putting validated transfer packages into the Archives' repository using Archivematica. You also run AIS scripts to import metadata from the transfer's `bag-info` file into the Accession record and generate accession forms and notices.

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

By whatever method, you must have permissions to access the Archives' VMs, i.e. your email address is on the mail-list that control access.
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
- Enter the `Transfer name` using the same convention used when saving the validated bag in[step 3.7 above](03-ingest.md#37-edit-save-the-transfer-package) – `ACNYYYY-NNN_Creator_Descriptor`, e.g. "ACN2021-100_SFUGeography_CommitteeFiles".
- Enter the `Accession number` without the `ACN` prefix, e.g. "2020-021".
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
- "Fatal" errors will cause Archivematica to cancel the ingest process; consult with other staff and Artefactual support as needed to resolve these on a case-by-case basis.

<br clear="all"/>

## 4.3 Import Bag data to AIS Accession record
<img align="right" width="400" src="../../screenshots/04-import-bag.png">

Use the `bag-info.txt` file from the validated transfer package to populate the AIS Accession record that you created previously in [step 2.2](#22-create-an-accession-record) to generate an `Accession number`.

Launch the import script from the AIS:
- Open the AIS Archives module.
- Go to the **Home > Accessions > Actions** tab.
- Click the `Import Bag metadata` link.
- You will be prompted to select a folder: **always select the top-level folder of the bag** (e.g. `ACN2021-100_SFUGeography_CommitteeFiles`).
- You can also launch the same import script from the Accession record itself, from the **Reports tab** > `Import SFU MoveIt bag` link.

The AIS routes you to a **Data Entry: SFU MoveIt Transfer** screen to review / verify / correct imported data and add other descriptive information as required.
- See the GitHub site for [AIS documentation](https://github.com/SFU-Arhives/ais-database) for detailed guidance on the fields in the [Accession records](https://github.com/SFU-Arhives/ais-database/blob/master/modules/archives/accession.md).
- The following notes highlight specifics relevant to the accessioning of digital transfers.

### Transfer tab

### Contact tab

### Description tab

### Scope and content tab

### Dates tab

### Management tab

### AIP tab



<br clear="all"/>

## 4.4 Output AIS forms and notices
<img align="right" width="400" src="../../screenshots/04-forms-notices.png">

<br clear="all"/>

###### Last updated: Jan 11, 2021
###### [< Previous: 4. Ingest](04-ingest.md) `|` [Next: 5. Completion >](#05-completion.md)
