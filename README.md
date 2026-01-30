# 📊 Financial Analysis Pipeline with LLM (OpenAI) + Finnhub


[![Open in Colab](https://img.shields.io/badge/Open%20in%20Colab-Finance-green?style=for-the-badge&logo=googlecolab&logoColor=white)](https://colab.research.google.com/github/BrunoReis136/API_fin_powered_by_OpenAI/blob/main/projeto_fin_gpt.ipynb)




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


🧠 Exemplo de Saída Gerada pelo Pipeline

Abaixo está um exemplo real de análise produzida pelo pipeline, a partir de dados estruturados (JSON) e interpretados pelo LLM sem invenção de informações:

<details> <summary><strong>📄 Exemplo – Análise Financeira (AAPL)</strong></summary> <br>

> ## 📊 Análise Financeira – Apple Inc. (AAPL)
> *Baseada exclusivamente no payload fornecido*
>
> ---
>
> ### 🔹 1. Preço e comportamento recente
>
> - **Último fechamento:** **258,28**
> - **Retorno em 21 dias:** **-5,65%**
> - **Volatilidade (21 dias):** **1,23%**
>
> **Leitura técnica:**  
> Apesar da **baixa volatilidade recente**, o ativo apresentou **queda relevante no curto prazo**, indicando um movimento de **correção ou realização de lucros**, sem sinais de estresse elevado no preço.  
> A combinação de retorno negativo com volatilidade contida sugere **pressão vendedora gradual**, não pânico.
>
> ---
>
> ### 🔹 2. Resultados (Earnings) – Qualidade do lucro
>
> **Histórico recente de EPS (últimos 4 trimestres):**
>
> | Período              | EPS Real | Estimativa | Surpresa | Surpresa % |
> | -------------------- | -------- | ---------- | -------- | ---------- |
> | 2025-12-31 (Q1/2026) | 2,84     | 2,73       | **+0,11** | **+4,19%** |
> | 2025-09-30 (Q4/2025) | 1,85     | 1,81       | **+0,04** | +2,35%     |
> | 2025-06-30 (Q3/2025) | 1,57     | 1,46       | **+0,11** | **+7,34%** |
> | 2025-03-31 (Q2/2025) | 1,65     | 1,66       | -0,01    | -0,58%     |
>
> **Leitura fundamentalista:**
>
> - **3 de 4 trimestres com surpresa positiva**, sendo **duas acima de 4%**, indicando **boa execução operacional**
> - O único trimestre negativo foi **marginal**, sem impacto material
> - Há **consistência na superação de expectativas**, especialmente nos períodos mais recentes
>
> ---
>
> ### 🔹 3. Tendências observáveis
>
> **📈 Fundamental:**  
> Tendência **positiva na previsibilidade e entrega de resultados**, com EPS acima do consenso na maior parte do período.
>
> **💲 Preço:**  
> **Desalinhamento de curto prazo** entre fundamentos (bons resultados) e preço (retorno negativo em 21 dias).
>
> **⚠️ Risco implícito:**  
> O mercado pode estar **antecipando desaceleração futura**, ajustando múltiplos, ou reagindo a fatores externos não refletidos no payload (ex.: macroeconomia, valuation).
>
> ---
>
> ### 🔹 4. Principais riscos identificáveis (com base nos dados)
>
> - **Risco de curto prazo:**  
>   Continuidade da correção caso o preço siga pressionado mesmo com resultados sólidos.
>
> - **Risco de valuation implícito:**  
>   A queda recente após sucessivas surpresas positivas pode indicar **expectativas já muito elevadas**, reduzindo o espaço para novas reprecificações positivas.
>
> - **Risco de assimetria:**  
>   Com volatilidade baixa, movimentos futuros podem ser **mais abruptos** caso haja mudança de narrativa.
>
> ---
>
> ### 🔹 5. Conclusão técnica
>
> - **Fundamentos recentes:**  
>   **Sólidos e consistentes**, com recorrentes surpresas positivas de lucro.
>
> - **Preço no curto prazo:**  
>   **Em correção**, sem aumento relevante de volatilidade.
>
> - **Contexto geral:**  
>   O ativo apresenta **qualidade operacional**, porém enfrenta **pressão de mercado no curto prazo**, sugerindo um momento de **ajuste**, e não de deterioração fundamental.
>
> ---
>
> ### 🧾 Resumo
>
> > **AAPL demonstra boa execução financeira**, mas o mercado parece estar **reprecificando expectativas**, criando um **descompasso temporário entre preço e fundamentos**.
>
> *Análise gerada automaticamente a partir de payload estruturado.  
> Não constitui recomendação de investimento.*


---
</details>


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
