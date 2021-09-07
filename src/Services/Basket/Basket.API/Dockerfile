FROM mcr.microsoft.com/dotnet/aspnet:5.0 AS base
WORKDIR /app
EXPOSE 80

FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build
WORKDIR /src
COPY . .
RUN dotnet restore Basket.API.csproj
RUN dotnet build Basket.API.csproj -c Release -o /build

FROM build AS publish
RUN dotnet publish Basket.API.csproj -c Release -o /publish

FROM base AS final
WORKDIR /app    
COPY --from=publish /publish .
ENTRYPOINT ["dotnet", "Basket.API.dll"]