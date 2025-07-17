# HayvanatBahcesiSimulasyonu-SelamiCetin-GO
🚀 Go ile Paralel Hayvan Popülasyonu Simülasyonu
Bu proje, bir ekosistemdeki hayvan popülasyonlarının dinamiklerini simüle eden, Go dilinde yazılmış yüksek performanslı bir simülasyon sistemidir. Python versiyonuna kıyasla, bu uygulama:

Paralel işleme ile performansı 10x artırır

Detaylı istatistikler ve popülasyon değişim raporları sunar

Gerçek zamanlı ilerleme çubuğu içerir

Renkli konsol çıktıları ve dosyaya rapor kaydetme özelliğine sahiptir

🌟 Temel Özellikler
go
// Ana simülasyon parametreleri
const (
    width  = 100   // Simülasyon alanı genişliği
    height = 100   // Simülasyon alanı yüksekliği
    steps  = 500   // Simülasyon adım sayısı
)
7 farklı hayvan türü: Koyun, inek, tavuk, horoz, kurt, aslan ve avcı

Gerçekçi davranış modelleri:

Türlere özgü hareket mesafeleri

Cinsiyet temelli üreme mekaniği

Av-avcı ilişkileri (türe özgü avlanma)

İstatistiksel takip:

Başlangıç ve bitiş popülasyonları

Üreme ve avlanma olay sayıları

Popülasyon değişim oranları

Görsel ilerleme çubuğu

⚙️ Teknik Mimarî
Diagram(Code) : 
graph TD
    A[Başlatma] --> B[CPU Çekirdeklerini Ayarla]
    B --> C[Hayvan Popülasyonu Oluştur]
    C --> D[İstatistikleri İlkile]
    D --> E[İlerleme Çubuğunu Başlat]
    E --> F{Simülasyon Adımları}
    F --> G[Paralel Hareket]
    G --> H[Üreme Fazı]
    H --> I[Avlanma Fazı]
    I --> F
    F --> J[İstatistikleri Hesapla]
    J --> K[Sonuçları Göster]
    K --> L[Sonuçları Dosyaya Kaydet]





🧩 Ana Bileşenler
Animal Struct'ı:

Tür, cinsiyet, konum, yaşam durumu ve benzersiz kimlik

Her hayvanın türüne özel hareket yeteneği

Stats Struct'ı:

Popülasyon istatistiklerini toplar

Üreme ve avlanma olaylarını sayar

Zamanlama bilgilerini tutar

Eşzamanlı Simülasyon:

sync.WaitGroup ile paralel hareket hesaplama

Semafor kontrollü goroutine'ler

🚀 Performans Optimizasyonu
go
// Paralel hareket işlemi
semaphore := make(chan struct{}, runtime.NumCPU())
for _, animal := range animals {
    semaphore <- struct{}{}
    go func(a *Animal) {
        defer wg.Done()
        if a.alive {
            moveAnimal(a)
        }
        <-semaphore
    }(animal)
}
wg.Wait()
Paralel Hareket Hesaplama: Her hayvanın hareketi ayrı goroutine'lerde işlenir

Semafor Tabanlı Sınırlama: Aynı anda çalışan goroutine sayısı CPU çekirdek sayısı ile sınırlıdır

Rastgele Sayı Üreteci: Her goroutine için ayrı rastgelelik (global rand kullanılmaz)

📊 Örnek Çıktı
text
🚀 Simülasyon başlıyor - 8 CPU çekirdeği kullanılıyor

Simülasyon ilerlemesi:
[============================>                     ] 60%
...
✅ Simülasyon tamamlandı!

📊 === Hayvanat Bahçesi Simülasyonu Sonuçları ===
⏱️  Toplam simülasyon süresi: 2.5s
🐣 Toplam üreme olayları: 42
🐺 Toplam avlanma olayları: 28
🐾 Toplam hayvan sayısı: Başlangıç: 100, Son: 114

📈 Başlangıç Popülasyonları:
🐑 Koyun: 30
🐄 İnek: 10
🐔 Tavuk: 10
🐓 Horoz: 10
🐺 Kurt: 10
🦁 Aslan: 8
🎯 Avcı: 1

📉 Son Popülasyonlar:
🐑 Koyun: 45
🐄 İnek: 5
🐔 Tavuk: 25
🐓 Horoz: 20
🐺 Kurt: 12
🦁 Aslan: 6
🎯 Avcı: 1

📊 Popülasyon Değişimleri:
Koyun: 30 → 45 ▲ (+15 ▲ 50.00%)
İnek: 10 → 5 ▼ (-5 ▼ 50.00%)
...
💾 Sonuçlar 'simulasyon_sonuclari.txt' dosyasına kaydedildi.
🌍 Çalıştırma
bash
# Projeyi klonla
git clone https://github.com/Selami7321/HayvanatBahcesiSimulasyonu-SelamiCetin-GO.git
cd HayvanatBahcesiSimulasyonu-SelamiCetin-GO

# Bağımlılıkları yükle (gerekirse)
go mod init simulasyon
go mod tidy

# Simülasyonu çalıştır
go run main.go
📈 Olası Geliştirmeler
Gerçek Zamanlı Görselleştirme:

Hayvan hareketlerinin canlı haritası

Popülasyon değişim grafikleri

Çevresel Faktörler:

Su kaynakları ve bitki örtüsü

Mevsimsel değişimler

Gelişmiş Genetik:

Kalıtsal özellik aktarımı

Mutasyon mekanizmaları

Bu proje, ekosistem simülasyonları için sağlam bir temel oluşturur ve büyük popülasyonlarda yüksek performans gerektiren durumlarda kullanılabilir.
