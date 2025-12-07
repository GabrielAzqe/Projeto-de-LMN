# 🌍 Agente de Viagens Inteligente 
### *Projeto  em PLN (UFABC – 2025.Q3)*  

<p align="center">
  <img src="https://img.icons8.com/external-flaticons-lineal-color-flat-icons/344/external-travel-vacation-planning-flaticons-lineal-color-flat-icons.png" width="140"/>
</p>

---

## ✨ Visão Geral

Este projeto implementa um **agente inteligente de viagens**, combinando:

- **LLMs (Google Gemini via LangChain)** :LLMs (Google Gemini via LangChain) são modelos avançados de linguagem que, integrados ao LangChain, conseguem entender pedidos, raciocinar passo a passo e usar ferramentas externas para entregar respostas completas e inteligentes.

  
- **Consultas reais através da SerpAPI**: A SerpAPI é um serviço que permite fazer buscas reais no Google via API, retornando resultados estruturados para serem usados por modelos e pipelines como os do LangChain.


- **Orquestração completa para gerar roteiros detalhados** :coordenar todas as etapas, ferramentas e modelos de IA para gerar roteiros detalhados de forma automática, estruturada e coerente de ponta a ponta.

O agente produz:

✔️ Datas ideais  
✔️ Voos reais  
✔️ Hotéis  
✔️ Atrações personalizadas  
✔️ Informações de câmbio  
✔️ Contexto histórico do destino  
✔️ Roteiro final completo baseado em dados reais  

---

# 🧠 Arquitetura (LangChain + SerpAPI)

<p align="center">
  <img src="https://iacomcafe.com.br/wp-content/uploads/2024/08/1_q1CkGPwS7g4-f9rNbPrkig.png" width="85%"/>
</p>




---

## 1️⃣ Planejamento via LLM (LangChain)

O modelo **Gemini 2.5 Flash** é utilizado para gerar:

- Datas ideais de ida e volta  
- Duração adequada da viagem  
- Interesses turísticos personalizados  
- Seleção de temporadas favoráveis  

Função: **`gerar_dados_viagem()`**

---

## 2️⃣ Identificação de Aeroportos com LLM

O LLM identifica o **código IATA** do principal aeroporto de cada cidade.

Função: **`descobrir_aeroporto()`**

---

## 3️⃣ Busca de Dados Reais (SerpAPI)

### ✈️ Voos  
Engine: `google_flights`  
Função: **`buscar_voos_reais()`**

### 🏨 Hotéis  
Engine: `google_hotels`  
Função: **`buscar_hoteis_reais()`**

### 🎡 Atrações  
Engine: `google`  
Função: **`pesquisar_atracoes()`**

### 💱 Câmbio  
Engine: `google`  
Função: **`buscar_cambio()`**

### 📚 História  
Engine: `google`  
Função: **`pesquisar_historia()`**

---

## 4️⃣ Síntese Final do Roteiro (LLM)

O LLM combina:

- Dados reais coletados  
- Contexto cultural e histórico  
- Interesses do usuário  
- Datas planejadas  

Resultado: um **roteiro completo e altamente detalhado**.

Função: **`agente_de_viagens()`**

---

---

# 🧠 Conceitos Teóricos, Fundamentos e Código de PLN Aplicado

## Orquestração e LangChain

O projeto adota uma arquitetura de **Orquestração** e **Pipelining** de agentes. Este é um conceito crucial no desenvolvimento de aplicações com LLMs, pois permite coordenar múltiplos componentes (LLM, APIs externas) para realizar uma tarefa complexa que o LLM sozinho não conseguiria executar de forma confiável ou com dados em tempo real.

### 🛠️ Boas Práticas de Engenharia Aplicadas
* **Modularidade:** As funções de busca (via SerpAPI) são isoladas, garantindo que cada componente possa ser testado e mantido separadamente, aderindo ao princípio de responsabilidade única.
* **Chains e Runnables:** O uso de **`RunnableSequence`** no LangChain define um fluxo de execução claro (`Prompt` $\rightarrow$ `LLM`) para as técnicas de PLN, tornando o processamento escalável e rastreável.
* **Controle de Temperatura:** Ajustamos a `temperature` do LLM de acordo com a tarefa:
    * **`temperature=0` (Zero Temp):** Usado para tarefas que exigem precisão e fidelidade (PLN, planejamento de datas), garantindo saídas determinísticas.
    * **`temperature=0.5` (Criativo):** Usado para a geração do roteiro final, permitindo criatividade e fluidez na redação.

---

## Retrieval Augmented Generation (RAG)

O projeto é uma aplicação clássica de **RAG**. Em vez de confiar apenas no conhecimento interno do LLM, a arquitetura primeiro **recupera** (*Retrieval*) dados externos e em tempo real (voos, hotéis, câmbio) via SerpAPI e, em seguida, **aumenta** (*Augmented*) o *prompt* do LLM com esses dados.

