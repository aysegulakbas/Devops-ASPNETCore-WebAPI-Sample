# Tek Aşama: Build ve Runtime
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS base
WORKDIR /app

# SDK imajını kullanarak uygulamayı derleyin ve yayınlayın
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /app

# Projeyi kopyala ve bağımlılıkları yükle
COPY SampleWebApiAspNetCore.csproj ./
RUN dotnet restore

# Tüm proje dosyalarını kopyala
COPY . ./
RUN dotnet publish -c Release -o /app/publish

# Uygulama çalıştırma aşamasına geç
FROM base AS final
WORKDIR /app
COPY --from=build /app/publish .

# Portu aç
EXPOSE 80

# Uygulamanın başlatılması
ENTRYPOINT ["dotnet", "SampleWebApiAspNetCore.dll"]
