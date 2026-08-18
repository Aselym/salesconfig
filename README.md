# salesconfig

Lisans yenileme ve satış takip uygulaması. Logo ERP'den (MS SQL Server)
lisans satışlarını, aboneliklerini ve genel ürün satışlarını çeker; süresi
dolmak üzere olan lisanslar için muhasebe/satış ekibine e-posta ve Windows
masaüstü bildirimi gönderir. Yönetici Paneli'nde gelir trendi, marka/temsilci
performansı ve otomatik üretilen tavsiyeleri gösteren bir özet ekranı vardır.

## Kullanılan araçlar / stack

**Backend**
- Python 3 — framework yok, stdlib `http.server` (`ThreadingHTTPServer`) ile elle route eşleme
- SQLite — uygulamanın kendi verisi (satış/abonelik/teklif/hatırlatma geçmişi)
- `pyodbc` + MS SQL Server — Logo ERP'ye salt-okunur bağlantı (lisans/fatura verisi)
- `smtplib` — SMTP üzerinden hatırlatma e-postaları
- PowerShell (toast bildirimi) — Windows masaüstü bildirimleri

**Frontend**
- React 19 + TypeScript
- Vite 8 (build aracı)
- Tailwind CSS v4
- Framer Motion (geçiş/animasyon)
- lucide-react (ikonlar)

## Çalıştırma

```bash
pip install -r requirements.txt
python app.py
```

Uygulama `http://localhost:5000` adresinde ayağa kalkar (Python sunucusu
hem API'yi hem `frontend/` klasörünün derlenmiş halini `static/` altından
sunar). Frontend'i yeniden derlemek için:

```bash
cd frontend
npm install
npm run build   # ../static altına derler
```

Geliştirme sırasında frontend'i ayrı çalıştırmak için `npm run dev`
(Vite, :5173) kullanılabilir.

## Ortam / kurulum notları

- Logo ERP bağlantı bilgileri (SQL sunucu/kullanıcı/şifre, firma/dönem no)
  ve SMTP ayarları uygulama içinden **Ayarlar** ekranından girilir —
  kod içinde hiçbir kimlik bilgisi tutulmaz.
- `license_reminders.db` (SQLite) ve `backups/` klasörü `.gitignore`'da;
  repoya dahil edilmez.
- Sürekli açık kalacak bir makineye kurulum ve LAN'dan erişime açma için
  `DEPLOY.md`'ye bakın.
