# Aşama 1: Temel Bileşenlerin İnşası Görev Listesi
- [x] Temel veri yapıları (Node, CustomList, CustomStack, CustomQueue, CustomHashTable)

# Aşama 2: Ağaç Topolojisi ve DomNode
- [x] `DomNode` ve `NaryTree` sınıfları

# Aşama 3: Parser Motoru
- [x] `Parser` klasörü ve `HtmlParser` motoru.
- [x] Karakter tabanlı tag ve attribute tokenization.

# Aşama 4: Arama ve Analiz Algoritmaları
- [x] `Algorithms` klasörünün ve `DomSearch` sınıfının oluşturulması.
- [x] Ağaç üzerinde gezerek çalışan DFS ve BFS aramaları.
- [x] `NaryTree` sınıfına `CustomHashTable` tabanlı ID önbelleği.

# Aşama 5: API ve UI (Frontend) Entegrasyonu
- [x] `DomEngine.Api` adında ASP.NET Core Web API projesinin oluşturulması ve Core projesinin referans olarak eklenmesi.
- [x] `ParserController` oluşturularak HTML parse isteği alan ve ağacı JSON döndüren endpoint yazılması.
- [x] `DomEngine.Web` klasörünün oluşturulması (Frontend).
- [x] Modern tasarımlı (Dark mode, neon renkler, glassmorphism vb.) Sol Panel (Metin Girişi) ve Sağ Panel (Dinamik Ağaç) arayüzünün kodlanması.
- [x] Frontend'in Fetch API kullanarak C# Web API'ye bağlanması ve JSON sonucunu açılır-kapanır hiyerarşik ağaç şeklinde ekrana çizdirmesi.

# Aşama 6: Docker Entegrasyonu
- [x] `DomEngine.Api` için `Dockerfile` oluşturulması (.NET 8 SDK & Runtime).
- [x] `DomEngine.Web` için `Dockerfile` ve `nginx.conf` oluşturulması (Nginx Reverse Proxy ile CORS sorunlarının kökten çözümü).
- [x] Frontend'deki statik IP/Port bağımlılığının kaldırılarak esnek hale getirilmesi.
- [x] `docker-compose.yml` yazılarak tüm sistemin tek komutla ayağa kaldırılacak şekle getirilmesi.

# Aşama 7: Parser ve Arama Motoru İyileştirmeleri
- [x] `HtmlParser.cs` içinde state machine tabanlı etiket ayrıştırma (Tırnak içindeki '>' sorununu çözme).
- [x] `CustomHashTable.cs` sınıfına `GetAllPairs()` metodunun eklenmesi.
- [x] `DomSearch.cs` içinde herhangi bir niteliğe (attribute) göre arama yapabilen BFS ve DFS metotlarının yazılması.
- [x] `ParserController.cs`'nin güncellenerek tüm nitelikleri Frontend'e göndermesi ve yeni arama algoritmalarını desteklemesi.
- [x] Frontend (`index.html`, `app.js`) tarafında yeni arama türleri için arayüz ve mantık güncellemelerinin yapılması.
