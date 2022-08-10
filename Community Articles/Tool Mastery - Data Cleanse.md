This is a recreation of the published article. The original version can be found [here](https://community.alteryx.com/t5/Alteryx-Designer-Knowledge-Base/Tool-Mastery-Data-Cleansing/ta-p/31753). <br><br>

## Tool Mastery | Data Cleansing <br><br>

**_This article is part of the Tool Mastery Series, a compilation of Knowledge Base contributions to introduce diverse working examples for Designer Tools. Here we'll delve into uses of the Data Cleansing Tool on our way to mastering the Alterxy Designer:_** <br><br>

You've got your long dataset and you want to combine it with another dataset for additional information. Your dataset is nice and clean. Everything is formatted the same, no null values...the whole package. You open up the data to join and right away you see a ton of clean-up that needs to happen: nulls to replace, strings to format appropriately, extra characters, white space, the list goes on. You launch the Designer, and while fast and accurate, you have to set up a new Multi-Field Formula Tool for each situation you need to fix. If only there was a single tool that did it all. <br><br>

If this describes your experiences with dirty data, you're in luck. Take a look at the Data Cleansing Tool in the preparation tool set. This tool, released with v10.5 of the Designer, will allow you to easily:

- Replace nulls
- Modify case
- Remove unwanted characters across any fields you select; string or numeric
- Trim leading and trailing white space

Some of the clean-up options depend on the field type. For instance, when replacing nulls if it's a string field it'll replace it with a blank value whereas if it's numeric it'll return a 0 value. Either way, this should make your data clean-up easier. <br><br>

Better still, this tool is a macro! Macros can be opened to see what's inside (right-click on the tool icon, choose "open macro: Cleanse.yxmc") to see exactly how it's doing its magic. Is there something you have to do with your datasets regularly that this tool doesn't do? Add it! You can add custom functions to this macro so you can keep your one tool clean-up intact. If you do add your own features, be sure to save the macro with a different name so you don't overwrite your existing tool. <br><br>

Take a look at the attached sample workflow (created in 10.5) demonstrating the "old way" and the new way of cleansing data!