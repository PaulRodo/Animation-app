# Animation Studio

Веб-приложение для создания анимаций с ИИ. Работает на GitHub Pages + Cloudflare Worker.

## 🚀 Первоначальная настройка (делается ОДИН раз)

### 1. GitHub: размещение приложения
1. Создай публичный репозиторий `animation-studio` на github.com
2. Загрузи туда файл `index.html`
3. Settings → Pages → Source: `Deploy from a branch` → `main` → `/ (root)` → Save
4. Через 1-2 минуты сайт доступен по адресу `https://ТВОЙ-ЛОГИН.github.io/animation-studio/`

### 2. OpenRouter: бесплатный доступ к ИИ
1. Зарегистрируйся на https://openrouter.ai
2. Keys → Create Key → скопируй ключ (начинается на `sk-or-v1-...`)

### 3. Cloudflare Worker: наш "мост" к ИИ
1. Зарегистрируйся на https://dash.cloudflare.com
2. Workers & Pages → Create → Worker → имя `animation-ai-proxy` → Deploy
3. Открой редактор кода, удали дефолтный код, вставь код из файла `cloudflare-worker.js`
4. Deploy
5. Settings → Variables and Secrets → Add:
   - Name: `OPENROUTER_API_KEY`
   - Value: твой ключ из OpenRouter
   - Жми Encrypt → Save
6. (Опционально) Добавь переменную `MODEL` = `meta-llama/llama-3.3-70b-instruct:free` (или другую бесплатную модель)
7. Скопируй URL воркера вида `https://animation-ai-proxy.твой-аккаунт.workers.dev`

### 4. Связка
1. Открой `index.html` на GitHub → карандаш (Edit) → найди строку
   `const WORKER_URL = 'https://YOUR-WORKER.YOUR-SUBDOMAIN.workers.dev';`
2. Замени на свой URL → Commit changes

Готово! Открывай `https://ТВОЙ-ЛОГИН.github.io/animation-studio/` и пользуйся.

## 📤 Экспорт в DaVinci Resolve

### PNG-последовательность (рекомендую)
1. Жми "PNG-последовательность" в приложении → скачается ZIP
2. Распакуй ZIP в папку
3. В Resolve: File → Import → Media, выбери все PNG → откроется как видео с альфой
4. Кинь на дорожку V2 над основным видео

### WebM
1. Жми "WebM" → скачается `.webm`
2. Перетащи в медиатеку Resolve
3. Если фон чёрный (нет прозрачности) — используй PNG

## 💰 Стоимость
Полностью бесплатно:
- GitHub Pages: бесплатно для публичных репозиториев
- Cloudflare Workers: 100 000 запросов/день бесплатно
- OpenRouter free-модели: 20 запросов/минуту бесплатно

## 🔧 Если что-то не работает
- **"YOUR-WORKER" в коде** → ты не поменял URL воркера в index.html
- **"AI did not return JSON"** → модель тупит, попробуй другой MODEL (например `google/gemini-2.0-flash-exp:free`)
- **"OpenRouter 429"** → превышен лимит 20 запросов/мин, подожди минуту
- **Прозрачность не работает в WebM** → используй PNG-последовательность