# 🏠 Home (Ana Sayfa)

Google Antigravity, IDE deneyimini "temsilci öncelikli" (agent-first) bir çağa taşıyan, temsilci tabanlı bir geliştirme platformudur. Geliştiricilerin alışık olduğu AI IDE deneyimini korurken, birden fazla temsilciyi farklı çalışma alanlarında (workspaces) yönetmenize olanak tanır.

Antigravity; editör, terminal ve tarayıcı üzerinde otonom olarak çalışabilen temsilciler aracılığıyla karmaşık yazılım görevlerini (özellik geliştirme, UI iterasyonu, hata ayıklama, raporlama vb.) uçtan uca planlayıp yürütür.

---

## ✨ Ana Özellikler

- **Yapay Zeka Güçlü IDE:** Geliştiricilerin ihtiyaç duyduğu Agent, Tab ve Command gibi AI özelliklerini barındırır.
- **Asenkron Temsilciler:** Tüm çalışma alanlarınızda paralel olarak çalışabilen yerel temsilciler.
- **Agent Manager (Temsilci Yöneticisi):** Planlama modu, sohbet arayüzü ve çıktı (artifact) incelemesi için tasarlanmış özel görünüm.
- **Çoklu Pencere Deneyimi:** Editör, Yönetici ve Tarayıcı pencerelerinden oluşan entegre bir yapı.
- **Tarayıcı Temsilcisi:** UI testi, dashboard okuma ve SCM işlemleri gibi görevleri tarayıcı üzerinden gerçekleştirebilir.

---

## 🖼️ Temel Yüzeyler (Core Surfaces)

1.  **Editor (Editör):** Tek bir çalışma alanına odaklanan, tam işlevli AI destekli IDE.
2.  **Browser (Tarayıcı):** (Önizleme aşamasında) IDE dışındaki yüzeylerde işlem yapabilen temsilci kabiliyetleri.
3.  **Agent Manager (Temsilci Yöneticisi):** (Önizleme aşamasında) Görevleri başlatmak ve izlemek için tasarlanmış "kodsuz" orkestrasyon görünümü.

---

## 📝 Anahtar Terimler

- **Agent (Temsilci):** Antigravity'deki temel AI birimidir. Hem editör içinde sıkı bir iş birliği yapabilir hem de Agent Manager üzerinden birden fazla kod tabanında izlenebilir.
- **Tab & Command:** Editör içindeki AI modlarıdır. **Tab** güçlü bir "otomatik tamamlama", **Command** ise satır içi talimat verme özelliğidir.
- **Artifacts (Çıktılar):** Temsilcinin işini yapmak veya kullanıcıya bilgi vermek için oluşturduğu her şeydir (Markdown dosyaları, diff görünümleri, mimari diyagramlar, ekran kayıtları vb.).

---

## 🚦 Navigasyon ve Başlangıç

- **Geçiş Yapma:** Agent Manager'ı açmak için Editör üzerindeki üst bar butonunu veya `Cmd + E` kısayolunu kullanabilirsiniz.
- **Odaklanma:** Agent Manager üzerinden belirli bir çalışma alanına "Focus Editor" diyerek hızlıca geçiş yapabilirsiniz.

---

[⬅️ Ana Menüye Dön](../README.md)
