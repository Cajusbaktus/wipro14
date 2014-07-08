Main skript to read, rechape and plot GHCN data
========================================================
set up environment
set the workindirektory to the local repository as root level (change this!)

```{r}
setwd("d:\\TUB\\Lehre\\SoSe14\\wiPro\\wipro14")
```

activate packages needed (install if functions are missin)

```{r}
library(ggplot2)
library(reshape)
```

source the functions needed

```{r}
source('src/datasets/wp_read_data_ghcn_func.r')   # function that reads the temperature data
source('src/datasets/wp_read_meta_ghcn_func.r')   # function that reads the meta data
source('src/utils/wp_temp_yrmean_ghcn_func.r')    # function that reads the meta data
source('src/utils/wp_merge_meta_temp_ghcn_func.r')# function that merges temperature and all meta data
```
Start computation:

1. get input ghcn (read meta and data - you need to change filepaths to your local copies of GHCN data!)
```{r}
filedata <- "d:\\TUB\\Lehre\\SoSe14\\wiPro\\GHCN\\ghcnm.v3.2.2.20140511\\ghcnm.tavg.v3.2.2.20140511.qca.dat"
filemeta <- "d:\\TUB\\Lehre\\SoSe14\\wiPro\\GHCN\\ghcnm.v3.2.2.20140511\\ghcnm.tavg.v3.2.2.20140511.qca.inv"
data <-wp_read_data_ghcn_func(filedata)
meta <-wp_read_meta_ghcn_func(filedata)
```
2. Compute mean of temperature (default is CLINO bit can be changed see documentation header of the function)
```{r}
temp<- wp_temp_yrmean_ghcn_func(data)
```
3. Merge computed temperature data with meta of the corresponding station ID 
```{r}
temp_meta<-wp_merge_meta_temp_ghcn_func(temp,meta)
```
4. Now comes the fun part :-) so I leave it up to you (lm(), qplot(), str()) go for it!!!
function lm () checkout this webseit: 
http://www.statmethods.net/stats/regression.html
information on how to use qplot(): 
http://www.statmethods.net/advgraphs/ggplot2.html
http://www.r-bloggers.com/basic-introduction-to-ggplot2/

```{r}
myplt<-qplot(sqrt(temp_meta$LATITUDE^2), temp_meta$temperature)
myplt <- myplt + stat_smooth(method="lm")
myplt

```

