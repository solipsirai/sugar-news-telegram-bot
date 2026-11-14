# Global Sugar & Ethanol News Bot

[English](#english) · [Türkçe](#türkçe)

## English

A Python Telegram bot that monitors 50 multilingual public news feeds and search queries for sugar, sugarcane, and ethanol. It filters unrelated items, suppresses duplicate alerts, and links to the original sources. It also checks UNICA and CONAB pages on dates configured in `official_dates.json`. Edit `feeds.json` to customize coverage.

### Setup

1. Install Python 3.12. Open Terminal or PowerShell in the project directory.
2. Create a virtual environment with `python -m venv .venv`. Activate it with `source .venv/bin/activate` on macOS/Linux or `.\.venv\Scripts\Activate.ps1` in PowerShell. Install dependencies with `python -m pip install -r requirements.txt`.
3. Copy `.env.example` to `.env` in the same directory. Create a bot using Telegram’s BotFather and enter your own `TELEGRAM_BOT_TOKEN` in `.env`. Message your bot, run `python bot.py --get-chat-id`, then enter the destination `TELEGRAM_CHAT_ID` in `.env`.
4. Run `python bot.py --dry-run` for a preview. Run `python bot.py --test-telegram` to send one test alert to your configured chat.
5. Run `python bot.py` for continuous monitoring or `python bot.py --once` for a single scan. The first normal scan establishes a baseline and suppresses existing articles. For Docker, run `docker compose up -d --build` after configuring `.env`.

### Data handling

Keep credentials and chat identifiers in your local `.env` file. Telegram receives the chat identifier and alert text when alerts are enabled. `--get-chat-id` prints chat identifiers locally. Keep its output private. The deduplication state stores recent headline fingerprints and feed initialization flags.

Gemini is optional and disabled by default. When you supply a Gemini API key, the bot sends the public RSS title, short excerpt, source, and region to Google for English translation and a brief assessment. Use public feeds only. Leave `GEMINI_API_KEY` blank to use original headlines without AI. Keep logs, state files, and credentials out of commits.

## Türkçe

Şeker, şeker kamışı ve etanol haberlerini 50 adet çok dilli açık RSS akışı ve haber aramasıyla izleyen bir Python Telegram botu. İlgisiz ve tekrarlanan haberleri filtreler, bildirimlere özgün kaynak bağlantısını ekler. UNICA ve CONAB sayfalarını `official_dates.json` dosyasındaki tarihlerde kontrol eder. Kaynak listesini `feeds.json` içinden düzenleyebilirsiniz.

### Kurulum

1. Python 3.12’yi kurun. Proje klasöründe Terminal veya PowerShell açın.
2. `python -m venv .venv` komutuyla sanal ortam oluşturun. Mac/Linux’ta `source .venv/bin/activate`, PowerShell’de `.\.venv\Scripts\Activate.ps1` ile etkinleştirin. `python -m pip install -r requirements.txt` çalıştırın.
3. `.env.example` dosyasını aynı klasörde `.env` adıyla kopyalayın. Telegram’da BotFather ile kendi botunuzu oluşturun ve `TELEGRAM_BOT_TOKEN` alanını doldurun. Botunuza mesaj gönderip `python bot.py --get-chat-id` çalıştırın. Bildirim alacak sohbetin kimliğini `TELEGRAM_CHAT_ID` olarak girin.
4. `python bot.py --dry-run` ile önizleme yapın. `python bot.py --test-telegram` ayarladığınız sohbete bir deneme bildirimi gönderir.
5. Sürekli izleme için `python bot.py`, tek tarama için `python bot.py --once` kullanın. İlk normal tarama mevcut haberleri kayda alır ve eski haberleri bildirim olarak göndermez. Docker kullanıyorsanız `.env` ayarından sonra `docker compose up -d --build` çalıştırın.

### Veri kullanımı

Bot anahtarını ve sohbet kimliğini yerel `.env` dosyasında saklayın. Telegram, bildirim gönderilirken sohbet kimliğini ve mesajı alır. `--get-chat-id` çıktısı sohbet kimliklerini gösterir. Bu çıktıyı paylaşmayın. Tekrar kontrolü için yerelde kısa süreli başlık özetleri (hash) ve kaynak başlangıç durumu tutulur.

Gemini isteğe bağlıdır ve varsayılan olarak kapalıdır. Anahtar girilirse herkese açık RSS başlığı, kısa önizleme, kaynak ve bölge bilgisi İngilizce çeviri ve kısa değerlendirme için Google’a gönderilir. Yalnızca açık haber kaynaklarını kullanın. Yapay zekâ kullanmadan özgün başlıkları almak için `GEMINI_API_KEY` alanını boş bırakın. Günlükleri, durum dosyalarını ve anahtarları depoya eklemeyin.
