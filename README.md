# 🌍✨ Agente de Viagens com IA — Documentação Oficial

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue" />
  <img src="https://img.shields.io/badge/Status-Ativo-brightgreen" />
  <img src="https://img.shields.io/badge/IA-LangChain-orange" />
  <img src="https://img.shields.io/badge/Google_Gemini-Suporte_Oficial-red" />
</p>

<p align="center">
  <img src="https://github.com/adalves-ufabc/2025.Q3-PLN/raw/main/assets/nlp-banner.png" width="80%" />
</p>

---

## 📘 Sobre o Projeto

Este repositório contém um **Agente de Viagens Inteligente** desenvolvido como parte do curso **Processamento de Linguagem Natural (PLN)** da UFABC — repositório base:

🔗 **https://github.com/adalves-ufabc/2025.Q3-PLN**

O projeto demonstra:

✔️ Uso de modelos de linguagem (LLMs)  
✔️ Construção de agentes com LangChain  
✔️ Ferramentas externas acopladas ao agente  
✔️ Interação natural e objetiva com o usuário  
✔️ Arquitetura modular seguindo boas práticas de PLN  

---

## 🚀 Funcionalidades do Agente

### 🤖 **Assistente de Viagem Inteligente**
O agente responde perguntas sobre viagens, por exemplo:

- “Quero fazer uma viagem para Santos amanhã.”  
- “Quais opções de hospedagem perto da praia?”  
- “Como está o tempo em Recife?”  

### 🔎 **Ferramentas Integradas**
O agente usa ferramentas do LangChain:

| Ferramenta | Função |
|-----------|--------|
| 🦆 DuckDuckGoSearchRun | Busca online em tempo real |
| 🌐 API de Contexto | Integra informações estruturadas |
| 🧠 Modelo Google Gemini | Geração de linguagem natural |

---

## 🧱 Arquitetura Técnica

<p align="center">
  <img src="https://github.com/adalves-ufabc/2025.Q3-PLN/raw/main/assets/llm-architecture.png" width="75%" />
</p>

### 🔧 Pipeline Geral

1. **Prompt do Usuário**  
2. **Agente ReAct do LangChain**  
3. **Ferramentas externas (Search / APIs)**  
4. **Modelo Google Gemini**  
5. **Resposta final organizada**

---

## 📂 Estrutura do Repositório

```
📦 projeto-agente-viagens
├── src/
│   ├── agent.py
│   ├── tools.py
│   ├── prompts.py
│   └── utils.py
├── examples/
│   └── demo.ipynb
├── assets/
│   ├── nlp-banner.png
│   └── llm-architecture.png
├── README.md
└── requirements.txt
```

---

## 🧠 Conceitos de PLN Utilizados (do repositório base)

Todos retirados e alinhados com:  
🔗 **https://github.com/adalves-ufabc/2025.Q3-PLN**

### 📌 Modelos de Linguagem Natural  
- Tokenização  
- Embeddings  
- Atenção e Transformers  
- Geração contextual  

### 📌 Agentes e Cadeias  
- LangChain ReAct  
- Raciocínio passo a passo  
- Ferramentas (Tools) externas  

### 📌 Boas práticas recomendadas  
- Modularização  
- Prompts controlados  
- Logs e interpretabilidade  

---

## 💻 Como Executar

### 1. Clone o repositório
```bash
git clone https://github.com/SEU_USUARIO/NOME_REPO.git
cd NOME_REPO
```

### 2. Instale as dependências
```bash
pip install -r requirements.txt
```

### 3. Configure sua API KEY
```bash
export GOOGLE_API_KEY="SUA_KEY_AQUI"
```

### 4. Execute o agente
```bash
python src/agent.py
```

---

## 📜 Licença

Este projeto segue a licença acadêmica do material base do curso **PLN — UFABC**.

---

## ✨ Autor

Projeto criado por **Gabriel**, com apoio conceitual do repositório-base da disciplina de PLN.

---

Se quiser adicionar **mais imagens**, **um logo próprio**, **badges personalizadas** ou transformar isso em **documentação completa (mkdocs / sphinx)**, posso gerar tudo para você!

