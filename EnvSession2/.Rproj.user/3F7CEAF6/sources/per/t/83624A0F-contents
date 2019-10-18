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
#install.packages("googleAuthR")
#install.packages("expss")

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
library(googleAuthR)
library(expss)
library(DT)

ui <- dashboardPage(skin = "purple",
                    dashboardHeader(title = "CADS Study Dashboard", titleWidth = 230),
                    dashboardSidebar(
                      sidebarMenu(
                        menuItem("Background Information", tabName = "objectives", icon = icon("globe")),
                        menuItem("Pre-Study Task", tabName = "prestudy_briefing", icon = icon("briefcase")),
                        menuItem("Environmental Regulator", tabName = "freshwater_source_expert", icon = icon("bell"))
                      )
                    ),
                    dashboardBody(
                      #Tab 1 Objective View
                      tabItems(
                        tabItem(tabName = "objectives", 
                                h2("Background Information"),
                                fluidRow(
                                  box(
                                    title = "Case Study Background", solidHeader = TRUE, width = 12,
                                    "Your goal here today is to design a shale gas wastewater management system under idealized conditions. There are two overall objectives to consider:", tags$b("overall financial cost"), ", and ", tags$b("environmental cost"), "calculated from air emission damages. Depending on your role, you will want to minimize either one of the objectives, or both.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Case Study Setup:"), " Unconventional shale gas exploration is done by pumping large quantities of fluids at high pressure down a wellbore and into the target rock formation. Hydraulic fracturing fluid commonly consists of water, proppant and chemical additives that open and enlarge fractures within the rock formation. These fractures can extend several hundred feet away from the wellbore. The proppants - sand, ceramic pellets or other small incompressible particles - hold open the newly created fractures. The operation requires large amount of freshwater each day to sustain its operation, usually in the range of 240,000 barrels a week. The majority of this demand is fulfilled by first transporting freshwater from a local freshwater source (local river, creek, pond, or lake) to a centralized impoundment area, and then send it to individual well sites. In addition, wastewater is also generated during the process, and return to surface containing materials such as brines, metals, and hydrocarbons. A portion of it can be reused for future fracturing operations, while the rest can either be treated centrally and discharged to surface water or transported and disposed in disposal wells.",
                                    tags$br(),
                                    tags$br(),
                                    "There are four expert roles for this case study, and you have been randomly assigned as one of these four roles:",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Well-pad Operator"), ", who is responsible for the overall operation of the drilling operation, and whose main objective is to minimize overall financial cost of the system.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Freshwater Expert"), ", who is responsible for transporting the freshwater from the appropriate water source to the impoundment, and subsequently to individual well pads. Their main objective is to minimize the freshwater transportation cost.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Wastewater Expert"), ", who is responsible for determining the fate of the wastewater produced during the operation, whether it treated and discharged, or stored in disposal wells. Their main objective is to minimize the overall wastewater management and transportation cost.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Environmental Advocate"), ", who is responsible for determining the freshwater source most appropriate for the operation. Their main objective is to minimize environmental cost created through air emissions damages.",
                                    tags$br(),
                                    tags$br(),
                                    "Detailed information about your role can be found in the next tab.",
                                    tags$br(),
                                    tags$br(),
                                    "During this study, you will complete one pre-study task and three subsequent design tasks.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Pre-study task:"), " Navigate to the tab labeled “Pre-Study Task”, you will have ten minutes to read through the detailed background information related to your role and answer three true or false questions on details of your role. If you answer any of the questions incorrectly, the correct answer along with an explanation will be displayed to you.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Task 1:"), " Navigate to tab labeled with your role. Based on the information given to you here and in the “Pre-Study Task”, without collaborating to other participants, you will have ten minutes to independent select the decision variables that you believe will generate the best design for both the system and your individual role. Once you generated the design you are satisfied with, please let the researcher know.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Task 2:")," Similar to task one, you will have 20 minutes to select the decision variables that you believe will generate the best design for the entire system and your individual role. However, you may now communicate with the other participants, and use their experience/knowledge to augment your information. If you so choose, you may at this time change design decisions to iterate to a different design. You can iterate as many times as you like under the time constraint. Once your group has created a design you are satisfied with, please let the researcher know.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Task 3:"), " Similar to task 2, you will have 20 minutes to select the decision variables that you believe will generate the best design for the entire system and your individual role. However, in addition to be able to communicate with the other participants, the overall system financial cost and environmental will be presented to you in near real time via an external display. If you so choose, you can change design decisions at any time to iterate to a different design. You can iterate as many times as you like under the time constraint. Once your group has created a design you are satisfied with, please let the researcher know."
                                  ))
                                
                        ),
                        
                        #Tab 2 Pretask Briefing
                        tabItem(tabName = "prestudy_briefing",
                                h2("Pre-Study Task"),
                                fluidRow(
                                  box(
                                    title = "Pre-Study Briefing: Environmental Regulator", solidHeader = TRUE, width = 12,
                                    tags$b("Individual Goal/System Goal:"), " Ensure that the wastewater management system produces the least amount of air emissions damages to the community.",
                                    tags$br(),
                                    tags$br(),
                                    "You are local community environmental regulator, and your main goal is to minimize the air emissions cost of the overall water management system. Each activity associated with withdrawing freshwater, transportation, treatment, and disposal all have associated air emissions damages made up from greenhouse gas and air particulate matter, that can be estimated on a dollar basis. Based on the decisions of other actors, the tool will provide you with the overall air emissions damages of the operation. However, from prior experience, you know that a well-designed system should not have more than $15 million in air emissions damages to the community.",
                                    tags$br(),
                                    tags$br(),
                                    "Environmental damages are calculated through an economic input-output model, that generally means that the greater the financial cost of the system, the higher the emissions damages will be. However, trucking emissions damages are calculated based on distance traveled, with increased damages on a per mile basis. Out of the three freshwater sources under consideration, the community has provided a preference on Stream to be the freshwater source. You will then want to ensure the firm uses Stream as the main freshwater source. However, the Stream has the highest freshwater withdraw cost, and it might lead to higher financial costs. If other participants are willing to compromise on other design decisions that would lower environmental cost, you would be open for them to use the Lake and River options.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Decision Variables:"),
                                    tags$br(),
                                    tags$br(),
                                    "You are responsible for one decision for the overall system:",
                                    tags$b("Freshwater source for the operation:"), " You will decide which freshwater source will be used for the firm’s operation. The three water sources are: a stream, which is 10 miles away from the fracking operation; a lake, which is 15 miles away; and a river, which is 35 miles away.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Relationship with other experts"),
                                    tags$br(),
                                    tags$br(),
                                    "Since your main goal is to minimize air emissions damages, you will want to push for the other experts to iterate through their design decisions to find the design with the lowest damages. However, you know that the operation has already received approval, so preventing the fracking operation entirely is impossible. You can only minimize the damages associated with the operation.",
                                    tags$br(),
                                    tags$br(),
                                    tags$b("Key Parameters"),
                                    tags$br(),
                                    tags$br(),
                                    tags$table(
                                      tags$tr(
                                        tags$th(tags$b("Pollutant")),
                                        tags$th(tags$b("Cost per Ton"))
                                      ),
                                      tags$tr(
                                        tags$td("NH3"),
                                        tags$td("$131,000")
                                      ),
                                      tags$tr(
                                        tags$td("NOx"),
                                        tags$td("$5,540")
                                      ),
                                      tags$tr(
                                        tags$td("PM2.5"),
                                        tags$td("$118,000")
                                      ),
                                      tags$tr(
                                        tags$td("SO2"),
                                        tags$td("$44,500")
                                      ),
                                      tags$tr(
                                        tags$td("VOC"),
                                        tags$td("$11,300")
                                      ),
                                      tags$tr(
                                        tags$td("CO2e"),
                                        tags$td("$40")
                                      )
                                    )
                                  ),
                                  box(
                                    title = "Validation Questions", solidHeader = TRUE, width = 12,
                                    radioButtons("question1", "Question 1: You would prefer the operation use the lake as the primary freshwater source.", selected = character(0),
                                                 choiceNames = list(
                                                   "True",
                                                   "False"
                                                 ),
                                                 choiceValues = list(
                                                   "True", "False"
                                                 )),
                                    textOutput("answer1"),
                                    
                                    radioButtons("question2", "Question 2: If a design has higher financial cost, it will generate higher air emissions damages as well.", selected = character(0),
                                                 choiceNames = list(
                                                   "True",
                                                   "False"
                                                 ),
                                                 choiceValues = list(
                                                   "True", "False"
                                                 )),
                                    textOutput("answer2"),
                                    
                                    radioButtons("question3", "Question 3: Your main motivation is to minimize financial cost associated with the overall operation.", selected = character(0),
                                                 choiceNames = list(
                                                   "True",
                                                   "False"
                                                 ),
                                                 choiceValues = list(
                                                   "True", "False"
                                                 )),
                                    textOutput("answer3")
                                    
                                  )
                                )),
                        
                        #Tab 3 Wastewater Decision
                        tabItem(tabName = "freshwater_source_expert", 
                                h2("Environmental Regulator"),
                                fluidRow(
                                  sidebarLayout(
                                    sidebarPanel(
                                      h3("Freshwater Sources"),
                                      selectInput("stream_source", h4("Use Stream as Freshwater Source?"),
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No"), selected = "Yes"),
                                      selectInput("river1_source", h4("Use Lake as Freshwater Source?"),
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No"), selected = "No"),
                                      selectInput("river2_source", h4("Use River as Freshwater Source?"),
                                                  choices = list("Yes" = "Yes",
                                                                 "No" = "No"), selected = "No"),
                                      actionButton("watersource_update", "Update", icon = icon("retweet"))
                                    ),
                                    
                                    mainPanel(
                                      box(
                                        title = "Key Parameters", width = 12, solidHeader = TRUE,
                                        tags$table(
                                          tags$tr(
                                            tags$th(tags$b("Pollutant")),
                                            tags$th(tags$b("Cost per Ton"))
                                          ),
                                          tags$tr(
                                            tags$td("NH3"),
                                            tags$td("$131,000")
                                          ),
                                          tags$tr(
                                            tags$td("NOx"),
                                            tags$td("$5,540")
                                          ),
                                          tags$tr(
                                            tags$td("PM2.5"),
                                            tags$td("$118,000")
                                          ),
                                          tags$tr(
                                            tags$td("SO2"),
                                            tags$td("$44,500")
                                          ),
                                          tags$tr(
                                            tags$td("VOC"),
                                            tags$td("$11,300")
                                          ),
                                          tags$tr(
                                            tags$td("CO2e"),
                                            tags$td("$40")
                                          )
                                        )
                                      ),
                                      box(
                                        title = "Environmental Impact", width = 12, solidHeader = TRUE,
                                        tableOutput("env_impact") 
                                      ),
                                      box(title = "Beaver County Freshwater Sources", width = 12, solidHeader = TRUE,
                                          leafletOutput("beaver_county_map")  
                                      )
                                    )
                                  )
                                )
                        )
                        
                      )
                    ))


