**Name**

wp_read_meta_ghcn_func

**Description**

Function for reading GHCN meta data (V3)
More information see:
ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README

**Usage**

meta<-wp_read_meta_ghcn_func(filepath)

**Input**

only the path of the GHCN meta data file (.inv) is required as input!

**Output**

metatable: data frame

**Author**

AlK
MaO

**Date**

03.07.2014

**TODO**
--------------------------------------------------------------------------


```{r}
wp_read_meta_ghcn_func <- function(datapath) {
metapath <- paste0(substr(datapath,1,nchar(datapath)-3),'inv')

metadata<-readLines(metapath)
```

as.() .. convert to selected datatype
gsub .. remove empty spaces
substr .. cut data from character input (input, from, to)

```{r}
ID          <- substr(metadata,1,11)
LATITUDE    <- as.numeric(gsub(" *$", "", substr(metadata,13,20))) 
LONGITUDE   <- as.numeric(gsub(" *$", "", substr(metadata,22,30)))
STNELEV     <- as.numeric(gsub(" *$", "", substr(metadata,32,37)))
NAME        <- gsub(" *$", "", substr(metadata,39,68))
GRELEV      <- as.integer(substr(metadata,70,73))
POPCLS      <- substr(metadata,74,74)
POPSIZ      <- as.integer(substr(metadata,75,79))
TOPO        <- substr(metadata,80,81)      
STVEG       <- substr(metadata,82,83)    
STLOC       <- substr(metadata,84,85)      
OCNDIS      <- as.integer(substr(metadata,86,87))
AIRSTN      <- substr(metadata,88,88)      
TOWNDIS     <- as.integer(substr(metadata,89,90))
GRVEG       <- substr(metadata,91,106)      
POPCSS      <- substr(metadata,107,107)      


metatable <- data.frame(ID,LATITUDE,LONGITUDE,STNELEV,NAME,GRELEV,POPCLS,
                        POPSIZ,TOPO,STVEG,STLOC,OCNDIS,AIRSTN,TOWNDIS,GRVEG,POPCSS, stringsAsFactors=F)

return(metatable)
}

```




