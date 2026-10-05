---
name: what-am-i-missing
description: Runs a gap analysis of a plan, brief, design doc or project against named laws, standards and market benchmarks, plus a premortem, and returns ranked findings with sources and add/change/remove/pivot recommendations. Use when the user shares a plan, brief, design doc, checklist, launch idea or project and asks what they are forgetting, missing or not covering — "o que estou esquecendo", "o que falta", "what am I missing", "pontos cegos", "blind spots", "gaps", "segundo a literatura / padrões do mercado / boas práticas", "industry standards", "furos no plano", "o que cortar no plano", "vale pivotar?". Not for line-editing prose.
---

# What Am I Missing

Gap analysis against named references plus a premortem, ending in add/change/remove/pivot recommendations.

## When NOT to run the full analysis
- **Vague idea.** It's vague if any of these is missing: the problem, the target user, or what success means. Don't produce findings. Ask the single missing question. Offer 2–4 concrete directions the idea could take, and flag any direction with a heavy regulatory path (name the regulator, no article numbers). End with "Escolha uma e eu rodo a análise completa."
- **One right answer.** Just answer it.
- **Line-editing a draft.** That's editing.
- **A fully irreversible decision.** There is nothing left to change. If only part of the plan is locked in (lease signed, stock bought), name that part in Leitura as a fixed constraint and analyze only what can still change.

## User limits win
If the user asks for brevity ("rapidinho", "em N linhas", "curto", "TL;DR"):
- With N lines total, write N−1 findings, one per line: severity, the gap, the cheapest check, and the ✅/🧠 marker.
- Line N holds the hidden assumption and one ➖.
- Sources and "Quer a análise completa?" may follow on one extra line.
- Skip every other section, but keep the markers.

Any other format or length the user sets also overrides the Response shape below.

## Pick the mode
| If the user… | Mode |
|---|---|
| names a topic, question, file, section or `foco: X` ("o que falta na minha política de privacidade?", "foco: segurança") | **Focused** |
| asks about the whole plan or project, or there's a project folder and no topic | **Global** |

If you can't tell which mode applies, use global and offer focused at the end. State the mode in Leitura.

**Global:**
- Map the project folder first (see step 1).
- Sweep every area that applies: product/UX, legal/compliance, security/privacy, accessibility, operations/infra, monetization/finance, marketing/distribution, metrics.
- Up to **7** findings.

**Focused:**
- Read only the files relevant to the focus.
- Use only references for that topic (1–6 of them). Go deeper: name articles, clauses and specific requirements.
- Up to **10** findings, all inside the focus.

## Process
1. **Minimum context.** You need three things: what it is, who it's for, and what success looks like.
   - Look in the conversation first. If there's a project folder, also read README, ROADMAP, CLAUDE.md, docs/, the manifests and the top-level structure. In focused mode, open these only if the three items aren't already clear.
   - If **what** or **who** is missing and can't be inferred, ask **one** question and stop.
   - If only **success** is unclear, assume it, state the assumption in Leitura, and continue.
   - If the user doesn't answer or says to proceed, assume, state it in Leitura, and continue.
   - Anything the user already tracks in a doc is not a finding.
2. **References.** Pick 3–6 named sources for global mode, or 1–6 for focused. See the quick reference below.
3. **Checklist sweep.** Compare the plan against each reference.
4. **Fresh-eyes web scan.** Run 1–3 WebSearches for recent changes in regulation, platform policy or the market.
5. **Premortem.** Imagine the plan has failed, at its first milestone or at 6 months, whichever comes first, and ask why. Then find the **hidden assumption**: the one thing that, if false, collapses the plan.
6. **Cut and rank.** Respect the mode's limit (7 global, 10 focused). Move the overflow to "Pode ficar pra depois".
   - The limit is a ceiling, not a target. Never pad. If fewer than 3 real gaps exist, report only those and write "Plano sólido nos pontos verificados" in Leitura.
   - Keep a 🟢 in Achados only if a 🔴/🟠 depends on it. Every other 🟢 goes to "Pode ficar pra depois".
   - Generic hygiene (renewals, backups, contact page, a 404 page) is a finding only if this plan makes it unusually risky.
7. **Recommendations.** Turn the findings into four types of change:
   - ➕ **Adicionar**: something is missing.
   - ✏️ **Mudar**: something exists, but it's wrong, weak or conflicts with a reference.
   - ➖ **Remover**: a reference contradicts it, it doesn't pay off its effort, it duplicates something, or it's risk with no benefit. Always look for one. Only remove things that exist in the plan or that it clearly implies. For something that may exist, write "se houver: remover X". In a short plan, this can mean removing or postponing a step the user implied, such as buying stock before the blocking checks.
   - 🔀 **Pivô**: change the audience, channel, model or core scope. Suggest it **only if** the hidden assumption is load-bearing **and** you have ✅ evidence against it (data, a benchmark, a regulation). If the evidence is only 🧠, write "Pivô condicional: se <checagem #N> confirmar, <pivô>".

