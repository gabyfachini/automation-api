# Plataforma de API de Automação (n8n)

Este projeto implementa uma API de automação usando n8n.

O objetivo é centralizar múltiplos serviços de utilidade em um único endpoint HTTP.

O cliente envia uma requisição contendo um campo `action`, e o fluxo de trabalho roteia a requisição para o serviço correspondente.

---

# Visão Geral

A API funciona como um roteador de serviços simples.

Cada requisição enviada ao endpoint principal contém um campo `action` que determina qual automação será executada.

Serviços disponíveis:

| Serviço | Descrição |

|--------|------------|

| gerador-de-senhas | Gera uma senha aleatória segura |

| dados-falso | Retorna dados aleatórios do usuário |

| citações-motivacionais | Retorna uma citação motivacional |

| validador-cpf | Valida o formato básico do CPF |

---

# Arquitetura do Fluxo de Trabalho

Fluxo principal do fluxo de trabalho:

Webhook
↓
API do Roteador (Nó Switch)
↓
Lógica do Serviço
↓
Responder ao Webhook

Cada serviço é implementado usando:

- Nó de Função para a lógica
- Resposta ao Webhook para a resposta da API

---
# Endpoint da API
POST /webhook/api

---

Exemplo de URL local:
http://localhost:5678/webhook/api

---

# Uso da API

Todas as requisições devem ser enviadas usando **POST** com JSON.

--- # Gerador de Senhas

Requisição:
```json
{

"action": "password-generator"
}
```

Resposta:
```json
{

"service": "password-generator",

"password": "A8#sF2kLmP9!"

}
```
---
# Dados Falsos

Requisição:
```json
{

"action": "fake-data"
}
```

Resposta:
```json
{
"service": "fake-data",

"nome": "Carlos",

"cidade": "Rio",

"idade": 34
}
```
---
# Citação Motivacional

Requisição:
```json
{

"action": "motivational-quotes"
}
```
Resposta:
```json
{

"service": "motivational-quotes",

"quote": "Feito é melhor que perfeito."

}
```
---
# Validador de CPF

Requisição:
```json
{
"action": "cpf-validator",

"cpf": "12345678900"
}
```
Resposta:
```json
{
"cpf": "12345678900",

"valido": true
}
```
Observação:
A validação atual verifica apenas o formato e o comprimento do CPF, não o algoritmo oficial brasileiro de validação de CPF.

---
# Tecnologias
- n8n
- JavaScript
- Webhooks HTTP
- Automação de Fluxo de Trabalho

---
# Executando o Projeto
- Abra o n8n
- Vá para Fluxos de Trabalho
- Clique em Importar
- Cole o JSON do fluxo de trabalho
- Ative o fluxo de trabalho
- Após a importação: Ative o fluxo de trabalho