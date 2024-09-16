FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build-env
WORKDIR /app/SampleWebApiAspNetCore

# Proje dosyasını kopyala ve bağımlılıkları yükle
COPY SampleWebApiAspNetCore.csproj ./
RUN dotnet restore

# Projenin geri kalanını kopyala ve build yap
COPY . ./
RUN dotnet publish -c Release -o /app/publish

# Production stage
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime
WORKDIR /app
COPY --from=build-env /app/publish .

EXPOSE 80
ENTRYPOINT ["dotnet", "SampleWebApiAspNetCore.dll"]
