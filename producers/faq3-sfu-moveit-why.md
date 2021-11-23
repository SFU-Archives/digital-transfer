###### [Digital Transfer](../README.md) `|` [Procedures for Producers](procedures.md) `|` [FAQs](faqs.md)
###### SFU MoveIt

# Why should I use SFU  MoveIt?
SFU MoveIt offers four main advantages over basic upload / copying of unpackaged files.

### 1. SFU MoveIt is based on standards
SFU MoveIt creates standardized transfer packages that implement the BagIt specification, ensuring that transfers are consistent and predictable in structure, regardless of content.

### 2. SFU MoveIt generates checksums.
SFU MoveIt creates a **checksum** for each file packaged. A checksum is an alpha-numeric value calculated by an algorithm applied to the file's underlying bitstream (the string of 0s and 1s). It functions as a kind of "digital fingerprint": any change to the bitstream will generate a completely different checksum when the same algorithm is applied. This enables the Archives to validate transfers by comparing the files' pre- and post-transfer checksums. In this way we can identify any files that suffered corruption or data loss during transmission and request users to re-send them.

(3) Preserves timestamps. SFU MoveIt preserves the original timestamps (date created and date modified) of the files included in the packages. This is useful metadata that would be lost if you simply copy / upload files to the deposit folder on SFU Vault.

(4) Incorporates user-supplied metadata. The information provided by users about the transfer is important contextual information, valuable for the long-term management of the materials and for their future understandability and use. SFU MoveIt retains the metadata within the transfer package itself so that it is carried forward with the records through their subsequent life in the digital preservation system.

SFU MoveIt is an open-source tool and may be freely adapted. For download (app or source code), visit the app's release page on GitHub. The latest version (2.0.6) was released in December 2020 and is available for both Windows and Mac OS.

The Windows version requires Windows 10.
The Mac version was designed and mainly tested in Mac 10.16; it requires minimum 10.14, though some users have reported difficulities using it with that operating system.

###### Last updated: Nov 19, 2021
