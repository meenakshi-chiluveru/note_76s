developer develops the code and push to git hub and we take code and and build and deploy to server
code is build by maven and reviewd by sonar software if the code reeviw will succes then that code artifact will upload to nexus repo
when artifact uploaded into nexus docker comes into picture and create docker image for our application and stored in docker registry after that we deployed that image to kubernetes cluster

when developer put the code in github we need to take code we have to build and deploy in old days we do manually now a days we are doing using automation tool jenkins

in jenkins we are going to create pipeline for to build and deploy the code

jenkins will integrated with all tools jenkins take code from github and jenkins will talk to maven to build the code

jenkins will integrate with sonar software to perform the code review
jenkins will integrated with nexus to upload artifact one upload done jenkins will integrate docker to craete application image once the image created jenkins will push docker image to docker regisrty once completed upolading image to docker registry jenkins will trigger kubernetes to deploy

when docker image is available in docker registry that will be dowload in to kubernetes and the application will be deployed in to kubernetes cluster