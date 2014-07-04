**Name**

wp_temp_yrmean_ghcn_func

**Description**

Functions for calculation of annual (yr) station means and their standard deviation of entire GHCN dataset 
or clino (climatological normals) time span of stations that have complete data for a specefied number of years within the clino timespan
- README Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README
- Data Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/

**Usage**
library(reshape)
MEAN <- wp_ghcn_yr_mean(data, SD=TRUE/FALSE, clino=TRUE/FALSE, valid_clino_yr)

Default: - SD       = F (standard deviation, logical)
         - sub      = c(1961,1990) (user defined time span default is clino, numeric)
         - valid_yr =  100 (percentage of minimum valid years, numerical)

**Input**

data: ghcn monthly (as data frame <- wp_read_data_ghcn_func())

**Output**
outdata (data frame)

**Example**

out <- wp_ghcn_yr_mean(ghcn_month,clino=T,valid_clino_yr=25)

**Author**

AlK, Moh ,MaO

**Date**

AlK 25.06.2014: first version
MaO 03.07.2014 improved code (base version of Moh)

**TODO**


```{r}

wp_temp_yrmean_ghcn_func <- function(data, SD=FALSE, sub=c(1960,1991),valid_yr=100) {

data <- subset(data, YEAR >= sub[1] & YEAR <= sub[2])  

cnt_yrs<-  sub[2]-sub[1]

molted_data<- melt(data, id.vars= c("ID","YEAR"), measure.vars=c("VALUE1","VALUE2","VALUE3","VALUE4","VALUE5","VALUE6","VALUE7","VALUE8","VALUE9","VALUE10","VALUE11","VALUE12"))

not_valid_months_stations <- cast(molted_data, ID~variable,function(x) cnt_yrs-length(x))





return(outdata)

}

```