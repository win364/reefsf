# Mines Predictor - Vercel Deployment

Этот проект представляет собой предсказатель для игры Mines, развернутый на Vercel.

## Проблема с подключением к серверу 8080

Если predictor не работает, нужно настроить переменную окружения в Vercel:

### 1. В настройках Vercel добавьте переменную окружения:

**Имя переменной:** `MINES_SERVER_URL`  
**Значение:** `http://localhost:8080` (или IP вашего сервера)

### 2. Если сервер 8080 не доступен из интернета:

Используйте туннель (ngrok, cloudflared) или публичный IP:

```
MINES_SERVER_URL=https://your-tunnel-url.ngrok.io
```

### 3. Альтернативное решение - изменить код:

В файле `api/mines-debug-state.js` измените строку:
```javascript
const upstreamUrl = process.env.MINES_SERVER_URL || 'http://localhost:8080';
```

На ваш реальный URL сервера.

## Структура проекта

```
public/
├── api/
│   ├── mines-debug-state.js      # API для получения состояния игры
│   └── predictor-snapshot.js     # API для получения snapshot
├── predictor.html                # Основной HTML файл
├── cellsFrame.40eb57f7e28f2ca52ad4.png
├── prod-rnd-frontend-php-orchestra.100hp.app/
│   └── static/
│       ├── css/
│       └── media/
├── vercel.json                   # Конфигурация Vercel
├── package.json                  # Зависимости
└── README.md                     # Этот файл
```

## Развертывание

1. Загрузите всю папку `public/` на Vercel
2. Настройте переменную окружения `MINES_SERVER_URL`
3. Убедитесь, что сервер 8080 доступен из интернета

## API Endpoints

- `GET /mines/debug/state` - Получение состояния игры
- `GET /predictor-snapshot` - Получение snapshot данных
- `GET /` - Основная страница predictor
