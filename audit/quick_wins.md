# Quick Wins — Alto Retorno, Baixo Esforço

Mudanças que não tocam na mecânica do jogo, cada uma isolada a uma zona pequena do [sporting-leoes-em-campo.html](../sporting-leoes-em-campo.html). Nenhuma exige mais do que CSS/SVG novo ou algumas linhas de JS.

---

## 1. Substituir o emoji da bola por um SVG próprio
**Onde:** [linha 534](../sporting-leoes-em-campo.html:534)
**Porquê primeiro:** é o objeto mais visto no jogo (60% das quedas) e o maior choque de estilo do projeto.
**Como:** trocar `el.textContent = '⚽';` por um `innerHTML` com um SVG plano simples (círculo branco + pentágonos/gomos verdes/dourados, contorno a condizer com o do escudo/leão — mesma espessura de traço, ~4-6px à escala do ícone). Reaproveitar a mesma paleta (`--green`, `--gold`) já definida em [linhas 17-32](../sporting-leoes-em-campo.html:17).
**Esforço:** ~20 min (desenhar/ajustar um SVG de bola simples).

## 2. Redesenhar o cartão vermelho como um cartão a sério
**Onde:** [linhas 210-215](../sporting-leoes-em-campo.html:210)
**Como:** manter o `<div>` mas dar-lhe proporção real de cartão (mais alto que largo já está certo), acrescentar `background: linear-gradient(155deg, #C71F3B, #8E0E22)` para dar volume, uma leve rotação aleatória por instância (`transform: rotate(...)`, variar em JS no `spawnFaller`) para parecer "atirado" e não colado à grelha, e opcionalmente um traço fino diagonal claro no canto para sugerir reflexo.
**Esforço:** ~15 min.

## 3. Mostrar o combo que já existe na lógica
**Onde:** variável `combo` já calculada em [linha 494](../sporting-leoes-em-campo.html:494)/[linha 648](../sporting-leoes-em-campo.html:648); HUD em [linhas 360-370](../sporting-leoes-em-campo.html:360)
**Como:** acrescentar um pequeno elemento (ex.: `<span id="combo">` perto do "Pontos") que só aparece quando `combo > 1`, com texto tipo "×2", "×3", a crescer ligeiramente em `font-size` ou brilho conforme o combo sobe. É trabalho de exibição apenas — o número já existe.
**Esforço:** ~20 min.

## 4. Unificar os botões táteis com a linguagem do botão CTA
**Onde:** `.touch-controls button`, [linhas 313-326](../sporting-leoes-em-campo.html:313), comparar com `button.cta`, [linhas 289-306](../sporting-leoes-em-campo.html:289)
**Como:** aplicar a mesma fórmula de profundidade do CTA (sombra deslocada sólida + deslocamento no `:active`) aos botões ◀ ▶, só trocando a cor de fundo (branco/verde em vez de dourado) para não competir com o CTA. Isto resolve, de um só golpe, a maior inconsistência de UI do projeto.
**Esforço:** ~10 min.

## 5. Corrigir o texto do ecrã inicial
**Onde:** [linha 415](../sporting-leoes-em-campo.html:415) — `Pronto para MARTELAR em campo?`
**Como:** alinhar com o tom do resto da cópia, ex.: `Pronto para entrar em campo?` (como estava originalmente) ou outra frase em Capitalização normal, sem maiúsculas a meio de frase.
**Esforço:** 1 min.

## 6. (bónus, quase grátis) Sombra elíptica sob o jogador
**Onde:** `.player`, [linhas 219-227](../sporting-leoes-em-campo.html:219)
**Como:** acrescentar um `<div>` ou `::after` com `border-radius:50%; background: rgba(0,0,0,0.35); filter: blur(4px);` posicionado por baixo do SVG do leão. Dá sensação imediata de volume/contacto com o chão por muito pouco esforço.
**Esforço:** ~10 min.

## 7. (bónus) Aumentar contraste do relvado
**Onde:** [linhas 18-19](../sporting-leoes-em-campo.html:18)
**Como:** escurecer `--green-deep` para algo como `#05391A` ou clarear ligeiramente `--green`. Uma alteração de duas linhas com efeito imediato na legibilidade dos objetos que caem.
**Esforço:** 5 min (mais alguns minutos a testar contraste).

---

**Tempo total estimado para todos os 7:** menos de 2 horas, e cobre 4 das 5 categorias da auditoria (estilo, cor, UI, feedback).
