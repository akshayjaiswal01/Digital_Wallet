# Stage 1: Build
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src

# Copy the csproj file only from current directory (because context is VaultPay.API)
COPY VaultPay.API.csproj ./

# Restore dependencies
RUN dotnet restore ./VaultPay.API.csproj

# Copy everything else
COPY . .

# Publish app
RUN dotnet publish -c Release -o /app/publish

# Stage 2: Runtime
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime
WORKDIR /app
COPY --from=build /app/publish .
ENTRYPOINT ["dotnet", "VaultPay.API.dll"]
