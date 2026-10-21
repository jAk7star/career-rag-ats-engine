---
name: career-rag-ats
description: Gera curriculos otimizados para sistemas ATS (em PDF e DOCX) e artigos ou posts tecnicos para LinkedIn usando uma base RAG de projetos reais, formacao e certificacoes.
---
# Career RAG & ATS Intelligence Engine

Esta habilidade opera o **CV ATS Intelligence Engine** e o gerador de conteúdo técnico para LinkedIn fundamentada estritamente nos fatos reais documentados em `data/master_profile.json`.

## Regras de Ouro (Invioláveis - Anti-Hallucination Guardrails)

1. **Integridade Factual Absoluta (Zero Alucinação):**
   - NUNCA invente experiências, ferramentas, idiomas ou certificações que não estejam em `data/master_profile.json`.
   - **Proibições expressas (Negative Constraints):** Nunca inclua "Assistência de Secretaria Escolar (SENAC)" nem "Projeto de Voluntariado na Plataforma Atados" (descartados da fonte da verdade).
   - **Precisão de Certificados:** Os cursos de AZ-900 e MS-900 pela Ka Solution devem ser listados estritamente como "Treinamentos Preparatórios" ou "Fundamentos", nunca como certificação oficial de exame Microsoft.

2. **Leitura Estrita da Base RAG Local (`data/master_profile.json`):**
   - Sempre leia `data/master_profile.json` antes de gerar currículos, análises de vagas ou artigos técnicos.

---

## Fluxo 1: Análise de Vaga e Geração de Currículo ATS (Multi-Layer Pipeline)

Quando o usuário enviar uma descrição de vaga ou pedir um currículo direcionado:

1. **Layer 1 & 2: Diagnóstico ATS (Parser, Matching & Scoring):**
   - Extraia as palavras-chave **Obrigatórias**, **Desejáveis** e **Adicionais** da vaga.
   - Cruze com `data/master_profile.json` classificando como `EXACT_MATCH`, `SEMANTIC_MATCH`, `TRANSFERABLE_MATCH`, `PARTIAL_MATCH` ou `NOT_IDENTIFIED`.
   - Gere uma tabela contendo: `Tipo de Habilidade | Keyword / Competência | Status (Tem / Parcial / Não Tem) | Evidência no Portfólio | Ação Recomendada`.
   - Calcule o percentual estimado de aderência técnica (Match Score de 0 a 100) e apresente os gaps reais sem mascarar bloqueadores.

2. **Layer 3 & 4: Otimização Semântica Ética:**
   - Adapte o **Título Alvo**, o **Resumo Profissional**, a ordem das **Competências Principais** (sempre no topo, logo abaixo do resumo) e os **Bullets de Projetos** usando a estrutura *Ação + Habilidade + Resultado + Evidência*.
   - Selecione apenas as certificações de `data/master_profile.json` que agregam valor direto à vaga alvo.

3. **Layer 5: Compilação em `.pdf` e `.docx` (Layout Coluna Única ATS):**
   - Execute `scripts/export_ats.py` (ou gere via interpretador Python usando `python-docx` e `reportlab`/`weasyprint`).
   - **Regras Visuais ATS:** Coluna única estrita, sem tabelas invisíveis, sem gráficos ou colunas laterais, fontes padrão (Arial, Calibri ou Helvetica), hierarquia clara de títulos e links diretos para o LinkedIn e GitHub.

---

## Fluxo 2: Artigos Técnicos e Posts para LinkedIn

Quando o usuário pedir um post ou artigo sobre seus projetos:
1. Estruture o texto destacando a dor real de negócio (ex.: estouro de tokens de API, lentidão em planilhas, riscos de LGPD).
2. Apresente a arquitetura da solução (ex.: higienização local pesada com Python/Pandas/Regex em arquitetura *Zero-Exposure* antes de acionar LLMs como Google Gemini, ou automação nativa via JavaScript/JSON).
3. Finalize com resultados práticos de engenharia e uma chamada para discussão técnica engajadora.


# Claude Code / Antigravity Commands
- `/ats-audit`: Executa o diagnóstico de aderência contra `data/master_profile.json`.
- `/build-cv`: Gera o currículo otimizado e invoca `python scripts/export_ats.py`.