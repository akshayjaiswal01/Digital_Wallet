# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

# Copy csproj and restore as distinct layers
COPY VaultPay.API/VaultPay.API.csproj VaultPay.API/
RUN dotnet restore VaultPay.API/VaultPay.API.csproj

# Copy everything else and build
COPY . .
WORKDIR /src/VaultPay.API
RUN dotnet publish -c Release -o /app/publish

# Stage 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "VaultPay.API.dll"]
