# Auditoria Visual — Resumo Geral

**Projeto avaliado:** [sporting-leoes-em-campo.html](../sporting-leoes-em-campo.html) (único artefacto visual/jogo na pasta de trabalho)
**Foco:** qualidade visual, apresentação e polimento — não mecânica de jogo nem código.

---

## 1. Impressão geral

O jogo **não parece um placeholder vazio** — já tem identidade de marca (verde/branco/dourado do Sporting), tipografia bem escolhida e uma estrutura de ecrã (HUD, campo, overlays) coerente. Mas também **não parece um produto acabado**: tem o aspeto de um protótipo funcional a que falta a "última camada" de acabamento — sombras de profundidade, partículas, textura de fundo, e consistência entre os elementos que caem no ecrã.

**O que o torna "low-end" agora mesmo:**
- A bola (emoji `⚽`, [linha 534](../sporting-leoes-em-campo.html:534)) não pertence ao mesmo mundo visual que o escudo/leão desenhado à mão em SVG — é o problema visual nº1 do projeto.
- O cartão vermelho é um retângulo CSS liso ([linhas 210-215](../sporting-leoes-em-campo.html:210)), sem nenhum detalhe — parece um marcador de "por fazer", não um elemento de jogo.
- O fundo do campo é só riscas repetidas de duas cores planas ([linhas 158-167](../sporting-leoes-em-campo.html:158)) — não há textura, relva, arquibancada ou luz ambiente.
- Não há qualquer partícula, brilho ou "flash" quando se apanha ou perde algo — o único feedback é um texto "+1" a subir ([linhas 239-251](../sporting-leoes-em-campo.html:239)) e um pequeno abanão ([linhas 230-235](../sporting-leoes-em-campo.html:230)).
- O texto do ecrã inicial tem uma inconsistência de tom: *"Pronto para MARTELAR em campo?"* ([linha 415](../sporting-leoes-em-campo.html:415)) — maiúsculas a meio da frase e uma palavra desalinhada do resto do texto (mais informal/agressiva do que o resto da cópia, que é neutra e clara). Isto lê-se como um erro de edição, não como uma escolha de estilo.

**O que já está bem conseguido:**
- Par tipográfico deliberado: Anton (display, condensado, "de estádio") + Work Sans (texto) — dá uma sensação desportiva sem parecer genérico ([linhas 100-115](../sporting-leoes-em-campo.html:100), [linhas 128-135](../sporting-leoes-em-campo.html:128)).
- Paleta de cor consistente e de marca (verde Sporting + dourado + branco), com tema escuro tratado corretamente via `prefers-color-scheme` ([linhas 17-55](../sporting-leoes-em-campo.html:17)).
- HUD limpo, bem espaçado, com números tabulares (`font-variant-numeric: tabular-nums`, [linha 133](../sporting-leoes-em-campo.html:133)) — evita que o placar "salte" ao mudar de dígitos.
- Botão principal (CTA) já tem uma linguagem de profundidade (sombra deslocada em vez de plana, com estado `:active` que "empurra" o botão) — [linhas 289-306](../sporting-leoes-em-campo.html:289). É o único elemento do projeto que já tem este nível de acabamento; o resto devia seguir o exemplo.
- Ecrãs de início e fim bem estruturados, com brasão, título, texto de apoio e CTA — hierarquia visual correta.

**O que melhorar primeiro:** ver [visual_priority_plan.md](visual_priority_plan.md) — resumidamente, unificar o estilo dos objetos que caem (bola, escudo, cartão) e dar profundidade ao fundo do campo são as duas mudanças que mais rapidamente tiram o "cheiro a protótipo" ao jogo.

---

## 2. Estilo de arte

Existe uma direção de estilo clara nas peças desenhadas à mão: **vetor plano, geométrico, com contorno dourado grosso** (o brasão/leão do jogador, [linhas 382-398](../sporting-leoes-em-campo.html:382), e o escudo que cai, [linha 536](../sporting-leoes-em-campo.html:536)). O problema é que **nem todos os elementos seguem essa linguagem**:

| Elemento | Estilo atual | Pertence ao mesmo mundo visual? |
|---|---|---|
| Leão/escudo do jogador | SVG vetor plano, contorno dourado 4px | ✅ referência do estilo |
| Escudo que cai (badge) | SVG vetor plano, contorno dourado 6px | ✅ consistente |
| Bola que cai | Emoji `⚽` do sistema operativo | ❌ estilo, sombreado e proporção diferentes; o aspeto muda consoante o browser/SO do jogador |
| Cartão vermelho | Retângulo CSS liso | ❌ sem nenhum traço de "desenho", contraste de qualidade brutal com os outros dois |
| Ícones de vida | SVG plano simples, 16px | ⚠️ estilo correto, mas demasiado pequeno para se perceber o desenho |

O leão em si é muito abstrato (elipse + duas circunferências para as orelhas + um "focinho" simples, [linhas 387-397](../sporting-leoes-em-campo.html:387)) — funciona como ícone à distância, mas não como mascote memorável em close-up (ex.: no ecrã inicial, onde aparece maior, [linhas 404-414](../sporting-leoes-em-campo.html:404)).

**Direção recomendada:** manter o vetor plano com contorno dourado (já funciona e é barato de produzir), mas (a) desenhar a bola e o cartão no mesmo idioma visual, e (b) acrescentar 1-2 camadas de sombreado simples (não gradiente completo, só uma segunda tonalidade de verde/dourado) às formas principais para lhes dar um mínimo de volume.

