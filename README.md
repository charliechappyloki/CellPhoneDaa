run_analysis is a function that creates a tidy data data frame from cellphone motion readings for the movements of 30 people.
	
	First install and load the dplyr package for ease of data frame manipulations.
	
	subjecttest is the 1 column subject table of people in the test group
	Xtest is the table of all the feature data collected from cell phone movement for the test group.
	ytest is the 1 column table consisting of the number corresponding to each activity- 1=walking, ect. for the test group
	
	subjecttrain is the 1 column subject table of people in the training data group
	Xtrain is the table of all the feature data collected from cell phone movement for the training data group.
	ytrain is the 1 column table consisting of the number corresponding to each activity- 1=walking, ect. for the training data     group
	
	testDF - the data frame merging the test subject, the test subject activity, and the test group data
	trainDF - the data frame merging the traing group subjects, the traing group activity, and the traing group data
	entireDF - combines the training and test data frames into one data frame of 30 people
  
  features - the list of names of the features of all the types of motion data recorded from the cell phones
	features <- c("subject","activity",features) ## adds the headers to subject and activity columns when the names are
	assigned in the next line of code -
	colnames(entireDF) <- features 
	
	meanSDdf <- select(entireDF, subject, activity,
		grep("mean()", names(entireDF), fixed=TRUE),
		grep("std()", names(entireDF), fixed=TRUE))  ## this code uses the dplr package. creates a data frame that selects
		                                                only the columns we need
	
	meanSDdf[meanSDdf$activity==1, 2] <- "walking"       ##these lines of code replace the number signifier of the activity
	meanSDdf[meanSDdf$activity==2, 2] <- "walkingUp"     ##with the more discriptive wording   
	meanSDdf[meanSDdf$activity==3, 2] <- "walkingDown"
	meanSDdf[meanSDdf$activity==4, 2] <- "sitting"
	meanSDdf[meanSDdf$activity==5, 2] <- "standing"
	meanSDdf[meanSDdf$activity==6, 2] <- "laying"
	
	finalTidy <- aggregate(meanSDdf, by=list(meanSDdf$subject, meanSDdf$activity), FUN=mean)
	finalTidy                                    ##this data frame creates the tidy data set with the average of each variable                                                ##for each activity and each subject. 
	
	tidyData <- finalTidy[,c(1:2, 5:70)]         ##these last lines of code fix up the little bit of untidiness caused by
	                                             ##my unenlightened use of the aggregate function
	colnames(tidyData)[1] <- "subject"
	colnames(tidyData)[2] <- "activity"
	tidyData
	}
