FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY . .
RUN dotnet restore Catalog.API.csproj
RUN dotnet build Catalog.API.csproj -c Release -o /build

FROM build AS publish
RUN dotnet publish Catalog.API.csproj -c Release -o /publish

FROM base AS FINAL
WORKDIR /app
COPY --from=publish /publish .
ENTRYPOINT [ "dotnet", "Catalog.API.dll" ]