---

## 3. Cor e iluminação

- **Paleta:** boa e consistente — verde Sporting, dourado, branco/creme, com contraste adequado entre texto e fundo (`--text` sobre `--paper`/`--cream`).
- **Contraste do campo de jogo:** as duas cores das riscas do relvado (`--green` `#0E7A3D` e `--green-deep` `#07461F`, [linhas 18-19](../sporting-leoes-em-campo.html:18)) estão próximas em luminosidade — dá uma textura subtil, mas também significa que os objetos que caem (sobretudo o cartão vermelho escuro) não se destacam tanto quanto podiam contra o fundo.
- **Luz/atmosfera:** existe só um gradiente radial muito ténue no topo do campo (`.stage::before`, [linhas 173-178](../sporting-leoes-em-campo.html:173)) — não há vinheta nos cantos, nem qualquer fonte de luz direcional (ex.: um "foco de estádio"), nem sombra de contacto dinâmica sob o jogador ou os objetos.
- **Separação figura/fundo:** o jogador e os "fallers" têm `drop-shadow` estático ([linha 204](../sporting-leoes-em-campo.html:204), [linha 225](../sporting-leoes-em-campo.html:225)), o que ajuda, mas não há nenhuma sombra elíptica no chão a acompanhar o jogador — um truque simples e muito usado em jogos casuais para vender profundidade.

**Recomendação:** escurecer ligeiramente os cantos do campo (vinheta), aumentar o contraste entre as duas tonalidades de verde, e acrescentar uma sombra elíptica sob o jogador que pulsa ligeiramente com o movimento.

---

## 4. Qualidade da interface (UI)

- **HUD** ([linhas 118-144](../sporting-leoes-em-campo.html:118)): bem espaçado, tipografia legível, cantos arredondados consistentes com o resto (`border-radius: 12px`, igual ao painel do campo). É o elemento de UI mais "acabado" do projeto.
- **Botão CTA** ([linhas 289-306](../sporting-leoes-em-campo.html:289)): tem uma linguagem de profundidade própria (sombra deslocada tipo "botão físico"). Bom.
- **Botões táteis (◀ ▶)** ([linhas 313-326](../sporting-leoes-em-campo.html:313)): planos, com contorno fino e sem sombra — **não seguem a mesma linguagem do botão CTA**. Isto é uma inconsistência real: dois sistemas de botão diferentes na mesma tela.
- **Ícones de vida:** a 16px ([linha 140](../sporting-leoes-em-campo.html:140)), o desenho (carinha do leão) é ilegível — na prática lê-se como três pontos dourados, não como três leões.
- **Combo invisível:** o jogo já calcula um combo/sequência (`combo`, [linha 494](../sporting-leoes-em-campo.html:494), usado em [linha 648](../sporting-leoes-em-campo.html:648)) mas **nunca o mostra ao jogador** — é trabalho de lógica já feito que não está a gerar nenhum retorno visual, a maior oportunidade perdida da interface.
- **Texto do ecrã inicial:** ver nota em "Impressão geral" sobre "MARTELAR" ([linha 415](../sporting-leoes-em-campo.html:415)) — quebra o tom neutro/institucional do resto da cópia.

**Modernidade geral da UI:** básica-mas-correta. Não parece 2010, mas também não tem nenhum dos sinais que associamos a produtos "premium" (glow, blur, micro-interações consistentes em todos os controlos).

---

## 5. Animação e feedback visual

Muito pouco feedback para a quantidade de eventos que o jogo já regista:

| Evento | Feedback atual | Suficiente? |
|---|---|---|
| Apanhar bola | Texto "+1" a subir | Fraco — sem partícula, sem "pop" no HUD |
| Apanhar escudo (+5, o prémio maior) | Igual à bola, só muda o número | Fraco — devia sentir-se maior que apanhar uma bola |
| Apanhar cartão / perder vida | Abanão do jogador (`shake`, 0.35s) | Aceitável, mas sozinho |
| Combo ativo | Nenhum | Em falta — o número existe no código mas não é mostrado |
| Fim de jogo / novo recorde | Muda o texto do overlay | Fraco para o momento mais importante da sessão |

Não há confetti, brilho, "screen flash", nem som. A animação existente (`shake`, `floatUp`) é funcional mas mínima — dá para perceber o que aconteceu, não dá para o sentir como satisfatório.

---

## 6. Fundo e ambiente

O campo sente-se **vazio e plano**: riscas + um retângulo de linhas brancas + um círculo central ([linhas 158-194](../sporting-leoes-em-campo.html:158)) — sem arquibancada, sem multidão, sem relva com textura, sem qualquer elemento que sugira um estádio real. Para um jogo cujo tema é precisamente "entrar em campo", é a maior desconexão entre o conceito e a execução.

**Maior alavanca de melhoria de fundo:** uma faixa desfocada de arquibancada/luzes no topo do campo (baixo contraste, para não distrair) mais uma leve textura de relva — sem exigir trabalho de conteúdo dinâmico, só CSS/gradientes adicionais.

---

Ver também: [visual_problems.md](visual_problems.md) · [quick_wins.md](quick_wins.md) · [high_impact_upgrades.md](high_impact_upgrades.md) · [visual_priority_plan.md](visual_priority_plan.md)
