FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 8080

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY CoreRest/CoreRest.csproj CoreRest/
RUN dotnet restore CoreRest/CoreRest.csproj
COPY . .
WORKDIR /src/CoreRest
RUN dotnet build CoreRest.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish CoreRest.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "CoreRest.dll"]
