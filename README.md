# DOM Engine Visualizer

Bu proje, bir web tarayıcısının arka planında gerçekleşen **HTML Ayrıştırma (Parsing)** ve **DOM Ağacı (Document Object Model) Oluşturma** sürecini simüle eden eğitsel bir veri yapıları projesidir. 

Projenin en temel özelliği; C# dilindeki hazır koleksiyonlar (`List<>`, `Dictionary<>` vb.) **kullanılmadan**, tüm temel veri yapılarının ve arama algoritmalarının sıfırdan yazılmış olmasıdır.

---

## 🛠️ Kullanılan Teknolojiler

- **Backend / Core Motor:** C# (.NET 8)
- **API Katmanı:** ASP.NET Core Web API
- **Frontend / Arayüz:** HTML5, CSS3 (Modern Dark Mode, Glassmorphism), Vanilla JavaScript (Fetch API)
- **Altyapı (Dağıtım):** Docker, Docker Compose, Nginx (Reverse Proxy ve CORS yönetimi için)

---

## 🧠 Veri Yapıları ve Algoritmalar

Bu projede arka planda çalışan motor, tamamen kendi yazdığımız veri yapıları üzerine inşa edilmiştir:

*   **N-ary Tree (Çoklu Ağaç):** HTML düğümlerini (DomNode) hiyerarşik bir ağaç yapısında, ebeveyn-çocuk (parent-child) ilişkisiyle tutar. Belgenin kökünden (`<html>`) başlayarak dallanır.
*   **CustomHashTable (Karma Tablo):** İki farklı kritik noktada kullanılmıştır:
    1.  **Nitelik Depolama (O(1)):** Her `DomNode`'un kendi içindeki özelliklerini (`id`, `class`, `src` vb.) hızlıca okuyabilmesi için bir özellik tablosu.
    2.  **ID Önbelleği (O(1) Arama):** `GetElementById` fonksiyonunun tüm ağacı dolaşmak yerine doğrudan düğüme ulaşabilmesi için `NaryTree` içindeki merkezi adresleme tablosu. Çarpışmaları (Collision) en aza indirmek için asal sayı tabanlı bir hash algoritması ve Chaining (Bağlı liste) kullanır.
*   **CustomStack (Yığın):** LIFO (Son giren ilk çıkar) mantığıyla HTML Parse işlemi sırasında açılan (`<div>`) ve kapanan (`</div>`) etiketlerin eşleşme kontrolü için kullanılmıştır.
*   **CustomList (Dinamik Dizi):** Düğümlerin çocuk listelerini esnek bir kapasiteyle tutmak için kullanılmıştır.
*   **CustomQueue (Kuyruk):** Gelişmiş BFS (Breadth-First Search) aramalarında kullanılmak üzere altyapı olarak tasarlanmıştır.
*   **DFS (Depth-First Search):** Ağacın derinliklerine inerek düğüm arama (`DomSearch` motoru) algoritmaları için kullanılmıştır.

---

## 🚀 Projeyi Local'de Çalıştırma (Tutorial)

Projeyi sisteminizde ayağa kaldırmanın iki yolu vardır. En kolayı ve önerileni **Docker** kullanmaktır.

### Yöntem 1: Docker ile Çalıştırma (Önerilen)
*Gereksinimler: Bilgisayarınızda Docker ve Docker Compose yüklü ve çalışır durumda olmalıdır. Eğer yüklü değilse [Docker Desktop Kurulum Rehberi](https://docs.docker.com/get-docker/)'ni inceleyebilirsiniz.*

1. Terminali (veya Komut İstemini) açın.
2. Projenin ana dizinine (`docker-compose.yml` dosyasının bulunduğu klasör) gidin:
   ```bash
   cd <projenin_bulundugu_konum>
   ```
3. Aşağıdaki komutu çalıştırarak hem API'yi hem de Frontend sunucusunu ayağa kaldırın:
   ```bash
   docker-compose up -d --build
   ```
4. Tarayıcınızı açın ve şu adrese gidin: **[http://localhost:3000](http://localhost:3000)**

### 🛑 Sistemi Kapatma (Önemli)
İşiniz bittiğinde arka planda sunucuların boşuna çalışıp RAM ve işlemci tüketmemesi için terminalde aynı dizindeyken şu komutu çalıştırarak sistemi tamamen kapatabilirsiniz:
```bash
docker-compose down
```

### Yöntem 2: Visual Studio (Docker Olmadan)
*Gereksinimler: Visual Studio 2022, .NET 8 SDK, VS Code (Live Server Eklentisi)*

1. Proje klasöründeki **`DomEngine.slnx`** dosyasını Visual Studio ile açın.
2. Üst menüden **DomEngine.Api** projesini Başlangıç Projesi (Startup Project) olarak seçin ve çalıştırın. (API genellikle `localhost:5000` veya `localhost:8080` portunda ayağa kalkar).
3. API çalışırken, **`DomEngine.Web`** klasörünü Visual Studio Code ile açın.
4. VS Code içindeki `app.js` dosyasında bulunan `fetch` isteklerinin port adresinin, çalışan API'nizin portu ile eşleştiğinden emin olun.
5. `index.html` dosyasına sağ tıklayıp **"Open with Live Server"** seçeneğine tıklayarak arayüzü başlatın.
