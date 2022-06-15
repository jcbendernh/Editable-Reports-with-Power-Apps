# Editable-Reports-with-Power-Apps
This is an instructional repository of how to enable the ability edit data in Power BI report using Power Apps.  

## Introduction
There is a new feature in Power BI where I can add a Power App to the Power BI report canvas and if I follow specific steps, I can use the Power App within the report to edit the content on the specific record of the report that I have highlighted. 

The published instructions are found here [Power Apps visual for Power BI](https://docs.microsoft.com/en-us/power-apps/maker/canvas-apps/powerapps-custom-visual).   However, I found that they are not entirely accurate.  Thus, I created this repository to walk through the steps I used to get it to work as expected.

Overall, I think this is a really great solution once you understand how to implement it.  Below are my findings as a result of walking through an example of querying an Azure SQL database via Direct Query in Power BI and then using the Power App to update the data behind the report and then perform a refresh on the report data.

For this example, I am using the SalesLT.Products table from the AdventureWorksLT Azure SQL database.

## Setting up the Report.

1. The first step is to ensure that you setup a DirectQuery to your data source. Below is a screenshot of my connection.

    ![picture alt](/images/Direct%20Query%20Connection.gif)

2. Next I created my table and ensured to add the unique value / primary key.  In this case it is ProductNumber.

    ![picture alt](/images/Power%20BI%20Table.gif)

## Adding and Configuring the Canvas App.

3. Next we will need to add the Canvas App to the Power BI Report, to do so click the Insert Tab | Power Apps Button.

    ![picture alt](/images/Insert%20Power%20Apps.gif)

4. Once the Power Apps control is added to the canvas, please add the unique value / primary key in the PowerApps Data field and click the Create New button and then click accept any popups to get you to the Power Apps Studio in the browser.

    ![picture alt](/images/PowerApps%20Data%20Value.gif)

5. Once in the Power Apps studio, it will create the form for you with a Gallery control. This is where the crux of the problem lies, you cannot use the Gallery to modify fields and submit their changes.  You must use a Form control and then embed your fields in the form along with a submit button.  To do so, perform the following steps...

6. Resize the gallery control on your Screen1 in the Power App to only take up the heading of the screen.  I resized it to the Height of 129 pixels.  

    ![picture alt](/images/Gallery%20Heaight.gif)

7. Next we will need to add a Power App connection to our data source so that the Power App can update the fields as necessary.  It is important to understand this connection is independent of the Power BI datasource you created earlier.   Later on we will tie the two together via a Power BI specific command.  Expand the hamburger in the upper left and click on Data and the Add data button.

    ![picture alt](/images/Power%20Apps%20Add%20Data.gif)

8.  Under select a data source, expand Connectors and select SQL Server.  Next click Add a Connection to input your SQL Server connection information including server and database names and click Connect 

    ![picture alt](/images/Choose%20a%20dataset.gif)

Notice that the SQL server connection requires a Power Apps premium license.  Any connector that has a diamond next to it will require a Power Apps premium license.  For more on this topic see [Connector reference overview](https://docs.microsoft.com/en-us/connectors/connector-reference/).

9. On the next screen, select your table and click Connect.  When finished you should see your connection under Data.

    ![picture alt](/images/New%20Data%20Connection.gif)

10. Next insert an Edit Form on Screen1 of the Canvas app and place it so it slightly overlaps the gallery.  For positioning, I gave it a Y value of 58 and connected the Data Source to my new Data Source.

11. Next click Edit Fields to add the fields you would like to utilize on your form.

12. Next we need to tie the Gallery1 value to the Form1 value.  To do so, lets modify the following values on the Advanced Tab of Gallery1. <br>
    OnSelect  `Navigate(Form1, ScreenTransition.None)` <br>
    Items  `LookUp(<data source>,<data source unique value>=First(PowerBIIntegration.Data).<power BI unique value>)`<br>
    For instance I used `LookUp('SalesLT.Product',ProductNumber=First(PowerBIIntegration.Data).ProductNumber)`<br>

    ![picture alt](/images/Gallery%20Advanced%20Values.gif)

13. Next modify the following values on the Advanced Tab of Form1.  <br>
    Item  `Gallery1.Selected` <br>
    Once this is set, you should start to see values in your fields that correspond to the record highlighted.<br>

    ![picture alt](/images/Form%20Advanced%20Values.gif)

14.  Last of all, we need to add a submit button and give it a command.  To do so, make sure FOrm1 is highlighed and goto the toolbar and click Insert | Button.  For the button properties, set the following on the advanced tab <br>
    OnSelect  `SubmitForm(Form1);PowerBIIntegration.Refresh()` <br>
    Text  `"Submit"`  <br>
    ![picture alt](/images/Submit%20Button.gif)

15.  Now Save your Power App to the The Cloud and close out of the Power App studio.

16.  If you Power App does not show up in the Power BI Canvas, delete the Power App control, repeat step 4 above but this time select Choose App and select your Power App that you just created.  It should now show in the report.  
    ![picture alt](/images/Finished%20Report.gif)

However it may not automatically refresh the report in the desktop when you click Submit, you may have to manually refresh in the desktop.  Once the report is published to the Power BI Web Service.  You should see the automatic refresh.
















