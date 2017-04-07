---
title: "P3:PM Air Pollution in USA"
author: "Jingbin Xu"
date: "2017/4/7"
output: html_document
---
# Part three
Write a function that takes a directory of data files and a threshold for complete cases and calculates the correlation between sulfate and nitrate for monitor locations where the number of completely observed cases(on all variables) is greater than the threshold. The function should return a vector of correlations for the monitors that meet the threshold requirement. If no monitors meet the threshold requirement, then the function should return a numeric vector of length 0.

```{r setup, include=FALSE}
corr <- function(directory, threshold = 0) {
setwd(file.path(getwd(), directory)) 

correlationVector = NULL 
  for (i in 1:332)
{
           
      if (i <10) { 
                         data <- read.csv(
                                          paste("0","0", as.character(i), ".csv", sep=""), header = T, na.strings=c("NA","NaN", " ")
                                    )}
      
else if (i>=10 & i<100) { 
                         data <- read.csv(
                                          paste("0", as.character(i), ".csv", sep=""),   header = T, na.strings=c("NA","NaN", " ") 
                                          
                                          )
                        }
                     
       
     else       { 
                        data <- read.csv(
                                         paste(as.character(i), ".csv", sep=""),  header = T, na.strings=c("NA","NaN", " ") 
                                        
                                         )
                }
  
    data = na.omit(data) 
    
    if (nrow(data) > threshold) {
                                  correlationVector = c(correlationVector, cor(data[,2], data[,3]))
                               }
    
    
  }
  
  
  
  setwd("..")  
  return (correlationVector)
}
```
