
## Tableau - Documentation & Reproducibility

Mention all the official documentation resources. (2) Are there ways to run the dashboard in a reproducible way locally (ie., creating a package?, Docker? Binder? Nothing is said about it?) Provide links/examples if you find that it is possible.

### Brief description

There are 3 main ways to use tableau: Tableau Desktop, Tableau Online, and Tableau Server.

For Tableau Desktop, it is possible to save a dashboard as a "packaged workbook". Packaged workbooks contain the workbook along with a copy of any local file data sources and background images. In this way, the workbook is no longer linked to the original data sources and images. Packaged workbooks are saved as a single file with a .twbx file extension. Anyone with the file has access to the full dashboard via Tableau Desktop.

It is also possible to publish workbooks and data to the web. This will allow people in your organization to view, interact with, download, edit, and save published views, even if they do not use Tableau Desktop. One feature of Tableau is that it is possible to publish workbook's and data to the web individually. For example, if you wanted to just make your dataset available to others, you could publish your data to the web, and allow others to create Tableau workbooks using that data. One thing to note with this approach, is that everyone is essentially sharing the same data source, and therefore any changes to the data would be reflected in any workbook that references it.

### Long description

There are 3 main ways to use tableau: Tableau Desktop, Tableau Online, and Tableau Server.

For Tableau Desktop, it is possible to save a dashboard as a "packaged workbook". Packaged workbooks contain the workbook along with a copy of any local file data sources and background images. In this way, the workbook is no longer linked to the original data sources and images. Packaged workbooks are saved as a single file with a .twbx file extension. Anyone with the file has access to the full dashboard via Tableau Desktop.

It is also possible to publish workbooks and data to the web. This will allow people in your organization to view, interact with, download, edit, and save published views, even if they do not use Tableau Desktop. One feature of Tableau is that it is possible to publish workbook's and data to the web individually. For example, if you wanted to just make your dataset available to others, you could publish your data to the web, and allow others to create Tableau workbooks using that data. One thing to note with this approach, is that everyone is essentially sharing the same data source, and therefore any changes to the data would be reflected in any workbook that references it.

Here are the official steps for publishing a tableau workbook online: <https://help.tableau.com/current/pro/desktop/en-us/publish_workbooks_howto.html>

If you find a packaged Tableau workbook online that you would like to work on locally, you just have to download the .twbx file and "Unpackage" the workbook.

On a Windows or macOS computer, rename the file with a .zip extension (for example, from myfile.twbx to myfile.zip) and then double-click it.

When you unpackage a workbook, you get a regular workbook file (.twb), along with a folder that contains the data sources and images that were packaged with the workbook.


### Links

Some useful links can be found below:

-   [Learn Tableau](https://www.tableau.com/learn)
-   [Official Documentation](https://www.tableau.com/support/help)
-   [How to Publish a Workbook](https://help.tableau.com/current/pro/desktop/en-us/publish_workbooks_howto.html)
