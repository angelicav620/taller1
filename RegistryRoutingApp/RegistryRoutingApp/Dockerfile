FROM microsoft/aspnetcore:latest AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:latest AS build
WORKDIR /src
COPY RegistryRoutingApp.sln ./
COPY RegistryRoutingApp/RegistryRoutingApp.csproj RegistryRoutingApp/
RUN dotnet restore -nowarn:msb3202,nu1503
COPY . .
WORKDIR /src/RegistryRoutingApp
RUN dotnet build -c Release -o /app

FROM build AS publish
RUN dotnet publish -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "RegistryRoutingApp.dll"]
