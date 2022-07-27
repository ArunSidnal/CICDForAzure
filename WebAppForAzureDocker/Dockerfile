FROM mcr.microsoft.com/dotnet/sdk:5.0 AS base
WORKDIR /app


FROM mcr.microsoft.com/dotnet/sdk:5.0 AS build

WORKDIR /src
COPY ["./WebAppForAzureDocker/WebAppForAzureDocker.csproj", "./"]
RUN dotnet restore "./WebAppForAzureDocker.csproj"
COPY . .
RUN dotnet build "./WebAppForAzureDocker.csproj" -c Release -o /app/build

FROM build as publish
RUN dotnet publish "./WebAppForAzureDocker.csproj" -c Release -o /app/publish

FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
CMD dotnet "WebAppForAzureDocker"
