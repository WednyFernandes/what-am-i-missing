---
name: what-am-i-missing
description: Use when the user shares a plan, brief, design doc, checklist, launch idea or document and asks what they are forgetting, missing or not covering — "o que estou esquecendo", "o que falta", "what am I missing", "pontos cegos", "blind spots", "gaps", "segundo a literatura / padrões do mercado / boas práticas", "industry standards", "furos no plano", "o que cortar", "o que mudar", "vale pivotar?".
---

# What Am I Missing

## Overview
This is a gap analysis against **named references**: laws, standards, frameworks and market benchmarks. A premortem pass then catches what no checklist lists. Each finding cites its source, says whether the source was checked now or recalled from memory, and ends with the cheapest next check. The answer closes with concrete recommendations to add, change, remove or pivot.

## When NOT to use
- A vague idea with no plan yet. Help plan it first.
- A question with one right answer. Just answer it.
- Line-editing a draft. That's editing, not a gap analysis.
- A decision that is already irreversible.

## Pick the mode first
| If the user… | Mode |
|---|---|
| names a specific topic, question, file, section or `foco: X` ("o que falta na minha política de privacidade?", "furos na monetização", "foco: segurança") | **Focused** |
| asks about the whole plan or project, or there's a project folder and no topic ("o que estou esquecendo nesse projeto?") | **Global** |

State the mode in **Leitura** ("Modo: focado em monetização"). If you can't tell which mode applies, use global and offer focused at the end.

**Global mode (whole project)**
- If there's a project folder, map it before judging. Read README, ROADMAP, CLAUDE.md, docs/, the manifests (package.json, pyproject…) and the top-level structure. Infer the domain, stage and audience from what you find.
- Sweep **every area** that applies: product/UX, legal/compliance, security/privacy, accessibility, operations/infra, monetization/finance, marketing/distribution, metrics.
- Add a **Cobertura por área** table after "Já coberto": one row per area, marked ✅ ok, ⚠️ gaps or ⬜ not reviewed. Areas you skimmed get ⬜. Don't mark them ✅.
- Findings: 3–7, across areas, ranked by severity.

**Focused mode (one question or area)**
- Use only references for **that topic**, and go deeper: name articles, clauses and specific requirements, not just the law's name.
- Findings: 3–10, all inside the focus. Severity still ranks them.
- Read only the files relevant to the focus. Don't scan the whole repo.
- Add **Fora do foco** at the end: at most 2 lines, and only for 🔴 items you happened to notice. If there are none, omit the section.
- Skip "Cobertura por área".

## Process

1. **Minimum context.** You need three things: what it is, who it's for, and what success looks like. Look for them in the conversation and in project docs (README, CLAUDE.md, ROADMAP) before asking. If one is missing, ask **one** question and move on. Anything the user already tracks in a doc is not a finding.
2. **Pick the references.** Choose 3–6 named sources that act as the checklist. See the quick reference below.
3. **Checklist sweep.** Compare the plan against each reference.
4. **Fresh-eyes web scan.** Run 1–3 WebSearches for recent changes in regulation, platform policy or the market for this domain. These are often the highest-impact findings, because no plan doc contains them.
5. **Premortem pass.** Assume it's 6 months later and the plan has failed, then ask why. This surfaces failures specific to this plan that no reference lists. Also find the **hidden assumption**: the one thing that, if false, collapses the plan.
6. **Cut and rank.** Keep **3–7 findings** in global mode or **3–10** in focused mode. Move the rest to "Pode ficar pra depois".
7. **Turn findings into recommendations.** Sort each change into one of four types:
   - ➕ **Adicionar**: something missing that should exist. This is what most findings become.
   - ✏️ **Mudar**: something that exists but is wrong, weak or conflicts with a reference.
   - ➖ **Remover**: something in the plan that a reference contradicts, that doesn't pay off its effort, that duplicates something else, or that adds risk with no benefit. Look for at least one candidate. Plans usually have extra scope.
   - 🔀 **Pivô**: change the core of the plan (audience, channel, model, scope). Suggest a pivot **only if** the hidden assumption is load-bearing **and** you found evidence against it (data, a benchmark, a regulation). Otherwise write "Pivô: não recomendado", with the reason in one line.

