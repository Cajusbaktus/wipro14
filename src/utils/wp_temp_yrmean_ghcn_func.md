**Name**

wp_temp_yrmean_ghcn_func

**Description**

Functions for calculation of annual (yr) station means and their standard deviation of entire GHCN dataset 
or clino (climatological normals) time span of stations that have complete data for a specefied number of years within the clino timespan
- README Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/README
- Data Link: ftp://ftp.ncdc.noaa.gov/pub/data/ghcn/v3/

**Usage**

MEAN <- wp_ghcn_yr_mean(data, SD=TRUE/FALSE, clino=TRUE/FALSE, valid_clino_yr)

Default: - SD       = F (standard deviation, logical)
         - sub      = c(1961,1990) (user defined time span default is clino, numeric)
         - valid_yr =  100 (percentage of minimum valid years, numerical)

**Input**
source(wp_read_data_ghcn_func())
data: ghcn monthly (as data frame)

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

wp_temp_yrmean_ghcn_func <- function(data, SD=FALSE, sub=c(1961,1990),valid_yr=100) {

data <- subset(data, YEAR >= sub[1] & YEAR <= sub[2])  



     
return(outdata)

}

```