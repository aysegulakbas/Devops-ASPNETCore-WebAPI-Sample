# Use a base image with .NET SDK and runtime
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env

# Set working directory
WORKDIR /app

# Copy project file and restore dependencies
COPY SampleWebApiAspNetCore.csproj ./
RUN dotnet restore

# Copy and build the application
COPY . ./
RUN dotnet publish -c Release -o /app/publish

# Use the runtime image to create the final image
FROM mcr.microsoft.com/dotnet/aspnet:7.0
WORKDIR /app
COPY --from=build-env /app/publish .

# Expose port and set entry point
EXPOSE 80
ENTRYPOINT ["dotnet", "SampleWebApiAspNetCore.dll"]
