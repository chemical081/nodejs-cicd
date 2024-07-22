# nodejs-cicd
A web app made with html, css, js and nodejs automated for cicd
![Screenshot_2024-07-22_13_52_00](https://github.com/user-attachments/assets/4acc590b-f952-416f-a56d-588481299cea)




### We can use any nodejs app for this project. But dependening on the project complexity additional dependencis or tools might be required. So, to follow along you can use my weather-app that is in my github repo. https://github.com/chemical081/weather-app.git 
![Weather App Screenshot](https://raw.githubusercontent.com/chemical081/weather-app/master/Screenshot-3.png)


## Prequisite
- install nodejs
- npm package
- install docker 
- install jenkins 


## Objective
- When we are push a code or make any changes in our github repo, the changes must be automatically updated.
- As we can see in the image we have used various services like AWS, jenkins, docker, scripting and more. So, the idea is to make all the services run if there is a change in the github repo.


#Step By step
Let's go through this step by step

Step1 : create a ec2 instance. I am using ubuntu so i will be using apt through the various tools installation. If you have a different distro use the packages accordingly.
        Tip : while creating the ec2 instance in the console > go to advance > and in the user date you can add bash scripts where we can simply add scripts to install various services.
        Or you can simply use the bash script that is in this repo to install docker and jenkins.

Step2 : If you have used the script file in the repo with ".sh" you will have already installed jenkins which is the second step.
        after you have installed jenkins and configure all the settings the only plugin that we are gonna be using is "github integration". To install this 
        go to jenkins homepage > manage jenkins > install github integration 

Step3 : Now we need to create a bridge between the jenkins and the github repo. To do this
        we go to our ec2 instance > create keys with "ssh-keygen" > and we can see two keys generated (a public one and a private)
        open the public key and copy it.

Step4 : go to github > settings > ssh amd gpg key > add new key > give name to the key and paste the copied public key.
        go to jenkins > create a job > freestyle project > name your job > in the github project url and github repo url > paste your github repo url and right below that we can add credentials 
        Then in the "kind section" > change it to SSH Username with private key > give a id > add a username > add the private key generated earlier > add it > save.
        go back > click build now and we can see that the repo will have been cloned in our ec2 instance.

Step5 : install nodejs and npm if you haven't already installed it.
        type server.js in the terminal and see weather the app is working or not.
        Note : if you are not able to view the web app in the browser, the problem might be with the security group. we have to allow the port 3000 that is running in the ec2 instance security.



Step6 : If you have already installed docker we can proceed to creating a "Dockerfile"
          you can find the docker file in the repo.

Step7 : build the image and run it in a container....see if it is working or not if yes then kill the container.
        now instead of writing the code in the terminal to build and run the cotainer images, we will write the code as a Build Step in the execute shell in Jenkins.

Step 8 : Build Now.
          We will be able to access it in the browser through port 3000.
        
        
        
  
