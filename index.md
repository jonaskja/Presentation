---
title       : Presentation of Shiny Application
subtitle    : Developing Data Products
author      : Jonas Kjærvik
job         : 
framework   : io2012        # {io2012, html5slides, shower, dzslides, ...}
highlighter : highlight.js  # {highlight.js, prettify, highlight}
hitheme     : tomorrow      # 
widgets     : [bootstrap]            # {mathjax, quiz, bootstrap}
mode        : selfcontained # {standalone, draft}
knit        : slidify::knit2slides
--- 

# Outline of Project

A simple workspace for students/researchers working with the same data. The application consist of four main options: 

1. View the data of choice
2. Get descriptive statistics of chosen variables (plot and table)
3. Perform regression analysis of chosen variables (linear and count)
4. Download the data (csv-file)

- Link to the app: https: https://jonaskja.shinyapps.io/ProjectApp/
- Link to the source code: https://github.com/jonaskja/ProjectApp/

--- 

# The layout of the application  

Uses ```library(shinydashboard)``` to create the main tabs on the left hand side 

![width](app.png)


---

# Example of functionality

- Based on the choices made by the user, the server calculates and prints the output
- All operations are reactive in the sense that the user input on the screen is pushed to the server 
- Example of reactive code in the tab "Analyze":
 

```r
  output$nbmodel.table <- renderTable({
    library(MASS)
    glm.nb(as.formula(paste(input$dependent," ~ ",paste(input$independent,collapse="+"))),data=Data)
  })           
```

If the variable "Goals" is chosen as dependent and "Behav_aut" as only independent, the server run this model:



```r
glm.nb(Goals ~ Behav_aut,data=Data)
```


---

# Example of functionality - continued


```
## 
## Call:  glm.nb(formula = Goals ~ Behav_aut, data = Data, init.theta = 1.431110433, 
##     link = log)
## 
## Coefficients:
## (Intercept)    Behav_aut  
##    2.953254     0.005171  
## 
## Degrees of Freedom: 76 Total (i.e. Null);  75 Residual
## Null Deviance:	    86.17 
## Residual Deviance: 83.07 	AIC: 628.2
```


The renderTable function create the object output$nbmodel.table which is printed using tableOutput("nbmodel.table").

