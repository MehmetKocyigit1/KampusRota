# 🚗 Kampus Rota (Full-Stack Monorepo)

[![.NET](https://img.shields.io/badge/.NET-8.0%20%7C%209.0-512BD4?logo=dotnet)](https://dotnet.microsoft.com/)
[![ASP.NET Core](https://img.shields.io/badge/ASP.NET%20Core-Web%20API-5C2D91)](https://learn.microsoft.com/aspnet/core)
[![.NET MAUI](https://img.shields.io/badge/.NET%20MAUI-Cross--Platform-512BD4)](https://learn.microsoft.com/dotnet/maui/)
[![Database](https://img.shields.io/badge/Database-SQL%20Server-CC2927?logo=microsoftsqlserver)](https://www.microsoft.com/sql-server)
[![Map](https://img.shields.io/badge/Map-MapLibre%20%7C%20OpenStreetMap-007AFF)](https://maplibre.org/)
[![Docker](https://img.shields.io/badge/Docker-Ready-blue?logo=docker)](https://www.docker.com/)
[![License](https://img.shields.io/badge/License-MIT-green.svg)](LICENSE)

**Kampus Rota**, üniversite kampüsleri ve şehir merkezleri arasında güvenli, ekonomik ve sürdürülebilir yolculuk paylaşımı (carpooling) sağlayan modern bir full-stack platformdur.

Bu repo, projenin **Backend (ASP.NET Core Clean Architecture)** ve **Frontend (Cross-Platform .NET MAUI)** projelerini tek bir monorepo yapısında birleştirmektedir.

---

## 🏛️ Mimari ve Proje Yapısı

```text
KampusRota/
├── KampusRota.sln                  # Tüm projeleri içeren ana Visual Studio çözümü
├── KampusRotaAPI/                  # Backend RESTful API Servisleri
│   ├── src/
│   │   ├── KampusRota.Domain/          # Temel Domain varlıkları ve enumlar
│   │   ├── KampusRota.Application/     # Servis sözleşmeleri, DTO'lar, iş kuralları
│   │   ├── KampusRota.Infrastructure/  # EF Core AppDbContext, DbInitializer, Servisler
│   │   └── KampusRota.API/             # Web API Controllers/Endpoints, Middleware, Swagger
│   ├── tests/
│   │   └── KampusRota.UnitTests/       # xUnit birim testleri
│   ├── Dockerfile                      # API Docker imajı
│   └── docker-compose.yml              # SQL Server + API konteyner orkestrasyonu
│
└── KampusRotaUI/                   # Mobil ve Masaüstü İstemci (.NET MAUI)
    ├── Models/                         # İstemci veri modelleri
    ├── Services/                       # HTTP API ve harita köprü servisleri
    ├── Views/                          # XAML ekranları (Giriş, Harita, İlanlar, Profil vb.)
    ├── Platforms/                      # Android, iOS, Windows platform konfigürasyonları
    └── Resources/                      # Stil, font, görsel ve harita şablonları
```

---

## ✨ Temel Özellikler

* **Çoklu Kampüs ve Açık Harita (MapLibre GL + OpenStreetMap):**
  * Türkiye genelindeki 24+ üniversite ve yüzlerce kampüs durağı desteği.
  * Ücretsiz, API anahtarı gerektirmeyen dinamik harita entegrasyonu.
* **Akıllı Üniversite Eşleştirme:**
  * Öğrenci kurumsal e-posta adresiyle (`@itu.edu.tr`, `@sdu.edu.tr` vb.) kayıt olduğunda otomatik üniversite tespiti ve ilgili kampüse odaklanma.
* **Yolculuk Paylaşımı (Carpooling) Akışı:**
  * İlan oluşturma, kalkış/varış durağı belirleme, filtreleme ve arama.
  * Katılım talepleri gönderme, sürücü onay/red mekanizması.
  * Yalnızca kadın öğrencilere özel yolculuk seçeneği.
  * Karşılıklı değerlendirme ve puanlama sistemi.
* **Kurumsal Clean Architecture:**
  * Bağımlılıkların dıştan içe doğru yönlendiği, test edilebilir ve sürdürülebilir mimari yapı.
* **Merkezi Hata Yönetimi:**
  * RFC 7807 (`application/problem+json`) standardında küresel hata yakalama.

---

## 🚀 Başlangıç ve Çalıştırma

### Gereksinimler
* [.NET 8 veya .NET 9 SDK](https://dotnet.microsoft.com/download)
* .NET MAUI Workload (`dotnet workload install maui`)
* Visual Studio 2022 (ASP.NET ve .NET MAUI iş yükleri yüklü) veya VS Code
* SQL Server veya Docker (isteğe bağlı)

### 1. Repoyu Klonlayın
```bash
git clone https://github.com/MehmetKocyigit1/KampusRota.git
cd KampusRota
```

### 2. Tek Çözümle Açma (Visual Studio)
Kök dizindeki `KampusRota.sln` dosyasını Visual Studio ile açarak hem API hem de Mobil projeyi tek bir pencereden yönetebilirsiniz:
* **Multiple Startup Projects** seçeneği ile hem `KampusRota.API` hem de `KampusRotaUI` projelerini aynı anda F5 ile başlatabilirsiniz.

### 3. Komut Satırından Çalıştırma

**Backend API'yi Başlatma:**
```bash
cd KampusRotaAPI
dotnet run --project src/KampusRota.API
```
> API varsayılan olarak `https://localhost:7040` / `http://localhost:5040` adresinde Swagger arayüzü ile çalışır.

**Mobil Uygulamayı Başlatma (Windows için örnek):**
```bash
cd KampusRotaUI
dotnet build -t:Run -f net8.0-windows10.0.19041.0
```

**Birim Testleri Çalıştırma:**
```bash
dotnet test KampusRotaAPI/tests/KampusRota.UnitTests/KampusRota.UnitTests.csproj
```

---

## 📄 Lisans

Bu proje [MIT Lisansı](LICENSE) altında lisanslanmıştır.
