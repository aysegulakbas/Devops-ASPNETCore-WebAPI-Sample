# .NET SDK kullanarak uygulamayı build ve publish ediyoruz
FROM mcr.microsoft.com/dotnet/sdk:7.0

WORKDIR /app

# Proje dosyalarını kopyalıyoruz
COPY . ./

# Uygulamayı restore, build ve publish ediyoruz
RUN dotnet restore
RUN dotnet build -c Release --no-restore
RUN dotnet publish -c Release -o /app/publish --no-build

# ASP.NET runtime'ı ile çalıştırmak için
# publish edilmiş dosyaları bu aşamada kullanıyoruz
WORKDIR /app/publish

# Uygulama portunu açıyoruz
EXPOSE 80

# Uygulama başlatma komutu
ENTRYPOINT ["dotnet", "SampleWebApiAspNetCore.dll"]
