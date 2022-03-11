
## Shiny - Documentation and Reproducibility

### Brief description

Shiny is an R package for building interactive web apps straight from R. You can visit [Shiny Website](https://shiny.rstudio.com/) for the most useful resources on mastering shiny or look for help from [RStudio Community](https://community.rstudio.com/c/shiny/8?_ga=2.131532047.1822684614.1646988228-658982915.1642896472) or [shinyapps-users Google group](https://groups.google.com/g/shinyapps-users). 

To ensure the Shiny app is deployed under a reproducible environment, there are two tools we can use: [renv](https://rstudio.github.io/renv/) and [Docker](https://www.docker.com/).

### Long description

### Official Documentation Resources

- [Shiny Website](https://shiny.rstudio.com/)
- [Mastering Shiny](https://mastering-shiny.org/)
- [Engineering Production-Grade Shiny Apps](https://engineering-shiny.org/)
- [Package 'shiny' - The Comprehensive R Archive Network](https://cran.r-project.org/web/packages/shiny/shiny.pdf)

#### Getting Help
- [RStudio Community](https://community.rstudio.com/c/shiny/8?_ga=2.131532047.1822684614.1646988228-658982915.1642896472)
- [shinyapps-users Google group](https://groups.google.com/g/shinyapps-users)

#### Gallery
- [Shiny User Showcase](https://shiny.rstudio.com/gallery/#user-showcase)
- [Shiny Demos](https://shiny.rstudio.com/gallery/#demos)

### Shiny - Run the dashbaord in a reproducible way locally
To ensure the app is deployed under the same configuration as your local application, there are two tools we can use here. 

#### 1. `{renv}`

`{renv}` package allows one to have a project-based library so others can run the dashboard locally.
To create a reproducible renv library, here are the steps to follow:

- Initiate the project with `renv::init()`.
  
  This function will create/modify the `.Rprofile` file at the root of your project, and creates a `renv.lock` file, which will list all the package dependencies.

```
# Loading and initiating {renv}
library(renv)
init()
```


- Install/remove packages.

```
# Installing attempt
install.packages("attempt")
# Create a fake script that launches {attempt}
write("library(attempt)", "script.R")

```

- Take a `snapshot()` of the state of your project.

```
# Snapshoting the current status of the environment
renv::snapshot(confirm = FALSE)
```

- `renv::restore()` the state of your project using renv.lock.

  if you are either working as a team or deploying to a server, you will have to restore the state of your project, which is now living somewhere else, inside your current project/deployment. And to do that, the function to call is `renv::restore()`, which will update your local project with the dependencies listed inside your Lockfile.


- Share .Rprofile, renv.lock, renv/activate.R and renv/settings.dcf files for reproducibility.


#### 2. Docker

Docker is a program that allows to download, install, create, launch and stop multiple operating systems, called containers, on a machine, which will be called the host. This host can be your local computer, or the server where you deploy your application/s.

**A. Building a Dockerfile with golem**

For a golem project, you can run the following from the root of your package:
```
golem::add_dockerfile()
```

**B. `{dockerfiler}`**

You can use dockerfiler package to generate a Dockerfile straight from R

```
# Creating a new Dockerfile object
my_dock <- Dockerfile$new()
# Adding RUN, ADD, WORKDIR and EXPOSE commands
my_dock$RUN("apt-get update && apt-get install -y git-core")
my_dock$ADD(".", "/")
my_dock$RUN("mkdir /build_zone")
my_dock$ADD(".", "/build_zone")
my_dock$WORKDIR("/build_zone")
my_dock$RUN(r(remotes::install_local(upgrade="never")))
my_dock$EXPOSE(80)
# Viewing the Dockerfile
my_dock
```

**C. Develop inside a Docker container**

If you plan on using Docker as a deployment mechanism, you can also use Docker as a local developer environment. 


### Links
* https://shiny.rstudio.com/
* https://mastering-shiny.org/
* https://engineering-shiny.org/
* https://github.com/ThinkR-open/golem
