## Shiny: Testing and databases

(1) List packages or other technologies used for testing the app. Is this a common practice for this technology?
(2) Is it easy to connect external databases? Mention resources about how to do that.

### Brief description

Testing is essential to all the applications and code that we develop, including Shiny app. Two testing packages are frequently used for Shiny testing in R that are [`testthat`](https://testthat.r-lib.org/) and [`Shinytest`](https://shiny.rstudio.com/articles/testing-overview.html).  

Shiny supports both local and remote connection to the storage database. By default, Shiny supports to save and load data files such as CSV to the local server. It's possible to load data to and export from the Shiny app including relational databases. There are majorly seven methods for storing persistent data remotely with a Shiny app: [local file system](https://shiny.rstudio.com/articles/persistent-data-storage.html#local), [Dropbox](https://shiny.rstudio.com/articles/persistent-data-storage.html#dropbox), [Amazon S3](https://shiny.rstudio.com/articles/persistent-data-storage.html#s3), [SQLite](https://shiny.rstudio.com/articles/persistent-data-storage.html#sqlite), [MySQL](https://shiny.rstudio.com/articles/persistent-data-storage.html#mysql), [Google Sheets](https://shiny.rstudio.com/articles/persistent-data-storage.html#gsheets), and [MongoDB](https://shiny.rstudio.com/articles/persistent-data-storage.html#mongodb).

### Long description

#### Shiny: Testing

The packages `testthat` and `shinytest` are required for the test presented for Shiny and could be installed with install.packages(). `shinytest` has the class `ShinyDriver` (see `?ShinyDriver`) which opens the Shiny app in a new R-Session as well as an instance of [PhantomJS](http://phantomjs.org/). Produced by developers of RStudio, [`Shinytest`](https://shiny.rstudio.com/articles/testing-overview.html) offers three principal classes of tests:
1. Unit tests: These are used to test that functions behave as expected.
2. Server function tests: By running the server function of a Shiny application to simulate a real client session, these tests can be used to test reactive components, and outputs in the server function of your Shiny app.
3. Snapshot-based tests: While your Shiny application is run in a headless web browser, user actions - such as clicking on buttons and setting inputs to particular values - are simulated. These tests then take snapshots of the state of the application and references those snapshots when evaluating the state of a future iteration of the application.

There are a handful of testing packages that can be implemented in Shiny apps; below are two of the most common ones. Below is a minimal example of a Shiny app (app.R) to be tested. Using the expectation functions of the package testthat it is thus easily possible to test the functions of the Shiny app. An advantage of this is that when calling `devtools::test()` both the tests of the Shiny app and other unit tests are taken into account.

```{r}
library(shinytest)
library(testthat)

context("Test Shiny app")

# open Shiny app and PhantomJS
app <- ShinyDriver$new("<path to app.R>")

test_that("output is correct", {
  # set num_input to 30
  app$setInputs(num_input = 30)
  # get text_out
  output <- app$getValue(name = "text_out")
  # test
  expect_equal(output, "The square of the number n is: n² = 900")  
})

# stop the Shiny app
app$stop()
```

#### Shiny: Database Connection
Connecting Shiny applications to a data source requires no additional platform-specific database connection implementation strategy. Simply using the `DBI` package allows R developers to connect their Shiny application to all the most frequently used Database Management Systems. Connecting your Shiny application to a data layer can be accomplished in different ways depending on what architecture is used to store application data. The most common data source connections can be made using the [`DBI`](https://dbi.r-dbi.org/) package. Persistent storage lets you do more with your Shiny apps. You can even use persistent storage to access and write to remote data sets that would otherwise be too big to manipulate in R.

The following table can serve as a reminder of the different storage types and when to use them. Remember that any method that uses local storage can only be used on Shiny Server, while any method that uses remote storage can be also used on shinyapps.io.

| Method            | Data type            | Local storage | Remote storage | R package     |
|-------------------|----------------------|---------------|----------------|---------------|
| Local file system | Arbitrary data       | YES           |                | \-            |
| Dropbox           | Arbitrary data       |               | YES            | rdrop2        |
| Amazon S3         | Arbitrary data       |               | YES            | aws.s3        |
| SQLite            | Structured data      | YES           |                | RSQLite       |
| MySQL             | Structured data      | YES           | YES            | RMySQL        |
| Google Sheets     | Structured data      |               | YES            | googlesheets4 |
| MongoDB           | Semi-structured data | YES           | YES            | mongolite     |

### Links
-   <https://testthat.r-lib.org>
-   <https://shiny.rstudio.com/articles/testing-overview.html>
-   <https://cran.r-project.org/web/packages/RSelenium/vignettes/shinytesting.html>
-   <https://mastering-shiny.org/scaling-testing.html>
-   <https://shiny.rstudio.com/articles/persistent-data-storage.html>
