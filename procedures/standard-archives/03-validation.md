###### [Digital Transfer](../../README.md) > [Standard Transfer: Procedures for Archives](00-introduction.md)
###### [1. Pre-Transfer](01-pre-transfer.md) `|` [2. Transfer](02-transfer.md) `|` 3. Validation `|` [4. Ingest](04-ingest.md) `|` [5. Completion](05-completion.md)

# 3. Validation
###### Status: under development
<img align="right" width="350" src="../../screenshots/03-validation.png">

Validation is the process of deciding whether or not to accept the transfer into the repository. It verifies that the transfer package complies with the BagIt specification, that no data was lost or corrupted during transmission, and that transfer contents meet expectations and are suitable for long-term preservation.

The analysis undertaken during validation also provides descriptive data that should be captured in the Accession record for later use during arrangement and description.

## Steps
- [3.1 Scan for viruses](#31-scan-for-viruses)
- [3.2 Validate bag](#32-validate-bag)
- [3.3 Document directory structure](#33-document-directory-structure)
- [3.4 Analyze files](#34-analyze-files)
- 3.5 Create analysis reports (FileAnalysis utility)
- 3.6 Accept or reject the transfer
- 3.7 Edit / save the transfer package
- 3.8 Update the Accession record (AIS)
- [Transfer Validation Checklist](../../downloads/checklist-validation.pdf)

This phase begins after you have downloaded the transfer package to your desktop ([step 2.3](03-validation#23-download-the-transfer-package)).

Before you start:
- Unzip the package.
- Create a project folder on your desktop for the various reports that will be created.

<br clear="all"/>

## 3.1 Scan for viruses
<img align="right" width="400" src="../../screenshots/03-clam-av.png">

Use [ClamAV](https://github.com/SFU-Archives/digital-repository-utilities/blob/master/utilities/clamav.md) to check the transfer package for viruses and other malware.

Run ClamAV via the command line in Terminal.
- Refresh the virus definitions database: `$ freshclam`
- Scan the transfer package: `$ clamscan -ri --log=<<log_file_path.txt>> <<transfer_folder>>`

The `log` flag means `clamscan` will output a `scan log` text file to the file path specified.
- The `-r` flag = "recursive": the scan will include all sub-directories in the transfer folders.
- The `-i` flag = "infected": the log will only print files that are infected, plus summary data.

If infected files are found:
- Confirm that you can safely delete the files and delete them.
- Make a note in the Accession record (e.g. in the Events section).
- Retain the `scan log` on the collection file as documentation.
- Follow up with the producer to make them aware that they have virus issues.

For more information about ClamAV (installation and use): [Digital Repository Utilities > ClamAV](https://github.com/SFU-Archives/digital-repository-utilities/blob/master/utilities/clamav.md).

## 3.2 Validate bag
<img align="right" width="400" src="../../screenshots/03-bagger.png">

Use Bagger to verify that the transfer package is a properly formed "bag" (complies with the BagIt specification) and that no data was lost or corrupted during deposit (the files' pre- and post-transfer checksums match).

To launch Bagger:
- Navigate to its install location (e.g. `Applications/bagger-2.8.1`.
- In the `bin` directory, double-click the `bagger` file.
- The Bagger interface opens; you may get a warning message in Terminal, but this can be disregarded.

To validate the transfer package:
- Click the `Open Existing Bag` button and navigate to the (unzipped) transfer package.
- Click the `Is Bag Complete` button to verify the structure of the package; you should get an `OK` popup.
- Click the `Validate Bag` button to verify the checksums; again you should get an `OK` popup.

If the transfer package fails validation:
- Determine the reason (structure incomplete or checksum fail).
- Consult with the producer, ask them to re-package their transfer and / or re-deposit.

You can also use Bagger to view the descriptive metadata provided by the producer through SFU MoveIt.
- In the transfer package, this producer-supplied metadata is contained in the `bag-info.txt` file.
- This information is useful [in making the validation decision to accept or reject the transfer](#36-accept-or-reject-the-transfer).

For more information about Bagger (installation and use): Digital Repository Utilities > Bagger (forthcoming).

## 3.3 Document directory structure
<img align="right" width="400" src="../../screenshots/03-tree.png">

Use Tree to capture the original directory structure of the transfer as a text representation. This provides an overview of the transfer and supports later appraisal, arrangement, and description.

Run Tree via the command line in Terminal: `$ tree -d -o <<file_path_for_output_report>> <<path_to_target_folder>>``
- The `-d` flag means Tree will list only directories; omit to show all contents down to the file level if desired.
- The `-o` flag = output a text report to the specified location (include the file name with `.txt` extenion, e.g. `tree.txt`).

For more information about Tree (installation and use): [Digital Repository Utilities > Tree](https://github.com/SFU-Archives/digital-repository-utilities/blob/master/utilities/tree.md).

## 3.4 Analyze files
<img align="right" width="400" src="../../screenshots/03-brunnhilde.png">

<img align="right" width="400" src="../../screenshots/03-brunnhilde-output.png">

Use Brunnhilde to generate reports that analyze the files and file formats included in the transfer.

Start Brunnhilde via the command line in Terminal: `$ python3 <<path_to_Brunnhilde_application_folder/main.py`
- The easiest way is to type `python3 `, then drag the `main.py` file into Terminal and hit `Return`.
- This will open the Brunnhilde interface.

In Brunnhilde:
- Make sure you **do not** run a virus scan (already done with ClamAV in step 3.2 above) – uncheck these boxes on the `Options` tab.
- Use the `Directory` tab to specify the transfer package as the `Source` – make sure the transfer package has been unzipped.
- Specify a project folder (e.g. on your deskotp) as the `Destination` for Brunnhilde output reports.
- Enter the `Accession number` (created in step 2.x), e.g. `ACN2021-100`; Brunnhilde will use this as the name of the folder for the output reports.
- Click the `Start scan` button: the `Status` field will show scan in progress.
- Depending on the size of the transfer, it may take several minutes to complete.

Brunnhilde generates an html and a number of csv reports to folder named by
- Open the `report.html` file in any web browser to view all output.
- Step 3.5 below imports the Brunnhilde csv data into a FileMaker database to facilitate viewing and working with the data, as well as creating printer-friendly reports.

For more information about Brunnhilde (installation and use): Digital Repository Utilities > Brunnhilde (forthcoming).

## 3.5 Create analysis reports
<img align="right" width="400" src="../../screenshots/03-analysis-reports.png">

Use the FileAnalysis utility, a custom FileMaker database, to work more easily with the Brunnhilde output data.
- Download a copy of the utility to your desktop project folder from the ARMD shared drive at `ITM002-40 > ArchivalProcessingUtilities`; if you'd like you can rename the file with a more descriptive name.

Open FileAnalysis and work through the five tabs.
- The screen sidebars give more detailed instructions.
- On `Tab 1. Import data`, upload the Brunnhilde csv files, copy and paste Tree output (created in [step 3.3 above](#33-document-directory-structure)), copy and paste the file paths of any infected files reported by ClamAv in [step 3.1](#31-scan-for-viruses).
- On `Tab 4. Create reports`, view summary results, navigate to the various Brunnhilde reports on a list screen (where data can be searched or sorted), create print or pdf reports.

The data and reports are useful for getting an overview of transfer contents, e.g.
- View the folder directory structure.
- Get a statistical analysis of file format groups.
- Identify problematic, unexpected, or unidentified file formats.
- Get the date range of the materials based on the `Last modified` time-stamps (though you must determine whether these are reliable or not).
- Identify duplicate files included in the transfer.

This information is useful for both validation ([decide whether or not to accept the transfer](#36-accept-or-reject-the-transfer)) and description ([when updating the Accession record](#38-update-the-accession-record)).

For more detailed documentation and guidance on use, see: Digital Repository Utilities > File Analysis utility (forthcoming).

## 3.6 Accept or reject the transfer
<img align="right" width="400" src="../../screenshots/03-validation-checklist.png">

Use the [Validation checklist](../../downloads/checklist-validation.pdf) with the information you have gathered to determine whether or not to accept the transfer for ingest.

The [Validation checklist](../../downloads/checklist-validation.pdf) identifies various tests to apply to the transfer, and it suggests the actions you should take in the event of a fail.
- Not all (in fact very few) "fails" require you to outright reject a transfer, but they point to issues that may need further analysis or follow-up for clarification with the producer.

## 3.7 Edit / save the transfer package
<img align="right" width="400" src="../../screenshots/03-edit-bag.png">

If you accept the transfer ("validates successfully"), use Bagger to add validation metadata to the transfer package. This means saving it as a new package.

To add metadata:
- Open the transfer package in Bagger ([see step 3.2 above](#32-validate-bag)).
- Add / edit the fields in Bagger's `Bag Info` panel; note that fields may be displayed in random order.
- `Internal-Sender-Identifier`: enter the Accession number in form YYYY-NNN (**do not include the ACN prefix**).
- `Internal-Sender-Description`: enter your own scope and content note if needed to elaborate / correct the producer's description (found in the `External-Sender-Description` field).
- `Internal-Validation-Date`: add the date of the validation decision in form YYYY-MM-NN.
- `Internal-Validation-By`: add the name of the archivist responsible for validation.
- `Internal-Validation-Note`: add any notes relating to the decision, e.g. validation test fails and how they were handled; can be left blank.

Click the `Save Bag As` button to save the transfer package as a new Bag.
- In the dialog box, click the `Save in > Browse` button to specify a new location and enter the new package name.
- Use the following naming convention: `ACNYYYY-NNN_Creator_Descriptor`; e.g. `ACN2021-100_SFUGeography_CommitteeFiles`.
- Leave the `Holey bag` box unchecked.
- Check both `Generate ... manifest` boxes and use "SHA256" as the `manifest algorithm`.
- Click the `OK` button.

## 3.8 Update the Accession record
<img align="right" width="400" src="../../screenshots/03-update-accession.png">

Update the AIS Accession record by importing the `bag-info.txt` file from the edited transfer packaged into the AIS.
- This will populate the Accession record with the metadata in the Bag.

In the AIS, navigate to the Accession record.


###### Last updated: Jan 7, 2021
###### [< Previous: Transfer](02-transfer.md) `|` [Next: 4. Ingest](04-ingest.md)
