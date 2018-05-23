
    docker run --rm -it microsoft/dotnet:2-runtime 
    docker run --rm -it -v ${PWD}:C:\api -p 8080:80 microsoft/aspnetcore:2  
    docker run --rm -it -v ${PWD}:/api -p 8080:80 microsoft/aspnetcore:2


Automate Building with a Dockerfile

    run --rm -it -v ${PWD}:/api -p 8080:80 microsoft/aspnetcore-build:2
    cd /api
    rm -rf bin/ obj/
    dotnet restore
    dotnet publish



Composing an ASP.NET Core App

    docker build -t aspnetcore/generator:multi . 
    docker run --rm -it -p 8080:80 aspnetcore/generator:multi


start a container and drop into the prompt
    docker run --rm -it microsoft/aspnetcore-build:2.0.8-2.1.200
    exit


docker run --rm -it -v ${PWD}:/api -p 8080:80 microsoft/aspnetcore-build:2.0.8-2.1.200

docker run --rm -it -v ${PWD}:C:\api -p 8080:80 microsoft/aspnetcore:2.0.8 


# this worked for me

docker run --rm -it -v "%cd%":C:\api microsoft/dotnet:2-runtime 

map a port to 8080 of the host machine
switch to windows containers

    docker run --rm -it -v "%cd%":C:\api -p 8080:80 microsoft/aspnetcore:2 
then browse to localhost:8080

switch to linux containers
C: drive is not shared by default , so go to tray > settings > shared drives > C

    docker run --rm -it -v "%cd%":/api -p 8080:80 microsoft/aspnetcore:2 
then browse to localhost:8080

## building docker file 
create the docker file 

    docker build -t eiu165/generator .    
 

    C:\src\aspnetcore-generator-api\api>docker image ls
    REPOSITORY             TAG                 IMAGE ID            CREATED             SIZE
    aspnetcore/generator   latest              1b8c6e2675cb        50 seconds ago      349MB 

now you do not need to copy the file 

    docker run --rm -it -p 8080:80 eiu165/generator 



## automation 

start to trace the events
    docker events --format "{{json .}}" | jq
    docker run --rm -it -p 8080:80 eiu165/generator 
    docker stop {name}


    docker run --rm -it -v "%cd%":/api -p 8080:80 microsoft/aspnetcore:2 
    cd /api
    rm -rf bin/ obj/
    dotnet restore
    dotnet publish


new docker file: 
    FROM microsoft/aspnetcore:2 
    WORKDIR /api 
    COPY . .   
    RUN dotnet restore 
    RUN dotnet publish
    ENTRYPOINT ["dotnet", "/publish/api.dll"]

now build the image

    docker build -t eiu165/generator:build . 

now run the container 

    docker run --rm -it -p 8080:80 eiu165/generator:build

view the images 

    docker image ls eiu165/generator
