# Site HS Eletric Performance

Página única em HTML, CSS e JS puros, mobile first, sem build e sem dependências.

```
index.html               a página (CSS e JS ficam dentro dela de propósito: nada bloqueia a renderização)
assets/fonts/            Barlow e Barlow Condensed em woff2, hospedadas no próprio site
assets/img/              logos em SVG, foto da instalação (AVIF, WebP e JPG), logo 512 px para o Google
favicon.ico, favicon.svg, apple-touch-icon.png, icon-*.png, site.webmanifest
og-image.jpg             prévia do link no WhatsApp, Facebook e LinkedIn (1200 × 630)
robots.txt, sitemap.xml
_headers                 cache para Netlify e Cloudflare Pages (os outros hosts ignoram)
```

Para testar localmente: `python3 -m http.server 8080` dentro da pasta e abrir `http://localhost:8080`.

## Antes de publicar

1. **Domínio.** O site está configurado para `https://www.hseletricperfomance.com`. No Netlify, adicione esse domínio em Domain management e deixe o `www` como domínio principal: o `hseletric.netlify.app` passa a redirecionar para ele. Se o domínio mudar um dia, troque o endereço (sem a barra final) nestes lugares:
   - `index.html`: `canonical`, `og:url`, `og:image` e os `@id`, `url`, `logo` e `image` dos dois blocos JSON-LD (11 ocorrências)
   - `robots.txt`: linha `Sitemap:`
   - `sitemap.xml`: `<loc>`
2. **Textos.** Confira com o eletricista o que foi escrito em nome da empresa: cidades atendidas (texto, FAQ e `areaServed` no JSON-LD), normas citadas (NBR 5410 e NBR 17019), proteções do circuito (disjuntor, DR, DPS) e as três etapas do atendimento.
3. **Logo.** Foi vetorizada a partir do post do Instagram: o "HS" foi traçado e o texto "ELETRIC PERFORMANCE" foi recomposto em fonte serifada equivalente (Times). Com o arquivo original, substitua `assets/img/logo-hs*.svg` e os ícones.
4. **Foto.** A foto do topo foi recortada do mesmo post. Fotos originais das instalações ficam melhores; mantenha o nome do arquivo ou atualize o `<picture>` do hero.

## WhatsApp

Todos os botões são links `https://wa.me/5547984152765?text=...` com mensagem pronta, e cada um tem um `data-origem` (cabeçalho, hero, serviço, botão fixo, contato, rodapé). Para trocar o número:

```sh
sed -i 's/5547984152765/55DDDNUMERO/g' index.html
```

O número também aparece como texto em três lugares, em `(47) 98415-2765`, e no JSON-LD (`telephone`).

## FAQ e dados estruturados

As perguntas aparecem na página e no JSON-LD `FAQPage` do `<head>`. Se mudar uma, mude a outra: o Google exige que os dados estruturados batam com o texto visível. Hoje o Google só mostra o FAQ em destaque para poucos tipos de site, mas o conteúdo continua ajudando em buscas longas ("precisa aumentar carga na Celesc para carregador") e em respostas de IA.

## Publicar

Qualquer hospedagem estática com HTTPS serve: Cloudflare Pages, Netlify, GitHub Pages ou Vercel. Domínio `.com.br` pelo registro.br.

## SEO local: o que depende de fora do site

O site resolve a parte técnica (velocidade no celular, títulos, dados estruturados, conteúdo). Para aparecer primeiro em "carregador carro elétrico Blumenau" ou "eletricista Blumenau", estes itens pesam tanto quanto ele:

1. **Perfil da Empresa no Google** (business.google.com). É o que aparece no mapa, acima dos resultados comuns. Categoria principal "Eletricista", serviços cadastrados (instalação de carregador para veículo elétrico, projeto luminotécnico, manutenção industrial), área de atendimento com as cidades, telefone, link para o site e fotos reais das instalações.
2. **Avaliações no Google.** Com mais de 200 carregadores instalados, pedir avaliação para os clientes é a ação de maior retorno. Responder todas.
3. **Google Search Console.** Verificar o domínio e enviar o `sitemap.xml`. O Bing Webmaster Tools importa a configuração do Search Console.
4. **Mesmos dados em todo lugar.** Nome, telefone e cidade iguais no site, no Google, no Instagram e em diretórios.
5. **Links para o site.** Bio do Instagram (@hs_eletric_performance, que já está no rodapé e no `sameAs` do JSON-LD), Perfil do Google e, se possível, as concessionárias Volvo e GWM da região indicando a HS como credenciada.
6. **Conteúdo real com o tempo.** Fotos de instalações com a cidade no texto alternativo e, quando houver material, páginas específicas (por cidade ou por marca de carro).

## Medir os contatos

Com Google Analytics 4 (gtag) ou Google Tag Manager instalado, cada clique no WhatsApp dispara o evento `contato_whatsapp` com o parâmetro `origem`. Marque esse evento como evento-chave no GA4 para ver quantos contatos o site gera e de qual botão.
