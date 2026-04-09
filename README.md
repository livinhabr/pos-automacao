# TempBot Brasil (Telegram + n8n + OpenWeather)

Bot do Telegram criado no n8n que informa a temperatura atual e a condição climática de cidades do Brasil, em tempo real.

## Objetivo
- Receber mensagens via Telegram (tempo real)
- Normalizar a entrada do usuário (trim, remoção de acentos e limpeza de texto)
- Consultar clima atual na OpenWeather
- Retornar resposta com dados estruturados (cidade, temperatura arredondada, sensação térmica, condição e umidade)
- Disponibilizar comandos `/start` e `/ajuda`

## Arquitetura do workflow (n8n)
Fluxo principal:
1. Telegram Trigger
2. Normalize input (Code) — limpeza e extração da cidade
3. Switch — rotas para `/start`, `/ajuda` e consulta padrão
4. OpenWeatherMap — consulta de clima atual
5. IF (Weather OK?) — tratamento de sucesso/erro
6. Set (Build reply) — montagem do texto com campos exatos e arredondamento
7. Telegram Send Message — envio da resposta ao usuário

## Credenciais necessárias (não versionar tokens)
Este projeto utiliza credenciais configuradas no n8n. Não inclua tokens ou chaves no repositório.

### 1) Telegram
- `TELEGRAM_BOT_TOKEN` (gerado no BotFather)

Como configurar no n8n:
- Credentials → Telegram API
  - Access Token: `TELEGRAM_BOT_TOKEN`

### 2) OpenWeather
- `OPENWEATHER_API_KEY` (API key do OpenWeather / OpenWeatherMap)

Como configurar no n8n:
- Credentials → OpenWeatherMap API (ou equivalente)
  - API Key / Token: `OPENWEATHER_API_KEY`

Observação:
- O workflow consulta em unidades métricas e utiliza como entrada a cidade normalizada no formato `Cidade,BR` (ex.: `Belo Horizonte,BR`).

## Como executar
1. Crie um bot no Telegram via BotFather e obtenha o token.
2. Crie uma API key na OpenWeather.
3. No n8n:
   - Crie as credenciais Telegram API e OpenWeatherMap API
   - Importe o arquivo `bot-temperatura-telegram.json`
   - Selecione as credenciais nos nós correspondentes
4. Ative o workflow (Active = ON)
5. Envie mensagens para o bot no Telegram para testar.

## Como usar no Telegram
Comandos:
- `/start` — mensagem de boas-vindas e exemplos
- `/ajuda` — instruções de uso

Exemplos de consulta:
- `Belo Horizonte`
- `Uberaba, MG`
- `Qual o clima em Belo Horizonte agora?`
- `/tempo Contagem`

## Tratamento de erros
- Se a cidade não for encontrada ou houver falha na consulta, o bot retorna uma mensagem orientando o envio no formato `Cidade, UF` (ex.: `Uberaba, MG`).

## Arquivos
- `bot-temperatura-telegram.json` — workflow exportado do n8n
