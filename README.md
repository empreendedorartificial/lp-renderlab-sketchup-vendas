# LP RenderLAB — Vendas pós-live (IA no SketchUp)

Página de VENDAS da assinatura do RenderLAB pra fase pós-live do lançamento da integração com o SketchUp. Cópia adaptada da `lp-renderlab-evento-sketchup/` (a página de captação original segue no ar e intocada). Identidade RenderLAB estrita (design guide em `marca/renderlab/`), logo RENDERLAB AI canônica.

## Deploy

**Tipo C** (worker + static assets em `public/`): `npx wrangler deploy` nesta pasta. Push NÃO publica.
**Domínio:** https://sketchup.montani3d.com.br/ (aprovado 13/07; workers.dev segue ativo como prévia).
**Repo:** https://github.com/empreendedorartificial/lp-renderlab-sketchup-vendas

## Estrutura da página

Hero (instale agora) → prova (2.000+, dentro do SketchUp, ~30s, tour 360 no WhatsApp) → **OFERTA DE LANÇAMENTO** (Starter Anual de R$1.970 por R$1.470) → **PLANOS** (Starter/Growth, toggle mensal/anual; Basic removido a pedido do Thiago em 14/07) → vídeo da integração → funcionalidades (tabs) → pra quem é → quem criou → FAQ de vendas → CTA final. Sem formulário, sem MailerLite/ManyChat, sem `confirmado.html`.

## Tracking e atribuição (crítico)

- Meta Pixel `2428536680685666` no `<head>`; `InitiateCheckout` (com `value` do plano) no clique de qualquer CTA.
- CTAs vão DIRETO pros payment links da Stripe (nunca pro renderlab.club, que não captura UTM).
- Cada link sai com `?client_reference_id=lpsk--<utm_content>` (sanitizado `[a-z0-9-]`, cortado em 60 chars; sem `utm_content` vira `lpsk-organico`). UTMs ficam em `sessionStorage` (`mnt_utm`) e sobrevivem à navegação.
- O worker `financeiro-sync` grava o `client_reference_id` na `stripe_atrib` do D1 e o painel mostra em "Origem das vendas".
- ⚠️ **A atribuição marca a PRIMEIRA venda** (comportamento do `stripe_atrib`); renovações de assinatura não carregam origem.

## Payment links (objeto `LINKS` no fim do index.html)

| Plano | Preço | Link |
|---|---|---|
| Starter mensal | R$197 | `7sY3cvba5fgv6AIe0ZeIw0h` |
| **Starter anual PROMO** | **R$1.470** | `bJeaEX4LH6JZbV2bSReIw0n` (plugado 14/07) |
| Growth mensal | R$397 | `aFa14n4LHfgvcZ6aONeIw0f` |
| Growth anual | R$3.970 | `6oUbJ16TPgkzf7ebSReIw0e` |

O Starter anual regular (R$1.970) NÃO aparece na página: no anual, o card do Starter usa a oferta de R$1.470, igual à seção da oferta.

## Pendência

Replay da live: embed VTurb `vid-6a559c5fbb9552173c6abb02` na seção do replay, funcionando (validado 14/07 após publicação do player na VTurb). Página sem pendências.

Decisões de 13/07: prazo da oferta é só "encerra em breve" (sem data, sem cronômetro); FAQ inclui resposta neutra sobre SketchUp não original (funciona, recomendação é usar o original).
