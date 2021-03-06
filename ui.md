```{r ui, eval=FALSE}
## packages
library(rCharts)
library(shinythemes)
library(markdown)

## load the FRED data
load('freddata.rda')

##Define UI
shinyUI(navbarPage("FRED-HEAD",
    #theme = shinytheme("journal"),
    ## Sidebar
    tabPanel("Plot",
    titlePanel(strong('FRED-Head: A Simple Dashboard for FRED Data', style="color: steelblue")),
    sidebarLayout(
        #title = "FRED-Head: A Simple Dashboard for FRED Data",
        sidebarPanel(width=3,
            selectInput(inputId = "concept",
                        label = "Select a concept to examine:",
                        choices = c("Inflation", "Unemployment", "Interest Rates", "Home Prices", "Industrial Production"),
                        selected = "Inflation"),
            helpText("Data shown here were ",
                    "pulled from the FRED ",
                    "database, maintained by ",
                    "the St. Louis Federal Reserve. ",
                    "To view these series and more, ",
                    a("visit the FRED site.",href="http://research.stlouisfed.org/fred2/", target="_blank"))
        ),
        ## Show the Plot
        mainPanel(
            showOutput("fredplot", "highcharts")
        )
        
    )),
############################################################################
    tabPanel("Documentation",
             titlePanel(strong('FRED-Head: A Simple Dashboard for FRED Data', style="color: steelblue")),
        fixedRow(
            column(6, includeMarkdown("user_documentation.md")),
            column(6, 
                   tabsetPanel(
                    tabPanel("ui.R"),
                    tabPanel("server.R")))
           
        ))
##############################################################################
))
```