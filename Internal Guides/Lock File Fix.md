## **Error: Database connection failed**

**Purpose**
This document explains how to troubleshoot the following error in Alteryx Server:

ERROR: Connection failed, please ensure server address and credentials are correct

**Cause**

This is a common error that you might see in the event of an unclean server shutdown. Most of the time this error occurs when the database does not shut down properly and the lock file does not get released. This prevents the database from starting the next time the Service is initiated and returns the error.

The error will display when trying to start the Service from the command line. A log file (LastStartUpError.txt) is written any time the service does not start properly. The location of this file can be found in System Settings on the Controller - General page in the Logging section. This file will contain the error text as shown below:

![Screenshot](/Internal%20Guides/Screenshots/LockFile.png)

**Initial Troubleshooting**
Follow the steps below to determine if the lock file is the cause:

1. Find where the database is installed from the Persistence screen in System Settings.
2. Open a Windows Folder Browse and navigate to the location where the database is installed.
3. Check to see if the database.lock file has a file size of anything other than 0kb.

If the lock file has a file size of 0kb, skip to the Additional Troubleshooting section.
If the lock file has a file size greater than 0kb, continue to the next section.

**Resolution**
This section details the steps necessary to resolve the error and test to make sure everything is working properly. We recommend that you backup the server instance before proceeding to protect against corruption.

Follow these steps to reset the lock file:

1. Delete the lock file.
2. Right-click in the directory and select **New - Text Document**
3. Check to make sure **Show File Extensions** is turned on.
4. Rename the new document to database.lock, making sure to remove the .txt extension.
5. Open a Windows Command Prompt and navigate to the \Software\bin directory:

    `cd \Program Files\Software\bin`
6. Start the database service to confirm it loads successfully

    `database --dbpath "directory path from System Settings" --auth --port 27018`
7. Wait for the line that says "Waiting for connections on port 27018".
8. Press Ctrl + c to shut down the database service.
9. Start up the Software service in the command prompt.

    `sc start service`
10. Check the **Task Manager - Processes** to verify the service is running.

**Additional Troubleshooting**
If the lock file was not the problem, follow the steps below to determine the cause:

1. Open a Windows Command Prompt and navigate to the \Alteryx\bin directory.
    `cd \Program Files\Software\bin`
2. Run the command `Service test` to determine the error.

If you are still unable to determine the cause of the error, collect the service log files for further investigation. The location of the logs can be found in System Settings on the Controller - General page.
