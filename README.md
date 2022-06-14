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









