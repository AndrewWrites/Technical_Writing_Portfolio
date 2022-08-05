This is a recreation of the published article. The original can be found [here](https://community.alteryx.com/t5/Alteryx-Designer-Knowledge-Base/Interface-Designer-Part-1-Macros/ta-p/22024).<br><br>

## Interface Designer Part 1 - Macros <br><br>

The Interface Designer is an often missed piece of setting up custom macros. To enable the Interface Designer, go to View - Interface Designer. Note that nothing will show in this window unless your workflow is saved as a .yxmc or .yxwz (macro or analytic app). <br> <br>

**First the basics:**<br>
The Interface Designer has 4 main views, designated by icons running down the left side of the window:
![interface](/Community%20Articles/Screenshots/Interface%20Designer%20-%20Macros/4%20Views.png)

From the top down, the views are:<br>
Layout View - Shows you the interface the end user will see when setting up the tool in their workflow.<br>
Test View - Allows you to enter values for your "Questions" to debug potential errors in the macro or app. <br>
Tree View - If you created macros or apps prior to version 9.0, this will be familiar to you as it is the old way of setting up your questions and actions. <br>
Properties - Allows you to set specific characteristics abotu your macro or app. <br><br>

For this article, we are going to focus on the Layout View, Test View, and Properties.<br><br>

**Layout:**<br>
The layout view is pretty simple. It shows you what the user will see when configuring your macro. From this view you can also reorder your questions or create nested groups depending on the interface tools you are using. You can also add tabs and label boxes for a more custom feel.<br><br>

Use the "Add" dropdown to add a label, group box, or tab to your interface. You can edit the text seen by the user in the standard configuration window.<br>
![add](/Community%20Articles/Screenshots/Interface%20Designer%20-%20Macros/Add_Layout.png)
<br>
Group Box - Adds a box so you can nest questions together<br>
Label - Adds custom text to the interface <br>
Link - Add a URL to a website or a file with a relative path. Webpage must be a full URL.<br>
Tab - Adds a tab to the interface that can be used to split up questions based on sections of a macro.<br><br>

Use the arrows on the right hand side to move the questions up or down, or between the tabs (left and right).<br><br>

**Test:**<br>
The Test view allows you to enter sample values to test the configuration of your macro. You can enter responses to your questions and then enter the Debug mode to ensure your actions are handling the respones correctly.<br>
![open debug](/Community%20Articles/Screenshots/Interface%20Designer%20-%20Macros/OpenDebug.png)
<br>
When you select Open Debug you'll notice that a new workflow opens with a text comment box at the top. If you scroll down you will see your macro tools but will notice the Interface tools ar enot there. Select any tool that an Action is connected to to ensure the value entered in the Test view window has come through properly. If there are any errors, you will see the standard error icon.<br><br>

**Properties:**<br>
The first option in the Properties view for macros is to change the icon. Each tool in Alteryx has it's own icon, and the base color and shape correspond to the category the tool fits in. All of these base icons are available when selecting the Standard Icon option. Use the dropdown to expand the window and scroll through available standard options. <br>
![icon](/Community%20Articles/Screenshots/Interface%20Designer%20-%20Macros/ChangeIcons.png)
<br>
You can also set up a custom icon by selecting that radio button. Using the Custom Icon allows you to either create an image outside of Alteryx, or perhaps us a company logo, to represent your macro. <br><br>

Another common setting used in macros is how the output records will be formatted. The default is expecting that every iteration of output will have the same schema, and Alteryx will throw an error if they are different.<br><br>

If your schema may change based on the data being fed into the macro, select the check box indicating that, and then choose a method to align the fields:<br>
![output](/Community%20Articles/Screenshots/Interface%20Designer%20-%20Macros/OutputOptions.png)
<br>
Similar to the Union tool, you can have your macro auto configure the fields by name or position allowing for greater flexibility with your data. These options can be particularly helpful when using the Dynamic Input tool within your  macro to open multiple files. These settings should allow the macro to continue opening files if the schema changes or if field names are slightly different. <br><br>

The final option in the Properties view is not used nearly as often but allows the user to create a custom Help file or link to be included with the macro. <br><br>

Note: Screenshots taken from version 10.5.
