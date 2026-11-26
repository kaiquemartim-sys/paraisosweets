# Paraíso Sweets | Mini site para link da bio

Site estático (só HTML e CSS, sem JavaScript) em que a página inteira é o flyer.
Áreas clicáveis invisíveis ficam por cima dos botões da imagem.

```
paraiso-sweets/
  index.html
  css/style.css
  assets/img/flyer.jpg   (flyer, 941 x 1671 px)
  assets/img/logo.png    (favicon, gerado a partir do logo do flyer)
  README.md
```

## 1. Links configurados

| Área do flyer | Destino |
|---|---|
| Logo | Instagram |
| Botão "Nossos Doces" | Instagram |
| Botão "Encomendas" | WhatsApp |
| Botão "Avaliações" | **falta o link** (veja abaixo) |
| Botão "Nossa Localização" | Google Maps (busca) |
| Botão grande "Faça já sua encomenda!" | WhatsApp |
| "Surubim - PE \| Delivery" | Google Maps (busca) |
| "@paraiso_sweets" | Instagram |

- **WhatsApp:** `https://wa.me/5581981811992` com a mensagem pronta
  "Olá! Vim pelo seu Instagram e gostaria de fazer um pedido."
- **Instagram:** `https://www.instagram.com/paraiso_sweets/`
- **Avaliações:** o flyer não mostra esse link. No `index.html`, procure por
  `SEU-LINK-AVALIACOES-AQUI` e cole o link das avaliações (por exemplo, a página
  da loja no Google).
- **Mapa:** abre uma busca por "Paraíso Sweets Doceria Surubim PE". Para apontar
  para a loja exata, abra o local no Google Maps, copie o link de "Compartilhar" e
  cole no `href` das áreas `.hit--loc` e `.hit--delivery`.

Para trocar o número de WhatsApp, use "Localizar e substituir" no `index.html` em
`5581981811992` (3 ocorrências). O formato é 55 + DDD + número, só dígitos.

Para mudar a mensagem pronta, substitua o texto depois de `?text=` (2 ocorrências no
`index.html`) por outro texto codificado em URL. Use qualquer "URL encoder" online.

## 2. Ver no computador

Dê dois cliques no `index.html`. Para simular o celular, aperte F12 no navegador e
ative o modo dispositivo (ex.: iPhone 14 Pro).

Opcionalmente, com Python instalado, rode dentro da pasta do site:

```
python -m http.server 8000
```

e acesse http://localhost:8000.

## 3. Publicar no GitHub Pages

1. Crie uma conta em github.com e um repositório público novo (ex.: `paraiso-sweets`).
2. "Add file" > "Upload files", arraste o **conteúdo** da pasta (`index.html`, `css`,
   `assets`, `README.md`) e confirme em "Commit changes". O `index.html` precisa ficar
   na raiz do repositório.
3. Em **Settings > Pages**, escolha **Deploy from a branch**, branch `main`,
   pasta `/ (root)` e clique em Save.
4. Em 1 a 2 minutos o site fica em `https://SEU-USUARIO.github.io/paraiso-sweets/`.
5. Cole esse endereço no campo "Link" do perfil do Instagram.

## 4. Publicar na Vercel

1. Crie conta em vercel.com (pode entrar com o GitHub).
2. Com o site no GitHub: "Add New > Project", escolha o repositório e clique em Deploy
   (Framework Preset: Other, sem build command).
3. Sem GitHub: instale o Node.js e rode dentro da pasta do site `npx vercel`,
   aceitando os padrões com Enter. Para produção, `npx vercel --prod`.

O endereço final será algo como `https://paraiso-sweets.vercel.app`.

## 5. Editar links e posição das áreas

**Links:** no `index.html`, cada área é uma âncora `<a class="hit ...">`. Altere o
`href` e o `aria-label` (texto lido por leitores de tela).

**Posição e tamanho:** no `css/style.css`, cada área tem uma linha como:

```
.hit--wa { left: 19.022%; top: 77.738%; width: 61.955%; height: 6.164%; }
```

Os valores são porcentagens da imagem (941 x 1671 px):

```
left   = x do canto esquerdo / 941  * 100
top    = y do canto superior / 1671 * 100
width  = largura do botão    / 941  * 100
height = altura do botão     / 1671 * 100
```

Para enxergar as áreas enquanto ajusta, adicione temporariamente no CSS:

```
.hit { outline: 2px solid blue; }
```

Remova a linha depois.

| Classe | Onde fica | Destino |
|---|---|---|
| `.hit--logo` | logo | Instagram |
| `.hit--doces` | "Nossos Doces" | Instagram |
| `.hit--enc` | "Encomendas" | WhatsApp |
| `.hit--aval` | "Avaliações" | link a preencher |
| `.hit--loc` | "Nossa Localização" | Google Maps |
| `.hit--wa` | "Faça já sua encomenda!" | WhatsApp |
| `.hit--delivery` | "Surubim - PE \| Delivery" | Google Maps |
| `.hit--ig` | "@paraiso_sweets" | Instagram |

**Trocar o flyer:** substitua `assets/img/flyer.jpg`, atualize `width` e `height` da
tag `<img>`, o `alt` e as porcentagens das áreas. Se a nova imagem não for vertical
9:16, revise também o bloco `@media (max-aspect-ratio: 9/16)` do CSS.

## Como funciona o preenchimento em telas altas

Em celulares mais compridos que o flyer, o espaço que sobra em cima e embaixo é
preenchido com as bordas do próprio flyer, espelhadas, desfocadas, levemente
escurecidas e com degradê (pseudo-elementos `::before` e `::after` do `.page`), sem
barras chapadas. O site também respeita a área segura do iPhone (`safe-area-inset`).