# Define server logic
server <- function(input, output) {
  
  
  options(googleAuthR.scopes.selected = c("https://www.googleapis.com/auth/drive.file", 
                                          "https://www.googleapis.com/auth/drive",
                                          "https://www.googleapis.com/auth/drive.readonly",
                                          "https://www.googleapis.com/auth/spreadsheets.readonly",
                                          "https://www.googleapis.com/auth/spreadsheets",
                                          "https://www.googleapis.com/auth/xapi.zoo"))
  options("googleAuthR.webapp.client_id" = "896066592625-9b26euhim8plpf9jqn2968mgd6dque1a.apps.googleusercontent.com")
  options("googleAuthR.client_secret" = "Gh_SXMEy8ZnMXU1hy6lKSlr6")
  
  #Register the googlesheet with R
  cads.main <- gs_url("https://docs.google.com/spreadsheets/d/1FxoHbmhxKiT2gLkKjbSCeiDYUataLwyz8M6cma99G_Q/edit#gid=691200881")
  
  #Registering the individual worksheets
  test.table <- eventReactive(input$objective_update1, {
    
    dv <- cads.main%>%
      gs_read(ws = "Sheet3")
    
  })
  
  plot.objective <- eventReactive(input$objective_update1, {
    
    obj <- cads.main%>%
      gs_read(ws = "Overall Objectives")
    objstacked <- gather(obj, "Design", "Cost", -1)
    value.stacked <- signif(objstacked[3], digits = 3)
    objstacked1 <- cbind(objstacked[-3], value.stacked)
    
    hchart(objstacked1, "column", hcaes(x = Category, y = Cost, group = Design))%>%
      hc_tooltip(valuePrefix = "$", valueSuffix = " Million USD")%>%
      hc_exporting(
        enabled = TRUE
      )
  })
  
  output$objective_plot <- renderHighchart(data.objective.plot())
  
  data.costbreakdown.plot <- eventReactive(input$objective_update1, {
    
    cost.breakdown <- cads.main%>%
      gs_read(ws = "Cost Breakdown")%>%signif(digits =3)
    
    cost.breakdown.stacked <- gather(cost.breakdown, "Classes", "Cost", -1)
    
    hchart(cost.breakdown.stacked, "column", hcaes(x = Design, y = Cost, group = Classes))%>%
      hc_plotOptions(column = list(stacking = "normal"))%>%
      hc_exporting(
        enabled = TRUE
      )
  })
  output$costbreakdown_plot <- renderHighchart(data.costbreakdown.plot())
  
  output$objective_plot1 <- renderHighchart(plot.objective())
  
  output$decision_table1 <- renderTable(test.table())
  
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
    wastewater.data <- signif(wellpad.operator.outputs$Cost/1000000, digits =3)
    wastewater.label <- c("Impoundment Cost", "Wastewater Storage Cost", "Frack Fluid Storage Cost")
    wastewater.out <- data.frame(wastewater.label, wastewater.data)
    colnames(wastewater.out) <- c("Category", "Cost in $million")
    wastewater.out
    
  })
  output$wellpad_operator_result <- renderTable(data.wastewater())
  
  data.freshwater.results <- eventReactive(input$freshwater_update, {
    
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$freshwater_impoundment_piping, anchor = "B3", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$freshwater_wellpad_piping, anchor = "B4", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$impoundment_pipe_size, anchor = "B6", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$wellpad_pipe_size, anchor = "B7", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    freshwater.expert.output <- cads.main%>%
      gs_read(ws = "Freshwater Transportation Expert", range = "A14:B21")
    
  })
  
  output$freshwater_expert_result <- renderTable(data.freshwater.results())
  
  data.environ.impact <- eventReactive(input$watersource_update, {
    
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$stream_source, anchor = "B10", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$river1_source, anchor = "B11", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Freshwater Transportation Expert", input = input$river2_source, anchor = "B12", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    env.regulator.output <- cads.main%>%
      gs_read(ws = "Environmental Damages", range = "A8:D17")
    env.data <- signif(env.regulator.output[-1]/1000000, digits = 3)
    colnames(env.data) <- c("GHG in $million", "Air Particulate in $million", "Total in $million")
    env.labels <- cbind(env.regulator.output[1], env.data)
  })
  
  output$env_impact <- renderTable(data.environ.impact())
  
  data.freshwater.params <- eventReactive(input$freshwater_update, {
    
    freshwater.expert.pipelineparam <- cads.main%>%
      gs_read(ws = "Freshwater Transportation Expert", range = "C2:E4")
    pipeparamslabel <- c("Impoundment Pipeline", "Wellpad Pipeline")
    pipeparams <- cbind(pipeparamslabel, freshwater.expert.pipelineparam)
    colnames(pipeparams) <- c("Pipeline Type", "Capital Cost of Pipeline ($)", "Upper Capacity of Pipeline", "Pump Cost of Pipeline ($)") 
    pipeparams
  })
  
  output$freshwater_pipeline_param <- renderTable(data.freshwater.params())
  
  data.wastewater.result <- eventReactive(input$wastewater_update, {
    gs_edit_cells(ss = cads.main, ws = "Waste Water Transportation Expert", input = input$central_treatment, anchor = "B3", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Waste Water Transportation Expert", input = input$wastewater_pipeline, anchor = "B4", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    gs_edit_cells(ss = cads.main, ws = "Waste Water Transportation Expert", input = input$wastewater_pipe, anchor = "B6", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    
    wastewater.expert.output <- cads.main%>%
      gs_read(ws = "Waste Water Transportation Expert", range = "A8:B13")%>%
      na.omit()
    wastewateroutput <- signif(wastewater.expert.output[2]/1000000, digits = 3)
    wasteoutput <- cbind(wastewater.expert.output[1],wastewateroutput)
    colnames(wasteoutput) <- c("Category", "Cost in $million")
    wasteoutput
    
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
  
  data.freshwater.validation1 <- eventReactive(input$question1, {
    gs_edit_cells(ss = cads.main, ws = "Validation Questions", input = input$question1, anchor = "B5", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    
    freshwater.answer1 <- ifelse(input$question1 == "False", "Your answer is correct", "Your answer is incorrect. You would prefer the stream to be used for the operation. However, if other participants are willing to make design choice tradeoffs that would lower air emissions damages, you would be willing to allow for other freshwater sources.")
  })
  
  output$answer1 <- renderText(data.freshwater.validation1())
  
  data.freshwater.validation2 <- eventReactive(input$question2, {
    gs_edit_cells(ss = cads.main, ws = "Validation Questions", input = input$question2, anchor = "C5", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    
    freshwater.answer2 <- ifelse(input$question2 == "True", "Your answer is correct", "Your answer is incorrect. Since air emissions damages are calculated using an economic input-output model, higher financial costs is often associated with higher air emissions damages, and vice versa.")
  })
  
  output$answer2 <- renderText(data.freshwater.validation2())
  
  data.freshwater.validation3 <- eventReactive(input$question3, {
    gs_edit_cells(ss = cads.main, ws = "Validation Questions", input = input$question3, anchor = "D5", byrow = FALSE, col_names = NULL, trim = FALSE, verbose = TRUE)
    
    freshwater.answer3 <- ifelse(input$question3 == "False", "Your answer is correct", "Your answer is incorrect. Your main motivation is to minimize the environmental cost resulting from air emissions from the overall operation.")
  })
  
  output$answer3 <- renderText(data.freshwater.validation3())
}

# Run the application 
shinyApp(ui = ui, server = server)

