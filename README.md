# Demo for Docker, JAR Running Terminal,
Demo Application : Spring Boot Sample COde , Docker, GKE, JAR File, from , GCP temiranl, no need of anything at laptop.
Direct development on GCP.


# Spring Boot Lazy Initialization example

## Versions Used
- Spring Boot - 2.2.0-M1
- H2 Database - 1.4.197

## Configuration
`spring.main.lazy-initialization` is set to `false` by default. This can be set to `true` to enable Lazy Initialization in the Spring Boot Project.

## Alternatives
- `http://localhost:8080/lazy` - Uses `LazyController` and `LazyService` which can be marked manually as `@Lazy` for specific Beans
# commands used on GCP CLI

./mvnw clean install  // for maven buld creating jar.
java -jar target/spring-boot-lazy-init-example 0.0.1-SNAPSHOT   //  running the and test it on local host

put the Jar file in DOcker image and push in container registry of GCP , this command worked successfully
 ./mvnw com.google.cloud.tools:jib-maven-plugin:build -Dimage=gcr.io/$GOOGLE_CLOUD_PROJECT/springboot-docker:v1
 
 getting credetionals from GKE and connecting to GKE
gcloud container clusters get-credentials cluster-1 --zone us-central1-c

verfy by using this comman
kubectl get nodes


but creating deployment first verify if Docker image created at GCP is working successully download and run local, then test 
by clicking web preview
docker run -ti --rm -p 8080:8080 gcr.io/$GOOGLE_CLOUD_PROJECT/springboot-docker:v1

create deployment
kubectl run springboot-docker --image  gcr.io/$GOOGLE_CLOUD_PROJECT/springboot-docker:v1 --port=8080

verify if pod is created
 kubectl get pods
 kubectl get deployments
 kubectl get services

for accessing now need to expose it to load balancer (good practive to put configuration with yaml, but here through the command line only)
kubectl expose deployment  spring-boot-example  --type=LoadBalancer

reference of tbis video
https://www.youtube.com/watch?v=jSYxW_c3M_E
