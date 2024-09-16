# Base image
FROM ubuntu:20.04

# Install prerequisites
RUN apt-get update && \
    apt-get install -y wget apt-transport-https gnupg && \
    wget https://packages.microsoft.com/config/ubuntu/20.04/prod.list && \
    mv prod.list /etc/apt/sources.list.d/mssql-release.list && \
    wget -q https://packages.microsoft.com/keys/microsoft.asc -O- | apt-key add - && \
    apt-get update

# Install .NET SDK
RUN apt-get install -y dotnet-sdk-7.0

# Install other dependencies if necessary
# RUN apt-get install -y [other-packages]

# Set the working directory
WORKDIR /app

# Copy the project files
COPY . /app

# Build the application
RUN dotnet build --configuration Release

# Publish the application
RUN dotnet publish --configuration Release --output /app/publish

# Set the entry point
ENTRYPOINT ["dotnet", "/app/publish/SampleWebApiAspNetCore.dll"]

# Expose the port
EXPOSE 80
