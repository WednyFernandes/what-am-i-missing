# Example: Roblox fishing simulator GDD (Portuguese)

This is a sample output of the `what-am-i-missing` skill, generated in September 2026. Policy facts can change, so check the linked sources before relying on them.

**Prompt:**
> "Meu GDD de um simulator no Roblox: o jogador pesca peixes, vende, compra varas melhores, tem um boss diário. Monetização: gamepass de 2x cash. O que estou esquecendo segundo literatura e padrões do mercado?"

---

**Leitura:** é um simulator de pesca no Roblox com o loop pescar → vender → comprar vara melhor → repetir, mais um boss diário e uma gamepass de 2x cash. Parto de três suposições: o público é o típico de simulator (crianças e adolescentes), a meta é retenção D1/D7 suficiente para o algoritmo de descoberta te mostrar, e a receita tem que pagar o desenvolvimento.

**Referências usadas**
- MDA (Hunicke, LeBlanc, Zubek, 2004): se as mecânicas geram a experiência que o jogador sente.
- Octalysis (Yu-kai Chou) e tipos de jogador de Bartle (1996): o que motiva o jogador a voltar.
- Política de Paid Random Items do Roblox, atualizada em 2026: odds, poções de sorte, menores no Brasil.
- Requisitos de publicação e DevEx do Roblox em 2026.
- Benchmarks do gênero: Fisch, Fish It e Catch 1 Billion Ducks.
- Métricas D1/D7/D30, conversão de pagantes e ARPDAU.

**Já coberto:** o core loop está completo e fechado (coletar, vender, melhorar). O boss diário já dá um motivo para voltar todo dia. A gamepass de 2x cash é a mais vendida em todo simulator.

## Achados

1. 🔴 **A sorte de pesca, se um dia for vendida por Robux, cai na política de itens aleatórios pagos, e no Brasil isso é proibido para menores.**
   - Em termos simples: peixe raro é sorteio. Se você vender "poção de sorte", isca boa ou baú de peixe por Robux, ou por uma moeda comprada com Robux, o Roblox exige mostrar antes da compra todos os resultados possíveis com a porcentagem exata, somando 100%. Desde 17/03/2026 itens aleatórios pagos não podem ser oferecidos a menores de 18 no Brasil.
   - Consequência: risco de moderação do jogo. Além disso, o produto nº 2 de quase todo jogo de pesca (o boost de sorte) teria que ficar bloqueado para boa parte do seu público brasileiro.
   - Fonte: Roblox Paid Random Items guidelines e anúncio de 2026 · ✅ verificado
   - Checagem mais barata: no design, chamar `PolicyService:GetPolicyInfoForPlayerAsync` e ler `ArePaidRandomItemsRestricted` antes de mostrar qualquer produto de sorte. Na UI, prever uma tabela de odds para cada vara, isca e zona (cerca de 1 h de design).

2. 🔴 **Só existe uma forma de pagar, então a receita tem teto baixo e é de compra única.**
   - Em termos simples: uma gamepass se compra uma vez e acabou. Os jogos do gênero vivem de Developer Products, que são compras repetíveis: boost temporário de sorte ou de cash, reviver ou pular etapa no boss, espaço extra de inventário, skins de vara e barco.
   - Consequência: o jogador mais engajado (a "baleia") não tem onde gastar depois da primeira compra, e o ARPDAU fica bem abaixo do benchmark.
   - Fonte: lojas de Fisch e Fish It; guia de monetização do Roblox · ✅ verificado (lojas) / 🧠 benchmark de ARPDAU
   - Checagem mais barata: abrir a loja de Fish It e de Fisch e listar o que cada um vende (20 min). Desenhar de 3 a 5 produtos de uma faixa só, com 1 ou 2 cosméticos e 2 a 3 boosts temporários.

