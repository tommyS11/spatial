# spatial


#install.packages("shiny")
#install.packages("tmap")
#install.packages("dplyr")

library(shiny)
library(tmap)
library(dplyr)


data('World')
ui <- fluidPage(
  tmapOutput('map'),
  selectInput('var', 'Select country',
              choices = c('Global', as.character(World$name)),
              selected = 'Global')
)
server <- function(input, output, session) {
  output$map <- renderTmap({
    if(input$var == 'Global'){
      qtm(World, 'name')
    }else{
      qtm(filter(World, name == input$var))
    }
  })
}
shinyApp(ui, server)
