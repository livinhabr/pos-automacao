# TempBot Brasil (Telegram + n8n + OpenWeather)

Bot do Telegram criado no n8n que informa a **temperatura atual** e a **condição climática** de qualquer cidade do Brasil, em tempo real.

## ✅ O que este projeto faz
- Recebe mensagens pelo Telegram (gatilho em tempo real)
- Normaliza o texto do usuário (trim, remoção de acentos, remoção de palavras “qual o clima em…”, etc.)
- Consulta o clima atual na OpenWeather
- Retorna uma mensagem amigável com:
  - cidade
  - temperatura arredondada
  - sensação térmica
  - condição
  - umidade
- Possui comandos `/start` e `/ajuda`

## 🧱 Arquitetura do workflow (n8n)
Fluxo principal:
1. **Telegram Trigger**
2. **Normalize input (Code)** — limpa e extrai a cidade
3. **Switch** — trata `/start` e `/ajuda`
4. **OpenWeatherMap** — busca o clima atual (métrico)
5. **IF (Weather OK?)** — separa sucesso/erro
6. **Set (Build reply)** — monta texto final com campos exatos
7. **Telegram Send Message** — envia a resposta

## 🔐 Credenciais necessárias (não coloque tokens no repositório)
Este projeto usa credenciais configuradas **no n8n** (nada de tokens no JSON/README).

### 1) Telegram
- **TELEGRAM_BOT_TOKEN** (gerado no BotFather)

**Como configurar no n8n**
- `Credentials` → **Telegram API**
  - Campo **Access Token**: `TELEGRAM_BOT_TOKEN`

### 2) OpenWeather
- **OPENWEATHER_API_KEY** (API key da OpenWeather / OpenWeatherMap)

**Como configurar no n8n**
- `Credentials` → **OpenWeatherMap API** (ou similar)
  - Campo **Access Token / API Key**: `OPENWEATHER_API_KEY`

> No workflow, o node OpenWeather está configurado em **Metric** e o input da cidade vem do campo normalizado `owmCity` (ex.: `Belo Horizonte,BR`).

## 🚀 Como rodar
1. Crie um bot no Telegram via **BotFather** e copie o token.
2. Crie uma API key na **OpenWeather**.
3. No n8n:
   - Crie as credenciais **Telegram API** e **OpenWeatherMap API**
   - Importe o workflow `bot-temperatura-telegram.json`
   - Abra o workflow e selecione as credenciais nos nós correspondentes
4. Ative o workflow (Active = ON)
5. No Telegram, abra o bot e teste.

## 💬 Como usar no Telegram
- `/start` → boas-vindas e exemplos
- `/ajuda` → instruções rápidas
- Envie uma cidade:
  - `Belo Horizonte`
  - `Uberaba, MG`
  - `Qual o clima em Belo Horizonte agora?`
  - `/tempo Contagem`

## 🧯 Tratamento de erros
- Se a cidade não for encontrada ou a API retornar erro, o bot responde:
  - “Não encontrei essa cidade 😕 Tenta no formato: Cidade, UF (ex.: Uberaba, MG).”

## 📦 Arquivos
- `bot-temperatura-telegram.json` — workflow exportado do n8n
