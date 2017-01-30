##These codes are generic.
###Simply replace the '2016'and'WI16.txt' in the first line with the year or state you want.





link_WI16="https://www.fhwa.dot.gov/bridge/nbi/2016/delimited/WI16.txt"

WI16=read.csv(link_WI16,colClasses = "character",sep=",")

##create the 5-digits FIPS code
WI16$FIPS=paste0(WI16$STATE_CODE_001,WI16$COUNTY_CODE_003)







##combine bridge ID, year, fips codes, condition ratings
attach(WI16)
WI16_required=cbind(
STRUCTURE_NUMBER_008,
YEAR_BUILT_027,
FIPS,
DECK_COND_058,SUPERSTRUCTURE_COND_059,SUBSTRUCTURE_COND_060,CHANNEL_COND_061,CULVERT_COND_062,OPERATING_RATING_064,INVENTORY_RATING_066)

##combine total cost,structure length and toll
WI16_mine=cbind(TOTAL_IMP_COST_096,STRUCTURE_LEN_MT_049,TOLL_020) 
output=as.data.frame(cbind(WI16_required,WI16_mine))



##output 
write.csv(output,file="myWI16")
