
## Testing and databases (Dash)
### Brief description

dash.testing is available for testing dash app in both python and R.  It provides some off-the-rack pytest fixtures and testing APIs, including browser testing APIs and dash APIs.
Bascially, dash.testing uses pytest and Selenium Webdriver for simulating the interaction inside a web browser.  We can use pytest fixture and the standard Python assert for verifying expectations and values.  For R, we can use dashr fixture which an instance of Python class for testing dash in R.  Visual Regression Testing tool, Percy, is also integrated in dash.testing so that we can test about the graphical aspects of a Dash App and do visual testing with Percy snapshot.

Dash Enterprise enables Dash Apps to use open source libraries to query external databases and datastores in callbacks or job queues.  Dash use standardized Python DB-API (PEP-0249) for database connection and query execution.  
Install the database driver and other dependency
Create connection and construct SQL query as in pythong DB-API


### Long description

To complete

### Links
* https://dash.plotly.com/testing
* https://dash.plotly.com/dash-enterprise/database-connections
