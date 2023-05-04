# Use an official .NET 6 SDK image as the base image
FROM mcr.microsoft.com/dotnet/sdk:6.0 AS build

# Set the working directory to /app
WORKDIR /app

# Copy the .csproj file and restore any dependencies (optional caching)
COPY *.csproj ./
RUN dotnet restore

# Copy the remaining files
COPY . .

# Build the application and its dependencies in release mode
RUN dotnet publish -c Release -o out

# Use a lightweight .NET 6 runtime image as the final image
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS runtime

# Set the working directory to /app
WORKDIR /app

# Copy the published output from the build image to the runtime image
COPY --from=build /app/out .

# Expose the port that the application listens on (adjust as necessary)
EXPOSE 80

# Start the application
ENTRYPOINT ["dotnet", "notification-backend-api.dll"]