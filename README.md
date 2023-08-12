<h1 align="center"> Containerizing JAVA App (SpringBoot) using Docker </h1>
<h2 align="center"> Containerizing/Dockerize SpringBoot application to deploy it in Kubernetes or in other environment in container form. </h2>

![imagegit](https://github.com/shankar439/Images/assets/70714976/71588a27-dc57-47ce-bff3-6369495088aa)

## Why we need to Containerize application and what are the advantages of it ?. 
  - `Any one can adopt to Containerization as the development and deployment need to be faster these days, this will be the right choose.`
  - ### Pros
    - `Portability` - Containers encapsulate applications and their dependencies making them run consistently in any environment that supports containerization.
    - `Isolation` - Containers provide a level of isolation between applications and their host environment makes them considering them as a separate vm.
    - `Scalability` - Containers allow applications to scale easily. By leveraging container orchestration platforms like Kubernetes, you can dynamically manage and scale containers based on demand.
    - `Faster Deployment and Rollback` - Since the containerized application includes all its dependencies, deployment becomes a matter of spinning up new containers. If an issue arises, rolling back to a previous version is straightforward by redeploying the earlier container image.
  - ### Cons
    - Debugging and Troubleshooting, Resource optimization and Learning curve make containers little challenging. 

### prerequisite
  - Any Operating System with Docker pre installed.
  - A sample SpringBoot application.

<br>
<br>



<h1 align="center">Lets Begin </h1>

- `This will be a quick tutorial.`

- Open the SpringBoot application in your favorite IDE i will open it in intelliJ.

<h2 align="center">Create a Docker file </h2>

- In the Project structure create a file with name `Dockerfile`, make sure the name of the file should be exactly like this.
- Inside the `Dockerfile` insert the below statements.

```yaml
FROM openjdk:11.0.6-jre-slim
ADD target/user-management.jar user-management.jar
EXPOSE 8080
CMD java -jar user-management.jar
```

## Explanation

- `Line 1` - As every Docker image need to be created from a base docker image, here i am using openjdk image with slim version as a base image to run my SpringBoot application.
- `Note - We can use` [Google Distroless images](https://github.com/GoogleContainerTools/distroless) `which are lightweight and secure as it eliminate the OS and only contain runtime EX: Java, Python, node `.
- `Line 2` - Copy the user-management.jar from the target folder into the image with the same name.
- `Line 3` - Here we exposing the image at port 8080.
- `Line 4` - This command that will be executed when the container starts, this command execute the java application which is in jar form.

<br>
<br>


<h2 align="center">Let's Create a Docker Image </h2>

- First lets build the artifact jar file using the maven run below cmd to create it
```yaml
mvn clean package
```


- Run the docker desktop before executing Docker commands.
- In the terminal enter the below cmd to build the Docker image.


```yaml
docker build -t spring:1 .
```

- Check if the image is created, using the below cmd
```yaml
docker images
```

- If the image exist run the docker image to in detached mode at port 8080, as we are exposing the imaged at port 8080.
```yaml
docker run -d -p 8080:8080 spring:1
```

- Once we run the docker image it is considered as container.
- To see the running containers use the below cmd .
```yaml
docker ps
```

- If our SpringBoot application is running lets check it in chrome using the localhost:8080.

<br>
<br>



<h2 align="center">Conclusion</h2>

- We have seen what is containerization and its advantages.
- Build an artifact of our SpringBoot application using Maven
- We created a Dockerfile and created a Docker image
- And we have run the Docker container and accessed it in chrome.



<br>

# END