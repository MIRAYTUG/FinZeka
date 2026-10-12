# FinZekâ — Türkiye Finansal Analiz Terminali

BIST günlük fiyatları, interaktif Plotly mum grafiği, MA20/MA50, RSI, MACD, TCMB döviz kuru API'si ve OpenAI araç çağırma destekli Türkçe sohbet içeren profesyonel web prototipi.

## Kurulum (yerel bilgisayarda)
```bash
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\\Scripts\\activate
pip install -r requirements.txt
cp .env.example .env      # Windows: copy .env.example .env
```
`.env` dosyasına kendi `OPENAI_API_KEY` değerini gir. GitHub'a yükleme.

```bash
uvicorn main:app --host 127.0.0.1 --port 8000 --reload
```
Tarayıcıda http://127.0.0.1:8000 aç.

## Google Colab üzerinden deneme
Notebook yüklemeye gerek kalmadan ZIP'i Colab'a yükleyip:
```python
!unzip -qo FinZekâ_AI_TR_Profesyonel_Web.zip
%cd FinZeka_Web
!pip -q install -r requirements.txt
from getpass import getpass
import os
os.environ['OPENAI_API_KEY'] = getpass('OpenAI API anahtarı: ')
```
Ardından Colab hücresinde sunucuyu başlat:
```python
import subprocess
server = subprocess.Popen(['uvicorn','main:app','--host','0.0.0.0','--port','8000'])
print('Sunucu başlatıldı')
```
Colab'da web arayüzünü görüntülemek için:
```python
from google.colab import output
output.serve_kernel_port_as_window(8000)
```
Not: Colab oturumu kapanınca demo da kapanır. Kalıcı yayın için HTTPS, auth, rate limiting, harcama limitleri, logların hassas verilerden arındırılması ve BIST lisansı gereklidir.

## Veri politikası
- Yahoo Finance / yfinance: BIST için günlük son erişilebilir OHLC; **gerçek zamanlı değildir**, ticari kullanım ve erişilebilirlik garantisi yoktur.
- TCMB: yayımlanan döviz gösterge kurları; canlı piyasa fiyatı değildir.
- TradingView: ayrı pencerede ilgili hisse grafiğini açma; scraping veya veri dışa aktarma yoktur.
- OpenAI: yalnızca sunucudan çağrılır; API anahtarı tarayıcıya gönderilmez. Her kullanıcı sorgusu ücretli olabilir.
- LLM sonuçları yanlış olabilir. Bilançolar/KAP/haberler bu sürümün veri kaynaklarına henüz dahil edilmedi.

## API uç noktaları
- `GET /api/health`
- `GET /api/symbols`
- `GET /api/stock/THYAO?period=3mo`
- `GET /api/fx`
- `POST /api/ask` JSON `{ "question": "ASELS RSI nedir?", "symbol": "ASELS" }`

## Yayına geçiş
BIST lisanslı veri sağlayıcısını `market_data` fonksiyonuna adapter olarak bağla. Veri kaynağı, as-of zamanı, gecikme durumu ve piyasa kapsamını koru. UI güncel veri kaynağını dinamik gösterir.


## TradingView entegrasyonu
Resmî Advanced Chart Widget `static/index.html` içine eklendi. Hisse kodu değişince `BIST:THYAO` gibi sembolle grafik yeniden yüklenir. Widget fiyat verileri sunucunun API uçlarına iletilmez ve LLM tarafından doğrudan okunmaz. Grafik TradingView ağ erişimi gerektirir; veri lisansı/gecikme widget tarafından belirlenir.
