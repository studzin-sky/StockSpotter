# Use the official Microsoft .NET Core runtime as a parent image
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app
EXPOSE 80
EXPOSE 443

# Use the SDK image to build the project files
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /src
COPY ["StockSpotter.API/StockSpotter.API.csproj", "StockSpotter.API/"]
RUN dotnet restore "StockSpotter.API/StockSpotter.API.csproj"
COPY . .
WORKDIR "/src/StockSpotter.API"
RUN dotnet build "StockSpotter.API.csproj" -c Release -o /app/build

FROM build AS publish
RUN dotnet publish "StockSpotter.API.csproj" -c Release -o /app/publish

# Final stage/image
FROM base AS final
WORKDIR /app
COPY --from=publish /app/publish .
ENTRYPOINT ["dotnet", "StockSpotter.API.dll"]
