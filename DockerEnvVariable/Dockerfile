FROM mcr.microsoft.com/dotnet/aspnet:5.0
COPY bin/publish/ ./app
WORKDIR /app
ENTRYPOINT ["dotnet", "DockerEnvVariable.dll"]