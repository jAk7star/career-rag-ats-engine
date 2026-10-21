# 🚀 Career RAG & ATS Intelligence Engine (`career-rag-ats`)

![Python](https://img.shields.io/badge/Python-3.10+-blue.svg)
![Prompt Engineering](https://img.shields.io/badge/Prompt%20Engineering-Multi--Layer-orange.svg)
![Architecture](https://img.shields.io/badge/Architecture-Zero--Hallucination%20RAG-green.svg)
![IDE Support](https://img.shields.io/badge/IDE-Antigravity%20%7C%20Cursor%20%7C%20VSCode%20%7C%20Claude%20Code-purple.svg)

> **Um motor de Engenharia de Prompt e Local JSON-RAG em múltiplas camadas para auditoria de vagas, cálculo determinístico de aderência (ATS Scoring) e compilação automatizada de currículos em `.pdf` e `.docx` com bloqueio estrito contra alucinações de LLMs.**

---

## 🎯 O Problema de Negócio e Engenharia
Modelos de Linguagem (LLMs) tradicionais sofrem de **alucinação criativa** ao adaptar currículos para descrições de vagas: eles inventam ferramentas que o candidato nunca usou, inflam certificações e geram layouts com tabelas ou colunas duplas que quebram a leitura de robôs **ATS** (*Applicant Tracking Systems* como Gupy, Workday, Greenhouse e Vagas.com).

## 💡 A Solução (`career-rag-ats`)
Este projeto implementa uma **Agent Skill modular e portável** baseada em **Structured Context Injection (Local JSON-RAG)** e **Multi-Layer Prompt Engineering**, separando estritamente:
1. **A Fonte da Verdade Imutável (`data/master_profile.json`):** Um banco de dados estruturado contendo apenas projetos auditados no GitHub, formação real e certificações verificadas.
2. **O Pipeline de Decisão em 5 Camadas (`prompts/SKILL.md`):**
   - **Layer 1 (Job & Resume Parser):** Extração atômica de requisitos obrigatórios, desejáveis e diferenciais.
   - **Layer 2 (Semantic & Factual Matching):** Classificação rigorosa em `EXACT_MATCH`, `SEMANTIC_MATCH`, `TRANSFERABLE_MATCH`, `PARTIAL_MATCH` e `NOT_IDENTIFIED`.
   - **Layer 3 (Scoring Engine):** Cálculo ponderado de aderência antes de qualquer reescrita de texto.
   - **Layer 4 (Ethical Optimization & Guardrails):** Reescrita orientada por *Ação + Habilidade + Resultado + Evidência*, com **Negative Constraints** explícitas (proibindo invenção de skills como SQL ou exames oficiais não realizados).
   - **Layer 5 (Single-Column ATS Compiler - `scripts/export_ats.py`):** Compilação programática em Python (`python-docx` e `reportlab`) gerando documentos 100% legíveis por parsers de RH.

---

## 🏗️ Arquitetura do Sistema

```text
[Descrição da Vaga (Input)] 
         │
         ▼
┌────────────────────────────────────────────────────────┐
│ LAYER 1 & 2: PARSER & FACTUAL MATCHING                 │
│ Cruza requisitos da vaga com `data/master_profile.json`│
└──────────────────────────┬─────────────────────────────┘
                           ▼
┌────────────────────────────────────────────────────────┐
│ LAYER 3: ATS SCORING & GAP ANALYSIS                    │
│ Gera Tabela de Aderência + Match Score (0-100)         │
└──────────────────────────┬─────────────────────────────┘
                           ▼
┌────────────────────────────────────────────────────────┐
│ LAYER 4: ZERO-HALLUCINATION OPTIMIZER (Guardrails)     │
│ Aplica Negative Constraints + Truthfulness Validator   │
└──────────────────────────┬─────────────────────────────┘
                           ▼
┌────────────────────────────────────────────────────────┐
│ LAYER 5: PYTHON ATS COMPILER (`scripts/export_ats.py`) │
│ Renderiza `.pdf` e `.docx` em layout de coluna única   │
└────────────────────────────────────────────────────────┘
```

---

## 💻 Portabilidade Multi-IDE (Como usar em outros ambientes)

Esta skill foi desenhada sob o padrão aberto **Agent Skills (`SKILL.md` + JSON Schema)**, sendo 100% replicável fora do chat em qualquer IDE moderna de AI Building:

1. **Antigravity / Claude Code:**
   - Copie o arquivo `ide_configs/CLAUDE.md` para a raiz do workspace ou adicione a pasta à sua biblioteca de `.skills/`.
2. **Cursor IDE / Windsurf:**
   - Utilize o arquivo `ide_configs/.cursorrules` na raiz do projeto. O agente lerá automaticamente o `data/master_profile.json` via `@file` e executará o `scripts/export_ats.py` no terminal.
3. **VS Code (GitHub Copilot / Continue / Cline):**
   - Adicione `prompts/SKILL.md` em `.github/copilot-instructions.md`.

---

## 🛠️ Como Executar o Compilador Localmente

`ash
# 1. Instale as dependencias de geracao documental
pip install python-docx reportlab

# 2. Configure a base factual (utilize o template de exemplo ou personalize com seus dados)
# No Linux/macOS: cp data/master_profile.example.json data/master_profile.json
# No Windows PowerShell: Copy-Item data/master_profile.example.json data/master_profile.json

# 3. Execute o compilador ATS conectado a sua base JSON
python scripts/export_ats.py
`
---
**Desenvolvido por:** [Jaques Gabriel Amaral Nunes](https://github.com/jAk7star)
