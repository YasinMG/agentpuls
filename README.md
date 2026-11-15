# AgentPulse – клик-демо платформы мониторинга KI-агентов

Статический сайт: один `index.html` + папка `fonts/`. Сервер, база данных и сборка не нужны.
Все данные примерные (симуляция). Реальных KI-агентов и внешних API-вызовов в демо нет.

```
agentpulse/
├── index.html                  ← вся платформа (HTML + CSS + JavaScript)
├── fonts/                      ← шрифты Inter и Space Grotesk (локально, без Google Fonts)
├── Dockerfile                  ← для своего сервера / VPS
├── docker-compose.yml
├── nginx.conf
├── staticwebapp.config.json    ← для Azure Static Web Apps
└── README.md
```

## 0. Посмотреть локально

Двойной клик по `index.html` — откроется в браузере.
Или через локальный сервер:

```bash
cd agentpulse
python3 -m http.server 8080
# открыть http://localhost:8080
```

---

## Вариант A — Netlify (самый быстрый, 2 минуты, бесплатно)

1. Зайти на https://app.netlify.com/drop
2. Перетащить **папку** `agentpulse` в окно браузера.
3. Готово — Netlify выдаст ссылку вида `https://…netlify.app`.
4. Свой домен: Site configuration → Domain management → Add domain
   (например `agentpulse.globalytics.org`) и у регистратора домена добавить CNAME-запись на адрес Netlify.

## Вариант B — Azure Static Web Apps (если клиенты в Microsoft-мире, регион Westeurope)

Через Azure CLI:

```bash
npm install -g @azure/static-web-apps-cli
az login
az group create --name rg-agentpulse --location westeurope
az staticwebapp create --name agentpulse --resource-group rg-agentpulse --location westeurope --sku Free
TOKEN=$(az staticwebapp secrets list --name agentpulse --query "properties.apiKey" -o tsv)
cd agentpulse
swa deploy . --deployment-token $TOKEN --env production
```

Свой домен: Azure Portal → Static Web App → Custom domains → Add → CNAME на `….azurestaticapps.net`.

## Вариант C — Свой сервер / VPS (например Hetzner, IONOS) через Docker

На сервере должен быть установлен Docker.

```bash
# папку скопировать на сервер
scp -r agentpulse user@SERVER-IP:/opt/

ssh user@SERVER-IP
cd /opt/agentpulse
docker compose up -d --build
# сайт работает на http://SERVER-IP:8080
```

HTTPS и домен — проще всего через Caddy (сертификат Let's Encrypt автоматически).
Файл `/etc/caddy/Caddyfile`:

```
agentpulse.globalytics.org {
    reverse_proxy localhost:8080
}
```

```bash
sudo systemctl reload caddy
```

DNS: у регистратора добавить A-запись `agentpulse` → IP сервера.

## Вариант D — GitHub Pages

```bash
cd agentpulse
git init && git add . && git commit -m "AgentPulse Demo"
git branch -M main
git remote add origin https://github.com/<USER>/agentpulse.git
git push -u origin main
```

GitHub → Settings → Pages → Source: `main` / root → Save.
Ссылка: `https://<USER>.github.io/agentpulse/`.
Внимание: на бесплатном тарифе репозиторий для Pages должен быть публичным.

## Вариант E — Обычный веб-хостинг (FTP)

Загрузить содержимое папки (`index.html` и `fonts/`) по FTP в каталог домена или поддомена
(например `/agentpulse/`). Остальные файлы (Docker, nginx) там не нужны.

---

## Обновить

Изменить `index.html` → заново загрузить (Netlify: перетащить папку ещё раз; Docker: `docker compose up -d --build`; Azure: `swa deploy` ещё раз).

## Перед публичным запуском в Германии

- **Impressum и Datenschutzerklärung** — ссылки нужны на любом публичном сайте.
- Шрифты уже подключены локально — сайт не обращается к Google Fonts.
- Демо не ставит cookies. В localStorage браузера сохраняются только две вещи: «тур просмотрен» и статусы подключений (без ключей).
- Не вводите в демо настоящие API-ключи: проверяется только формат, ничего никуда не отправляется.
