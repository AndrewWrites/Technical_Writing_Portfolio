This is a recreation of the published article. The original can be found [here](https://community.alteryx.com/t5/Alteryx-Designer-Knowledge-Base/Interface-Designer-Part-2-Analtyic-Apps/ta-p/22031).<br><br>

## Interface Designer Part 2 - Analytic Apps<br><br>

This is part 2 of my Interface Designer series. Click [here](https://community.alteryx.com/t5/Alteryx-Designer-Knowledge-Base/Interface-Designer-Part-1-Macros/ta-p/22024) for part 1 (Macros and the basics):<br><br>

This article will focus on the options specific to Analytic Apps. The majority of the Interface Designer options are the same for apps and macros including the Layout, Test, and Tree views.<br><br>

One feature to point out that is very handy for analytic apps can be found in the Test view window. When testing your app using the debug option, a cool feature is the ability to save your test values so that you can quickly bring them back later without having to re-enter them every time. In the App Values section on the right-hand side of the Test view, you'll see the option to Reset, Save, Open, and View:<br>
![appvalues](/Community%20Articles/Screenshots/Interface%20Designer%20-%20Apps/SaveValues.png)
<br>
Enter your test values and select Save to write a file locally with the values you're using. The next time you want to test, simply select Open and point to the file to save yourself some time. <br><br>

**Properties:**<br>
The main difference in the Interface Designer between macros and apps will be found in the Properties view.<br>
![properties](/Community%20Articles/Screenshots/Interface%20Designer%20-%20Apps/App_Properties.png)
<br>
The first difference is the option to have the app run a second app when it completes. This is a chained app where you just specify the name of the second app and it will automatically call it when the first app completes. This allows you to set up a process to format a file and then run the analysis.<br><br>

You'll also see an option to have the app return results to the user. This is helpful when running apps on the Gallery so the user can see their results. When you select the box for "On Success - Show Results to User", you can select the output tools (Output Data and Render tools for Gallery runs) to return the results for saving. <br><br>

You can create custom output messages and upload an image to display in the interface itself. Images are for desktop only, and will not show up when the app runs in the Gallery.