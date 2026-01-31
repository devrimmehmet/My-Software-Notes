# 🤖 Agent (Temsilci)

Temsilci, Google Antigravity'nin temel AI işlevselliğidir. Mevcut kodunuz üzerinde akıl yürütebilen, araçları (terminal, tarayıcı vb.) kullanabilen ve kullanıcıyla görevler/çıktılar aracılığıyla iletişim kuran çok adımlı bir sistemdir.

---

## 🧠 1. Modeller (Models)

Antigravity, farklı görevler için özelleşmiş bir model hiyerarşisi kullanır.

### Ana Akıl Yürütme Modelleri

Kullanıcılar, sohbet kutusunun altındaki seçim menüsünden şu modelleri seçebilir:

- **Gemini Serisi:** Gemini 3 Pro (High/Low), Gemini 3 Flash.
- **Claude Serisi:** Claude Sonnet 4.5, Claude Opus 4.5 (Thinking).
- **Diğer:** GPT-OSS.

> **Not:** Bir model seçimi bir konuşma turu boyunca "yapışkan" (sticky) kalır. Tur devam ederken model değiştirirseniz, değişiklik bir sonraki kullanıcı mesajında aktif olur.

### Yardımcı Modeller (Özelleştirilemez)

- **Nano Banana Pro:** UI maketleri, mimari diyagramlar ve görseller oluşturmak için kullanılır.
- **Gemini 2.5 Pro UI Checkpoint:** Tarayıcıyı kontrol etmek (tıklama, kaydırma) için kullanılır.
- **Gemini 2.5 Flash:** Bağlam özetleme ve kontrol noktaları oluşturmak için arka planda çalışır.

---

## ⚙️ 2. Temsilci Modları ve Ayarları

Yeni bir sohbet başlatırken iki ana moddan birini seçebilirsiniz:

1. **Planning (Planlama) Modu:** Karmaşık görevler ve derin araştırma içindir. Temsilci önce plan yapar, görev grupları oluşturur ve çıktıları (artifacts) hazırlar.
2. **Fast (Hızlı) Mod:** Değişken adı değiştirme veya basit terminal komutları gibi hızlı, yerel görevler içindir. Planlama aşamasını atlar.

### Kritik Politikalar

- **Artifact Review Policy:** Temsilcinin planlarını uygulamadan önce onay isteyip istemeyeceğini belirler (_Always Proceed_ veya _Request Review_).
- **Terminal Command Auto Execution:** Terminal komutlarının otomatik çalıştırılma izni (İzin verilen/yasaklanan komut listeleri ile yapılandırılabilir).

---

## 📜 3. Rules (Kurallar) ve Workflows (İş Akışları)

### 📂 Proje Dizin Yapısı ve .agent Klasörü 🏗️

Antigravity'nin projenizi tam kapasiteyle anlayabilmesi için kök dizinde şu hiyerarşiyi kullanmanız önerilir:

```text
proje-kok-dizini/
├── .agent/                # Antigravity yapılandırma merkezi
│   ├── rules/             # Projeye özel kurallar (.md)
│   ├── skills/            # Özelleşmiş yetenek paketleri
│   │   └── yetenek-adi/
│   │       └── SKILL.md
│   └── workflows/         # Tekrarlanan iş akışları (.md)
├── .gitignore             # Agent'ın erişmemesi gereken yerler
└── ~/.gemini/             # Global ayarlar ve kurallar
```

### Kurallar (Rules)

Temsilcinin kod yazarken, dosya oluştururken veya terminal kullanırken uyması gereken manuel kısıtlamalardır. Temsilciye "nasıl" davranması gerektiğini dikte eder.

**Global Kurallar:** `~/.gemini/GEMINI.md` konumundadır. Tüm projelerinizde (örn: "Her zaman Türkçe yorum satırı kullan") geçerli olur.

**Workspace (Çalışma Alanı) Kuralları:** `.agent/rules/` klasöründedir. Sadece o projeye özeldir (örn: "Bu projede sadece Tailwind CSS kullan").

#### Aktivasyon Yöntemleri

- **Always On:** Kural her zaman devrededir.
- **Manual:** `@kural-adi` şeklinde sizin tarafınızdan çağrılır.
- **Glob:** Belirli dosya türlerinde (örn: `*.ts`) otomatik tetiklenir.
- **Model Decision:** Temsilci, kuralın içeriğine bakarak gerek duyduğunda kendisi uygular.

---

### İş Akışları (Workflows) 🔄

Tekrarlanan, çok adımlı görevleri otomatize eden adım dizileridir. Temsilciye bir süreci (trajectory) nasıl yöneteceğini öğretir.

- **Kullanım:** Sohbet ekranına `/iş-akışı-adı` yazarak tetiklenir.
- **Örnek:** `/hazirlik` komutuyla temsilciye;
  1. Testleri çalıştır
  2. Hata yoksa build al
  3. Değişiklikleri raporla

- **Otomatik Oluşturma:** Temsilciden, yapmış olduğunuz uzun bir sohbet geçmişine bakarak bunu bir `/workflow` dosyasına dönüştürmesini isteyebilirsiniz.

---

## 🛠️ 4. Yetenekler (Skills) 🧠

Yetenekler, temsilciye yeni fonksiyonel kabiliyetler kazandıran paketlerdir. Kurallardan farkı, içinde temsilcinin çalıştırabileceği yardımcı betikler (scripts) ve şablonlar barındırabilmesidir.

### Yapı

Her yetenek bir klasördür ve içinde mutlaka bir `SKILL.md` bulunmalıdır.

### SKILL.md Anatomisi

```text
---
name: yetenek-adi
description: Bu yetenek X işlemini yapmak için kullanılır. (Temsilci burayı okuyarak karar verir)

# Yetenek Talimatları

Burada temsilciye bu yeteneği nasıl kullanacağı detaylıca anlatılır.
```

- **Global Kurallar:** `~/.gemini/GEMINI.md` konumunda bulunur ve tüm projelerde geçerlidir.
- **Workspace Kurallar:** Proje kök dizinindeki `.agent/rules` klasöründe bulunur.
- **Aktivasyon:** Kurallar; her zaman açık, manuel (`@mention`), model kararı veya dosya uzantısına göre (Glob) tetiklenebilir.

---

## 🏗️ 5. Görev Grupları ve Tarayıcı Temsilcisi

- **Task Groups (Görev Grupları):** Karmaşık görevleri küçük birimlere böler. Her birimin ilerlemesini ve etkilenen dosyaları panelden takip edebilirsiniz.
- **Browser Subagent:** Tarayıcı ile etkileşime girerken devreye giren özel bir alt temsilcidir. Sizden bağımsız olarak sekmelerde işlem yapabilir (DOM okuma, tıklama vb.). Bu sırada sayfa üzerinde mavi bir çerçeve belirir.

---

## 🛡️ 6. Güvenlik: Secure Mode ve Sandboxing

- **Secure Mode:** Temsilcinin dış dünyaya erişimini kısıtlar. Terminal ve tarayıcı işlemleri için her zaman onay ister. `.gitignore` kurallarına sıkı sıkıya uyar.
- **Sandboxing:** Terminal komutlarını kernel düzeyinde izole eder. Temsilcinin çalışma alanı dışındaki dosyalara zarar vermesini engeller (Şu an macOS'te Seatbelt ile çalışır).

---

[⬅️ Ana Menüye Dön](../README.md)
