# jenkins:
----------
<details>
<summary> What is jenkins?</summary><br><b>
  it is a coontinuous integartion (CI) and continuous deployment (CD) tool.
 </b><details>

<details>
 <summary>what is CI and CD?</summary><br><b>
 
 CI means integrate the developers code. CD means deliver or deploy the code into the different envirnoment (QA,pre-production,production).

- It is a java based application.
- it will help to automate the process of code integraton,code build,code delivery.
- it is a opensource tool like hudson/bamboo/teamcity.
- jenkins has original name as hudson.

- Jenkins is the core part of the devops.
- jenkins will connect to the scm,qa,tomcat,production,etc. to interact with these system. 
- it is interacted with those systems with the plugins.
- it is plugin based tool.
- nearly 1000+ plugins jenkins will support.
 </b><details>

### important section of jenkins?
 
 - Plugin management.
 - global tool management.
 - job management.
 - jenkins dashboard.
 - user management.
 - security management.
 - slave connection.

### Role of Devops Engineer (or) Build and Release Engineer?
  
 - Installation and configuration.
 - plugin management.
 - user management.
 - security management.
 - global tool management.
 - creating jobs.
 - monitoring jobs.
 - jobs pipeline
 - integrating different tools.
 - taking jenkins backup.


NOTE: in jenkins server git must and should install.

Plugin Management:
-----------------
### what is plugin ?
  plugin is a additional software.it will help to interact with the other systems.

 under plugin mangement we can install,update,remove the plugins.

Manage jenkins--manage plugins


### Global tool management:
---------------------------
these are tools it will help develop the application like maven.

difference between tool and plugin 
 we can maintin multiple versions of tool.
but we can maintain only single version of plugin.

Manage jenkins----global tool configuration

### Job management:
-------------------
#### what is job?
  job means task. to build ,integration ,delivery these kind of tasks we can handle in jenkins job management.

 job is a core part of the jenkins.job will pull the code from scm server.build the application if successfully build delivery the code.

### There are different types of jobs:
--------------------------------------
1)free style
   we can integrate any type of files.
2)maven job
   we can integrate only java files
3)pipeline jobs
  sequence of jobs, one job is connected to anothr job.
4)multipipe line jobs

Q)how to schedule a job in jenkins?
 - get the code from scm server (github)
 - setting trigger (build process trigger)
 - setup build environment 
 - build acion
 - post build action


build maven Job in jenkins:
---------------------------

code compile:
code test:
code integration:
code package:

for job pipeline install the "build pipeline plugin"

here trigger the job as build after other job.

deploy:
-------
for deploy the code into tomcat install "deploy to container plugin"

at post build action setup the "deploy war/ear to container"

backup:
-------
for jenkins server backup install "backup plugin"


### email notification in jenkins

install the plugin "email extension plugin", "email extension template plugin"

configure mailserver,port,smtp authentication in "system configure"

## Jfrog 
- First we have to install jenkins
- we have to install Jfrog Plugin => Navigate to Manage Jenkins => plugins => Available plugins => 

## SonarQube Installation
	
- First we have to install jenkins
- 


































































