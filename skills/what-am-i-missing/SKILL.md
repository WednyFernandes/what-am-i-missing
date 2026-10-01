---
name: what-am-i-missing
description: Use when the user shares a plan, brief, design doc, checklist, launch idea or document and asks what they are forgetting, missing or not covering — "o que estou esquecendo", "o que falta", "what am I missing", "pontos cegos", "blind spots", "gaps", "segundo a literatura / padrões do mercado / boas práticas", "industry standards", "furos no plano".
---

# What Am I Missing

## Overview
This is a gap analysis against **named references**: laws, standards, frameworks and market benchmarks. A premortem pass then catches what no checklist lists. Each finding cites its source, says whether the source was checked now or recalled from memory, and ends with the cheapest next check.

## When NOT to use
- A vague idea with no plan yet. Help plan it first.
- A question with one right answer. Just answer it.
- Line-editing a draft. That's editing, not a gap analysis.
- A decision that is already irreversible.

## Process

1. **Minimum context.** You need three things: what it is, who it's for, and what success looks like. Look for them in the conversation and in project docs (README, CLAUDE.md, ROADMAP) before asking. If one is missing, ask **one** question and move on. Anything the user already tracks in a doc is not a finding.
2. **Pick the references.** Choose 3–6 named sources that act as the checklist. See the quick reference below.
3. **Checklist sweep.** Compare the plan against each reference.
4. **Fresh-eyes web scan.** Run 1–3 WebSearches for recent changes in regulation, platform policy or the market for this domain. These are often the highest-impact findings, because no plan doc contains them.
5. **Premortem pass.** Assume it's 6 months later and the plan has failed, then ask why. This surfaces failures specific to this plan that no reference lists. Also find the **hidden assumption**: the one thing that, if false, collapses the plan.
6. **Cut and rank.** Keep **3–7 findings**. Move the rest to "Pode ficar pra depois".

## Response shape (in this order, in the user's language)

1. **Leitura**: what the plan is, who it's for, what success looks like, and your assumptions, in 1–3 lines.
2. **Referências usadas**: one line per reference, giving its name, year or version, and what it covers.
3. **Já coberto**: one line on what the user already has. This builds trust that you read their plan.
4. **Achados**: 3–7 findings ranked by severity. Write each one in this format:
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
7. **Comece por**: the first 3 actions, ranked by impact ÷ effort. Each action names the finding it closes.
8. **Fontes**: links for every ✅.
9. End with one question: *"Quais desses você já sabia?"* If a gap was already known, it needs a checklist line, not an explanation.

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
- Delivering more than 7 findings. A list of 20 doesn't get read. Push the rest down to "Pode ficar pra depois".
- Listing things the user already said or already tracks.
- Citing "a literatura" generically. Name the work.
- Stating a norm number confidently from memory. Verify it or mark it 🧠.
- Skipping the domains the owner is weak in. If the owner is a dev, look hard at legal and marketing. If the owner is a designer, look hard at operations and finance.
