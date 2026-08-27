# Plano de Prioridades Visuais

Resumo executivo da auditoria a [sporting-leoes-em-campo.html](../sporting-leoes-em-campo.html). Detalhe completo em [visual_summary.md](visual_summary.md), [visual_problems.md](visual_problems.md), [quick_wins.md](quick_wins.md) e [high_impact_upgrades.md](high_impact_upgrades.md).

---

## Top 5 problemas visuais

1. **Bola em emoji vs. resto em vetor desenhado** ([linha 534](../sporting-leoes-em-campo.html:534)) — maior choque de estilo do projeto, e é o objeto mais visto no jogo.
2. **Cartão vermelho sem nenhum desenho** ([linhas 210-215](../sporting-leoes-em-campo.html:210)) — retângulo liso, lê-se como placeholder.
3. **Fundo do campo plano e sem atmosfera** ([linhas 158-194](../sporting-leoes-em-campo.html:158)) — sem arquibancada, luz ou textura; maior desconexão entre o tema "estádio" e a execução.
4. **Praticamente sem feedback visual de ações** ([linhas 548-575](../sporting-leoes-em-campo.html:548)) — apanhar e perder têm quase o mesmo peso visual (texto + abanão), sem partículas nem diferenciação entre recompensas.
5. **Inconsistência entre sistemas de botão** ([linhas 289-306](../sporting-leoes-em-campo.html:289) vs. [313-326](../sporting-leoes-em-campo.html:313)) — o CTA parece "premium", os botões táteis parecem outro projeto.

## Top 5 quick wins

1. Desenhar a bola em SVG próprio, no mesmo estilo do escudo/leão — [detalhe](quick_wins.md#1-substituir-o-emoji-da-bola-por-um-svg-próprio).
2. Dar volume e rotação ao cartão vermelho — [detalhe](quick_wins.md#2-redesenhar-o-cartão-vermelho-como-um-cartão-a-sério).
3. Mostrar o combo que a lógica já calcula — [detalhe](quick_wins.md#3-mostrar-o-combo-que-já-existe-na-lógica).
4. Unificar os botões táteis com a linguagem do CTA — [detalhe](quick_wins.md#4-unificar-os-botões-táteis-com-a-linguagem-do-botão-cta).
5. Corrigir o texto "MARTELAR" do ecrã inicial — [detalhe](quick_wins.md#5-corrigir-o-texto-do-ecrã-inicial).

## Top 5 upgrades de alto impacto

1. Sistema de partículas + "pop" no HUD em cada apanha — [detalhe](high_impact_upgrades.md#1-sistema-de-partículas--pop-no-hud-ao-apanhar-objetos).
2. Diferenciar visualmente o escudo (+5) da bola (+1) — [detalhe](high_impact_upgrades.md#2-diferenciar-visualmente-o-prémio-maior-escudo-5-da-bola-1).
3. Camada de atmosfera no fundo (arquibancada, luz, vinheta) — [detalhe](high_impact_upgrades.md#3-camada-de-atmosfera-no-fundo-do-campo).
4. Celebração visual no "novo recorde" — [detalhe](high_impact_upgrades.md#4-momento-de-novo-recorde-com-celebração-visual).
5. Som sintetizado leve para apanhas, perdas e fim de jogo — [detalhe](high_impact_upgrades.md#5-som-sintetizado-leve-web-audio-sem-ficheiros-externos).

---

## O que mudar primeiro

Ordem recomendada, por retorno visual imediato face ao esforço:

1. **Todos os quick wins** (itens 1-7 em [quick_wins.md](quick_wins.md)) — menos de 2 horas no total, resolvem a maior parte dos problemas de *consistência* (o que mais grita "não acabado" à primeira vista).
2. **Upgrade 1 — sistema de partículas.** Sem isto, qualquer outra melhoria de feedback (recompensa maior, recorde) fica sem base para se apoiar.
3. **Upgrade 3 — atmosfera de fundo.** Independente das partículas, pode avançar em paralelo; é a mudança que mais aproxima o jogo do seu próprio tema (Sporting, "entrar em campo").

Estes três passos, por esta ordem, cobrem os 5 problemas do topo da lista.

## O que pode esperar

- **Upgrade 2 (diferenciação do escudo)** e **Upgrade 4 (celebração de recorde)** dependem do sistema de partículas já existir — fazer depois desse, não antes.
- **Upgrade 5 (som)** é o que mais isoladamente muda a perceção de qualidade, mas é também o mais independente de tudo o resto — pode ficar para uma segunda fase sem penalizar as restantes melhorias.
- Refinamentos menores como aumentar os ícones de vida ou detalhar mais o leão (ver [visual_problems.md](visual_problems.md), A3/A4) têm impacto real mas baixo; fazem sentido como polimento final, depois do resto.

## Fora de âmbito desta auditoria

Esta auditoria não avalia mecânica de jogo, equilíbrio de dificuldade, performance ou acessibilidade funcional — só apresentação visual. Não recomenda redesenhar o conceito do jogo: a direção de estilo atual (vetor plano, contorno dourado, paleta Sporting) já é boa e deve ser mantida como base de todas as mudanças acima.
