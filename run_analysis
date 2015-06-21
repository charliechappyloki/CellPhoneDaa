run_analysis <- function{
	install.packages("dplyr")
	library(dplyr)
	subjecttest <- read.table("./UCI_HAR_Dataset/subject_test.txt")
	Xtest <- read.table("./UCI_HAR_Dataset/X_test.txt")
	ytest <- read.table("./UCI_HAR_Dataset/y_test.txt")
	subjecttrain <- read.table("./UCI_HAR_Dataset/subject_train.txt")
	Xtrain <- read.table("./UCI_HAR_Dataset/X_train.txt")
	ytrain <- read.table("./UCI_HAR_Dataset/y_train.txt")
	testDF <- cbind(subjecttest, ytest, Xtest)
	trainDF <- cbind(subjecttrain, ytrain, Xtrain)
	entireDF <- rbind(testDF, trainDF)
	features <- readLines("./UCI_HAR_Dataset/features.txt")
	features <- c("subject","activity",features)
	colnames(entireDF) <- features
	meanSDdf <- select(entireDF, subject, activity,
		grep("mean()", names(entireDF), fixed=TRUE),
		grep("std()", names(entireDF), fixed=TRUE))
	meanSDdf[meanSDdf$activity==1, 2] <- "walking"
	meanSDdf[meanSDdf$activity==2, 2] <- "walkingUp"
	meanSDdf[meanSDdf$activity==3, 2] <- "walkingDown"
	meanSDdf[meanSDdf$activity==4, 2] <- "sitting"
	meanSDdf[meanSDdf$activity==5, 2] <- "standing"
	meanSDdf[meanSDdf$activity==6, 2] <- "laying"
	finalTidy <- aggregate(meanSDdf, by=list(meanSDdf$subject, meanSDdf$activity), FUN=mean)
	finalTidy
	tidyData <- finalTidy[,c(1:2, 5:70)]
	colnames(tidyData)[1] <- "subject"
	colnames(tidyData)[2] <- "activity"
	tidyData
	}
