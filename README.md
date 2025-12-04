# 🌍 Agente de Viagens Inteligente — IA + Dados Reais  
### *Projeto acadêmico baseado em PLN (UFABC – 2025.Q3)*  

<p align="center">
  <img src="https://img.icons8.com/external-flaticons-lineal-color-flat-icons/344/external-travel-vacation-planning-flaticons-lineal-color-flat-icons.png" width="140"/>
</p>

---

## ✨ Visão Geral

Este projeto implementa um **agente inteligente de viagens**, combinando:

- **LLMs (Google Gemini via LangChain)**
- **Consultas reais através da SerpAPI**
- **Orquestração completa para gerar roteiros detalhados**

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
  <img src="https://i.imgur.com/rOfCqQb.png" width="85%"/>
</p>

A arquitetura segue **4 grandes etapas**:

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

# 📁 Estrutura da Aplicação

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


---

# 🚀 Como Executar

### 1. Configure suas chaves
```bash
export GOOGLE_API_KEY="sua_google_ai_key"
export SERPAPI_API_KEY="sua_serpapi_key"


📚 Relação com o Repositório (UFABC – 2025.Q3)

Este projeto demonstra, na prática, os conceitos estudados em PLN:

Uso de LLMs

Prompt Engineering

Orquestração de ferramentas externas

Integração com APIs

Arquitetura modular

Aplicações reais de PLN com dados externos

🧑‍💻 Autores

Leandro Cabral e Gabriel Azevedo
Projeto desenvolvido no contexto do curso de PLN da UFABC.

<p align="center"> <img src="https://img.icons8.com/color/96/airplane-take-off.png" width="90"/> </p>


---


