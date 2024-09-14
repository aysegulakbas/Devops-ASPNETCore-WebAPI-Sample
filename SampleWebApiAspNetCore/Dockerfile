# Stage 1: Build Stage
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env
WORKDIR /app

# Copy the project file and restore dependencies
COPY SampleWebApiAspNetCore.csproj ./SampleWebApiAspNetCore/
WORKDIR /app/SampleWebApiAspNetCore
RUN dotnet restore

# Copy the entire project and build the application
COPY . ./
RUN dotnet publish -c Release -o /app/publish

# Stage 2: Production Stage
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime
WORKDIR /app

# Copy only the build output from the previous stage
COPY --from=build-env /app/publish .

# Expose the application port
EXPOSE 80

# Set the entry point for the application
ENTRYPOINT ["dotnet", "SampleWebApiAspNetCore.dll"]
