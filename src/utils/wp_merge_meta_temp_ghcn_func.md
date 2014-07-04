**Name**
wp_merge_meta_temp_ghcn_func

**Input**
temp: mean temp data - output from wp_temp_yrmean_ghcn_func (named numeric)
meta: meata data output from wp_read_meta_ghcn_func (data frame)
```{r}

wp_merge_meta_temp_ghcn_func -<function(temp, meta){

merged<-merge(temp,meta,by.x = c("stationid"), by.y=c("ID"))
  
merged$temperature<-(as.numeric(as.character((merged$temperaure))))
merged$POPCLS<-as.factor(merged$POPCLS)
merged$TOPO  <-as.factor(merged$TOPO)
merged$STVEG <-as.factor(merged$STVEG)
merged$STLOC <-as.factor(merged$STLOC)
merged$AIRSTN<-as.factor(merged$AIRSTN)
merged$GRVEG <-as.factor(merged$GRVEG)
merged$POPCSS<-as.factor(merged$POPCSS)

merged$POPSIZ[merged$POPSIZ<=0] <- NA
merged$OCNDIS[merged$OCNDIS<=0] <- NA
merged$TOWNDIS[merged$TOWNDIS<=0] <- NA
merged$STNELEV[merged$STNELEV<=0] <- NA

return(merged)

}

```



