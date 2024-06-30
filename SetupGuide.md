# Çalışma Ortamı Rehberi

## Gereksinimler

- .NET 6 SDK
- PostgreSQL
- RabbitMQ (CloudAMQP veya yerel sunucu)
- Visual Studio veya Visual Studio Code

## Kurulum

1. **Proje Deposu**: Projeyi klonlayın.

   ```bash
   git clone https://github.com/kullanıcı/InstantReservation.git
   cd InstantReservation

2. **Bağımlılıklar**: Gerekli bağımlılıkları yükleyin.

    ```bash
   dotnet restore
   
3. **Veritabanı**: PostgreSQL sunucusunu başlatın ve appsettings.json dosyasında bağlantı dizesini ayarlayın.

   ```json
   "ConnectionStrings": {
    "DefaultConnection": "Host=localhost;Database=instantreservation;User ID=kullanıcı;Password=şifre;Port=5432;"}

4. **RabbitMQ**: RabbitMQ bağlantı ayarlarını appsettings.json dosyasında yapın.

   ```json
   "RabbitMQ": {
    "HostName": "host_adresi",
    "UserName": "kullanıcı",
    "Password": "şifre",
    "VirtualHost": "vhost_adı"
   }
   
5. **Veritabanı Güncellemesi**: Veritabanını EF Core Migrations ile güncelleyin.

   ```bash
   dotnet ef database update
   
## Çalıştırma 

   ```bash
   dotnet run 
```
- API'yi tarayıcıda görüntüleyin: http://localhost:5000/swagger

## Test Etme

- Postman veya Swagger kullanarak API'yi test edebilirsiniz.

## Ortam Değişkenleri 

- ASPNETCORE_ENVIRONMENT: Development veya Production olarak ayarlanabilir.




