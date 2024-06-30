
### ARCHITECTURE.md

# Proje Mimarisi

## Katmanlar

### 1. Application

- **Commands**: CRUD işlemleri için komut sınıfları ve işleyiciler içerir.
- **Queries**: Veri sorgulama işlemleri için sorgu sınıfları ve işleyiciler içerir.

### 2. Domain

- **Entities**: Uygulamanın temel varlıklarını tanımlar (örneğin, `Reservation`).

### 3. Infrastructure

- **Messaging**: RabbitMQ mesajlaşma altyapısını içerir (publisher ve consumer).
- **Persistence**: Veritabanı erişim katmanını içerir (EF Core).

### 4. Presentation

- **API**: ASP.NET Core MVC kullanılarak oluşturulmuş API denetleyicilerini içerir.
- **SignalR**: Gerçek zamanlı iletişim için SignalR hub'larını içerir.

## İş Akışı

1. **Rezervasyon Oluşturma**:
   - `CreateReservationCommand` API üzerinden alınır.
   - `CreateReservationCommandHandler` tarafından işlenir.
   - Rezervasyon veritabanına kaydedilir.
   - SignalR ile tüm istemcilere bildirim gönderilir.
   - RabbitMQ kuyruğuna mesaj eklenir.

2. **Rezervasyonları Listeleme**:
   - `GetReservationsQuery` API üzerinden alınır.
   - `GetReservationsQueryHandler` tarafından işlenir.
   - Tüm rezervasyonlar veritabanından alınır ve istemciye döndürülür.

## Teknolojiler

- **ASP.NET Core**: Web API ve gerçek zamanlı iletişim.
- **Entity Framework Core**: Veritabanı işlemleri.
- **MediatR**: CQRS desenini uygular.
- **RabbitMQ**: Mesajlaşma altyapısı.
- **SignalR**: Gerçek zamanlı bildirimler.

## Bağımlılıklar

- `MediatR`: Komut/sorgu desenini uygular.
- `RabbitMQ.Client`: Mesaj kuyruğu işlemleri için kullanılır.
- `Microsoft.EntityFrameworkCore`: ORM için kullanılır.

## Sınıf Diyagramı

```plaintext
+-------------------+
|   Reservations    |
+-------------------+
| - Id              |
| - GuestName       |
| - CheckInDate     |
| - CheckOutDate    |
| - RoomNumber      |
| - CreatedAt       |
+-------------------+

+-------------------+
|   ReservationHub  |
+-------------------+
| + SendMessage()   |
+-------------------+

+-------------------+
|  CreateReservation|
+-------------------+
| - GuestName       |
| - CheckInDate     |
| - CheckOutDate    |
| - RoomNumber      |
+-------------------+
| + Handle()        |
+-------------------+

+-------------------+
|  GetReservations  |
+-------------------+
|                   |
+-------------------+
| + Handle()        |
+-------------------+

+-------------------+
|  RabbitMqPublisher|
+-------------------+
| + PublishMessage()|
+-------------------+

+-------------------+
|  RabbitMqConsumer |
+-------------------+
| + ExecuteAsync()  |
+-------------------+
