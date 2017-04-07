---
title: "P2:PM Air Pollution in USA"
author: "Jingbin Xu"
date: "2017/4/7"
---

# Part two
Write a function that reads a directory full of files and reports the number of completely observed cases in each data file. The function should return a dataframe where the first column is the name of the file and the second column is the number of complete cases.

```{r}
knitr::opts_chunk$set(echo = TRUE)
complete <- function(directory, id = 1:332) {
  
  
  dataframe = NULL  
  setwd(file.path(getwd(), directory)) 
  for (i in id){
    
      if (i <10) { 
                         data <- read.csv(paste("0","0", as.character(i), ".csv", sep=""),  header = T, na.strings=c("NA","NaN", " "))
                 }
      
else if (i>=10 & i<100) { 
                         data <- read.csv(paste("0", as.character(i), ".csv", sep=""),  header = T, na.strings=c("NA","NaN", " ") 
                                          )
                        }
                     
       

     else       { data <- read.csv(paste(as.character(i), ".csv", sep=""),    header = T, na.strings=c("NA","NaN", " ") 
                                        )
                }
  

    data = na.omit(data) 
    data = as.matrix(data)
    dataframe = rbind(dataframe, c(i,nrow(data))) 
    
    
  }
  
  setwd("..")  
  dataframe = data.frame(dataframe)  
  names(dataframe) = c('id', 'nobs') #
  return (dataframe) 
}

```
