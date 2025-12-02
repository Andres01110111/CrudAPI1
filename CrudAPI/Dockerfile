# Imagen base para compilar
FROM mcr.microsoft.com/dotnet/sdk:8.0 AS build
WORKDIR /src

# Copiar solución y proyecto
COPY *.sln .
COPY CrudAPI1/CrudAPI/*.csproj CrudAPI1/CrudAPI/

RUN dotnet restore

# Copiar el resto del código
COPY . .
WORKDIR /src/CrudAPI1/CrudAPI
RUN dotnet publish -c Release -o /app/publish

# Imagen final
FROM mcr.microsoft.com/dotnet/aspnet:8.0 AS runtime
WORKDIR /app

COPY --from=build /app/publish .

EXPOSE 8080
ENV ASPNETCORE_URLS=http://0.0.0.0:8080

ENTRYPOINT ["dotnet", "CrudAPI.dll"]