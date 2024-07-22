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

![launching-ec2](https://github.com/user-attachments/assets/19504b54-ba71-4785-8a74-3ce88ac81ad0)

Step1 : create a ec2 instance. I am using ubuntu so i will be using apt through the various tools installation. If you have a different distro use the packages accordingly.
        Tip : while creating the ec2 instance in the console > go to advance > and in the user date you can add bash scripts where we can simply add scripts to install various services.
        Or you can simply use the bash script that is in this repo to install docker and jenkins. 
        ![check-instances](https://github.com/user-attachments/assets/1939ebc7-4b94-493f-9f17-3f5261a9dd4d)  <br />
        

        
After the instance is up and running ssh into the instance:
![connectin-ec2](https://github.com/user-attachments/assets/6440fa42-7145-407e-a0b1-3681e8e5ec14) <br />
<br />

after the connection : 
![ssh-from-the-terminal](https://github.com/user-attachments/assets/ca180cab-0ee5-4470-8c9b-7fc9ad77027c)




Step2 : If you have used the script file in the repo with ".sh" you will have already installed jenkins which is the second step.
        after you have installed jenkins and configure all the settings the only plugin that we are gonna be using is "github integration". To install this 
        go to jenkins homepage > manage jenkins > install github integration <br />
        <br />
        To check wheather we have docker and jenkins installed we can use <br />
        ```bash
        docker -v 
        ```
        ```bash
        systemctl status jenkins
        ```
        ![checking-docker-jenkins](https://github.com/user-attachments/assets/fdb662c5-3c64-4e0b-9175-a3fe625bc320)

check the script file in the repo if it is not yet installed. <br/>

and we need to install github integration plugin:
![github-integration-plugin](https://github.com/user-attachments/assets/a19d9a31-dfd9-40a7-b9b3-a662c01b7c12) <br />

jenkins home page:
![jenkins-home](https://github.com/user-attachments/assets/36ec289e-3f25-43df-b40a-ab1bfb5ddda7)


Step3 : Now we need to create a bridge between the jenkins and the github repo. To do this
        we go to our ec2 instance > create keys with "ssh-keygen" > and we can see two keys generated (a public one and a private)
        open the public key and copy it.

After the key is generated we can add it into our github and jenkins server. The public key is for github and jenkins will use the private key.
![github-jenkin](https://github.com/user-attachments/assets/f40736da-e632-4d6f-ba8e-5a4c7a101974)


![github-jenkin-2](https://github.com/user-attachments/assets/ae18f0d5-349d-475b-93e0-040f8dab5491)

        

Step4 : go to github > settings > ssh amd gpg key > add new key > give name to the key and paste the copied public key.
        go to jenkins > in the github project url and github repo url > paste your github repo url and right below that we can add credentials 
        Then in the "kind section" > change it to SSH Username with private key > give a id > add a username > add the private key generated earlier > add it > save.
        go back > click build now and we can see that the repo will have been cloned in our ec2 instance.

after the key setup are complete, github and jenkins will be connected and if we click on build the job from the left menu
![build-jobs](https://github.com/user-attachments/assets/8b68e984-9370-4cd6-8fa8-ce75d57fccbb)
a clone of the github repo will be avaliable in the ec2 instance
![bridge-complete](https://github.com/user-attachments/assets/1fa8666c-2b9f-4abc-ba52-94765a60c4ce)

Step5 : install nodejs and npm if you haven't already installed it.
        type server.js in the terminal and see weather the app is working or not.
        Note : if you are not able to view the web app in the browser, the problem might be with the security group. we have to allow the port 3000 that is running in the ec2 instance security.



Step6 : If you have already installed docker we can proceed to creating a "Dockerfile"
          you can find the docker file in the repo.
          ![write-dockerfile](https://github.com/user-attachments/assets/bf30fce5-d1f8-43a3-b963-7d7e837fdaee)


Step7 : build the image and run it in a container....see if it is working or not if yes then kill the container.
        now instead of writing the code in the terminal to build and run the cotainer images, we will write the code as a Build Step in the execute shell in Jenkins.
![image-build](https://github.com/user-attachments/assets/c00d20a4-5aa6-4981-bc82-e40c07ccf72a)
<br />
running the image in a container
![image-run](https://github.com/user-attachments/assets/0cdcf435-c1a8-472d-95a3-c8adefec796a)<br />

<br />
Also we can check the images using:

```bash
docker images
```

![image-build-check](https://github.com/user-attachments/assets/208ffdd0-aceb-4f0c-931d-589cf44402b5)
<br />
and we can also check the if the container is running or not 


```bash
docker ps
```

![container-check](https://github.com/user-attachments/assets/925c9927-1acd-4d37-bb72-2bc9f8e01247)



Step 8 : Build Now.
          We will be able to access it in the browser through port 3000.


Finally, we use github webhooks to create a trigger for if there is any changes in the repo. So, any changes in the github repo will result in running all these process again.
   ![app-deployed](https://github.com/user-attachments/assets/15a63a78-3f2e-4776-b7d2-84f38bec72d1)
     
  
