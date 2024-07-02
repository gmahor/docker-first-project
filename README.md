# docker-first-project
This is a basic of docker with buildpack commond


-t = tag
-f = file
docker ps => running images -a 
docker images => all images 
docker rm => for removing running ports
docker rmi => removing images
docker build -t bootimage . = build image
docker run --name bootProject -it -d bootimage => run docker image

Build Docker image
username/service_name
gourav60/accounts
docker build  .  -t gourav60/accounts:v1

docker inspect image imagename = this will provide you the details of image

run docker image
docker run -d -p 8080:8080 56b8 => 56b8 this is your docker image first 4 digits

we can create image with our springboot also by using this command:- 
1. adding this in pom
<build>
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
                <configuration>
                    <image>
                        <name>gourav60/${project.artifactId}:v1</name>
                    </image>
                    <excludes>
                        <exclude>
                            <groupId>org.projectlombok</groupId>
                            <artifactId>lombok</artifactId>
                        </exclude>
                    </excludes>
                </configuration>
            </plugin>
        </plugins>
    </build>

2. run this command on cmd
mvn spring-boot:build-image

3.  docker run -d -p 8080:8080 b0d8

Push image to docker hub
docker image push docker.io/gourav60/accounts:v1

Pull Image from docker hub
docker pull gourav60/cards:v1

docker compose 
1. You need to install docker compose for using docker compose in you project.

this is use for run multiple service same time without running service one by one.

1. create docker-compose.yml file
 then use this values
     services:
  accounts:
    image: "gourav60/accounts:v1"
    container_name: accounts-ms
    ports:
      - "8080:8080"
    deploy:
      resources:
        limits:
          memory: 700m
    networks:
      - eazybank
  loans:
    image: "gourav60/loans:v1"
    container_name: loans-ms
    ports:
      - "8090:8090"
    deploy:
      resources:
        limits:
          memory: 700m
    networks:
      - eazybank
  cards:
    image: "gourav60/cards:v1"
    container_name: cards-ms
    ports:
      - "9000:9000"
    deploy:
      resources:
        limits:
          memory: 700m
    networks:
      - eazybank
networks:
  eazybank:
    driver: "bridge"

2. run docker compose file
   go to the dict of docker-compose.yml and then run 
   
   docker compose up

3. to stop docker compose 
   docker compose down