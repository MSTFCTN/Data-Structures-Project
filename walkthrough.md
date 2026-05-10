# Arama Motoru Evrenselleşti (Universal Search)! 🚀

Harika bir vizyonla arama motorumuzu çok daha modern ve güçlü bir hale getirdik! 

Artık sistemi kullanırken "Şu Class mıydı, Tag mıydı, Hangi Attribute'tu?" diye düşünmenize gerek yok. Tıpkı modern tarayıcıların "Inspect" panellerinde olduğu gibi, aradığınız kelime neyse sadece onu yazıyorsunuz ve motorumuz onu ağacın her hücresinde (etiket adında, nitelik anahtarlarında ve nitelik değerlerinde) köşe bucak arıyor.

İşte yapılan köklü değişiklikler:

### 1. Eski Hantal Arama Metotları Silindi
`DomSearch.cs` içindeki `GetElementsByClassName`, `GetElementsByTagName`, `GetElementsByAttribute` gibi kısıtlayıcı tüm metotları sildik. Yerine yepyeni iki tane süper metot yazdık:
- `SearchDFS` (Derinlik Öncelikli Evrensel Arama)
- `SearchBFS` (Genişlik Öncelikli Evrensel Arama)

Bu metotlar artık "Kısmi Eşleşme" (`Contains`) destekliyor. Yani `wrapper` yazarsanız, `test-wrapper` sınıfına sahip elemanları da bulur!

### 2. O(1) Performans Gösterisi Korundu
Ders projesi olduğu için algoritmaların zaman karmaşıklığı (Time Complexity) çok önemli. Bu yüzden Hash Table'ın `O(1)` performansını sergilemek için **"ID ile Arama"** seçeneğini UI'da ve API'de baş köşede tuttuk. Geriye kalan tüm O(N) sorgular Evrensel DFS/BFS içine hapsedildi.

### 3. Kullanıcı Arayüzü (UI) Çok Daha Sade
Sol taraftaki açılır menüyü (Dropdown) kalabalıktan kurtardık. Artık sadece 3 seçeneğimiz var:
- **ID (Hızlı O(1))**
- **Genel Arama (DFS O(N))**
- **Genel Arama (BFS O(N))**

Placeholder (yer tutucu metin) de "Örn: div, active, container..." şeklinde çok daha kullanıcı dostu bir yapıya kavuştu.

---

### 🧪 Nasıl Test Edebilirsiniz?
Backend (C#) tarafındaki algoritmaları tamamen değiştirdiğimiz için projeyi son bir kez (ve umarım bu geceki son derleme olur 😄) yeniden derlememiz gerekiyor:

```bash
docker-compose up -d --build
```
Daha sonra tarayıcıda `http://localhost:3000` adresini açıp (veya **CTRL+F5** ile yenileyip), Genel Arama (DFS veya BFS) modunda sadece `active` veya `link` yazarak arama yapmayı deneyin! Nasıl fişek gibi bulduğunu göreceksiniz. ⚡
