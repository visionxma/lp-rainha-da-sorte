# Rainha da Sorte — Landing Page

Landing page mobile-first do Rainha da Sorte, aplicativo de análise de resultados de roleta.

**No ar:** https://rainhadasorte.jogadorpro.com/

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

### Pixel & Link Manager

Primeiro script do `<head>`, antes de qualquer outro rastreador. Ele carrega os pixels
cadastrados no painel para o domínio atual e intercepta os links de WhatsApp/Telegram,
mandando-os para o rotacionador de grupos.

- Domínio cadastrado: `rainhadasorte.jogadorpro.com`
  (site id `4d97e554-41c1-4025-b5be-6a5fe8e0cfb2`)
- Pixels cadastrados para o domínio: **nenhum** até o momento — enquanto não houver,
  o console mostra `Pixels encontrados: 0` e nenhum pixel é carregado.

O interceptador chama `stopImmediatePropagation()` nos links do Telegram. Por isso o
listener do `dataLayer` (abaixo) está registrado na **fase de captura** — do contrário
o evento `clique_cta` deixaria de disparar.

### Google Tag Manager

Container `GTM-PVBZQ4FW`: script no `<head>` (depois do Pixel Manager) e `noscript` no
início do `<body>`.

> Não cadastre esse mesmo container como pixel `google_tag_manager` no painel: ele
> carregaria duas vezes e os eventos contariam em dobro.

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
