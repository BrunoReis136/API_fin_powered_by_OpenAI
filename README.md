# 📊 Financial Analysis Pipeline with LLM (OpenAI) + Finnhub

Este projeto demonstra um **pipeline profissional de análise financeira automatizada**, combinando:

* 📈 **Dados de mercado** (API Finnhub)
* 🤖 **Análise qualitativa com LLM** (OpenAI)
* 🧠 Tratamento de exceções, rate limits e segurança de credenciais
* 🧪 Execução via **Google Colab** ou ambiente local

O foco do projeto é **arquitetura, boas práticas, segurança e clareza analítica**, sendo adequado para **portfólio profissional em Data Science / Engenharia de Dados / IA aplicada a Finanças**.

---

## 🧩 Visão Geral da Arquitetura

```
[Finnhub API] ──▶ Payload Financeiro (JSON)
                       │
                       ▼
              Prompt Estruturado
                       │
                       ▼
               OpenAI Responses API
                       │
                       ▼
              Resumo Técnico Financeiro
```

O modelo **não inventa dados**: ele apenas interpreta e contextualiza o payload recebido.

---

## ⚙️ Funcionalidades Principais

* ✔ Coleta de dados financeiros estruturados
* ✔ Serialização segura do payload em JSON
* ✔ Prompt técnico e restritivo (anti-alucinação)
* ✔ Uso da API `responses` (padrão atual OpenAI)
* ✔ Tratamento de erros:

  * API Key ausente
  * Rate limit / quota
  * Erros de rede
* ✔ Código compatível com **Colab Secrets** e **variáveis de ambiente**

---

## 🔐 Segurança e Uso de API Keys

Este projeto **NÃO expõe credenciais**.

### 🔑 Como as chaves são tratadas

O código tenta obter a chave na seguinte ordem:

1. Variável de ambiente (`OPENAI_API_KEY`)
2. Google Colab Secrets (`userdata.get()`)

Se nenhuma estiver disponível, a execução é interrompida com erro explícito.

```python
if api_key is None:
    raise RuntimeError(
        "API key não encontrada. Defina OPENAI_API_KEY como variável de ambiente ou Colab Secret."
    )
```

📌 **As chaves nunca são hardcoded** e **não são visíveis** para terceiros.

---

## 🚀 Como Executar

### ▶️ Opção 1: Google Colab (Recomendado)

1. Abra o notebook no Colab
2. Clique em **Secrets** (ícone de chave 🔑)
3. Adicione:

   * `OPENAI_API_KEY`
   * `FINNHUB_API_KEY`
4. Execute as células normalmente

⚠️ Observação: Cada usuário executa o notebook em **ambiente isolado**. As chaves não são compartilhadas.

---

### ▶️ Opção 2: Execução Local

Defina as variáveis de ambiente antes de rodar:

```bash
export OPENAI_API_KEY="sua_chave"
export FINNHUB_API_KEY="sua_chave"
```

Depois execute o notebook ou script Python.

---

## 📉 Rate Limits e Quotas

O projeto inclui tratamento para erros do tipo:

* `RateLimitError (429)`
* `insufficient_quota`

Esses erros são **esperados** em APIs pagas e são tratados para:

* Não quebrar a aplicação
* Informar claramente a causa
* Permitir fallback ou nova tentativa

---

## 📌 Observação para Avaliadores

* Os **outputs finais** (análises, tabelas e resumos) podem estar salvos no notebook
* A execução das APIs **exige chaves próprias**, o que é padrão de mercado
* O valor do projeto está em:

  * Arquitetura
  * Clareza do código
  * Segurança
  * Qualidade da análise gerada

Nenhuma expectativa de execução automática com credenciais do autor.

---

## 🛠 Tecnologias Utilizadas

* Python 3.10+
* Google Colab
* OpenAI Python SDK (Responses API)
* Finnhub API
* JSON / Pandas

---

## 📚 Possíveis Extensões

* Cache de respostas (Redis / SQLite)
* Batch analysis de múltiplos ativos
* Agendamento automático (Airflow / Cron)
* Dashboard (Streamlit / Flask)
* Fine-tuning ou RAG com histórico financeiro

---

## 📄 Licença

Projeto disponibilizado para fins educacionais e de portfólio.

O uso das APIs está sujeito aos termos da OpenAI e Finnhub.

---

## 👤 Autor

**Bruno Henrique Reis**
Projeto desenvolvido como demonstração de pipeline profissional de análise financeira com IA.
