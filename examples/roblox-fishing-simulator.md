# Example: Roblox fishing simulator GDD (Portuguese)

This is a sample output of `what-am-i-missing` v1.3.0, generated in October 2026. Policy facts can change, so check the linked sources before relying on them.

**Prompt:**
> Meu GDD de um simulator no Roblox: o jogador pesca peixes, vende, compra varas melhores, tem um boss diário. Monetização: gamepass de 2x cash. O que estou esquecendo segundo literatura e padrões do mercado?

---

**Leitura**
Simulator de pesca no Roblox (pescar → vender → comprar vara melhor → boss diário), monetizado por uma gamepass de 2x cash. Público assumido: jogadores de Roblox de 9 a 16 anos, com o Brasil como mercado principal. Sucesso assumido: chegar a uma CCU estável e a uma receita que pague o desenvolvimento nos primeiros 3 meses. Modo **global**, jurisdição **Brasil**, mais as políticas globais do Roblox.

**Referências usadas**
- **MDA** (Hunicke, LeBlanc & Zubek, 2004): mecânica → dinâmica → estética. Usei para checar se o loop gera sensação, e não só números.
- **Octalysis** (Yu-kai Chou, 2015): motivações de longo prazo, como coleção/posse, social e escassez.
- **Roblox: requisitos de Paid Random Items** (DevForum, maio de 2026) e a **documentação de monetização** do Roblox.
- **ECA Digital, Lei 15.211/2025** (em vigor desde 17/03/2026, fiscalizada pela ANPD): loot boxes e práticas de uso compulsivo para menores.
- **Benchmark do gênero**: Fisch e Fish It!, os dois jogos de pesca com mais de 1M de CCU.
- **Métricas D1/D7/D30** e funil de onboarding (padrão de mercado F2P).

**Já coberto**
O loop central (coletar → vender → melhorar) está fechado, o boss diário dá um motivo para voltar e já existe uma forma de monetizar.

| Área | Status |
|---|---|
| Produto/UX (loop, FTUE, coleção) | ⚠️ |
| Legal/compliance (PRI, ECA Digital) | ⚠️ |
| Segurança/dados (exploits, DataStore) | ⚠️ |
| Acessibilidade | ⬜ |
| Operações/live-ops | ⚠️ |
| Monetização/economia | ⚠️ |
| Marketing/distribuição | ⚠️ |
| Métricas | ⚠️ |

**Achados**

1. 🔴 O GDD não trata a sorte paga nem o público menor de idade no Brasil.
   - Em termos simples: pescar já é sorteio. Se o jogador puder comprar com Robux, direta ou indiretamente, qualquer coisa que dê um resultado aleatório (isca de sorte, poção de luck, baú de peixe), isso é um "Paid Random Item". O Brasil está na lista de países onde esse tipo de item é restrito, e o ECA Digital proíbe loot box em jogos que menores podem acessar.
   - Consequência: o jogo pode ser moderado ou derrubado pelo Roblox, e um caso de "sorte paga" para criança no Brasil pode virar sanção da ANPD. Retrabalhar a loja depois do lançamento custa caro.
   - Fonte: Roblox, Clarifying Requirements for Paid Random Items · ✅ verificado. ECA Digital (Rádio Senado) · ✅ verificado. Se a gamepass de 2x cash torna a cash "comprada com Robux": ❓ incerto.
   - Checagem mais barata: listar todo item que mistura Robux e aleatoriedade. Em cada um, aplicar `PolicyService:GetPolicyInfoForPlayerAsync` → `ArePaidRandomItemsRestricted`, mostrar as odds em % somando 100% e oferecer uma alternativa determinística. Leva cerca de 2h no papel.

