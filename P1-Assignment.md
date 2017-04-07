---
title: 'P1: PM Air Pollution in USA'
author: "Jingbin Xu"
date: "2017/4/7"
output:
  html_document: default
  pdf_document: default
---

# Data
The *specdata.zip* contains 332 CSV files containing pollution monitoring data from fine particulate matter (PM) air pollution at 332 locations in the USA. Each file contains data from a single monitor and the ID number for each monitor is contained in the file name. For example, data for monitor 200 is contained in the file "200.csv". Each file contains three variables. **Data**: the data of the observation in (year-month-day) format, **Sulfate**: the level of sulfate PM in the air on that date (measured in micrograms per cubic meter), and **Nitrate**: the level of nitrate PM in the air on that data (measured in micrograms per cubic meter)

# Part one
Write a function named "pollutantmean" that calculates the mean of a pollutant (sulfate or nitrate) across a specified list of monitors. The function "pollutantmean" takes three arguments:'directory', 'pollutant' and 'id'. Given a vector monitor ID numbers, 'pollutantmean' reads that monitors particulate matter data from the directory specified in the 'directory' argument and returns the mean of the pollutant across all of the monitors, ignoring any missing values coded as NA.
```{r setup, include=FALSE}
pollutantmean <- function(directory, pollutant, id = 1:332) {
  
  setwd(file.path(getwd(), directory)) ## setting the directory
  total = 0                            ## the sum of all observed values of pollutant (either sulfate or nitrate)
  observations = 0                     ## the total number of observed values of pollutant (either sulfate or nitrate)
  
  #Looping thru the directory's files specified in the 'id' argument 
  for (i in id)
{
    
    
      ## Due to the format of the filename, i.e 001, 010  instead of 1, 10. I became aware that the following method works but not efficient, 
      ## but at the time of the completion of this assignment, it was the only way I knew how to do it.           
      if (i <10) { 
                         data <- read.csv(paste("0","0", as.character(i), ".csv", sep=""),  ## for example, if 'id' =7, we get 007.csv
                                          header = T, 
                                          na.strings=c("NA","NaN", " "))
                 }
      
else if (i>=10 & i<100) { 
                         data <- read.csv(paste("0", as.character(i), ".csv", sep=""),  ## for example, if 'id' = 17, we get 017.csv
                                          header = T, 
                                          na.strings=c("NA","NaN", " ") 
                                          )
                        }
                     
       

     else       { 
                        data <- read.csv(paste(as.character(i), ".csv", sep=""),     ## Normal
                                         header = T, 
                                         na.strings=c("NA","NaN", " ") 
                                        )
                }
  
  ## getting rid of all the "NA" values and, consequently, all the non-complete ovservations (the ones with at least one NA in row)
 data = na.omit(data)    
 ##  cumulative addition of the complete observations
 observations = observations + nrow(data)
 ## depending the poluttant ( sulfate or nitrate), we aggregate the observed values
  if (pollutant == "sulfate") {total = total + sum(data$sulfate)}
 else {total = total + sum(data$nitrate)}

}
  
  ## reset directory path
  setwd("..")
  ## returning the mean of the pollutant values
  return (total/observations)

}
```

# Output
```{r}
pollutantmean("specdata", "sulfate", 1:10)
pollutantmean("specdata", "nitrate", 70:72)
pollutantmean("specdata", "nitrate", 23)
```
