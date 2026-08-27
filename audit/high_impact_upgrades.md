# Upgrades de Alto Impacto

Mudanças mais trabalhosas do que os [quick wins](quick_wins.md), mas que mudam claramente a perceção de "protótipo" para "produto acabado". Todas continuam dentro de [sporting-leoes-em-campo.html](../sporting-leoes-em-campo.html), sem exigir motor de jogo novo nem assets externos.

---

## 1. Sistema de partículas + "pop" no HUD ao apanhar objetos
**Onde:** `popFloater`, [linhas 548-557](../sporting-leoes-em-campo.html:548), chamada em [linhas 650](../sporting-leoes-em-campo.html:650) e [654](../sporting-leoes-em-campo.html:654); `scoreEl`, [linha 656](../sporting-leoes-em-campo.html:656)
**O que fazer:**
- Ao apanhar, gerar 6-10 pequenos `<div>` (pontos/estrelas douradas) na posição da apanha, com uma animação CSS de "explosão" radial (`transform: translate(...) scale(0)` + `opacity: 0` no fim), reaproveitando o padrão já usado em `.floater`/`floatUp` ([linhas 239-251](../sporting-leoes-em-campo.html:239)).
- No HUD, aplicar uma pequena animação de "pulso" (`scale(1) → scale(1.25) → scale(1)`, ~150ms) ao `#score` sempre que o valor muda, em vez de só trocar o `textContent`.
**Porquê alto impacto:** é o evento que mais vezes acontece numa sessão — sentir-se bem 50+ vezes por jogo vale mais do que qualquer ajuste único.
**Esforço:** meio dia (sistema de partículas simples em DOM/CSS, sem canvas).

## 2. Diferenciar visualmente o prémio maior (escudo, +5) da bola (+1)
**Onde:** `spawnFaller`, [linhas 519-544](../sporting-leoes-em-campo.html:519); apanha do badge, [linhas 651-654](../sporting-leoes-em-campo.html:651)
**O que fazer:** dar ao escudo um leve brilho pulsante enquanto cai (`filter: drop-shadow(0 0 6px var(--gold))` a animar), e ao apanhar, um efeito maior que o da bola — partícula dourada mais intensa, texto "+5" maior, talvez um leve "flash" de tela em dourado muito subtil.
**Porquê alto impacto:** ensina o jogador, só pela imagem, qual é o objeto valioso — e recompensas visualmente distintas são um dos sinais mais fortes de design de jogo "premium".
**Esforço:** ~2-3 horas.

## 3. Camada de atmosfera no fundo do campo
**Onde:** `.stage`, [linhas 158-171](../sporting-leoes-em-campo.html:158); `.stage::before`, [linhas 173-178](../sporting-leoes-em-campo.html:173)
**O que fazer:**
- Faixa desfocada no topo sugerindo arquibancada/multidão (pode ser só um `linear-gradient` com "manchas" de cor de baixo contraste — não precisa ser uma ilustração literal).
- Um "foco de luz" radial lento (`background-position` a animar muito devagar) para sugerir holofotes de estádio.
- Vinheta nos cantos (`box-shadow: inset 0 0 60px rgba(0,0,0,0.4)` sobre `.stage-wrap`) para focar o olhar no centro, onde a ação acontece.
**Porquê alto impacto:** é a mudança que mais diretamente resolve a sensação de "campo vazio" identificada na auditoria — e o jogo já está tematicamente ligado a um estádio, por isso a atmosfera reforça o conceito em vez de o desviar.
**Esforço:** meio dia.

## 4. Momento de "novo recorde" com celebração visual
**Onde:** `endGame`, [linhas 579-595](../sporting-leoes-em-campo.html:579); `.overlay .final`, [linhas 282-286](../sporting-leoes-em-campo.html:282)
**O que fazer:** quando `score > best` ([linha 584](../sporting-leoes-em-campo.html:584)), disparar confetti simples (dezenas de retângulos/pontos coloridos com `--green`/`--gold`/`--white` a cair com rotação, CSS puro), fazer o brasão do ecrã final brilhar/pulsar, e diferenciar claramente a cor/tamanho do texto "Novo recorde!" do "Fim de jogo" normal.
**Porquê alto impacto:** é o pico emocional da sessão de jogo — o momento com maior probabilidade de o jogador querer partilhar um ecrã (print/vídeo), por isso é onde o polimento visual tem mais retorno percebido.
**Esforço:** ~3-4 horas.

## 5. Som sintetizado leve (Web Audio, sem ficheiros externos)
**Onde:** eventos já existentes — apanha ([linhas 644-655](../sporting-leoes-em-campo.html:644)), perda de vida (`loseLife`, [linhas 562-575](../sporting-leoes-em-campo.html:562)), fim de jogo (`endGame`, [linha 579](../sporting-leoes-em-campo.html:579))
**O que fazer:** usar `AudioContext`/`OscillatorNode` (sem pedir ficheiros `.mp3`/`.wav`) para gerar 3-4 sons curtos e simples: um "blip" agudo ao apanhar bola, um "ping" mais rico ao apanhar escudo, um som grave/áspero ao perder vida, um pequeno jingle ascendente no fim de jogo. Tudo em poucas linhas de JS, sem assets a carregar.
**Porquê alto impacto:** som é frequentemente o fator isolado com maior efeito na perceção de "qualidade" de um jogo casual — e como não há nenhum atualmente, mesmo um sistema simples é um salto grande.
**Esforço:** meio dia (afinar os sons para não soarem irritantes).

---

**Nota de sequenciação:** os itens 1 e 2 partilham a mesma infraestrutura (sistema de partículas) — vale a pena implementá-los juntos. O item 3 é independente e pode avançar em paralelo. Ver [visual_priority_plan.md](visual_priority_plan.md) para a ordem recomendada face aos quick wins.
