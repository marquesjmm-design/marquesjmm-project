# Problemas Visuais Detalhados

Ficheiro de referência: [sporting-leoes-em-campo.html](../sporting-leoes-em-campo.html)

Cada problema indica onde está no código, porque é que "parece barato", e o que fazer sem reescrever o jogo.

---

## A. Estilo de arte

### A1. A bola usa emoji do sistema, não um desenho próprio
**Onde:** [linha 534](../sporting-leoes-em-campo.html:534) — `el.textContent = '⚽';`
**Problema:** o emoji `⚽` é renderizado pelo tipo de letra de emoji do sistema operativo/browser do jogador (Segoe UI Emoji no Windows, Noto no Android, Apple Color Emoji no iOS...). Tem sombreado 3D fotorrealista, cores e proporções que não têm nada a ver com o vetor plano/dourado do resto do jogo. É o elemento mais "gerado à pressa" do ecrã, porque literalmente não foi desenhado — foi importado do sistema.
**Impacto:** alto — é o objeto que mais aparece no ecrã (60% dos "fallers", [linha 523](../sporting-leoes-em-campo.html:523)).

### A2. O cartão vermelho é um retângulo sem nenhum detalhe
**Onde:** [linhas 210-215](../sporting-leoes-em-campo.html:210)
**Problema:** `background: var(--card-red); border-radius: 3px;` — sem forma de cartão de árbitro (proporção, canto biselado, textura), sem ícone, sem gradiente. É indistinguível de um `<div>` de teste.
**Impacto:** alto — é o elemento que devia comunicar perigo/penalização, e neste momento não comunica nada além de "vermelho".

### A3. O leão é demasiado simples para um close-up
**Onde:** [linhas 387-397](../sporting-leoes-em-campo.html:387) (jogador) e [linhas 408-413](../sporting-leoes-em-campo.html:408) (ecrã inicial, a 74×82px)
**Problema:** elipse + 2 círculos + um traço para a boca. Funciona a 64px como ícone rápido de reconhecer, mas no ecrã inicial, onde aparece maior e é o primeiro elemento que o jogador vê, a simplicidade lê-se como inacabado em vez de "estilizado".
**Impacto:** médio.

### A4. Ícones de vida ilegíveis
**Onde:** [linha 140](../sporting-leoes-em-campo.html:140) — `.life{ width:16px; height:16px; }`
**Problema:** a 16px, o desenho da carinha do leão dentro do círculo dourado ([linha 469](../sporting-leoes-em-campo.html:469)) perde-se — na prática o jogador vê três pontos dourados.
**Impacto:** baixo/médio (afeta legibilidade, não só estética).

---

## B. Cor e iluminação

### B1. Contraste do relvado é baixo entre as duas tonalidades de verde
**Onde:** [linhas 18-19](../sporting-leoes-em-campo.html:18) — `--green: #0E7A3D; --green-deep: #07461F;`
**Problema:** ambas são verdes escuros e saturados, próximos em luminosidade. As riscas ([linhas 162-167](../sporting-leoes-em-campo.html:162)) dão textura mas não ajudam os objetos que caem a destacar-se do fundo.
**Impacto:** médio — afeta legibilidade durante o jogo, não só estética.

### B2. Sem vinheta nem foco de luz
**Onde:** `.stage::before`, [linhas 173-178](../sporting-leoes-em-campo.html:173)
**Problema:** o único efeito de luz é um gradiente radial muito ténue (`rgba(255,255,255,0.10)`) no topo. Não há escurecimento nos cantos (vinheta) nem nenhuma fonte de luz que sugira "foco de estádio" — o campo parece iluminado uniformemente, o que é visualmente plano.
**Impacto:** médio.

### B3. Sem sombra de contacto dinâmica
**Onde:** `.player`, [linhas 219-227](../sporting-leoes-em-campo.html:219); `.faller`, [linhas 198-207](../sporting-leoes-em-campo.html:198)
**Problema:** só existe `filter: drop-shadow(...)`, uma sombra estática "atrás" do elemento. Não há uma sombra elíptica projetada no chão (comum em jogos casuais para dar sensação de profundidade/altura).
**Impacto:** médio.

---

## C. Qualidade de UI

