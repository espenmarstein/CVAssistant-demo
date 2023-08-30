# Bruke OpenAI sitt GPT API

Det finnes flere forskjellige APIer for å bruke OpenAI sine GPT-modeller, men hovedsakelig kan det være lurt å forholde seg til OpenAI sitt API og Azure OpenAI Service.

## OpenAI API

For å få tilgang til APIet til OpenAI må du registrere deg på [OpenAI](https://platform.openai.com/). Her får du en nøkkel du kan bruke, på formatet `sk-...`, som du må inkludere i alle forespørsler til APIet (bytt ut `$OPENAI_API_KEY`).

```bash
curl https://api.openai.com/v1/chat/completions \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer $OPENAI_API_KEY" \
  -d '{
    "model": "gpt-3.5-turbo",
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "Hello!"
      }
    ]
  }'
```

## Azure OpenAI Service

Selve kjerne-APIet er nesten det samme som OpenAI sitt API, men du må inkludere nøkkelen (`$AZURE_OPENAI_API_KEY`) i `api-key`-headeren, i stedet. Også må du flytte model-versjonen fra selve requst-bodyen til URLen (til det navnet du har gitt den i Azure). Det kan se slik ut:

```bash
curl https://{openai-instans}.openai.azure.com/openai/deployments/{deployment-name}/chat/completions?api-version=2023-08-01-preview \
  -H "Content-Type: application/json" \
  -H "api-key: $AZURE_OPENAI_API_KEY" \
  -d '{
    "messages": [
      {
        "role": "system",
        "content": "You are a helpful assistant."
      },
      {
        "role": "user",
        "content": "Hello!"
      }
    ]
  }'
```
