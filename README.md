# Human Activity Recognition Using Smartphones:

# I.  Introduction:

Since 1870 a large growth in human life expectancy has been observed in Europe. This growth has expanded in the whole world principally due to the great achievements in health care field. As a result, the proportion of elderly people is rapidly increasing. Aging people in general lives in isolated conditions. In addition to that some of them are not capable to live normally and take advantages from health care facilities services. Building remote monitoring systems for elderly patients who live alone or without permanent caretaking will improve their quality of life. For better decision making these remote monitoring systems needs some regular and trustful information about patients.

#### Project Origins:
To fulfil remote monitoring systems’ requirements [Jorge Luis Reyes Ortiz](https://www.icephd.org/wiki/index.php/Jorge_Luis_Reyes_Ortiz) has developed a complete [Human Activity Recognition System](https://en.wikipedia.org/wiki/Activity_recognition) able to detect and recognize 12 different activities performed by humans in their daily living in online mode using smartphones. The recognition part of his system is based on an [SVM model](https://en.wikipedia.org/wiki/Support_vector_machine) already trained, capable of predicting activities performed by users. Necessary datasets of users’ movements will be collected from smartphone sensors ([accelerometer](https://en.wikipedia.org/wiki/Accelerometer) and [gyroscope](https://en.wikipedia.org/wiki/Gyroscope)). The datasets will be processed and fed to the prediction model to recognize performed activities.

To build the final model embedded in this HAR system. An offline version of this system needs to be created for two reasons:
##### 1. To construct the signal processing pipeline and process the original data collected.
##### 2. To build the train-test pipelines and test different state of art ML alogrithms to choose the optimal one.


#### Project Overview:
The goal of this project is to build a machine learning model and a signal processing pipeline in offline mode capable of processing signals collected using smart phone inertial sensors (accelerometer and gyroscope) and producing useful datasets will be used as inputs of a machine learning model capable of recognizing some of human daily activities (sitting, walking …) included in the dataset (see datasets and Inputs section) with a low error rate. The signal processing pipeline and the final model could be used as a good source of information about patient’s daily activities needed by remote monitoring systems mentioned earlier

# II. Software Requirements:
This project requires **Python 3.5 ** and the following Python libraries installed:
- [Python 3.5](https://www.python.org/download/releases/3.0/) 
- [NumPy](http://www.numpy.org/)  , [SciPy](https://www.scipy.org/) , [Pandas](https://pandas.pydata.org/) , [matplotlib](http://matplotlib.org/)
- [Statsmodel](http://www.statsmodels.org/stable/index.html)  , [Spectrum](https://pypi.org/project/spectrum/) , [scikit-learn](http://scikit-learn.org/stable/)
#### Install:
We recommend to install [Anaconda](https://www.continuum.io/downloads), a pre-packaged Python distribution that contains some of the necessary libraries and software for this project make to install an Anaconda environment that includes python 3.x . 
You will also need to have software installed to run and execute an [iPython Notebook](http://ipython.org/notebook.html)

You could import the used environment via the YAML file.

# III. Project Architecture:

This repository includes three main directories and 7 files:

### III-1. Directories:

	- `\Description-Images\`: This folder includes images used for aesthetic purposes
	
	- `\Reports\`: Contains an HTML version of each notebook + 2 reports
	
	- `.\Data\`: Under this Directory you will find all Datasets used in this project.
		- `.\Original-Data\`: contains the original Datasets brought by Jorge Luis Reyes Ortiz.	
			- `. \UCI-HAR-Dataset\`:  The first version of this Dataset V 1.0
			- `. \HAPT-Dataset\`: The second version V 2.0
		
		
		-`.\ New Data\`: Under this directory you will find the processed datasets generated from the original 
		                 ones using: `Part_I--Signal-Processing-Pipeline.ipynb`. 
		
### III-2. Notebooks:

	- `Part_I--Signal-Processing-Pipeline.ipynb`: This is jupyter notebook file which contains the signal processing 
	                                              pipeline, visualizations and detailed analysis of each step 
						      performed in this part.	
	
	- `Part_II--Machine-Learning-Part.ipynb`:  This is jupyter notebook file which contains  python code related to 
	                                           machine learning, visualizations and detailed analysis of each step 
						   performed to build the final model.
	

	- `UCI_HAR_Dataset_V1.ipynb`:
	- `UCI_HAR_Dataset_V1_Inertial_Signals.ipynb`:
	

	- `HAPT_RawData_statistics_V2.ipynb`
	- `HAPT_ML_V2.ipynb`
	
	- `README.md` : It contains a short description of this project and necessary steps to 
	                run it successfully.


# IV. Datasets and Inputs:
## IV-1. Original Datasets
### . The general process:

### A. The Experiment:
The experiments were carried out with a group of 30 volunteers within an age bracket of 19-48 years. They performed a protocol of activities composed of six basic activities: three static postures (standing, sitting, lying) and three dynamic activities (walking, walking downstairs and walking upstairs). The experiment also included postural transitions that occurred between the static postures. These are: stand-to-sit, sit-to-stand, sit-to-lie, lie-to-sit, stand-to-lie, and lie-to-stand. 
All the participants were wearing a smartphone (Samsung Galaxy S II) on the waist during the experiment execution. They captured 3-axial linear acceleration and 3-axial angular velocity at a constant rate of 50Hz using the embedded accelerometer and gyroscope of the device. The experiments were video-recorded to label the data manually. The resulted dataset stored in the directory `Raw-Data` could be considered as the original labelled dataset and from it different subsets would be generated.
### B. Data Splitting:
This `Raw-Data` was randomly partitioned into two sets, where 70% of the volunteers was selected for generating the training data and 30% the test data.
### C. Signal Processing:
##### Noise filtering:
The features selected for this database come from the accelerometer and gyroscope 3-axial raw signals t_Acc-XYZ and t_Gyro-XYZ. These time domain signals (prefix 't' to denote time) were captured at a constant rate of 50 Hz. Then they were filtered using a median filter and a 3rd order low pass Butterworth filter with a corner frequency of 20 Hz to remove noise. 
1-	Median Filter:  was applied to reduce background noise
2-	A 3rd order Low pass Butterworth filter with a cut-off, frequency = 20hz was applied to remove high frequency noise.
Resulted Signals are:  total_acc_XYZ and Gyro_XYZ.
##### Gravity filtering:
Similarly, the acceleration signal total-acc-XYZ was then separated into body and gravity acceleration signals (tBodyAcc-XYZ and tGravityAcc-XYZ) using another low pass Butterworth filter with a corner frequency of 0.3 Hz. Since the gravitational force is assumed to have only low frequency components.
Resulted components are: total_acc-XYZ ==> tBody_acc-XYZ + tGravity_acc-XYZ


### D. Activity Selection:
From the processed signals above presented in the picture above, they extract data points and activity labels related only to the first six basic activities which are: standing, sitting, lying, walking, walking downstairs and walking upstairs to build the first version of this dataset.
In the second version which concerns basic activities and postural transitions all the 12 activities were selected.
### E. Feature Selection:
Subsequently, the body linear acceleration and angular velocity were derived in time to obtain Jerk signals (tBodyAccJerk-XYZ and tBodyGyroJerk-XYZ). Also, the magnitude of these three-dimensional signals was calculated using the Euclidean norm (tBodyAccMag, tGravityAccMag, tBodyAccJerkMag, tBodyGyroMag, tBodyGyroJerkMag). 
Finally, a Fast Fourier Transform (FFT) was applied to some of these signals producing fBodyAcc-XYZ, fBodyAccJerk-XYZ, fBodyGyro-XYZ, fBodyAccJerkMag, fBodyGyroMag, fBodyGyroJerkMag. (Note the 'f' to indicate frequency domain signals). 
These signals were used to estimate variables of the feature vector for each pattern:  
'-XYZ' is used to denote 3-axial signals in the X, Y and Z directions.
### F. Windowing:
These features were then sampled in fixed-width sliding windows of 2.56 sec and 50% overlap (128 readings/window).
### G. Features Generation:
From each window, a vector of 561 features was obtained by calculating variables from the time and frequency domain. See 'features_info.txt' for more details.



