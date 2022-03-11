
## Testing and databases (Dash)

### Brief description
dash.testing is the offical package available on Dash website for testing dash app in both python and R.  It provides some off-the-rack pytest fixtures and testing APIs, including browser testing APIs and dash APIs.  There is also an open source pytest-dash package but it is deprecated since the release of dash.testing.  As dash.testing is incorporated in dash, it is intended to draft the best practice for intergration test of dash app.

Bascially, dash.testing uses pytest and Selenium Webdriver for simulating the interaction inside a web browser.  We can use pytest fixture and the standard Python assert statements for verifying expectations and values.  With dashr fixture, an instance of Python class providing a reliable framework to execute the app, we can use the same set of testing API calls as in testing Python app.   Visual Regression Testing tool, Percy, is also integrated in dash.testing so that we can test about the graphical aspects of a Dash App and do visual testing with Percy snapshot.

Dash Enterprise enables Dash Apps to use open source libraries to query external databases and datastores in callbacks or job queues.  Dash use standardized Python DB-API (PEP-0249) for database connection and query execution.  As it adopts the standard API, it is easy and straight forward for us to connect to external databases. 

### Long description
#### Testing
For using dash.testing, we need to install dash.testing and webdrivers (or use remote Selenium-grid for testing).  The dash.testing package does not guarantee that the given selenium grid works well so it is useful to change the logging level or customize the browser options for testing.  

A test case is composed of preparation, actions, and checkpoints.  pytest allow us to use the standard Python assert for verifying expectations and values.
Sample codes for prepartion and action
```
start_server(app)
wait_for_text_to_equal("#nully-wrapper", "0", timeout=4)
```
Sample code for checkpoint
```
assert dash_duo.find_element("#nully-wrapper").text == "0"
```

For testing dash app in R.  we need to define a string with a valid path to a .R file and pass it to `start_server`.  After that, we can use dashr fixture, an instance of Python class which provides a reliable framework to execute the app and test one or more of its features via Selenium WebDriver.

#### Database
To connect external database, we need to install the database driver and other system dependency.  After creating and testing the database connection, we can construct SQL query as in python DB-API.  
Sample Coode for connection and query
```
def try_connection():
    try:
        with postgres_engine.connect() as connection:
            stmt = text("SELECT 1")
            connection.execute(stmt)
        print("Connection to database successful.")

    except Exception as e:
        print("Connection to database failed, retrying.")
        raise Exception

t = text("SELECT * FROM users WHERE id=:user_id")
result = pd.read_sql(t, params={'user_id': 12})
```







### Links
* https://dash.plotly.com/testing
* https://dash.plotly.com/dash-enterprise/database-connections
