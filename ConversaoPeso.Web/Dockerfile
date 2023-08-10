# Learn about building .NET container images:
# https://github.com/dotnet/dotnet-docker/blob/main/samples/README.md
FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /source

# copy csproj and restore as distinct layers
COPY ConversaoPeso.Web.csproj .
RUN dotnet restore ConversaoPeso.Web.csproj

# copy everything else and build app
COPY . .
RUN dotnet publish ConversaoPeso.Web.csproj -c Release -o /app /p:UseAppHost=false


# final stage/image
FROM mcr.microsoft.com/dotnet/aspnet:5.0
WORKDIR /app
COPY --from=build /app .
ENTRYPOINT ["dotnet", "ConversaoPeso.Web.dll"]