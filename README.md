# Editable-Reports-with-Power-Apps
This is an instructional repository of how to enable the ability edit data in Power BI report using Power Apps.

##Introduction
There is a new feature in Power BI where I can add a Power App to the Power BI report canvas and if I follow specific steps, I can use the Power App to edit the content on the specific record of the Power BI report that I have highlighted. 

The published instructions are found here [Power Apps visual for Power BI](https://docs.microsoft.com/en-us/power-apps/maker/canvas-apps/powerapps-custom-visual).   However, I found that they are not entirely accurate.  Thus, I created this repository to walk through the steps I used to get it to work as expected.

Overall, I think this is a really great solution once you understand how to implement it.  Below are my findings as a result of walking through an example of querying an Azure SQL database via Direct Query in Power BI and then using the Power App to update the data behind the report and then perform a refresh on the report data.

For this example, I am using the SalesLT.Products table from the AdventureWorksLT database.

##Setting up the Report.

1. The first step is to ensure that you setup a DirectQuery to your data source. Below is a screenshot of my connection.
![picture alt](/images/Direct%20Query%20Connection.gif)



