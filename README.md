# Hamming SEC-DED Kod Simülatörü

Bu proje, Hamming Single Error Correction - Double Error Detection (SEC-DED) kodlama algoritmasını interaktif olarak öğrenmek ve test etmek için geliştirilmiş bir web tabanlı simülatördür.

### 🎥 Detaylı anlatım videosunu izlemek isterseniz -> [YouTube videosu](https://www.youtube.com/watch?v=XcU6nmkFBxM&t=1s)

## 🎯 Özellikler

- **Hamming SEC-DED Kod Oluşturma**: 8, 16 veya 32 bitlik veri için otomatik kod üretimi
- **Hata Enjeksiyonu**: Tek ve çift bit hataları ekleme
- **Manuel Hata Ekleme**: Belirli pozisyonlara hata ekleme imkanı
- **Hata Tespit ve Düzeltme**: Otomatik hata analizi ve düzeltme
- **Görsel Geri Bildirim**: Renk kodlu durum göstergeleri
- **Responsive Tasarım**: Tüm cihazlarda uyumlu arayüz

## 🚀 Hızlı Başlangıç

### Kurulum

1. **Projeyi klonlayın:**
```bash
git clone https://github.com/korayga/hamming-code.git
cd hamming-code
```

2. **Dosyaları yerel sunucuda çalıştırın:**
```bash
# Python 3 ile
python -m http.server 8000

# PHP ile
php -S localhost:8000
```

3. **Tarayıcıda açın:**
```
http://localhost:8000
```

Veya doğrudan `index.html` dosyasını tarayıcıda açabilirsiniz.

## 📁 Proje Yapısı

```
hamming-sec-ded-simulator/
├── index.html          # Ana HTML dosyası
├── style.css           # CSS stilleri
├── bg.png             # Arka plan görseli 
└── README.md          
```

## 🎮 Kullanım Kılavuzu

### 1. Veri Girişi
- **Desteklenen formatlar**: 8, 16 veya 32 bit binary veri
- **Geçerli karakterler**: Sadece '0' ve '1'
- **Örnek girişler**:
  - 8 bit: `10101010`
  - 16 bit: `1010101011001100`
  - 32 bit: `10101010110011001111000011110000`

### 2. Hamming Kodu Oluşturma
1. Veri girişi alanına binary veriyi girin
2. "Hamming SEC-DED Kodu Oluştur" butonuna tıklayın
3. Oluşturulan kod otomatik olarak gösterilecektir

### 3. Hata Enjeksiyonu

#### Otomatik Hata Ekleme:
- **Tek Hata**: Rastgele bir bit pozisyonunda hata oluşturur
- **Çift Hata**: Rastgele iki farklı bit pozisyonunda hata oluşturur

#### Manuel Hata Ekleme:
1. "Bit pozisyonu" alanına hata eklemek istediğiniz pozisyonu girin 
2. "Hata Ekle" butonuna tıklayın

### 4. Hata Tespit ve Düzeltme
- "Hata Tespiti ve Düzeltme" butonuna tıklayın
- Sistem otomatik olarak:
  - Hata var mı kontrol eder
  - Tek hataları tespit edip düzeltir
  - Çift hataları sadece tespit eder (düzeltemez)
  - Sonucu renkli göstergelerle belirtir

## 🔧 Teknik Detaylar

### Hamming SEC-DED Algoritması

#### Kod Yapısı:
- **Veri bitleri**: Orijinal bilgi
- **Parity bitleri**: Hata tespiti için (pozisyon: 2^i)
- **SEC biti**: Çift hata tespiti için ek parite

#### Parity Bit Hesaplaması:
```
2^r ≥ (m + r + 1)
```
- `m`: Veri bit sayısı
- `r`: Gerekli parity bit sayısı

#### Hata Tespit Mantığı:
- **Sendrom = 0, SEC = 0**: Hata yok
- **Sendrom ≠ 0, SEC = 1**: Tek hata (düzeltilebilir)
- **Sendrom = 0, SEC = 1**: SEC bitinde hata
- **Sendrom ≠ 0, SEC = 0**: Çift hata (tespit edilir ama düzeltilmez)

### Kod Mimarisi

#### Temel Fonksiyonlar:
- `createHammingCode()`: Ana kod oluşturma
- `generateSECDEDCode()`: SEC-DED algoritması
- `performSECDEDDecoding()`: Hata tespit ve düzeltme
- `injectSingleError()`: Tek bit hata enjeksiyonu
- `injectDoubleError()`: Çift bit hata enjeksiyonu

#### Global Değişkenler:
- `mevcutKod[]`: Aktif Hamming kodu
- `orijinalVeri`: Kullanıcı girişi
- `parityBitSayisi`: Hesaplanan parity sayısı

#### Durum Göstergeleri: 
  - 🟢 Yeşil: Hata yok
  - 🟡 Sarı: Tek hata (düzeltildi)
  - 🔴 Kırmızı: Çift hata (düzeltilemez)

## 🔍 Örnek Senaryolar

### Senaryo 1: Başarılı Kod Oluşturma
```
Giriş: 10101010
Çıkış: SEC-DED Hamming kodu başarıyla oluşturuldu
```

### Senaryo 2: Tek Hata Düzeltme
```
1. Kod oluştur :10101010
2. Hamming Kod Dönüştür: 1010010 1 1000
3. Tek hata ekle: örneğin Bit 5
4. Hatalı kod :1010010 0 1000
5. Tespit et : "Tek hata tespit edildi ve düzeltildi (Bit 5)"
6. Kod geri döner:1010010 1 1000 başarılı şekilde ilk koda geri dönülür
```

### Senaryo 3: Çift Hata Tespiti
```
1.Kod oluştur :10101010
2. Hamming Koda Dönüştür: 101001011000
3. Çift hata ekle: Bit 3 ve 7
4. Tespit et: "Çift hata tespit edildi - Düzeltilemez!"
```

## 🚨 Sınırlamalar

- Sadece 8, 16, 32 bit veri desteği
- Sadece binary (0,1) girişler kabul edilir
- Çift hatalar tespit edilir ancak düzeltilmez
- Üç veya daha fazla hata desteklenmez

## 👥 Geliştirici

- **E-posta**:koraygarip@gmail.com
- **GitHub**: [https://github.com/korayga]

