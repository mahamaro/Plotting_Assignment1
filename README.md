# Plotting_Assignment1
##Reading data
 household_power_consumption <- read.csv("C:/Users/andry/Documents/R/Exploratory Data analysis/exdata_data_household_power_consumption/household_power_consumption.txt", sep=";", stringsAsFactors=FALSE)
 household_power_consumption$DateTime<-with(household_power_consumption, strptime(paste(Date, Time, sep=" "),"%d/%m/%Y %H:%M:%S"))

 str(household_power_consumption)

 household_power_consumption$Date<-as.Date(household_power_consumption$Date,format="%d/%m/%Y")

 head(household_power_consumption)
 str(household_power_consumption)
 subdata <- subset(household_power_consumption, household_power_consumption$Date %in% as.Date(c("2007-02-01", "2007-02-02")))
 str(subdata)

##Plotting

hist(as.numeric(subdata$Global_active_power), main="Global Active Power")
hist(as.numeric(subdata$Global_active_power), main="Global Active Power", xlab="Global Active Power(Kilowatts)", col=2)

	## saving to plot1.png

with(subdata, hist(as.numeric(subdata$Global_active_power), main="Global Active Power", xlab="Global Active Power(Kilowatts)", col=2))
dev.copy(png, file="plot1.png")
dev.off()

## plot2
plot(as.numeric(subdata$Global_active_power),type="l",xaxt="n",xlab=" ",ylab="Global Active Power(Kilowatts)")
dev.copy(png, file="plot2.png")
dev.off()

##Plot3

## converting energy sub mettering as.numeric
subdata$Sub_metering_1<- as.numeric(subdata$Sub_metering_1)
subdata$Sub_metering_2<- as.numeric(subdata$Sub_metering_2)

	###ploting them together
plot(subdata$Sub_metering_1, type="n", xaxt="n",xlab="", ylab="Energy Sub metering")
points(subdata$Sub_metering_1, type="l")
points(subdata$Sub_metering_2, type="l", col="red")
points(subdata$Sub_metering_3, type="l", col="blue")
	### legend
legend("topright", c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), col=c(1, 2, 4), merge=TRUE, lty = c(1, 1, 1))
	###saving plot.png
dev.copy(png, file="plot3.png")
dev.off()
##Plot4
###creating Datetime_voltage plot
str(subdata)
plot(x=subdata$DateTime, y=as.numeric(subdata$Voltage), type="l")
##save Datetime_voltage
dev.copy(png, file="DateTime.png")
dev.off()

###Creating Global_active_power by DateTime
plot(x=subdata$DateTime, y=as.numeric(subdata$Global_reactive_power), type="l")
dev.copy(png, file="reactivepower.png")
dev.off()

##plot4.png
par(mfcol=c(2,2))
plot(as.numeric(subdata$Global_active_power),type="l",xaxt="n",xlab=" ",ylab="Global Active Power(Kilowatts)")
plot(subdata$Sub_metering_1, type="n", xaxt="n",xlab="", ylab="Energy Sub metering")
points(subdata$Sub_metering_1, type="l")
points(subdata$Sub_metering_2, type="l", col="red")
points(subdata$Sub_metering_3, type="l", col="blue")
	### legend
legend("topright", c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), col=c(1, 2, 4),  lty = c(1, 1, 1), bty="n", cex=0.75)
plot(x=subdata$DateTime, y=as.numeric(subdata$Voltage), type="l", xlab="datetime", ylab="Voltage")
plot(x=subdata$DateTime, y=as.numeric(subdata$Global_reactive_power), type="l", xlab="datetime", ylab="Global_reactive_power")
	###copy Plot4.png
dev.copy(png, file="Plot4.png")
dev.off()
