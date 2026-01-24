# 1EGIT Gaming – Team Creator

## Kullanıcı Kılavuzu

## 1. Genel Amaç

Bu site, Counter-Strike 2 oyuncuları için rank (seviye) bazlı dengeli takım oluşturma amacıyla hazırlanmış, tarayıcıdan çalışan bir 'Team Creator' uygulamasıdır.

Temel olarak amaç:

* Oyuncu ekleme (isim + CS2 rank)
* Yedek (Bench) oyuncu yönetimi
* Oyuncu rank’larını ikonlu şekilde düzenleme
* Otomatik ve dengeli takım oluşturma
* Takımlar içinde manuel oyuncu takası
* Sonuçları tek tıkla kopyalama
* Firebase varsa **canlı senkron**, yoksa **localStorage** ile çalışma

---

## 2. Arayüz Genel Yapısı

Sayfa iki ana bölümden oluşur:

### Sol Ana Alan (Main Container)

* Oyuncu ekleme
* Aktif oyuncu listesi
* Takım ayarları
* Takım oluşturma ve sonuçlar

### Sağ Panel – Bench (Yedek Oyuncular)

* Aktif olmayan oyuncular
* Toplu ekleme
* Rank düzenleme
* Seçili oyuncuları aktif listeye alma

Mobil görünümde bu panel üst tarafa taşınır.

---

## 3. Üst Bilgi Alanı

Sağ üst köşede:

* **Server IP:** `95.173.175.173`
* **Password:** `3113`

Bu alan tamamen bilgilendirme amaçlıdır. Uygulamanın çalışmasını etkilemez.

---

## 4. Oyuncu Ekleme (Add New Player)

### Alanlar

1. **Name**

   * Oyuncunun adı
   * Boş bırakılamaz
   * Aynı isimle ikinci kez eklenemez

2. **CS2 Rank**

   * Rank ikonuyla birlikte dropdown
   * Varsayılan: **Gold Nova III (Rank 9)**
   * Rank değiştikçe ikon otomatik güncellenir

3. **+ Add**

   * Oyuncuyu aktif listeye ekler

> Enter tuşu ile de ekleme yapılabilir.

---

## 5. Active Players (Aktif Oyuncular)

### Liste Özellikleri

* Oyuncular **rank’a göre yüksekten düşüğe** sıralanır
* Her oyuncu kartında:

  * Oyuncu adı
  * Rank ikonu
  * Rank değiştirme dropdown’u
  * Silme (✕) butonu

### Rank Değiştirme

* Oyuncu kartındaki küçük dropdown’a tıklanır
* Açılan menüde:

  * Tüm rank’lar
  * Her rank’ın **ikonu + kısa adı + tam adı**
* Seçim anında güncellenir

### Oyuncu Silme

* ✕ ikonuna basılır
* Onay istenir
* Oyuncu aktif listeden kaldırılır

---

## 6. Bench (Yedek Oyuncular)

Bench paneli, aktif oyuna girmeyen oyuncular içindir.

### Bench’e Oyuncu Ekleme

* Sağ panelde isim girilir
* `+` butonuna basılır
* Varsayılan rank: Gold Nova III

### Bench Listesi

Her bench oyuncusunda:

* Checkbox (seçim için)
* Rank ikonu
* Oyuncu adı
* Rank dropdown
* Silme butonu

### Bench’ten Aktif Listeye Alma

1. Checkbox ile oyuncular seçilir
2. **Add Selected** butonuna basılır
3. Seçilen oyuncular aktif listeye eklenir
4. Aktif olan bench oyuncuları checkbox’ta pasif görünür

### Select All

* Tüm uygun bench oyuncularını seçer / seçimi kaldırır

---

## 7. Takım Ayarları

### Number of Teams

* Oluşturulacak takım sayısı
* Minimum: 2
* Maksimum: aktif oyuncu sayısı

### Players per Team

* 0 → otomatik dağıtım
* > 0 → sabit oyuncu sayısı
* Yetersiz oyuncu varsa hata verir

---

## 8. Balanced Team Oluşturma

### 🎲 Create Balanced Teams

Bu buton:

* Oyuncuları rank gücüne göre sıralar
* Takımlara **zig-zag** mantığıyla dağıtır
* Ortalama rank’ları dengede tutmaya çalışır
* Butona her basışta hafif randomizasyon yapar

### Oluşan Takımlar

Her takımda:

* Takım adı (T / CT)
* Oyuncu sayısı
* Ortalama rank (Avg)
* Oyuncu listesi:

  * Sıra numarası
  * Rank ikonu
  * Oyuncu adı
  * Rank kısa adı

---

## 9. Manuel Oyuncu Takası (Swap)

1. Takımdaki bir oyuncuya tıkla → seçilir
2. Başka bir oyuncuya tıkla → yer değiştirir
3. Takım güçleri otomatik güncellenir

Bu özellik, otomatik dağıtımdan sonra ince ayar yapmak içindir.

---

## 10. Sonuçları Kopyalama

### 📋 Copy Results

* Takımları metin formatında panoya kopyalar
* Discord / WhatsApp / Steam chat için uygundur
* Kopyalama sonrası buton geçici olarak “Copied!” olur

---

## 11. Veri Saklama ve Senkronizasyon

### Firebase Aktifse

* Oyuncular ve bench **canlı senkron**
* Birden fazla kullanıcı aynı anda görebilir

### Firebase Yoksa

* Tarayıcı **localStorage** kullanılır
* Sayfa yenilense bile veriler kalır

Kod otomatik olarak durumu algılar.

---

## 12. Kimler İçin Uygun?

* CS2 lobby kuran arkadaş grupları
* Community / Discord sunucuları
* PUG (Pick-up game) organizasyonları
* Streamer / turnuva öncesi hızlı takım bölme

---

## Kısa Özet

* Kurulum gerektirmeden çalışır
* Rank ikonlarını aktif kullanır
* Dengeli takım üretir
* Manuel kontrol imkânı verir
* Tek dosya ile hem online hem offline çalışır
