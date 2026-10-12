# Render üzerinde FinZekâ TR yayını

1. Bu klasördeki dosyaları bir GitHub deposuna yükleyin (main.py, requirements.txt, static/, render.yaml). .env ve API anahtarlarını yüklemeyin.
2. Render -> New -> Blueprint -> GitHub deposunu seçin -> Deploy.
3. Environment altında OPENAI_API_KEY değerini secret olarak ayarlayın. OPENAI_MODEL varsayılan gpt-4.1-mini.
4. Dağıtım bitince Render'ın verdiği https://...onrender.com adresini açın.
5. https://...onrender.com/api/health ile sunucu sağlığını kontrol edin. `openai_configured: true` API anahtarının tanımlandığını gösterir ama kredi/izin erişimini doğrulamaz.
6. İlk yüklemede yfinance erişim kısıtları veya veri boşluğu çıkabilir. FinZekâ BIST verileri gecikmeli günlük fiyat olarak etiketlenmiştir; gerçek zamanlı lisanslı veri değildir.

Notlar: Platformun ücretleri, ücretsiz hizmetin uyuma geçmesi ve limitleri değişebilir. Web sitesini herkese açık yayınlamak için veri lisansını, API kullanım maliyetini ve sorgu kötüye kullanımına karşı kimlik doğrulama/rate limiting gereksinimlerini değerlendirin.
