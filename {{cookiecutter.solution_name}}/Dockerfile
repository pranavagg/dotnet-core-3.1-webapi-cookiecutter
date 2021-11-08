FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build
WORKDIR /source

COPY *.sln .
COPY {{cookiecutter.api_name}}/*.csproj ./{{cookiecutter.api_name}}/
COPY {{cookiecutter.api_name}}.Tests/*.csproj ./{{cookiecutter.api_name}}.Tests/
# RUN dotnet restore

# copy everything else and build app
COPY {{cookiecutter.api_name}}/. ./{{cookiecutter.api_name}}/
WORKDIR /source/{{cookiecutter.api_name}}
RUN dotnet publish -c release -o /app

# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:3.1
WORKDIR /app
COPY --from=build /app ./
ENTRYPOINT ["dotnet", "{{cookiecutter.api_name}}.dll"]