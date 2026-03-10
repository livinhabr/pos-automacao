# Bot de Temperatura no Telegram com n8n

## Sobre o projeto
Este projeto foi desenvolvido para a avaliação da disciplina **Agentes e Automação** da pós-graduação.

A proposta consiste na criação de um chatbot no Telegram utilizando **n8n**, capaz de informar a **temperatura atual** e a **condição climática** de cidades do Brasil a partir da mensagem enviada pelo usuário.

## Como funciona
O fluxo foi construído no n8n e segue esta lógica:

1. O usuário envia uma mensagem no Telegram informando uma cidade
2. O **Telegram Trigger** recebe a mensagem
3. Um **AI Agent** interpreta o texto do usuário
4. O agente utiliza a ferramenta **Tavily Search** para consultar o clima atual da cidade informada
5. O resultado é processado com apoio do modelo **Google Gemini**
6. A resposta é enviada de volta ao usuário no Telegram

## Exemplo de uso
Usuário:
`Qual o clima em Belo Horizonte agora?`

Resposta esperada:
`A temperatura atual em Belo Horizonte é de aproximadamente 27°C com chuva ligeira.`

## Tecnologias utilizadas
- **n8n**
- **Telegram Bot**
- **Google Gemini**
- **Tavily Search API**

## Estrutura do workflow
O workflow contém os principais nós abaixo:

- **Telegram Trigger**: recebe as mensagens do usuário
- **AI Agent**: interpreta a solicitação e conduz a consulta
- **Google Gemini Chat Model**: apoia o processamento da resposta
- **Tavily Search**: busca a temperatura atual da cidade informada
- **Get a chat**: identifica o chat de destino
- **Send a text message**: envia a resposta final ao usuário

## Objetivo da automação
Automatizar o atendimento no Telegram para responder, de forma rápida e objetiva, consultas sobre temperatura e clima atual de cidades brasileiras.

## Como importar o projeto no n8n
1. Baixe o arquivo JSON deste repositório
2. Acesse sua instância do n8n
3. Clique em **Import workflow**
4. Selecione o arquivo JSON do projeto
5. Configure as credenciais necessárias
6. Ative o fluxo

## Credenciais necessárias
Para executar o projeto, é necessário configurar:

- credencial da API do Telegram
- credencial do Google Gemini
- credencial de autenticação da Tavily API

## Observações
Este repositório contém o workflow exportado em JSON para fins acadêmicos e demonstrativos.

Por segurança, tokens, chaves e demais credenciais sensíveis devem ser configurados localmente no n8n e **não devem ser expostos publicamente**.

## Autor
Projeto desenvolvido por **Lívia Bragança** para a avaliação da pós-graduação.
