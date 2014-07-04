**Name**

wp_temp_yrmean_ghcn_func

**Description**

Functions for calculation of annual (yr) station means and their standard deviation of entire GHCN dataset 
or clino (climatological normals) time span of stations that have complete data for a specefied number of years within the clino timespan
- README Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README
- Data Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/

**Usage**
library(reshape)
MEAN <- wp_temp_yrmean_ghcn_func(data, SD=TRUE/FALSE, clino=TRUE/FALSE, valid_clino_yr)

Default:-agg_meth:mean (default) aggrigation method of monthly means for annual mean 
                  (options other than default: 'sd', 'max','min', character)  
        - sub    :c(1961,1990) (user defined time span default is clino, numeric)
        - valid  :100 (percentage of minimum valid years, numeric)

**Input**

data: ghcn monthly (as data frame <- wp_read_data_ghcn_func())

**Output**
outdata (data frame)

**Example**

max_clino<-wp_temp_yrmean_ghcn_func(data, agg_meth='max')

**Author**

AlK, Moh ,MaO

**Date**

AlK 25.06.2014: first version
MaO 03.07.2014 improved code (base version of Moh)

**TODO**


```{r}

wp_temp_yrmean_ghcn_func <- function(data, sub=c(1961,1990),valid=100, agg_meth = 'mean') {
library(reshape)
data <- subset(data, YEAR >= sub[1] & YEAR <= sub[2])  

cnt_yrs<-  sub[2]-sub[1]

molted_data<- melt(data, id.vars= c("ID","YEAR"), measure.vars=c("VALUE1","VALUE2","VALUE3","VALUE4","VALUE5","VALUE6","VALUE7","VALUE8","VALUE9","VALUE10","VALUE11","VALUE12"))

if (agg_meth == 'sd'){
             outdata <- subset(apply(cast(molted_data, ID~variable,mean),1,sd),
                apply(cast(molted_data, ID~variable,function(x) sum(!is.na(x))/((cnt_yrs+1)*0.01)),1,mean) == valid)
} 
if(agg_meth == 'max'){ 
            outdata <- subset(apply(cast(molted_data, ID~variable,mean),1,max),
              apply(cast(molted_data, ID~variable,function(x) sum(!is.na(x))/((cnt_yrs+1)*0.01)),1,mean) == valid)
} 
if(agg_meth == 'min'){ 
            outdata <- subset(apply(cast(molted_data, ID~variable,mean),1,min),
              apply(cast(molted_data, ID~variable,function(x) sum(!is.na(x))/((cnt_yrs+1)*0.01)),1,mean) == valid)
}  
if(agg_meth == 'mean'){
              outdata <- subset(apply(cast(molted_data, ID~variable,mean),1,mean),
                apply(cast(molted_data, ID~variable,function(x) sum(!is.na(x))/((cnt_yrs+1)*0.01)),1,mean) == valid)
}

stationid  <-names(outdata)
temperature <- as.vector(outdata)
outdata     <- data.frame(cbind(stationid,temperature))
return(outdata)

}

```