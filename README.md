# teamcity_server
https://gist.github.com/akanchhaS/baffec93085249167c538f776d9cea58

# Setting up team city server and agent on your local machine with Snyk security plugin

TeamCity is one of the popular Build Automation tools and requires running of the Server and agent. 

There are different ways of installing it which you can read more about [here](https://www.jetbrains.com/help/teamcity/install-and-start-teamcity-server.html). This document specifically lists out the steps of running it locally.

Note: This doc covers basic steps to get the Teamcity and snyk security plugin set up and running. 

## Prerequisites

Docker to be installed and present on your machine. 

## Steps: 

1. Create mapping directories for the teamcity/data, teamcity/logs and teamcity/conf
`cd` to the directory where you want to set your teamcity configs and then run the following commands

````
mkdir teamcity/data
mkdir teamcity/logs
mkdir teamcity/conf
````
2. Copy the above `docker-compose.yml` in the same directory 
3. Run `docker-compose build` 
4. Run `docker-compose up`

The above command will spin up the `teamcity agent` and `teamcity server` and now you can access your Teamcity set up by accessing the `http://localhost:8111` on your browser.

> Note: To add Snyk security plugin in Teamcity, navigate to Administration > Server Administration - Plugins. Next Browser plugins and search Snyk security - then hit Get :smile: 


<img width="1653" alt="image" src="https://user-images.githubusercontent.com/32653970/176549033-d2772722-1670-476d-bc32-816f829ec55b.png">

<img width="1034" alt="image" src="https://user-images.githubusercontent.com/32653970/176549215-914eb944-e6e2-4010-b69d-6881a7246f96.png">

<img width="1396" alt="image" src="https://user-images.githubusercontent.com/32653970/176549326-6fb182b1-214d-45de-bd98-2d9f42604970.png">


## Setting up Snyk security as one of your Build Steps

> Note: the following steps would come in once you have logged in to your teamcity server, set up a project (Admin - Create project) and are setting up Snyk as one of the build steps.

1. Go to your Buids - Edit configuration - Build Steps
2. Select `Parameters` from the left pane and Select `Add New Parameter` 
3. In the dialog box provide the vairable name as `SNYK_TOKEN` and as value [provide the API token](https://docs.snyk.io/snyk-api-info/authentication-for-api) and hit `Save`
4. Now that your parameter is set up, come to the Build Steps and click the `Add Build Step` Button 
5. Select Snyk Security - set up the fields as per your requirements; For the `Snyk API Token` field click on the small icon next to the textbox for the drop down to appear and select the `SNYK_TOKEN` 
6. Hit `Save`
7. You are now good to run your Build!

> Note: You want to always add the Snyk security step after the dependencies have been installed for Snyk to test the open source dependencies. And hence, under execute step the value would be - if all previous steps finished successfully.


<img width="1123" alt="image" src="https://user-images.githubusercontent.com/32653970/176551728-aeab6650-f39f-4c2e-83b9-f90db5860a55.png">

<img width="1196" alt="image" src="https://user-images.githubusercontent.com/32653970/176552690-68b997ce-0300-4980-b586-78adfba320a0.png">

<img width="1573" alt="image" src="https://user-images.githubusercontent.com/32653970/176551465-f9c7636a-c1eb-4371-8c79-926275976254.png">

<img width="1310" alt="image" src="https://user-images.githubusercontent.com/32653970/176552477-642d7d81-66f4-4f68-a9ca-2aca976159a7.png">
