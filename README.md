# JENKINS
This is a project of  Pipeline Automation using jenkins .
Steps that i followed to make this project
1. I first create a local git repository then create two branches in that repository i.e. dev and master .
2. Then i create a webpage in dev branch.
3. Then i go to and create 3 jobs in jenkins that are :-
Test - this job will create an environment for QAT then deploy webpage on webserver so that QAT can test the webpage.
PRODUCTION - this job will create a new  environment and then deploys the  webpage on webserver for clien.
MERGE - it will merge master and dev branch.
4. Now when developer commit webpage from dev branch then TEST job will run and do the same . For this job i use build trigger remotely option and then paste url in post commit hook.

5. When QAT team pass the webpage then they will run a url that will run MERGE job automatically.

6. Now MERGE job will run and merge master branch with dev branch and due to this webpage gets copied to master branch. 
Here i do merging by using the following steps.
- go to source code management option
- paste your repository url
- add your credentials in option given below the url
- click on additional behaviours
- click on add and then select 'Merge Before Build' option
- now go to post-build action and then select git publisher
- now tick only first two options
 
7. When MERGE job finishes then PRODUCTION job will run automatically.
   This job runs automatically because in this job selected poll SCM and schedule it to check github automatically after every 1 minute.
   Since this job only runs when there is some change in master branch and due to merging the master branch gets updated and since it is checking after every 1 minute.
   So it will run and then download the webpage and then deploys it on the webserver so that client can see our site.
8. This is a simple example of Pipeline Automation using jenkins.

In this i use DOCKER to create environment by the following command
docker -itd -p 8082:80 -v /folder:/usr/local/apache2/htdocs --name webos httpd

Note - use different ports for test and production webservers.
