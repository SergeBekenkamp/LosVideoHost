FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY LoSVideoHostBackend/LoSVideoHostBackend.csproj LoSVideoHostBackend/
RUN dotnet restore LoSVideoHostBackend/LoSVideoHostBackend.csproj
COPY . .
WORKDIR /src/LoSVideoHostBackend
RUN dotnet build LoSVideoHostBackend.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish LoSVideoHostBackend.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "LoSVideoHostBackend.dll"]