## Response shape
The section names below are labels. Translate them, and the closing question, into the user's language (Reading, References used, Already covered, Findings, Hidden assumption, Can wait, Recommendations, Start with, Sources, "Which of these did you already know?"). For a small plan with few findings, merge Já coberto into Leitura and drop any empty section.

1. **Leitura**: the plan, its audience, what success means, the mode, the jurisdiction assumed, and your assumptions. 1–3 lines.
2. **Referências usadas**: one line each, with name, year or version, and what it covers.
3. **Já coberto**: one line on what the user already has.
   - *Global only:* a **Cobertura por área** table. Mark each area ✅ ok, ⚠️ gaps, ⬜ not reviewed (also use this for areas you only skimmed) or n/a (doesn't apply).
4. **Achados**: ranked by severity.
   ```
   N. 🔴/🟠/🟢 <Lacuna, uma frase concreta>
      - Em termos simples: <sem jargão>
      - Consequência: <o que acontece de concreto se ignorar>
      - Fonte: <referência> · ✅ verificado | 🧠 memória (confirmar) | ❓ incerto
      - Checagem mais barata: <ação concreta, tempo/custo se souber>
   ```
   Severity: 🔴 blocks the plan (legal, safety, platform ban, money loss), 🟠 high impact, 🟢 nice to have.
5. **Premissa escondida**: one sentence, plus one early-warning signal the user can observe or measure.
6. **Pode ficar pra depois**: 2–4 items, each with its revisit trigger ("quando passar de 100 pedidos/mês").
7. **Recomendações**: a table grouped ➕, ✏️, ➖, 🔀.

   | Tipo | Recomendação | Por quê | Esforço |
   |---|---|---|---|
   | ➕/✏️/➖/🔀 | <ação concreta> | achado #N ou premissa | baixo/médio/alto |

   - Every finding maps to at least one row.
   - Always include a ➖ row. If nothing should go, write `➖ | nada a remover | <motivo> | —`.
   - Always include a 🔀 row. With no pivot, write `🔀 | pivô não recomendado | <motivo> | —`.
   - If you recommend a pivot, mark the rows that only apply without it with "(sem pivô)".
8. **Comece por**: the 3 rows with the highest impact ÷ effort, whatever their position in the table.
9. **Fontes**: a link for every ✅. For facts read from the project, give the file path instead.
10. *Focused only:* **Fora do foco**: at most 2 lines, 🔴 only. Omit the section if there are none.
11. Close with: *"Quais desses você já sabia?"*

## Verification rule
- ✅ means you opened the source itself: the law text, the regulator's page, the official docs, or the article for a market fact. A search-results summary alone counts as 🧠.
- Before marking a **law, regulation, norm number, tax rule or platform policy** ✅, verify it with WebSearch or WebFetch.
- If you can't verify it, mark it 🧠 and add "confirmar".
- Never invent article, RDC or ISO numbers. Name the regulator and the topic instead.
- Frameworks and benchmarks can stay 🧠.

**No web access?**
- Skip step 4 and mark every legal or policy claim 🧠 (confirmar).
- In Fontes, write "Sem acesso à web: nada verificado nesta rodada".
- Make the first cheapest check a manual verification of the top 🔴.

## Quick reference: default reference sets
These assume Brazil. For any other jurisdiction, swap in the local equivalents (FTC and state consumer law, GDPR/DSA, the local tax and advertising regulators) and say which jurisdiction you assumed in Leitura.

| Domain | Start with |
|---|---|
| E-commerce | CDC, Decreto 7.962/2013, LGPD, sector regulator (ANVISA/MAPA/INMETRO), NF-e, CONAR |
| Game (Roblox) | MDA, Octalysis/Bartle, Roblox Community Standards + paid-random-item policy, top-5 genre benchmark, D1/D7 metrics |
| SaaS / app | Lean Canvas, AARRR, OWASP Top 10, WCAG 2.2, LGPD/GDPR, app-store guidelines |
| Website / blog | Search Central guidelines, Core Web Vitals, WCAG 2.2, LGPD/GDPR (third-party requests too, not just cookies), host/platform docs |
| Landing page / marketing | AIDA/PAS, Cialdini, Core Web Vitals, CONAR/FTC disclosure |
| Business plan | Business Model Canvas, Porter 5 Forças, unit economics (CAC/LTV), local tax regime |

## Common mistakes
- **Generic best practice instead of a finding.** Each finding names a concrete consequence for **this** plan.
- **Only recommending additions.** A plan that never hears "remove X" or "change Y" just gets heavier.
- **Citing "a literatura" generically.** Name the work.
- **Skipping the owner's weak domains.** A dev owner gets a hard look at legal and marketing. A designer owner gets a hard look at operations and finance.
