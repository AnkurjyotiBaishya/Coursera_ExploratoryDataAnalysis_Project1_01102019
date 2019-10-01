# Coursera_ExploratoryDataAnalysis_Projec1_01102019
Week 1 Peer Review Assignment of Coursera's Exploratory Data Analysis course

#This is the submission to Project 1 of Exploratory Data Analysis,the Coursera course. Following is the full code.

#Full Code



#LOADING DATA
full.data <- read.table("household_power_consumption.txt", header=TRUE, sep=";", na.strings = "?", colClasses = c('character','character','numeric','numeric','numeric','numeric','numeric','numeric','numeric'))

#converting classes
full.data$Dates <- as.Date(full.data$Date,"%d/%m/%Y")
full.data$Date.Time <- paste(full.data$Dates, full.data$Time, sep = " ")
full.data$Times <- strptime(full.data$Date.Time, format = "%Y-%m-%d %H:%M:%S")

#subsetting necessary data
power.consumption <- full.data[which(full.data$Dates >= "2007-02-01" & full.data$Dates <= "2007-02-02"),]
power.consumption$Weekdays <- weekdays(power.consumption$Dates)



#MAKING PLOTS

#Plot 1
png("plot1.png", width = 480, height = 480)
hist(power.consumption$Global_active_power, col = "red", xlab = "Global Active Power (kilowatts)", ylab = "Frequency", main = "Global Active Power")
dev.off()

#Plot 2
png("plot2.png", width = 480, height = 480)
plot(x = power.consumption$Times, y = power.consumption$Global_active_power, type = "l", xlab = "", ylab = "Global Active Power (kilowatts)")
dev.off()

#Plot 3
png("plot3.png", width = 480, height = 480)
plot(x = power.consumption$Times, y = power.consumption$Sub_metering_1, type = "l", xlab = "", ylab = "Energy sub metering")
lines(x = power.consumption$Times, y = power.consumption$Sub_metering_2, col = "red")
lines(x = power.consumption$Times, y = power.consumption$Sub_metering_3, col = "blue")
legend("topright", c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lty = 1, col = c("black", "red", "blue"))
dev.off()

#Plot 4
png("plot4.png", width = 480, height = 480)
par(mfrow = c(2,2))
plot(x = power.consumption$Times, y = power.consumption$Global_active_power, type = "l", xlab = "", ylab = "Global Active Power")
plot(x = power.consumption$Times, y = power.consumption$Voltage, type = "l", xlab = "datetime", ylab = "Voltage")
plot(x = power.consumption$Times, y = power.consumption$Sub_metering_1, type = "l", xlab = "", ylab = "Energy sub metering")
lines(x = power.consumption$Times, y = power.consumption$Sub_metering_2, col = "red")
lines(x = power.consumption$Times, y = power.consumption$Sub_metering_3, col = "blue")
legend("topright", c("Sub_metering_1", "Sub_metering_2", "Sub_metering_3"), lty = 1, col = c("black", "red", "blue"))
plot(x = power.consumption$Times, y = power.consumption$Global_reactive_power, type = "l", xlab = "datetime", ylab = "Global_reactive_power")
dev.off()

#end
