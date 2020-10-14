							Windchill Deployment Script
				================================================
The Windchill build needs to be copied to %WT_HOME%/wtSafeArea/siteMod on the Windchill server. From there, 
the build script will deploy all of the artifacts to %WT_HOME% and then load them into Windchill. 

NOTE: Most artifacts can be overlayed and loaded more than once, but certain artifacts like templates cannot and 
must be cleared out of the system or renamed via the Windchill UI before an updated build can be run. 

Build Contents:
	codebase - 	contains the Publication Structure and Information Structure templates
	loadFiles -	contains the load files for object initialization rules, preferences, container templates, type 
				definitions and workflows.
	loadXMLFiles - contains the XML load files for the container templates and import rule XSL file.
	src	-		custom Java class source files.
	tasks -		empty at the moment, but will contain any Info*Engine tasks
	wtCustom - 	contains custom enumerations and rbInfo files   
	srclib - 	contains .jar files and class libraries needed for the customizations contained in the build
	config - 	contains Windchill settings that will be set during the build
	build.xml -	the Ant deployment script
	
Deployment Instructions:
1. 	Unzip the build .zip file and copy the contents to %WT_HOME%/wtSafeArea/siteMod on the Windchill server.
	Note: if the wtSafeArea or siteMod directories do not already exist, create them. 
2.	Open a Windchill shell. 
	Note: if the Method Server is not already running, start it.
3. 	Change directories to %WT_HOME%/wtSafeArea/siteMod.
	cd %WT_HOME%/wtSafeArea/siteMod
4.	Run the following command to compile the custom class files:
	ant -f deploy.xml compile
5.	Select "n" when prompted to restart Windchill.
6.	Run the following command to deploy the custom enumerations and run the makeJar task:
	ant -f deploy.xml deployEnumerations
7.	Select "y" when prompted to restart Windchill.
	IMPORTANT: Windchill has to be restarted before proceeding to the next step.	
8.	Run the following command to deploy the Windchill atrifacts:
	ant -f deploy.xml init
9. 	Enter your Windchill username when prompted. 
	NOTE: this user must have Site admin privileges. 
10.	Enter your Windchill password when prompted.
11.	Enter the Windchill Organization name when prompted (e.g. Defense).
12.	Check the deploy_<timestamp>.log file for any errors.
13. Log into Windchill and verify that all artifacts like types, OIRs, templates, etc. were deployed.