3. 🟠 **Falta um "porquê" de longo prazo além do número subindo, como uma coleção ou index de peixes.**
   - Em termos simples: pelo MDA, "vara melhor → peixe mais caro" só gera a sensação de progresso. Falta descoberta e coleção, que é o que segura o jogador do tipo Explorer/Collector (Bartle) e o drive de Posse/Realização (Octalysis).
   - Consequência: o D7 cai assim que o jogador entende que a próxima vara é só "x1,5".
   - Fonte: MDA; Octalysis; padrão Fisch e Fish It · 🧠 memória
   - Checagem mais barata: escrever no GDD a tabela de peixes (raridade × zona × vara mínima) e conferir se cada vara destrava algo novo, e não só um multiplicador (1 h).

4. 🟠 **O boss diário não tem regras definidas: horário, fuso, quem perdeu e se é coletivo.**
   - Consequência: metade da base nunca vê o melhor conteúdo. Ou o boss vira farm por exploit (sair e voltar, trocar de servidor).
   - Fonte: benchmark de gênero · 🧠 memória (confirmar)
   - Checagem mais barata: decidir se o boss é um spawn rotativo por servidor ou um cooldown pessoal de 24 h, com lock por `UserId` e reset em UTC (30 min).

5. 🟠 **O plano não tem retenção nem social além do boss: daily reward, códigos, convite, grupo.**
   - Consequência: o jogo não sai da descoberta orgânica, e você perde o canal gratuito de marketing das listas de códigos.
   - Fonte: padrão de mercado · ✅ verificado (existência) / 🧠 impacto
   - Checagem mais barata: incluir no MVP o sistema de códigos e o daily streak (meio dia).

6. 🟠 **Monetização agressiva demais mata o jogo, e o próprio benchmark prova isso.**
   - Em termos simples: o Fisch dominou o Roblox no fim de 2024 e desabou depois de encher o jogo de microtransações.
   - Fonte: análises do caso Fisch e Fish It · ✅ verificado
   - Checagem mais barata: regra no GDD de que um jogador grátis alcança toda vara em X horas e pagar só encurta o tempo. Validar numa planilha de economia (2 h).

7. 🟢 **Custo e requisito de publicação de 2026.**
   - Desde 19/05/2026, publicar para todos custa 1.000 Robux por jogo, a menos que você mantenha Plus/Premium por 2 meses seguidos.
   - Fonte: DevForum · ✅ verificado
   - Checagem mais barata: ler o anúncio (10 min) e colocar o item no cronograma.

**Premissa escondida:** o plano assume que "vara melhor" basta como motivação para voltar. Sinal de alerta: se no teste a maioria dos jogadores comprar 2 ou 3 varas e sair antes do primeiro boss, a progressão está rasa.

**Pode ficar pra depois**
- Trade entre jogadores: quando houver base estável, porque o trade traz scam e exige moderação.
- Rebirth/prestige: quando os primeiros jogadores chegarem à última vara.
- Leaderboards globais: quando passar de uns 500 CCU.

**Comece por**
1. Escrever a tabela de peixes e coleção e a regra de que o jogador grátis alcança tudo. Fecha os achados 3 e 6.
2. Desenhar 3 a 5 Developer Products sem sorte paga, ou com a checagem de `PolicyService` e a tabela de odds. Fecha os achados 1 e 2.
3. Incluir códigos e daily streak no MVP e definir as regras do boss. Fecha os achados 4 e 5.

**Fontes**
- [Paid random items policy guidelines](https://create.roblox.com/docs/production/monetization/paid-random-items)
- [Clarifying Requirements for Paid Random Items](https://devforum.roblox.com/t/clarifying-requirements-for-paid-random-items/4654622)
- [New Publishing Requirements & Evaluation Process](https://devforum.roblox.com/t/new-publishing-requirements-evaluation-process-for-games/4573166)
- [Fisch Gamepasses (wiki)](https://fisch.fandom.com/wiki/Gamepasses)
- [Fish It: How a Simplified Copycat Became One of Roblox's Biggest Hits](https://www.maxpowergaming.co/post/fish-it-how-a-simplified-copycat-became-one-of-roblox-s-biggest-hits)

Quais desses você já sabia?