* **Vantagem:** Garante que o roteiro final seja baseado em **informações verificáveis, atuais e reais** (preços, datas), superando a limitação de conhecimento estático dos LLMs.

---

## Aplicação das Técnicas de PLN 

O projeto cumpre o requisito de aplicar, no mínimo, **DUAS** técnicas de PLN diretamente no *corpus* obtido através da API, utilizando o LangChain para encadear o prompt e o LLM.

### A. Sumarização de Textos (Técnica 1)

O LLM é instruído a resumir informações extensas sobre história e atrações, transformando dados brutos da web em conteúdo conciso e de fácil consumo para o viajante.

```python
# Bloco: SUMARIZAÇÃO DE TEXTOS com LangChain

template_sumario = """
Você receberá um texto sobre turismo (atrações, história, etc.).
Resuma o conteúdo em até 2 parágrafos, em português simples e claro.

TEXTO:
{texto}
"""

prompt_sumario = PromptTemplate(
    input_variables=["texto"],
    template=template_sumario
)
```
# A cadeia orquestra o Prompt e o LLM
cadeia_sumarizacao = RunnableSequence(


### C. Extração de Palavras-chave (Técnica 2)

Esta técnica utiliza o LLM para realizar a **extração** de termos relevantes (cultura, gastronomia, atrações) a partir do corpus de dados históricos e turísticos. As palavras-chave obtidas são cruciais, pois são usadas pelo LLM final para validar e justificar a criação do roteiro.

```python
# Bloco: EXTRAÇÃO DE PALAVRAS-CHAVE com LangChain

template_keywords = """
Extraia as principais palavras-chave (no máximo 10) do texto abaixo,
relacionadas a turismo, atrações, cultura, gastronomia e experiências de viagem.
Responda como uma lista separada por vírgula.

TEXTO:
{texto}
"""

prompt_keywords = PromptTemplate(
    input_variables=["texto"],
    template=template_keywords
)

cadeia_keywords = RunnableSequence(
    prompt_keywords,
    llm_zero_temp
)

def extrair_palavras_chave(texto):
    if not texto or "não encontrada" in texto.lower():
        return "Sem palavras-chave (texto insuficiente)."
    resp = cadeia_keywords.invoke({"texto": texto})
    return resp.content.strip()

```
### E. Análise de Sentimentos (Técnica 3 - Extra)

O projeto inclui esta técnica para classificar e justificar o sentimento (e.g., MUITO POSITIVO, POSITIVO, NEGATIVO) com base nas descrições ou avaliações de hotéis reais retornadas pela API. Essa análise de PLN permite que o LLM crie um roteiro mais consciente da qualidade das opções de hospedagem, integrando a percepção do viajante final.

```python
# Bloco: ANÁLISE DE SENTIMENTOS com LangChain

template_sentimento = """
Você receberá reviews / descrições de hotéis ou atrações.

Classifique o sentimento geral como:
- MUITO POSITIVO
- POSITIVO
- NEUTRO
- NEGATIVO
- MUITO NEGATIVO

Explique brevemente o porquê.

TEXTO:
{texto}
"""

prompt_sentimento = PromptTemplate(
    input_variables=["texto"],
    template=template_sentimento
)

# A cadeia orquestra o Prompt e o LLM
cadeia_sentimento = RunnableSequence(
    prompt_sentimento,
    llm_zero_temp # LLM com temperatura baixa (0) para classificação objetiva
)

def analisar_sentimento(texto):
    if not texto or "Nenhum hotel encontrado" in texto:
        return "Não há texto suficiente para análise de sentimento."
    resp = cadeia_sentimento.invoke({"texto": texto})
    return resp.content
```
----

# 📁 Estrutura da Aplicação

```bash
├── agente_de_viagens()
│
├── gerar_dados_viagem() # LLM: datas + interesses
├── descobrir_aeroporto() # LLM: código IATA
│
├── buscar_voos_reais() # SerpAPI – Google Flights
├── buscar_hoteis_reais() # SerpAPI – Google Hotels
├── pesquisar_atracoes() # SerpAPI – Google Search
├── buscar_cambio() # SerpAPI – Google Search
├── pesquisar_historia() # SerpAPI – Google Search
│
└── síntese final com Gemini
```

---

# 🚀 Como Executar

### 1. Configure suas chaves
```bash
export GOOGLE_API_KEY="sua_google_ai_key"
export SERPAPI_API_KEY="sua_serpapi_key"


```

# 📚 Relação com o Repositório (UFABC – 2025.Q3)

Este projeto demonstra, na prática, os conceitos estudados em PLN:

Uso de LLMs

Prompt Engineering

Orquestração de ferramentas externas

Integração com APIs

Arquitetura modular

Aplicações reais de PLN com dados externos

--

# 🧑‍💻 Autores

Leandro Cabral e Gabriel Azevedo
Projeto desenvolvido no contexto do curso de PLN da UFABC.

<p align="center"> <img src="https://img.icons8.com/color/96/airplane-take-off.png" width="90"/> </p>


---


