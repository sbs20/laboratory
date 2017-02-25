# Upgrading an evaluation licence

If the old ISO or DVD has gone missing then download an evaluation
version of the operating system and upgrade. [Instructions from
here](https://social.technet.microsoft.com/Forums/windows/en-US/4211c642-b15d-49ea-8124-f0628aa0f92e/activate-windows-server-2012-evaluation-standard-version-with-a-product-key-oem?forum=winserver8gen)

**This assumes that you have a legitimate key already**

Open an elevated command prompt...

`DISM /online /Get-CurrentEdition`

Response should be something like

`ServerStandardEval`

Then run this but replacing <EDITION_ID>

`DISM /online /Set-Edition:<EDITION_ID> /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula`

e.g.

`DISM /online /Set-Edition:ServerStandard /ProductKey:XXXXX-XXXXX-XXXXX-XXXXX-XXXXX /AcceptEula`

