# Overview
This is a Spring Microservices to create a build and deployment pipeline. It was built and then deployed all of the services to Amazon's Elastic Container Service (ECS).

Architecture of this microservices:

1.  A Spring Cloud Config server. It is deployed as Docker container and manage a services configuration information using a file system or GitHub-based repository.
2.  A Eureka server running as a Spring-Cloud based service allow multiple service instances to register with it.  Clients that need to call a service will use Eureka to lookup the physical location of the target service.
3.  A Zuul API Gateway.  All of this microservices can be routed through the gateway and have pre, response and
post policies enforced on the calls.
4.  A organization service that will manage organization data used within EagleEye.
5.  A new version of the organization service.  This service is used to demonstrate how to use the Zuul API gateway to route to different versions of a service.
6.  A special routes services that the API gateway will call to determine whether or not it should route a user's service call to a different service then the one they were originally calling.  This service is used in conjunction with the orgservice-new service to determine whether a call to the organization service gets routed to an old version of the organization service vs. a new version of the service.
7.  A licensing service that will manage licensing data used within EagleEye.
8.  A Kafka message bus to transport messages between services.


# Software needed
1.	[Apache Maven] (http://maven.apache.org). Version 3.6.0 and Java 8
2.	[Docker] (http://docker.com). Docker V1.9
# Building the Docker Images 
To build the code as a docker image, open a command-line window change to the directory 
Run the following maven command.  This command will execute the [Spotify docker plugin](https://github.com/spotify/docker-maven-plugin) defined in the pom.xml file.  

   **mvn clean package docker:build**

If everything builds successfully, a message indicating that the build was successful.

# Running the services 
Using docker-compose to start the actual image.  To start the docker image,
change to the directory containing  
.  Issue the following docker-compose command:

   **docker-compose -f docker/common/docker-compose.yml up**

If everything starts correctly, a bunch of Spring Boot information fly by on standard out.  At this point all of the services needed for the microservices code will be running.
![-](/image/success.png)
