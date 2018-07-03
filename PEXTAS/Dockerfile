FROM microsoft/aspnetcore:2.0 AS base
WORKDIR /app
EXPOSE 80

FROM microsoft/aspnetcore-build:2.0 AS build
WORKDIR /src
COPY PEXTAS/PEXTAS.csproj PEXTAS/
RUN dotnet restore PEXTAS/PEXTAS.csproj
COPY . .
WORKDIR /src/PEXTAS
RUN dotnet build PEXTAS.csproj -c Release -o /app

FROM build AS publish
RUN dotnet publish PEXTAS.csproj -c Release -o /app

FROM base AS final
WORKDIR /app
COPY --from=publish /app .
ENTRYPOINT ["dotnet", "PEXTAS.dll"]