## Response shape (in this order, in the user's language)

1. **Leitura**: what the plan is, who it's for, what success looks like, and your assumptions, in 1–3 lines.
2. **Referências usadas**: one line per reference, giving its name, year or version, and what it covers.
3. **Já coberto**: one line on what the user already has. This builds trust that you read their plan.
   - *Global only:* a **Cobertura por área** table.
4. **Achados**: 3–7 findings (global) or 3–10 (focused), ranked by severity. Write each one in this format:
   ```
   N. 🔴/🟠/🟢 <Lacuna, uma frase concreta>
      - Em termos simples: <o que é, sem jargão>
      - Consequência: <o que acontece de concreto se ignorar>
      - Fonte: <referência> · ✅ verificado | 🧠 memória (confirmar) | ❓ incerto
      - Checagem mais barata: <ação concreta, com tempo/custo se souber>
   ```
   Severity levels: 🔴 blocks the plan (legal, safety, platform ban, money loss), 🟠 high impact, 🟢 nice to have.
5. **Premissa escondida**: one sentence naming the load-bearing assumption, plus one early-warning signal the user can observe or measure.
6. **Pode ficar pra depois**: 2–4 low-priority items, each with the trigger for revisiting it ("quando passar de 100 pedidos/mês").
7. **Recomendações**: a table with every change, grouped by type in the order ➕, ✏️, ➖, 🔀.

   | Tipo | Recomendação | Por quê | Esforço |
   |---|---|---|---|
   | ➕/✏️/➖/🔀 | <ação concreta> | achado #N ou premissa | baixo/médio/alto |

   - Every finding maps to at least one row.
   - Include at least one ➖ row. If nothing should be removed, say so in one line.
   - Always include the 🔀 row: either a pivot, or "não recomendado" with the reason.
8. **Comece por**: the first 3 rows of Recomendações, ranked by impact ÷ effort.
9. **Fontes**: links for every ✅.
   - *Focused only:* **Fora do foco**, with at most 2 🔴 items, placed before the closing question.
10. End with one question: *"Quais desses você já sabia?"* If a gap was already known, it needs a checklist line, not an explanation.

## Verification rule
If a finding cites a **law, regulation, norm number, tax rule or platform policy**, verify it with WebSearch or WebFetch before marking it ✅. These change, and a wrong norm number is worse than none. If you can't verify it, mark it 🧠 and add "confirmar". Never invent article, RDC or ISO numbers. When unsure of the number, name the regulator and the topic instead.

Frameworks and benchmarks (MDA, Canvas, competitor patterns) can stay 🧠.

## Quick reference: default reference sets
| Domain | Start with |
|---|---|
| E-commerce BR | CDC, Decreto 7.962/2013, LGPD, sector regulator (ANVISA/MAPA/INMETRO), NF-e, CONAR |
| Game (Roblox) | MDA, Octalysis/Bartle, Roblox Community Standards + monetization/paid-random-item policy, top-5 genre benchmark, D1/D7 metrics |
| SaaS / app | Lean Canvas, AARRR, OWASP Top 10, WCAG 2.2, LGPD/GDPR, app-store guidelines |
| Landing page / marketing | AIDA/PAS, Cialdini, Core Web Vitals, CONAR/FTC disclosure |
| Business plan | Business Model Canvas, Porter 5 Forças, unit economics (CAC/LTV), local tax regime |

## Common mistakes
- Writing generic best practice instead of a finding. Every finding names a concrete consequence for **this** plan.
- Writing "considere testar X". Name the cheapest concrete check instead, e.g. "ligue pra vigilância sanitária (15 min)".
- Only recommending additions. A gap analysis that never says "remove X" or "change Y" makes the plan heavier, not better.
- Suggesting a pivot because it sounds bold. A pivot needs the hidden assumption plus evidence against it.
- Delivering more than 7 findings. A list of 20 doesn't get read. Push the rest down to "Pode ficar pra depois".
- Listing things the user already said or already tracks.
- Citing "a literatura" generically. Name the work.
- Stating a norm number confidently from memory. Verify it or mark it 🧠.
- Skipping the domains the owner is weak in. If the owner is a dev, look hard at legal and marketing. If the owner is a designer, look hard at operations and finance.
