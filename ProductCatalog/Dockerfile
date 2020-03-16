FROM mcr.microsoft.com/dotnet/core/sdk:3.1 AS build-env
WORKDIR /app

# Copy csproj and restore as distinct layers
COPY ./*.sln .
COPY ./ProductCatalog/*.csproj ./ProductCatalog/
RUN dotnet restore

# Copy everything else and build
COPY ./ProductCatalog/. ./ProductCatalog
WORKDIR /app/ProductCatalog
RUN dotnet publish -c Release -o app

# Build runtime image
FROM mcr.microsoft.com/dotnet/core/aspnet:3.1 AS runtime
WORKDIR /app
COPY --from=build-env /app/ProductCatalog/app .
ENTRYPOINT ["dotnet", "ProductCatalog.dll"]