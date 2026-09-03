# İkinci El Telefon İlan Analiz Sistemi

Bu proje, HTML formatında sunulan ikinci el telefon ilanlarını ayıklamak, Nesne Yönelimli Programlama (OOP) yapılarıyla modellemek, Pandas ile düzenleyip CSV formatında saklamak ve NumPy kütüphanesiyle temel pazar analizleri gerçekleştirmek amacıyla hazırlanmış bir Python çalışmasıdır.

---

## Proje Dosya Yapısı

```text
├── p7.py                 # İlanları çeken, işleyen ve analiz eden ana kod dosyası
├── telefon_ilanlari.csv  # Kodun ürettiği ve kaydedilen ilan veri seti
├── requirements.txt      # Projenin çalışması için gereken Python kütüphaneleri
├── .gitignore            # Git takibi dışında bırakılan geçici dosyalar
└── README.md             # Proje tanıtım ve kullanım dokümantasyonu
```

---

## Kodun İçeriği ve Kullanılan Yapılar

Proje geliştirilirken Python'ın temel ve orta düzey konseptleri uygulanmıştır:

1. **Nesne Yönelimli Programlama (OOP):**
   - `PhoneListing` sınıfı oluşturularak her telefon ilanının **model**, **fiyat**, **şehir** ve **durum** özellikleri tek bir çatı altında toplanmıştır.
   - `__str__` metodu tanımlanarak ilan nesnelerinin ekrana düzenli ve okunabilir şekilde yazdırılması sağlanmıştır.

2. **Özel Iterator Protokolü (`__iter__` ve `__next__`):**
   - `Koleksiyon` adında özel bir sınıf yazılmıştır. Bu sınıf sayesinde ilan listesi üzerinde Python'ın yerleşik döngü mantığıyla adım adım gezinebilen özel bir iterator yapısı kurulmuştur.

3. **Generator Fonksiyonu (`yield`):**
   - `bütce_araligi_üret` fonksiyonu ile belirli bir bütçe aralığı (örneğin 0 - 30.000 TL arası, 10.000 TL adımlarla) dinamik ve belleği yormayan `yield` yapısıyla üretilmiştir.

4. **HTML Parsing ve Veri Temizleme:**
   - HTML içeriği taranarak her ilanın `<div>` bloğu altındaki başlık (`<h2>`), fiyat, şehir ve durum etiketleri ayrıştırılmıştır.
   - Sayısal analiz yapılabilmesi için fiyat verisindeki "TL", nokta ve boşluk karakterleri temizlenerek tamsayıya (`int`) dönüştürülmüştür.

5. **Pandas ile Veri Seti Oluşturma:**
   - Ayıklanan ilanlar sözlük formatında toplanmış ve bir Pandas `DataFrame` yapısına aktarılmıştır.
   - Türkçe karakterlerin bozulmaması için `utf-8-sig` kodlaması kullanılarak `telefon_ilanlari.csv` dosyasına kaydedilmiştir.

6. **NumPy ile İstatistiksel Hesaplamalar:**
   - Temizlenen fiyatlar bir NumPy dizisine (`ndarray`) dönüştürülmüş ve şu analizler yapılmıştır:
     - **Ortalama Fiyat** (`np.mean`)
     - **En Düşük ve En Yüksek Fiyat** (`np.min`, `np.max`)
     - **Medyan (Ortanca Değer)** (`np.median`)
     - **Standart Sapma** (`np.std`)
     - 20.000 TL altı ve 30.000 TL üstü ilan sayımları (`np.sum`)

---

## Kullanılan Teknolojiler

- **Python 3**
- `beautifulsoup4`: HTML içeriğindeki etiketleri bulmak ve ayıklamak için.
- `pandas`: Toplanan verileri tabloya dönüştürüp CSV olarak kaydetmek için.
- `numpy`: Fiyat listesi üzerinde matematiksel ve istatistiksel hesaplamalar için.
- `html.parser`: Python'ın yerleşik HTML ayrıştırıcısı.

---

## Kurulum ve Çalıştırma

Projeyi yerel bilgisayarınızda çalıştırmak için:

1. **Gerekli kütüphaneleri yükleyin:**
   ```bash
   pip install -r requirements.txt
   ```

2. **Programı çalıştırın:**
   ```bash
   ikinci-el-telefon-analizi
   ```

Kod çalıştığında `telefon_ilanlari.csv` dosyası güncellenir ve terminal ekranında ilanların fiyat dağılımına ait analiz özeti listelenir.
