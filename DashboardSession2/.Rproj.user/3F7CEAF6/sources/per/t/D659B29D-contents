#
# This is a Shiny web application. You can run the application by clicking
# the 'Run App' button above.
#
# Find out more about building applications with Shiny here:
#
#    http://shiny.rstudio.com/
#

#install.packages("googlesheets")
#install.packages("rlang")
#install.packages("dplyr")
#install.packages("curl")
#install.packages("openssl")
#install.packages("hms")
#install.packages("highcharter")
#install.packages("tidyr")
#install.packages("httr")
#install.packages("leaflet")
#install.packages("googledrive")

library(googlesheets)
library(rlang)
library(curl)
library(openssl)
library(hms)
library(dplyr)
library(shiny)
library(shinydashboard)
library(tables)
library(tidyr)
library(highcharter)
library(httr)
library(leaflet)
library(jsonlite)
library(leaflet)
library(googledrive)
library(DT)


ui <- dashboardPage(skin = "purple",
                    dashboardHeader(title = "CADS Study Dashboard", titleWidth = 150),
                    dashboardSidebar(
                      sidebarMenu(
                        menuItem("Overall Objectives", tabName = "objectives", icon = icon("globe")),
                        menuItem("Wellpad Operator", tabName = "wellpad_operator", icon = icon("bell")),
                        menuItem("Freshwater Expert", tabName = "freshwater_expert", icon = icon("tint")),
                        menuItem("Environmental Regulator", tabName = "freshwater_source_expert", icon = icon("street-view")),
                        menuItem("Wastewater Expert", tabName = "wastewater_expert", icon = icon("asterisk")),
                        menuItem("Demos", tabName = "demos")
                      )
                    ),
                    dashboardBody(
                      #Tab 1 Objective View
                      tabItems(
                        tabItem(tabName = "objectives", 
                                h2("Overall Objectives"),
                                fluidRow(
                                  box(
                                    width = 12,
                                    actionButton("objective_update1", "Update", icon = icon("retweet")),
                                    actionButton("design_update", "New Design", icon = icon("plus")),
                                    actionButton("download", "Download Designs", icon = icon("download")),
                                    textOutput(h3("row_ns"))
                                  )),
                                fluidRow(
                                  box(
                                    title = "Overall Objective Comparison", width = 6, solidHeader = TRUE,
                                    highchartOutput("objective_plot1")
                                  ),
                                  box(
                                    title = "Cost Category Breakdown", width = 6, solidHeader = TRUE,
                                    highchartOutput("costbreakdown_plot")
                                  ),
                                  box(
                                    title = "Decision Variables", width = 12, solidHeader = TRUE,
                                    dataTableOutput("decision_table1"))
                                )),
                        
                        #Tab 2 Wellpad Decision
                        tabItem(tabName = "wellpad_operator", 
                                h2("Wellpad Operator"), 
                                fluidRow(
                                  sidebarLayout(
                                    sidebarPanel(
                                      h3("Decision Variables"),
                                      selectInput("wastewater_reuse", h4("Reuse Wastewater?"), 
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No"),
                                                  selected = NULL),
                                      selectInput("wastewater_storage", h4("Store Wastewater?"),
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No")),
                                      actionButton("wellpad_update", "Update", icon = icon("retweet"))
                                    ),
                                    
                                    mainPanel(
                                      box(
                                        title = "Wellpad Operator Description", width = 12, solidHeader = TRUE,
                                        "As the well pad operator, your main goal is to minimize the financial cost of the waste water management system in order to promote your firm’s overall profitability. 
                                        With your experience, you know that allowing for wastewater reuse will lower your cost, since this will reduce your freshwater demand. You will need to work with your transportation experts to make sure their proposed solution meet the water volume demand at the lowest cost. Other than minimizing financial cost, you do not care about the other objectives, and would be very resistant to changes that will increase the financial cost. 
                                        However, you will need to work with the environmental regulator and advocates on the overall fracking operation, and you will need to have their buy-in for the final design."
                                      ),
                                      box(
                                        title = "Wellpad Operator Result", width = 12, solidHeader = TRUE,
                                        tableOutput("wellpad_operator_result")  
                                      )
                                      )
                                  )
                        )),
                        
                        #Tab 3 Freshwater Expert
                        tabItem(tabName = "freshwater_expert",
                                h2("Freshwater Expert"),
                                fluidRow(
                                  sidebarLayout(
                                    sidebarPanel(
                                      h3("Decision Variables"),
                                      selectInput("freshwater_impoundment_piping", h4("Use Piping to Transport Freshwater to Impoundment?"),
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No")),
                                      selectInput("freshwater_wellpad_piping", h4("Use Piping to Transport Freshwater to Wellpad?"),
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No")),
                                      selectInput("impoundment_pipe_size", h4("Impoundment Pipe Size"),
                                                  choices = list("Small" = "Small Pipeline",
                                                                 "Medium" = "Medium Pipeline",
                                                                 "Large" = "Large Pipeline")),
                                      selectInput("wellpad_pipe_size", h4("Wellpad Pipe Size"),
                                                  choices = list("Small" = "Small Pipeline",
                                                                 "Medium" = "Medium Pipeline",
                                                                 "Large" = "Large Pipeline")),
                                      actionButton("freshwater_update", "Update", icon = icon("retweet"))
                                    ),
                                    mainPanel(
                                      box(
                                        title = "Freshwater Expert Description", width = 12, solidHeader = TRUE,
                                        "You are the freshwater transportation expert, and you have innate knowledge on the different transportation options and their costs.
                                        You know that due to the high capital cost of pipelines, trucks would be more economical, unless extremely large quantities of freshwater is required. 
                                        However, trucking will have much higher emissions when compared against pipeline options. There are three pipeline sizes available to you, with different pipeline capacity ranging from 200,000 barrels of water per week to 1,200,000 per week.
                                        Each size also has different capital costs, ranging from $240,000 to $400,000. However, pumping cost is the same regardless of the pipe size, at $0.005 per barrel-mile, which is lower than the trucking cost of $0.053 per barrel-mile
                                        "
                                      ),
                                      box(
                                        title = "Freshwater Pipeline Parameters", width = 6, solidHeader = TRUE,
                                        tableOutput("freshwater_pipeline_param")
                                        
                                      ),
                                      box(
                                        title = "Freshwater Results", width = 6, solidHeader = TRUE,
                                        tableOutput("freshwater_expert_result")  
                                      )
                                      )
                                  )
                                )
                                
                        ),
                        #Tab 4 Freshwater Source
                        tabItem(tabName = "freshwater_source_expert", 
                                h2("Environmental Regulator"),
                                fluidRow(
                                  sidebarLayout(
                                    sidebarPanel(
                                      h3("Freshwater Sources"),
                                      selectInput("stream_source", h4("Use Connoquenessing Creek as Freshwater Source?"),
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No")),
                                      selectInput("river1_source", h4("Use Racoon Creek as Freshwater Source?"),
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No")),
                                      selectInput("river2_source", h4("Use Fishpot Run as Freshwater Source?"),
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No")),
                                      actionButton("watersource_update", "Update", icon = icon("retweet"))
                                    ),
                                    
                                    mainPanel(
                                      box(
                                        title = "Environmental Regulator Description", width = 12, solidHeader = TRUE,
                                        "Your role as the environmental regulator is to balance the environmental needs of the local community against the financial cost of the shale gas project. 
                                        While you understand that the shale gas project will bring immediate economic benefit to the region, there are significant environmental impact.
                                        Given the local community's needs, your preference is to have the oil and gas company withdraw water from the Connoquenessing Creek, instead of using either Racoon Creek and Fishpot Run.
                                        However, if the company is willing to compromise on their other decisions, you would be open for them to withdraw water from Fishpot Run."
                                      ),
                                      box(title = "Beaver County Freshwater Sources", width = 12, solidHeader = TRUE,
                                          leafletOutput("beaver_county_map")  
                                      ),
                                      box(
                                        title = "Environmental Impact", width = 12, solidHeader = TRUE,
                                        tableOutput("env_impact") 
                                      )
                                      
                                      )
                                  )
                                )
                        ),
                        
                        #Tab 5 Waste Expert
                        tabItem(tabName = "wastewater_expert",
                                h2("Wastewater Expert"),
                                fluidRow(
                                  sidebarLayout(
                                    sidebarPanel(
                                      h3("Decision Variables"),
                                      selectInput("central_treatment", h4("Use Centralized Treatment Facility?"), 
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No"),
                                                  selected = NULL),
                                      selectInput("wastewater_pipeline", h4("Use Pipeline to Transport Wastewater to Central Facility?"),
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No")),
                                      selectInput("wastewater_pipe", h4("Pipe Size"),
                                                  choices = list("Small" = "Small Pipeline",
                                                                 "Medium" = "Medium Pipeline",
                                                                 "Large" = "Large Pipeline")),
                                      actionButton("wastewater_update", "Update", icon = icon("retweet"))
                                    ),
                                    
                                    mainPanel(
                                      box(
                                        title = "Wastewater Expert Description", width = 12, solidHeader = TRUE,
                                        "You are the expert in wastewater treatment and transportation of fracking fluid. 
                                        Your years of industry knowledge will allow you to make quick and accurate estimation of the cost of wastewater treatment and transportation options.
                                        You know that due to the high capital cost of pipelines, trucks would be more economical, unless extremely large quantities of freshwater is required. 
                                        However, trucking will have much higher emissions when compared against pipeline options. There are three pipeline sizes available to you, with different pipeline capacity ranging from 200,000 barrels of water per week to 1,200,000 barrels per week.
                                        Each size also has different capital costs, ranging from $240,000 to $400,000. However, pumping cost is the same regardless of the pipe size, at $0.005 per barrel-mile, which is lower than the trucking cost of $0.053 per barrel-mile.
                                        Finally, you know that when compared against freshwater transportation, you will need to transport far less wastewater, especially if wastewater is reused for fracking or if it is sent to central treatment first.
                                        "
                                      ),
                                      box(
                                        title = "Wastewater Pipeline Parameters", width = 6, solidHeader = TRUE,
                                        tableOutput("wastewater_params")),
                                      box(
                                        title = "Wastewater Results", width = 6, solidHeader = TRUE,
                                        tableOutput("wastewater_result")
                                      )
                                      )
                                  )
                                ))
                        )
))


# Define server logic
server <- function(input, output) {
  
  #Register the googlesheet with R
  cads.main <- gs_url("https://docs.google.com/spreadsheets/d/1FxoHbmhxKiT2gLkKjbSCeiDYUataLwyz8M6cma99G_Q/edit#gid=229843704")
  
  #Registering the individual worksheets
  test.table <- eventReactive(input$objective_update1, {
    
    dv <- cads.main%>%
      gs_read(ws = "Task3Decisions")
    
  })
  
  plot.objective <- eventReactive(input$objective_update1, {
    
    obj <- cads.main%>%
      gs_read(ws = "Task3Objective")
    objstacked <- gather(obj, "Design", "Cost", -1)
    value.stacked <- signif(objstacked[3], digits = 3)
    objstacked1 <- cbind(objstacked[-3], value.stacked)
    
    hchart(objstacked1, "column", hcaes(x = Category, y = Cost, group = Design))%>%
      hc_tooltip(valuePrefix = "$", valueSuffix = " Million USD")%>%
      hc_yAxis(title = list(text = "Cost ($ Millions)"))%>%
      hc_exporting(
        enabled = TRUE
      )
  })
  
  output$objective_plot <- renderHighchart(data.objective.plot())
  
  data.costbreakdown.plot <- eventReactive(input$objective_update1, {
    
    cost.breakdown <- cads.main%>%
      gs_read(ws = "Task3CostBreakdown")%>%signif(digits =3)
    
    cost.breakdown.stacked <- gather(cost.breakdown, "Classes", "Cost", -1)
    
    hchart(cost.breakdown.stacked, "column", hcaes(x = Design, y = Cost, group = Classes))%>%
      hc_plotOptions(column = list(stacking = "normal"))%>%
      hc_yAxis(title = list(text = "Cost ($ Millions)"))%>%
      hc_exporting(
        enabled = TRUE
      )
  })
  output$costbreakdown_plot <- renderHighchart(data.costbreakdown.plot())
  
  output$objective_plot1 <- renderHighchart(plot.objective())
  
  output$decision_table1 <- renderDataTable(test.table(), options = list(pageLength = 13))
  
  data.new <- eventReactive(input$design_update, {
    
    raw.cost.breakdown <- cads.main%>%
      gs_read_cellfeed(ws = "Cost Breakdown")
    
    raw.objectives <- cads.main%>%
      gs_read_cellfeed(ws = "Overall Objectives")
    
    raw.variables <- cads.main%>%
      gs_read_cellfeed(ws = "Sheet3")
    
    row.costbreakdown.i <- max(raw.cost.breakdown$row)
    row.costbreakdown.i <- row.costbreakdown.i + 1
    
    col.objectives.i <- as.numeric(max(raw.objectives$col))
    col.objectives.i <- col.objectives.i+1
    
    col.variables.i <- as.numeric(max(raw.variables$col))
    col.variables.i <- col.variables.i + 1
    
    cost.formula.input <- raw.cost.breakdown%>%
      subset(row == row.costbreakdown.i-1)
    
    objective.formula.input <- raw.objectives%>%
      subset(col == col.objectives.i - 1)
    
    variable.formula.input <- raw.variables%>%
      subset(col == col.variables.i - 1)
    
    cost.value.input <- raw.cost.breakdown%>%
      subset(row == row.costbreakdown.i-1)
    
    objective.value.input <- raw.objectives%>%
      subset(col == col.objectives.i -1)
    
    variable.value.input <- raw.variables%>%
      subset(col == col.variables.i - 1)
    
    
    #Add Formulas first
    gs_edit_cells(cads.main, ws = "Cost Breakdown", input = cost.formula.input$input_value, anchor = paste("A", row.costbreakdown.i, sep = ""), byrow = TRUE)
    gs_edit_cells(cads.main, ws = "Overall Objectives", input = objective.formula.input$input_value, anchor = paste(LETTERS[col.objectives.i], "1", sep = ""), byrow = FALSE)
    gs_edit_cells(cads.main, ws = "Sheet3", input = variable.formula.input$input_value, anchor = paste(LETTERS[col.variables.i], "1", sep = ""), byrow = FALSE)
    
    #Add Values
    gs_edit_cells(cads.main, ws = "Cost Breakdown", input = cost.value.input$value, anchor = paste("A", row.costbreakdown.i - 1, sep = ""), byrow = TRUE)
    gs_edit_cells(cads.main, ws = "Overall Objectives", input = objective.value.input$value, anchor = paste(LETTERS[col.objectives.i - 1], "1", sep = ""), byrow = FALSE)
    gs_edit_cells(cads.main, ws = "Sheet3", input = variable.value.input$value, anchor = paste(LETTERS[col.variables.i - 1], "1", sep = ""), byrow = FALSE)
    "New Design is Ready!"
  })
  
  output$row_ns <- renderText(data.new())
  
  observeEvent(input$download, {
    
    gs_download(cads.main, to = "OverallResults.xlsx")
    drive_upload("OverallResults.xlsx")
    
  })
  
  data.wastewater <- eventReactive(input$wellpad_update, {
    
    gs_edit_cells(ss = cads.main, ws = "Wellpad Operator", input = input$wastewater_reuse, anchor = "B2", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Wellpad Operator", input = input$wastewater_storage, anchor = "B3", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    wellpad.operator.decisions <- cads.main%>%
      gs_read(ws = "Wellpad Operator", range = "A1:B3")
    wellpad.operator.outputs <- cads.main%>%
      gs_read(ws = "Wellpad Operator", range = "A4:B8")
    
  })
  output$wellpad_operator_result <- renderTable(data.wastewater())
  
  data.freshwater.results <- eventReactive(input$freshwater_update, {
    
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$freshwater_impoundment_piping, anchor = "B3", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$freshwater_wellpad_piping, anchor = "B4", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$impoundment_pipe_size, anchor = "B6", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$wellpad_pipe_size, anchor = "B7", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    freshwater.expert.output <- cads.main%>%
      gs_read(ws = "Freshwater Transportation Expert", range = "A14:B22")
    
  })
  
  output$freshwater_expert_result <- renderTable(data.freshwater.results())
  
  data.environ.impact <- eventReactive(input$watersource_update, {
    env.regulator.output <- cads.main%>%
      gs_read(ws = "Environmental Damages", range = "A8:D17")
  })
  
  output$env_impact <- renderTable(data.environ.impact())
  
  data.freshwater.source <- eventReactive(input$watersource_update, {
    
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$stream_source, anchor = "B10", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$river1_source, anchor = "B11", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$river2_source, anchor = "B12", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    
    freshwater.expert.output <- cads.main%>%
      gs_read(ws = "Freshwater Transportation Expert", range = "A14:B22")
    
  })
  
  output$freshwater_expert_result <- renderTable(data.freshwater.source())
  
  data.freshwater.params <- eventReactive(input$freshwater_update, {
    
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$freshwater_impoundment_piping, anchor = "B3", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$freshwater_wellpad_piping, anchor = "B4", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$impoundment_pipe_size, anchor = "B6", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$wellpad_pipe_size, anchor = "B7", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    freshwater.expert.pipelineparam <- cads.main%>%
      gs_read(ws = "Freshwater Transportation Expert", range = "C2:E4")
  })
  
  output$freshwater_pipeline_param <- renderTable(data.freshwater.params())
  
  data.wastewater.result <- eventReactive(input$wastewater_update, {
    gs_edit_cells(ss = cads.main, ws = "Waste Water Transportation Expert", input = input$central_treatment, anchor = "B3", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Waste Water Transportation Expert", input = input$wastewater_pipeline, anchor = "B4", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Waste Water Transportation Expert", input = input$wastewater_pipe, anchor = "B6", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    
    wastewater.expert.output <- cads.main%>%
      gs_read(ws = "Waste Water Transportation Expert", range = "A8:B13")%>%
      na.omit()
    
  })
  output$wastewater_result <- renderTable(data.wastewater.result())
  
  data.wastewater.params <- eventReactive(input$wastewater_update, {
    
    gs_edit_cells(ss = cads.main, ws = "Waste Water Transportation Expert", input = input$wastewater_pipeline, anchor = "B4", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Waste Water Transportation Expert", input = input$wastewater_pipe, anchor = "B6", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    
    wastewater.expert.param <- cads.main%>%
      gs_read(ws = "Waste Water Transportation Expert", range = "C5:E6")%>%
      na.omit()
  })  
  
  output$wastewater_params <- renderTable(data.wastewater.params())
  
  output$beaver_county_map <- renderLeaflet({
    longlat <- cads.main%>%
      gs_read(ws = "Scenario Parameters", range = "G3:J6")
    
    leaflet(data = longlat)%>%
      addTiles()%>%
      setView(-80.1,40.55, zoom = 9)%>%
      addMarkers(~Long, ~Lat, label = ~FreshwaterLocations, popup = paste("Location", longlat$FreshwaterLocations, "<br>", "Distance from the wellpad: ", longlat$Distance, " Miles"))
    
    
  })
  
  selectedData <- reactive({
    iris[, c(input$xcol, input$ycol)]
  })
  
  clusters <- reactive({
    kmeans(selectedData(), input$clusters)
  })
  
  output$plot1 <- renderPlot({
    palette(c("#E41A1C", "#377EB8", "#4DAF4A", "#984EA3",
              "#FF7F00", "#FFFF33", "#A65628", "#F781BF", "#999999"))
    
    par(mar = c(5.1, 4.1, 0, 1))
    plot(selectedData(),
         col = clusters()$cluster,
         pch = 20, cex = 3)
    points(clusters()$centers, pch = 4, cex = 4, lwd = 4)
  })
}

# Run the application 
shinyApp(ui = ui, server = server)

