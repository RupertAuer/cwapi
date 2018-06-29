FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY cwapi/cwapi.csproj cwapi/
RUN dotnet restore cwapi/cwapi.csproj
COPY . .
WORKDIR /src/cwapi
RUN dotnet build cwapi.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish cwapi.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "cwapi.dll"]
