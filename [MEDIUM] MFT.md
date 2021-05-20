**MFT**
===================  
[Challenge Link](https://hubchallenges.s3-eu-west-1.amazonaws.com/Forensics/MFT)

> An incident handler has acquired a MFT file from NTFS partition from an employee workstation  which is suspected to steal excel file sheets so , can you help.

From the description I knew that we need to parse this MFT file as I am learner, we know that we have couple of tools which can parse, but I prefer to wotk with [Eric Zimmerman's tools](https://ericzimmerman.github.io/#!index.md) 
 
 | Tool | Version | Description |
| --- | --- | --- |
| `MFTECmd` | [0.5.1.0](https://f001.backblazeb2.com/file/EricZimmermanTools/MFTECmd.zip) |  $MFT, $Boot, $J, $SDS, and $LogFile (coming soon) parser. Handles locked files |
| `MFTExplorer` | [1.4.0.0](https://f001.backblazeb2.com/file/EricZimmermanTools/MFTExplorer.zip) |  Graphical $MFT viewer |
 
 AboutDFIR (https://aboutdfir.com/toolsandartifacts/windows/mft-explorer-mftecmd/) has great turotial which may help you to find the flag for current challenge
 
I parsed the file with it.

![](images/mft.png)

I was looking for an excel file so I searched the output for **.xlsx**, the excel files extension.  
I found a file with a base64-encoded name.. I decoded it and got the flag. 
