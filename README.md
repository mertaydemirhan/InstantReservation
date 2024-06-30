# InstantReservation

InstantReservation, otel rezervasyonlarını yönetmek için geliştirilmiş bir API'dir. Bu proje, SignalR ve RabbitMQ kullanarak gerçek zamanlı iletişim ve mesajlaşma imkanı sağlar.

## Başlarken

### Gereksinimler

- .NET 6 SDK
- PostgreSQL
- RabbitMQ (CloudAMQP veya yerel sunucu)

### Kurulum

1. Projeyi klonlayın:

   ```bash
   git clone https://github.com/kullanıcı/InstantReservation.git
   cd InstantReservation

2. Bağlantı dizesini ve RabbitMQ ayarlarını appsettings.json dosyasında güncelleyin:

   ```json
   {"ConnectionStrings": {"DefaultConnection": "Host=localhost;Database=instantreservation;User ID=kullanıcı;Password=şifre;Port=5432;"},
   "RabbitMQ": {"HostName": "host_adresi","UserName": "kullanıcı","Password": "şifre","VirtualHost": "vhost_adı"}}
   
3. Veritabanını güncelleyin:

   ```bash
   dotnet ef database update
   
4. Uygulamayı başlatın:

   ```bash
   dotnet run

## API Kullanımı

- Swagger arayüzü ile API'yi keşfedin: http://localhost:5000/swagger

### Örnek İstekler

- Rezervasyon Oluşturma:

  ```http
  POST /api/Reservations
  Content-Type: application/json
  
  {
      "guestName": "Mahmut Orhan",
      "checkInDate": "2024-07-01T14:00:00",
      "checkOutDate": "2024-08-01T14:00:00",
      "roomNumber": "101"
  }

## Teknolojiler
 
- ASP.NET Core
- Entity Framework Core
- MediatR
- SignalR
- RabbitMQ   

## API Sonuçları

- /api/Reservations [GET]: Tüm rezervasyonları döner.
- /api/Reservations [POST]: Yeni rezervasyon oluşturur.

## Bağlantılar

- [RabbitMQ](https://www.rabbitmq.com/)
- [SignalR](https://dotnet.microsoft.com/apps/aspnet/signalr)