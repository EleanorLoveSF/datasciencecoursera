---
title: 'P1: PM Air Pollution in USA'
author: "Jingbin Xu"
date: "2017/4/7"
---

# Data
The *specdata.zip* contains 332 CSV files containing pollution monitoring data from fine particulate matter (PM) air pollution at 332 locations in the USA. Each file contains data from a single monitor and the ID number for each monitor is contained in the file name. For example, data for monitor 200 is contained in the file "200.csv". Each file contains three variables. **Data**: the data of the observation in (year-month-day) format, **Sulfate**: the level of sulfate PM in the air on that date (measured in micrograms per cubic meter), and **Nitrate**: the level of nitrate PM in the air on that data (measured in micrograms per cubic meter)

# Part one
Write a function named "pollutantmean" that calculates the mean of a pollutant (sulfate or nitrate) across a specified list of monitors. The function "pollutantmean" takes three arguments:'directory', 'pollutant' and 'id'. Given a vector monitor ID numbers, 'pollutantmean' reads that monitors particulate matter data from the directory specified in the 'directory' argument and returns the mean of the pollutant across all of the monitors, ignoring any missing values coded as NA.
```{r setup, include=FALSE}
pollutantmean <- function(directory, pollutant, id = 1:332) {
  
  setwd(file.path(getwd(), directory)) 
  total = 0                         
  observations = 0                
  

  for (i in id)
{
    
    
    
      if (i <10) { 
                         data <- read.csv(paste("0","0", as.character(i), ".csv", sep=""),  
                                          header = T, 
                                          na.strings=c("NA","NaN", " "))
                 }
      
else if (i>=10 & i<100) { 
                         data <- read.csv(paste("0", as.character(i), ".csv", sep=""),  
                                          header = T, 
                                          na.strings=c("NA","NaN", " ") 
                                          )
                        }
                     
       

     else       { 
                        data <- read.csv(paste(as.character(i), ".csv", sep=""),     
                                         header = T, 
                                         na.strings=c("NA","NaN", " ") 
                                        )
                }
  
  
 data = na.omit(data)    

 observations = observations + nrow(data)
 
  if (pollutant == "sulfate") {total = total + sum(data$sulfate)}
 else {total = total + sum(data$nitrate)}

}
  

  setwd("..")

  return (total/observations)

}
```
