# Base image olarak .NET SDK kullanıyoruz
FROM mcr.microsoft.com/dotnet/sdk:7.0 AS build
WORKDIR /app

# Proje dosyalarını kopyalıyoruz
COPY . ./

# Uygulamayı restore ediyor ve build ediyoruz
RUN dotnet restore
RUN dotnet build -c Release --no-restore

# Uygulamayı publish ediyoruz
RUN dotnet publish -c Release -o /app/publish --no-build

# Runtime aşamasında sadece ASP.NET runtime'ı kullanıyoruz
FROM mcr.microsoft.com/dotnet/aspnet:7.0 AS runtime
WORKDIR /app

# Publish edilen dosyaları runtime container'a kopyalıyoruz
COPY --from=build /app/publish .

# Uygulama portunu açıyoruz
EXPOSE 80

# Uygulama başlatma komutu
ENTRYPOINT ["dotnet", "SampleWebApiAspNetCore.dll"]
