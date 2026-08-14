# Rainha da Sorte — Landing Page

Landing page mobile-first do Rainha da Sorte, aplicativo de análise de resultados de roleta.

## Estrutura

```
index.html          página completa (HTML + CSS + JS inline)
hero.jpg            imagem original da hero (fonte, não usada em produção)
assets/hero.webp    hero otimizada — 103 KB (formato servido)
assets/hero.jpg     hero otimizada — 330 KB (fallback)
```

Sem build e sem dependências: é só publicar a pasta em qualquer host estático
(GitHub Pages, Vercel, Netlify, Cloudflare Pages).

## Rodando localmente

```bash
python3 -m http.server 8000
# abra http://localhost:8000
```

## Rastreamento

Google Tag Manager `GTM-PVBZQ4FW` (script no `<head>` e `noscript` no início do `<body>`).

Cada CTA dispara um evento no `dataLayer`:

```js
{ event: 'clique_cta', local_cta: 'hero', destino_cta: 'telegram' }
```

Valores de `local_cta`: `hero`, `cta_final`, `barra_fixa`, `rodape_telegram`, `rodape_instagram`.

No GTM, crie um acionador de **Evento personalizado** com o nome `clique_cta` e
variáveis de camada de dados para `local_cta` e `destino_cta`.

## Links

Os CTAs apontam para o grupo do Telegram. Para trocar por um checkout ou pelo link
do app, procure o comentário `TODO` no `index.html` e substitua os `href`.

## Aviso

Conteúdo destinado a maiores de 18 anos. O aviso legal no rodapé deixa explícito que
as indicações são informativas e não garantem resultado ou retorno financeiro —
manter esse texto ajuda na aprovação de anúncios em Meta e Google.
