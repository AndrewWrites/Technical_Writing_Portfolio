This is a recreation of the published article. The original can be found [here](https://community.alteryx.com/t5/Alteryx-Server-Knowledge-Base/Query-Scheduler-Database-from-Alteryx/ta-p/10534).<br><br>

## Query Scheduler Database from Alteryx<br><br>

**Is it possible to query the data on the "View Schedules" tab of the scheduler?**<br><br>

This question has come up a few times recently and the answer is yes. The method depends on whether you are using MongoDB (Server) or SQLite(Designer + Scheduler).<br><br>

**Let's go over MongoDB (Server) first:**<br><br>

First you'll need some information from you System Settings (Controller - Persistence section):<br>
![SystemSettings](/Community%20Articles/Screenshots/Querey%20Scheduler%20database/SystemSettings.jpg)
<br><br>

You'll need the Host information, Username, and Password. You'll see 2 options for password; Admin and regular. For this you want to use the regular password which can be copied and pasted into the connector.<br><br>

Once you have this information, configure the MongoDB Input tool (Connectors tool set):<br>
![MongoInput](/Community%20Articles/Screenshots/Querey%20Scheduler%20database/MongoDBInput.jpg)
<br><br>
The "Host" information goes in the Server input. Username and Password go in their respective boxes. The database you need to query is AlteryxService.<br><br>

The Collection dropdown should auto populate with the tables you can pull from, however, you may need to run the workflow once to refresh the list. Note that you will get an error stating that Database and Collection must be specified. <br><br>

Once you've established your connection, you can use the rest of the tool configurations to set up any other information you want such as record limits:<br>
![recordlimits](/Community%20Articles/Screenshots/Querey%20Scheduler%20database/BottomMongoDB.jpg)
<br>

You can find more infomration on the specifics of these options in the help file by selecting the ? icon in the tool configuration. <br><br>

**Next we'll go over how to connect using SQLite (Designer + Scheduler):**<br><br>

For this option it's pretty stragith forward. You'll use your standard Input Data tool.<br><br>

Browse to:<br>
ProgramData\Alteryx\Service\Persistence\AS_Schedules<br><br>

The fiel you are looking for is called "_TheData.sqlite".<br>
![inputdata](/Community%20Articles/Screenshots/Querey%20Scheduler%20database/SQLite_Method.jpg)
<br><br>

**Parse the data:**<br>

With both methods, you'll get a variety of infomration back including computer name,  username, run dates, etc. There will also be a field called "ServiceData" that is a blob field with a binary object. This field contains additional information about the record you are viewing and can easily be parsed using the ServiceDataParser macro attached below.<br><br>

The ServiceDataParser.yxmc was created by Kory Cunningham, and is necessary to make use of the additional field. The original macro is included in the Gallery Usage Report App available on the [downloads page](http://downloads.alteryx.com). <br>
Note that in some cases you may encounter an error when trying to use the macro that states "This tool is not licensed". This happens because the macro uses a generic tool that some older licenses don't enable. If you come across this error, reach out to our Fulfillment team to obtain an appropriate license.<br><br>

**Pull it all together:**<br>
The final step here is to join the information from the various Mngo tables back together (if pulling from multiple tables). The key table for this process is the Queue table (AS_Queue) as it holds all of the IDs necessary to join back to the other tables (AS_Results, AS_Schedules, AS_Applications) in order to get all the data together.<br><br>

 You'll need multiple joins to make this work as outlined below:<br>
 1. Join the Schedules table to the Queue table using the AS_Application_ID field.
 2. Join the results of Step 1 to the AS_Results table using the AS_Queue_ID field.
 3. Join the results of Step 2 to the AS_Applications table using the AS_Application_ID field and the Mongo_id field (from Mongo Input tool).<br>
Note that in order to use the Mongo_id,  you'll need to parse it out to remove the unneeded infomration. You can do this using a simple RegEx expression within the RegEx tool:<br>
`."(.*)".*` <br>

I've also attached a sample workflow detailing this process. Note that the workflow probably won't run until you update the credentials to match your own as it is set up for my instance of Mongo. You can use the workflow as a template for your own connections.<br><br>

If you want to take this process a step further, take a look at this [article](https://community.alteryx.com/t5/Alteryx-Designer-Knowledge-Base/Extract-Scheduler-Data-with-Alteryx-Macro/ta-p/32531). It will show you how to use an Alteryx macro to accomplish this (downloadable from the Gallery) and also includes a link to show you how to build a Tableau dashboard to make the infomration easier to consume! <br><br>

All screen shots and directions are taken from Alteryx version 10.1.6.<br><br>

**Update for 11.0 release**<br>
In 11.0, the option to schedule workflows from the Gallery was added. I've updated the sample workflow to show how to bring those in and identify them separately. There's a bit of extra parsing necessary. Take a look at the "PullFromMongo_Updated_v11.yxzp" file attached.