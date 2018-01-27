# Dallas-data-analysis

install.packages("rsatscan")
library(rsatscan)

#resetting parameter file:
#create a .cas and .geo file

#setting working directory 
#td = tempdir()

td="C:/Users/monsu/Documents/UniLeeds/RSATSCAN/"

setwd(td)

Result <- NULL

data <- read.table(file="Dallas_Police_RMS_for_SatScan_UTM2.csv", sep=",", head=TRUE)

getwd()
#------------------------------------------------
library(rgdal)
#import the boundary shapefile
districts <- readOGR(dsn=".", "final_districtMap") # head(data)


#the coordinate of the districts shapefile
coord_Sys <- crs(districts)

# manually set the colors for the plot!
colfunc <- colorRampPalette(c("white", "black"))
colfunc <- colfunc(15)
colfunc <- colfunc[order(as.numeric(districts$Population))]

#normalise the population column for plotting

x <- as.numeric(as.vector(districts@data$Population))
x <- 1/x

