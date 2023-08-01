# Docker file

A `Dockerfile` is a plain text file containing all the commands needed to build an image. Dockerfiles are written in a minimal scripting language designed for building and configuring images. They document the operations required to build an image, starting with a base image.

```dockerfile title="Sample Dockerfile"
FROM mcr.microsoft.com/dotnet/core/sdk:2.2
WORKDIR /app
COPY myapp_code .
RUN dotnet build -c Release -o /rel
EXPOSE 80
WORKDIR /rel
ENTRYPOINT ["dotnet", "myapp.dll"]
```

!!! info ""
    By convention, applications meant to be packaged as Docker images typically have a Dockerfile located in the root of their source code, and it's almost always named `Dockerfile`.


The `docker build` command creates a new image by running a Dockerfile. The syntax or this command has several parameters:

- The *f* flag indicates the name of the Dockerfile to use.
- The *t* flag specifies the name of the image to be created, in this example, *myapp:v1*.
- The final parameter, *.*, provides the *build context* for the source files for the **COPY** command: the set of files on the host computer needed during the build process.


```shell
docker build -t myapp:v1 .
```

Behind the scenes, the `docker build` command creates a container, runs commands in it, then commits the changes to a new image

## Steps
- Create a `Dockerfile` for a new container image based on a starter image from Docker Hub
- Add files to an image using Dockerfile commands
- Configure an image's startup command with Dockerfile commands
- Build and run a web application packaged in a Docker image
- Deploy a Docker image using the Azure Container Instance service