### C1. Dois sistemas de botão diferentes na mesma tela
**Onde:** `button.cta`, [linhas 289-306](../sporting-leoes-em-campo.html:289) vs. `.touch-controls button`, [linhas 313-326](../sporting-leoes-em-campo.html:313)
**Problema:** o CTA tem sombra deslocada + estado `:active` que "empurra" o botão (linguagem de profundidade/físico). Os botões ◀ ▶ são planos, com só um contorno fino. São dois sistemas de botão diferentes a coexistir.
**Impacto:** médio-alto — inconsistência de UI é um dos sinais mais reconhecíveis de "falta de polimento".

### C2. Combo calculado mas nunca mostrado
**Onde:** variável `combo`, [linha 494](../sporting-leoes-em-campo.html:494); usada em [linhas 647-648](../sporting-leoes-em-campo.html:647) e [linha 652](../sporting-leoes-em-campo.html:652), nunca escrita no DOM.
**Problema:** o jogo já sabe quando o jogador está "em sequência" e até já dá bónus de pontos por isso ([linha 648](../sporting-leoes-em-campo.html:648)), mas essa informação nunca chega ao ecrã. É lógica de jogo "desperdiçada" do ponto de vista visual.
**Impacto:** alto — é a oportunidade de UI com melhor relação esforço/retorno de todo o projeto (o cálculo já existe).

### C3. Texto do ecrã inicial inconsistente em tom
**Onde:** [linha 415](../sporting-leoes-em-campo.html:415) — `<h2>Pronto para MARTELAR em campo?</h2>`
**Problema:** maiúsculas a meio de frase e uma palavra ("MARTELAR") mais informal/agressiva do que o resto da cópia do jogo, que é neutra ("Apanha as bolas, junta os escudos, foge dos cartões vermelhos", [linha 355](../sporting-leoes-em-campo.html:355)). Lê-se como resíduo de edição, não como escolha de voz.
**Impacto:** baixo, mas rápido de corrigir e visível logo no primeiro ecrã.

---

## D. Animação e feedback

### D1. Sem partículas nem "flash" em nenhum evento
**Onde:** `popFloater`, [linhas 548-557](../sporting-leoes-em-campo.html:548); `loseLife`, [linhas 562-575](../sporting-leoes-em-campo.html:562)
**Problema:** o único feedback de "apanhar" é texto a subir; o único feedback de "perder vida" é um abanão de 0.35s. Não há burst de partículas, não há flash de cor no ecrã, não há escala/"pop" no número do HUD.
**Impacto:** alto — é a categoria com maior défice face ao resto do projeto.

### D2. Apanhar o escudo (+5) sente-se igual a apanhar uma bola (+1)
**Onde:** [linhas 646-655](../sporting-leoes-em-campo.html:646)
**Problema:** ambos disparam a mesma função `popFloater` com o mesmo estilo visual, só muda o número. O prémio maior do jogo não tem nenhuma celebração maior.
**Impacto:** médio.

### D3. Fim de jogo / novo recorde é um momento visualmente pequeno
**Onde:** `endGame()`, [linhas 579-595](../sporting-leoes-em-campo.html:579)
**Problema:** só muda texto (`endTitle.textContent = 'Novo recorde!'`, [linha 589](../sporting-leoes-em-campo.html:589)) — não há confetti, brilho no brasão, nem qualquer diferenciação visual entre "fim de jogo normal" e "novo recorde", que é o momento mais importante da sessão para o jogador.
**Impacto:** médio-alto.

---

## E. Fundo e ambiente

### E1. Campo sem contexto de estádio
**Onde:** `.stage`, [linhas 158-171](../sporting-leoes-em-campo.html:158); `.pitch-line`/`.pitch-circle`, [linhas 180-194](../sporting-leoes-em-campo.html:180)
**Problema:** riscas + linhas brancas + círculo — sem arquibancada, multidão, bandeiras ou luzes de estádio. Para um jogo temático (Sporting, "entrar em campo"), é a maior lacuna entre conceito e execução visual.
**Impacto:** alto.

### E2. Sem sensação de progressão visual
**Onde:** dificuldade sobe só por velocidade (`spawnInterval`, [linha 622](../sporting-leoes-em-campo.html:622); `speed`, [linha 542](../sporting-leoes-em-campo.html:542))
**Problema:** o jogo fica mais difícil, mas o ecrã tem exatamente o mesmo aspeto do primeiro ao último segundo — não há nenhuma pista visual (cor, luz, intensidade) de que a partida está a escalar.
**Impacto:** baixo/médio.

---

Ver priorização completa em [visual_priority_plan.md](visual_priority_plan.md).