2. 🟠 O GDD não diz por que alguém sairia de Fisch ou Fish It! para jogar o seu.
   - Em termos simples: o nicho tem dois gigantes. O Fish It! passou de 2,7M de jogadores simultâneos e o Fisch de 1,2M. Sem um diferencial, o algoritmo de descoberta compara o seu jogo diretamente com eles.
   - Consequência: o jogo recebe pouco tráfego orgânico, o CTR do thumbnail fica baixo e ele morre na primeira semana.
   - Fonte: MaxPower Gaming sobre Fish It! · ✅ verificado.
   - Checagem mais barata: escrever, em uma frase, o que o jogo tem que nenhum dos dois tem (tema, mecânica, social) e testar 2 ou 3 thumbnails com anúncio pago pequeno. Gasta de 1 a 3 dias e poucos dólares.

3. 🟠 A monetização tem um produto só, e ele é permanente.
   - Em termos simples: uma gamepass de 2x cash se compra uma vez e pronto. O Roblox oferece developer products (itens recompráveis), assinaturas, servidores privados, anúncios imersivos e otimização de preço. Os simulators de sucesso vivem de consumíveis: boosts temporários, revive no boss, slots extras.
   - Consequência: a receita trava no primeiro pagamento de cada jogador, porque não existe um segundo motivo para gastar.
   - Fonte: Roblox Docs, Monetization · ✅ verificado. Padrão do gênero · 🧠 memória (confirmar).
   - Checagem mais barata: montar uma tabela com 3 a 5 gamepasses (2x cash, auto-sell, inventário maior, VIP) e 3 a 5 developer products determinísticos, sem sorte paga (ver #1). Leva 1h.

4. 🟠 Faltam o primeiro minuto, a coleção e o AFK, que são os pilares do líder do gênero.
   - Em termos simples: o Fish It! cresceu com pesca simples e sem falha, raridade mostrada como "1 em X", missões que guiam o jogador o tempo todo e modo AFK, chegando a sessões médias de 30 minutos. Seu GDD não tem índice de peixes (o "álbum"), tutorial nem modo AFK.
   - Consequência: o jogador sai antes de entender o loop e o D1 cai. Sem um álbum para completar, o motivo de coleção do Octalysis fica vazio.
   - Fonte: MaxPower Gaming · ✅ verificado. MDA/Octalysis · 🧠 memória.
   - Checagem mais barata: roteirizar os primeiros 60 segundos (spawn → primeiro peixe → primeira venda → primeira meta visível) e adicionar um Índice de Peixes com contagem "x/120". Leva 2h de design.

5. 🟠 A economia não tem sinks nem fim de progressão.
   - Em termos simples: a cash entra pela pesca e só sai pelas varas. Quando o jogador compra a última vara, o jogo acaba para ele. A gamepass de 2x encurta esse caminho pela metade justamente para quem pagou.
   - Consequência: o jogador que pagou vê o conteúdo acabar primeiro e é o primeiro a sair. Moedas também inflacionam se surgir trade.
   - Fonte: Padrão de simulators (rebirth/prestige, sinks) · 🧠 memória (confirmar).
   - Checagem mais barata: planilha de cash/hora por vara, com e sem 2x, mostrando quantas horas levam até a última vara. Adicionar rebirth e pelo menos 2 sinks (isca, upgrade de barco/área). Leva 2h.

6. 🟠 Não há plano contra exploits e perda de save.
   - Em termos simples: venda, preço e recompensa do boss precisam ser calculados no servidor. Se o cliente informa "peguei peixe X", alguém vai mentir. Um DataStore sem session locking pode duplicar ou apagar progresso.
   - Consequência: aparecem dupes de cash e quebram a economia e o ranking. Uma perda de save gera avaliações negativas e reembolsos de Robux.
   - Fonte: Boas práticas de RemoteEvents/DataStore do Roblox · 🧠 memória (confirmar).
   - Checagem mais barata: listar cada RemoteEvent e marcar o que o servidor valida. Usar ProfileStore/ProfileService ou session locking próprio. Leva 2 a 4h.

7. 🟠 Sem métricas nem cadência de live-ops.
   - Em termos simples: o GDD não diz como você vai saber se deu certo (D1, D7, conversão, tempo de sessão), nem com que frequência sai conteúdo novo. Os líderes do gênero atualizam toda semana.
   - Consequência: você não sabe se o problema é o onboarding, o loop ou a loja, e o jogo esfria entre as atualizações.
   - Fonte: Padrão F2P D1/D7 e Roblox Analytics · 🧠 memória (confirmar).
   - Checagem mais barata: definir metas (por exemplo D1 ≥ 25% e D7 ≥ 8%, ambos a confirmar no seu nicho), instrumentar funnel events no onboarding e fazer um calendário de 6 semanas de updates. Leva 2h.

**Premissa escondida**
Que um loop de pesca parecido com o dos líderes atrai jogadores mesmo com Fisch e Fish It! dominando o nicho. Sinal de alerta: o CTR do thumbnail e o D1 do primeiro teste pago ficarem bem abaixo da média que o Creator Dashboard mostra para o gênero.

**Pode ficar pra depois**
- Trade entre jogadores: quando passar de cerca de 1k CCU estável, porque pede antifraude.
- Acessibilidade (legenda e cor de raridade além do brilho): no primeiro polimento de UI.
- Versões traduzidas além de PT/EN: quando mais de 20% da CCU vier de outro idioma.
- Assinatura mensal (VIP): quando houver conteúdo suficiente para justificar um benefício recorrente.

**Recomendações**

| Tipo | Recomendação | Por quê | Esforço |
|---|---|---|---|
| ➕ | Checagem de `ArePaidRandomItemsRestricted` com odds em % e alternativa determinística | achado #1 | baixo |
| ➕ | Índice de Peixes, raridade "1 em X", tutorial de 60s e modo AFK | achado #4 | médio |
| ➕ | 3 a 5 developer products consumíveis sem aleatoriedade e mais gamepasses de conveniência | achado #3 | baixo |
| ➕ | Rebirth/prestige e 2 sinks de cash | achado #5 | médio |
| ➕ | Validação no servidor de todo RemoteEvent e DataStore com session locking | achado #6 | médio |
| ➕ | Metas D1/D7, funnel events e calendário de updates de 6 semanas | achado #7 | baixo |
| ✏️ | Reescrever o pitch com um diferencial explícito frente a Fisch e Fish It! | achado #2, premissa | baixo |
| ✏️ | Rebalancear a 2x cash para não encurtar a progressão de quem paga | achado #5 | baixo |
| ➖ | Tirar do MVP qualquer item pago com resultado aleatório (luck pago, baús) | achado #1, é risco sem benefício no lançamento | baixo |
| ➖ | Adiar o boss diário para depois de validar o loop central (é o sistema mais caro) | premissa, achado #4 | baixo |
| 🔀 | Pivô condicional: se a checagem #2 mostrar CTR/D1 bem abaixo do gênero, manter o código do loop e trocar o tema (outra criatura ou outro cenário fora da pesca) | premissa, achado #2 | médio |

**Comece por**
1. ➖ Tirar a sorte paga do MVP e ➕ aplicar a checagem de PolicyService. É barato e remove o único 🔴.
2. ✏️ Escrever o diferencial e testar thumbnails, porque isso decide se vale construir o resto.
3. ➕ Montar os developer products consumíveis, porque a receita multiplica com quase nenhum código.

**Fontes**
- ✅ [Roblox DevForum: Clarifying Requirements for Paid Random Items (maio de 2026)](https://devforum.roblox.com/t/clarifying-requirements-for-paid-random-items/4654622)
- ✅ [Rádio Senado: ECA Digital proíbe rolagem infinita e caixa de recompensa em games infantojuvenis](https://www12.senado.leg.br/radio/1/noticia/2026/03/27/eca-digital-proibe-rolagem-infinita-e-caixa-de-recompensa-em-games-infantojuvenis)
- ✅ [MaxPower Gaming: Fish It, how a simplified copycat became one of Roblox's biggest hits](https://www.maxpowergaming.co/post/fish-it-how-a-simplified-copycat-became-one-of-roblox-s-biggest-hits)
- ✅ [Roblox Docs: Monetization](https://create.roblox.com/docs/production/monetization)

*Quais desses você já sabia?*
