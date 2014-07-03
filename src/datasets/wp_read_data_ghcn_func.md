**Name**

wp_read_data_ghcn_func

**Description**

Functions for reading GHCN data
More information see:
ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README

**Usage** 

data<-wp_read_data_ghcn_func(filepath)

**Input**
datapath: absolute file path


**Output**
datatable: data frame


**Author**

AlK
MaO

**Date**

08.05.2014

**TODO**

- nix

Functions for reading GHCN data
=========================================

1. read data information
------------------------
only the path of the GHCN data file (.dat) is required as input!

```{r}
wp_read_func_GHCN_dat <- function(datapath) {
  
data<-readLines(datapath)
```

ab hier noch nicht so richtig schön... geht kürzer, aber nicht schneller .. :)

```{r}
ID  <- substr(data,1,11)
YEAR <- as.integer(substr(data,12,15))
ELEMENT     <- substr(data,16,19)

VALUE1      <- as.numeric(substr(data,20,24))/100.   # transform to °C (see README)
DMFLAG1      <- substr(data,25,25)   
QCFLAG1      <- substr(data,26,26)     
DSFLAG1      <- substr(data,27,27)    

VALUE2      <- as.numeric(substr(data,28,32))/100.   # transform to °C (see README)
DMFLAG2      <- substr(data,33,33)   
QCFLAG2      <- substr(data,34,34)     
DSFLAG2      <- substr(data,35,35)    

VALUE3      <- as.numeric(substr(data,36,40))/100.   # transform to °C (see README)
DMFLAG3      <- substr(data,41,41)   
QCFLAG3      <- substr(data,42,42)     
DSFLAG3      <- substr(data,43,43)    

VALUE4      <- as.numeric(substr(data,44,48))/100.   # transform to °C (see README)
DMFLAG4      <- substr(data,49,49)   
QCFLAG4      <- substr(data,50,50)     
DSFLAG4      <- substr(data,51,51)   

VALUE5      <- as.numeric(substr(data,52,56))/100.   # transform to °C (see README)
DMFLAG5      <- substr(data,57,57)   
QCFLAG5      <- substr(data,58,58)     
DSFLAG5      <- substr(data,59,59)  

VALUE6      <- as.numeric(substr(data,60,64))/100.   # transform to °C (see README)
DMFLAG6      <- substr(data,65,65)   
QCFLAG6      <- substr(data,66,66)     
DSFLAG6      <- substr(data,67,67)  

VALUE7      <- as.numeric(substr(data,68,72))/100.   # transform to °C (see README)
DMFLAG7      <- substr(data,73,73)   
QCFLAG7      <- substr(data,74,74)     
DSFLAG7      <- substr(data,75,75)  

VALUE8     <- as.numeric(substr(data,76,80))/100.   # transform to °C (see README)
DMFLAG8      <- substr(data,81,81)   
QCFLAG8     <- substr(data,82,82)     
DSFLAG8      <- substr(data,83,83)  

VALUE9      <- as.numeric(substr(data,84,88))/100.   # transform to °C (see README)
DMFLAG9      <- substr(data,89,89)   
QCFLAG9      <- substr(data,90,90)     
DSFLAG9      <- substr(data,91,91)  

VALUE10      <- as.numeric(substr(data,92,96))/100.   # transform to °C (see README)
DMFLAG10      <- substr(data,97,97)   
QCFLAG10      <- substr(data,98,98)     
DSFLAG10      <- substr(data,99,99)  

VALUE11      <- as.numeric(substr(data,100,104))/100.   # transform to °C (see README)
DMFLAG11      <- substr(data,105,105)   
QCFLAG11      <- substr(data,106,106)     
DSFLAG11      <- substr(data,107,107)  

VALUE12      <- as.numeric(substr(data,108,112))/100.   # transform to °C (see README)
DMFLAG12      <- substr(data,113,113)   
QCFLAG12      <- substr(data,114,114)     
DSFLAG12      <- substr(data,115,115)  
```

hier fehlen (noch) die anderen Daten .. Flag, etc..

```{r}

datatable <- data.frame(ID,YEAR,ELEMENT,
                        VALUE1,DMFLAG1,QCFLAG1,DSFLAG1,
                        VALUE2,DMFLAG2,QCFLAG2,DSFLAG2,
                        VALUE3,DMFLAG3,QCFLAG3,DSFLAG3,
                        VALUE4,DMFLAG4,QCFLAG4,DSFLAG4,
                        VALUE5,DMFLAG5,QCFLAG5,DSFLAG5,
                        VALUE6,DMFLAG6,QCFLAG6,DSFLAG6,
                        VALUE7,DMFLAG7,QCFLAG7,DSFLAG7,
                        VALUE8,DMFLAG8,QCFLAG8,DSFLAG8,
                        VALUE9,DMFLAG9,QCFLAG9,DSFLAG9,
                        VALUE10,DMFLAG10,QCFLAG10,DSFLAG10,
                        VALUE11,DMFLAG11,QCFLAG11,DSFLAG11,
                        VALUE12,DMFLAG12,QCFLAG12,DSFLAG12,
                        stringsAsFactors=F)

datatable[datatable==-99.99] <- NA       # Exclude missing values

return(datatable)
}

```