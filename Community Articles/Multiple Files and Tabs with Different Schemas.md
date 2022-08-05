This is a recreation of the published article. The original can be found [here](https://community.alteryx.com/t5/Alteryx-Designer-Knowledge-Base/Read-in-Multiple-Excel-Files-with-Multiple-Tabs-that-have/ta-p/51145).

## Read in Multiple Excel Files, with Multiple Tabs that have Different Schemas <br><br>

One of the best things about Alteryx is the ability to read in multiple files very easily and automatically combine them into a single dataset. This becomes a bit trickier when dealing with files that have different schemas or Excel files with multiple tabs. Adding both multiple Excel files, and having the schema change within each tab takes it to another level. <br><br>
If your tabs have the same schema, the article you want to read is [here](https://community.alteryx.com/t5/Alteryx-Designer-Knowledge-Base/How-To-Import-Multiple-Excel-Sheets-or-a-Specific-Excel-Range/ta-p/398220). <br><br>
The way to accomplish the task if the tabs have (or may have) different schemas (field names change depending on the sheet) is to use nested batch macros. I've attached a sample workflow built in 11.0 that demonstrates the process.

![workflow](/Community%20Articles/Screenshots/main%20workflow.png)

In the main workflow pictured above, the Directory Input tool pulls in the file paths of all of the XLSX files in the directory you're pointing to. Note that you may need to redirect this tool in the sample to a directory on your machine.
![macro1](/Community%20Articles/Screenshots/Macro1.png)

Most of the magic happens in the macro pictured above. This macro takes the FullPath field and updates the main Input Data tool to read the first file in the list from the Directory Input. It is configured to read the list of sheet names within that first file, but also to output the full path from the Input Data tool. A new field is formatted in the Formula tool for an acceptable full file path for an Excel file, including the desired sheet name. This final file path is passed into the 2nd macro as the control parameter.

![macro2](/Community%20Articles/Screenshots/Macro2.png)

The second macro is very simple. It takes the file path received from the first macro, updates th Input Data tool, reads in that file and then passes it back to the first macro. It repeats this process once for each sheet in each of the files being passed from the Directory Input tool.<br>

Each batch macro holds the data until each batch is completed and combines it all into one large dataset. <br>

Note: the sample was created in 11.0 and will not open in earlier versions.
