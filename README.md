# Docker environemnt variable

This is a demo app to show how we can set `ASPNETCORE_ENVIRONMENT` in the
docker container at the time of docker container start.

This sample app is having two different connection strings in `appsettings.json`
and `appsettings.Development.json`. 

```
"ConnectionStrings": {
  "ConStr": "prd con str"
}
```
```
"ConnectionStrings": {
  "ConStr": "dev con str"
}
```

When you request the `Home > Index` method then the application logs the value of 
the connection string.

```c#
string conStr = _configuration.GetConnectionString("ConStr");
_logger.LogInformation(conStr);
```

When we run this app from Visual Studio then we can provide the `ASPNETCORE_ENVIRONMENT` 
value in `launchSettings.json` and based on that you can see the output in the log.

```
"environmentVariables": {
  "ASPNETCORE_ENVIRONMENT": "Development"
}
```

But when we publish the app and store it in a docker image and run a container
from that image then we can't use `launchSettings.json`. In that case we can 
provide the value of `ASPNETCORE_ENVIRONMENT` at the time of docker container run.

To create a docker image

```
docker build -t dockerenvvariable:1.0.0 .
```

To run a container from the image with `ASPNETCORE_ENVIRONMENT` value

```
docker run --name dockerenvvariable-c1 -p 80:80 -e ASPNETCORE_ENVIRONMENT=Development dockerenvvariable:1.0.0
```

Request `http:\\localhost:80` from a browser and you can see the value `dev con str` in the 
log file.

## Tech stack

Visual Studio 2019, ASP.NET 5 and docker desktop.
