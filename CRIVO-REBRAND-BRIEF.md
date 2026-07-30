# Brief — Rebranding do site (template → Crivo Hub · Programa de Mentores Internos)

> Este arquivo é a fonte única da verdade para a troca de conteúdo/cores/tipografia/logo do template
> em `index.html` + `assets/`. Qualquer sessão de chat/agente que for executar o trabalho deve seguir
> este documento à risca antes de inventar texto, cor ou estrutura.

## 0. Regra de ouro

**NÃO alterar o layout.** Isso significa: não mexer em grid/flex, não adicionar ou remover cards/itens
dentro de um bloco, não reordenar seções, não tocar em classes/IDs/scripts (carrosséis, parallax,
contadores, animações GSAP/AOS). Alterar **apenas**:

1. Cores (paleta Crivo).
2. Tipografia (fonte Unbounded).
3. Uso da logo.
4. Todo o conteúdo textual (títulos, parágrafos, menu, formulário, alt text, `<title>`, `lang`).
5. Padding/margin — **só pontualmente**, e só quando o novo texto (mais longo/curto que o original)
   quebrar visualmente um botão, título ou bloco. É ajuste cirúrgico, não redesenho.

Onde não houver dado real disponível (telefone, endereço, redes sociais, fotos dos depoimentos, logos
de clientes em alta resolução), usar um placeholder claramente marcado (`[PLACEHOLDER: ...]`) — **não
parar para perguntar por essas informações específicas: o usuário já sabe que estão faltando e vai
enviá-las depois.** Continue o trabalho normalmente com o placeholder marcado. Para qualquer outra
ambiguidade fora dessa lista conhecida, aí sim pergunte antes de inventar.

---

## 1. Caminhos

- Página: `index.html`
- Assets: `assets/` (`css/`, `js/`, `images/`, `fonts/`)
- Logo Crivo já baixada em: `assets/images/logo-crivo.png` (128×59px, fundo transparente, baixada de
  `https://crivohub.com.br/wp-content/uploads/2025/06/Design-sem-nome-32.png`). É a única resolução
  disponível — se ficar borrada em algum uso maior, pedir ao usuário uma versão em alta
  resolução/SVG antes de forçar upscale.
- Conteúdo textual de origem: `Crivo_Hub_Programa_Mentorias (1).pdf` (13 slides, já transcrito na
  seção 5 abaixo — não é necessário reabrir o PDF).

---

## 2. Cores

Paleta oficial Crivo:

| Nome | Hex |
|---|---|
| Branco | `#ffffff` |
| Laranja Crivo (accent) | `#f18707` |
| Azul Crivo (primary/text) | `#054156` |
| Azul escuro (secondary) | `#022734` |

O template já centraliza a cor principal em variáveis CSS em `assets/css/style.css` (linhas ~71-79):

```css
:root{
  --theme-color: #FF6F0F;      → trocar para #F18707 (laranja Crivo)
  --theme-color-2: #2661FF;    → trocar para #054156 (azul Crivo)
  --secondary-color: #000000;  → trocar para #022734 (azul escuro Crivo)
  --text-color: rgba(0,0,0,0.70); → trocar para rgba(5,65,86,0.75)  /* #054156 com opacidade */
  --title-color: #000000;      → trocar para #054156
}
```

Isso resolve a maior parte, pois `assets/css/color.css` já aplica `var(--theme-color)` em cor de
texto/hover, background e border em ~280 seletores.

**Porém** existem cores hardcoded (hex fixo, fora de variável) em vários `module-css/*.css` usados por
`index.html` — principalmente `banner.css`, `header.css`, `service.css`, `portfolio.css`, `skills.css`,
`clients.css`, `testimonial.css`, `instagram.css`, `contact.css`, `footer.css`. São, tipicamente, os
fundos escuros ("dark mode" do template, tons de preto/cinza) e alguns detalhes de texto/ícone. É
preciso:

1. Buscar por `#` (hex) nesses arquivos.
2. Substituir tons escuros genéricos (pretos/cinzas usados como "dark bg") por `#054156` ou `#022734`
   (mantendo a mesma função visual — se era plano de fundo escuro, continua escuro, só que azul Crivo).
3. Substituir qualquer laranja/azul remanescente do tema antigo pela paleta Crivo.
4. Testar visualmente cada seção depois (contraste de texto branco sobre os novos fundos).

Há também um widget `.demo-switch` (botões de sol/lua para alternar light/dark mode) no topo do body
— é um artefato de demonstração do template, não faz parte da marca Crivo. Recomenda-se remover esse
bloco (é conteúdo/estrutura de demo, não uma feature do produto), mas isso é uma decisão do
executor/usuário — se preferir manter por segurança, apenas garantir que os dois modos usem a paleta
Crivo.

---

## 3. Tipografia

Kit de marca da Crivo usa uma única família em todos os papéis, variando o peso:

```
--e-global-typography-primary-font-family: "Unbounded";  weight 600
--e-global-typography-secondary-font-family: "Unbounded"; weight 400
--e-global-typography-text-font-family: "Unbounded";      weight 400
--e-global-typography-accent-font-family: "Unbounded";    weight 500
```

No template atual, a tipografia é controlada por duas variáveis em `style.css`:

```css
--text-font: 'Satoshi', sans-serif;   → trocar para 'Unbounded', sans-serif
--title-font: 'Outfit', sans-serif;   → trocar para 'Unbounded', sans-serif
```

Passos:

1. No `<head>` de `index.html`, trocar o `<link>` do Google Fonts (atualmente carrega "Outfit") por:
   `https://fonts.googleapis.com/css2?family=Unbounded:wght@400;500;600;700&display=swap`
   (incluir 700 porque alguns elementos usam `font-weight: bold` do navegador).
2. Remover (ou deixar de referenciar) `assets/css/satoshi-font.css`, já que a fonte Satoshi deixa de
   ser usada — não precisa apagar os arquivos de fonte física, só o `<link>` no `<head>`.
3. Depois da troca, checar visualmente títulos grandes (banner, seção de contato) e textos pequenos
   (rodapé, tags de skills) — Unbounded é uma fonte geométrica/display; se algum texto de corpo ficar
   difícil de ler em tamanho pequeno, é aceitável um ajuste pontual de `font-size`/`line-height`
   (entra na regra de "ajuste cirúrgico", não é mudar layout).

---

## 4. Logo

Arquivos atualmente referenciados em `index.html` (buscar por esses nomes):

- `assets/images/logo.png` (light-logo do header, linha ~98)
- `assets/images/logo-2.png` (dark-logo do header, sticky-header e menu mobile — linhas ~99, 190, 221)
- `assets/images/logo-3.png` (logo do rodapé, linha ~712)

Trocar todas as referências para `assets/images/logo-crivo.png`. **Decisão do usuário: usar esta
versão (128×59px) por enquanto, mesmo sendo a única disponível — não bloquear o trabalho por isso.**
Como não há variante clara/branca separada, verificar visualmente se ela mantém contraste tanto em
fundos claros (header padrão) quanto em fundos escuros (footer, dark_bg, se mantidos com fundo azul
escuro). Se sumir/ficar ilegível em algum fundo escuro, é aceitável adicionar um fundo/box sutil atrás
da logo nesse ponto específico (ajuste pontual, permitido pela regra 0.5) — não recriar a logo do
zero e não gerar uma versão reversa por conta própria.

---

## 5. Conteúdo textual — mapeamento seção a seção

O template é uma landing page de portfólio pessoal com 9 blocos fixos, nessa ordem: **header/menu →
banner (hero) → service (3 cards) → portfolio (carrossel de 3) → skills (timeline 3 + awards 2 + tags)
→ clients (logos) → testimonial (carrossel de 3) → instagram (carrossel de imagens) → contact + footer**.

O conteúdo do PDF "Crivo Hub · Programa de Mentores Internos" tem 13 telas. Abaixo, o mapeamento
sugerido — respeitando a quantidade de itens que cada bloco já suporta (não dá pra adicionar um 4º
card num carrossel de 3 sem mexer em CSS/JS de layout).

### 5.1 Header / menu

O menu atual é um mega-menu de demonstração do template com dropdowns para dezenas de páginas que não
existem no projeto (Home, About, Work, Service, Blog...). Como este projeto é uma **página única**
(`index.html`), trocar os itens de menu por âncoras internas da própria página:

- Início
- Contexto
- Formatos
- Resultados
- Como Funciona
- Diferenciais
- Contato

Remover os submenus (dropdowns) que apontam para páginas inexistentes do template (about.html,
portfolio-2.html, blog.html etc.) — isso é limpeza de conteúdo/links, não mudança de layout.

Botão "Let's Talk" do header → **"Fale com a gente"** (usar o mesmo texto em todos os CTAs
equivalentes do site para consistência).

Bloco "Contact Info" do menu mobile (endereço/telefone/email genéricos) → `[PLACEHOLDER]` por enquanto
(dado real vem depois do usuário — não bloquear).

### 5.2 Banner (hero) — Slide 1 do PDF

- Kicker: **"Programa de Mentores Internos"**
- Headline principal (h2): **"Todo mundo tem um lugar para aprender e para ensinar."**
- Quote box (troca a citação "Design tells a story..."): usar o foco do programa (slide 5) como frase
  de apoio: **"Fortalecer uma cultura de aprendizagem colaborativa, fomentar a inteligência coletiva
  por meio da troca de experiências e potencializar as forças de cada participante."**
  Assinatura: **"Lilian Lacanna — Anfitriã de Aprendizagem, Crivo Hub"**
- Campo de e-mail do form: placeholder **"seuemail@empresa.com"**
- Botão: **"Quero saber mais"**

### 5.3 Service-section → "Formatos de mentoria" (Slide 6 — 3 cards, encaixe exato)

- Texto lateral rotacionado "service" → **"formatos"**
- Título: **"Formatos <span>de Mentoria.</span>"**
- Subtítulo: **"Três formatos de atuação, uma mesma crença: todo mundo tem um lugar para aprender e
  para ensinar."**
- Bloco de destaque ("Let's / EXPLORE / ALL.") → **"Vamos / CRIAR / JUNTOS."**
- 3 itens (título em 2 linhas + link "Explore More" → "Saiba mais"):
  1. **"Mentoria <br/>entre pares"** — colaboração horizontal real, troca entre times, rede interna
     mais forte.
  2. **"Mentoria <br/>Cruzada"** — aceleração de carreira, orientação prática, clareza de objetivos.
  3. **"Mentoria <br/>reversa"** — liderados ensinam líderes: novas perspectivas, menos pontos cegos.

### 5.4 Portfolio-section → "Resultados que a Crivo já entregou" (Slide 7 — carrossel de 3, encaixe exato)

- Texto lateral "Work" → **"Resultados"**
- Título: **"Resultados <span>que já entregamos.</span>"**
- Subtítulo: **"Programas de mentoria com impacto medido em engajamento, retenção e performance."**
- 3 cards (título + parágrafo):
  1. **"Grupo Fleury — 4,75/5 de avaliação média"** — "Ganhos consistentes em autoconfiança,
     comunicação, posicionamento estratégico, liderança humanizada, escuta ativa e colaboração."
  2. **"Assaí — 3 promoções a gerente regional"** — "Otimização do aprendizado, aumento da integração
     entre líderes e fortalecimento de competências essenciais para crescimento na carreira."
  3. **"Ajinomoto Brasil — 16x mais faturamento em um dos projetos"** — "Mentoria como parte do
     programa de protagonismo da liderança. Resultado: destaque internacional em resultado e
     inovação."

As imagens do carrossel (`portfolio-1/2/3.png`) são fotos de estoque decorativas do template — trocar
por logos/fotos reais dos clientes é opcional/nice-to-have, não obrigatório (pedir ao usuário se
quiser essa camada extra).

### 5.5 Skills-section → "Contexto e Preparo" (Slides 2, 3, 8 e 10)

Este bloco tem 3 sub-áreas fixas: timeline de 3 itens (ano/título/empresa), 2 "prêmios" (número/texto/ano)
e uma lista de tags (~7-8 + botão "& more…"). Reaproveitar como estatísticas + competências:

- Título da seção: **"Contexto <span>e Preparo.</span>"**
- Coluna esquerda "Experience" → **"Por que agora"**, 3 itens reaproveitando os campos
  ano/título/empresa como número/categoria/detalhe:
  1. **83%** · Geração Z · "diz que mentoria é essencial para o sucesso"
  2. **98%** · Fortune 500 · "já usam mentoria hoje (eram 25% em 2007)"
  3. **2x** · Mais lucro · "em empresas com programas estruturados de mentoria"
- Coluna direita "Award & Achievement" → **"Impacto comprovado"**, 2 itens:
  1. **97%** — "dos mentores desenvolvem habilidades verificáveis de liderança" (fonte: Mentorloop)
  2. **84%** — "dos CEOs dizem que a mentoria ajuda a evitar erros caros" (fonte: Harvard Business
     Review)
- Bloco inferior "Skills" → **"Competências trabalhadas com os mentores"**, tags (slide 10):
  1. Papéis do mentor
  2. Contexto atual
  3. Neurociência da autossabotagem
  4. Roda de competências
  5. Engajamento do mentorado
  6. Problem Learning Canvas
  7. Escuta ativa
  - Botão final "& more…" → **"& mais…"** (mantém a função JS de expandir, só troca o texto)

### 5.6 Clients-section (logos em carrossel)

O PDF cita 3 clientes nominalmente: **Grupo Fleury, Assaí, Ajinomoto Brasil**. O bloco atual espera
~10-15 arquivos de logo repetidos em loop. Os logos reais desses clientes ainda não foram enviados
(o usuário vai enviar depois) — **por enquanto**, trocar os `<img>` por wordmarks em texto simples com
o nome dos clientes (Grupo Fleury / Assaí / Ajinomoto Brasil, repetidos no loop como já é hoje), sem
bloquear o trabalho. Pode exigir pequeno ajuste de padding/alinhamento vertical dentro do `<li>`,
permitido pela regra 0.5. Quando os arquivos de logo chegarem, é só substituir os `<img>` de volta em
`assets/images/clients/clients-*.png`.

**Não inventar/gerar logos.**

### 5.7 Testimonial-section → "Histórias incríveis" (Slide 9 — carrossel de 3, encaixe exato)

1. **Letícia Mendes Morais Leite** — Mentorada · Grupo Fleury
   "Levo dessa experiência um grande aprendizado sobre autoconhecimento, confiança e protagonismo. A
   mentoria me ajudou a enxergar capacidades que muitas vezes eu mesma não reconhecia."
2. **André Gervásio** — Mentor · Grupo Fleury
   "Todos os momentos foram marcantes e muito bem sentidos de ambas as partes. Na penúltima sessão, a
   mentorada terminou o agradecimento em lágrimas pela mudança de comportamento frente ao que
   buscamos."
3. **Normando Filho** — Diretor executivo · Ajinomoto Brasil
   "Os participantes agora estão mais abertos, prontos e dispostos para desafios grandes e diferentes
   porque confiam mais em si e nos outros. Um dos projetos passou de R$ 30 mil para R$ 500 mil, depois
   R$ 1 milhão, e fechou o ano com R$ 10 milhões de faturamento."

Fotos (`testimonial-1.jpg` etc.) são de estoque — manter como placeholder genérico por enquanto; o
usuário vai enviar as fotos reais depois (não bloquear, e não inventar/gerar rostos de pessoas reais).

### 5.8 Instagram-section (carrossel de imagens, sem legenda por item)

Esta é a seção com menor aderência ao conteúdo do PDF, pois estruturalmente só comporta um título +
imagens (sem espaço de texto por slide). Sugestão: reaproveitar como **"Siga a Crivo Hub"**, apontando
para o Instagram/site real da Crivo. Por enquanto, manter as imagens atuais do template como
placeholder (não bloquear); quando o usuário enviar imagens de marca da Crivo, substituir
`assets/images/resource/instagram-1/2/3.jpg` por elas.

- Título: **"Siga a <span>Crivo Hub.</span>"**

### 5.9 Contact-section → CTA final (Slide 13 — Propósito)

- Texto lateral "Let's talk" → **"Vamos<br/>conversar"**
- Título: **"Vamos fazer esse <span class="color-text">movimento juntos!</span>"**
- Botão de destaque ("Let's / Rock & Roll") → **"Fale / com a Crivo"**
- Form: label "Name*" → **"Nome*"**; "Email*" → **"E-mail*"**; textarea "Describe Your Project" →
  **"Conte sobre sua empresa e o objetivo com a mentoria"**; botão "Let's Talk" → **"Enviar mensagem"**
- Coluna de info (3 itens ícone+label+valor): e-mail/telefone reais da Crivo ainda não foram enviados
  — usar `[PLACEHOLDER]` por enquanto, sem bloquear. O 3º item (atualmente "Office"/endereço) pode
  virar **"Site"** apontando para `https://crivohub.com.br/` (esse já é real, pode usar direto).
- "Find Me on Google Map" → **"Conheça a <a href="https://crivohub.com.br/">Crivo Hub</a>"**

### 5.10 Footer

- Copyright: **"© 2026 Crivo Hub. Todos os direitos reservados."**
- Logo: `logo-crivo.png`
- Social links: perfis reais das redes sociais ainda não foram enviados — por enquanto, apontar os
  links para `https://crivohub.com.br/` como fallback (não bloquear); trocar pelos perfis reais quando
  o usuário enviar.

---

## 6. Outros ajustes de conteúdo (não visuais)

- `<html lang="en">` → `<html lang="pt-BR">`
- `<title>Potu - HTML 5 Template Preview</title>` → **`Crivo Hub · Programa de Mentores Internos`**
- Qualquer texto remanescente do template genérico (nomes fictícios "Jon Kabir", "Rashed Kabir",
  "rakabir.com", "Chicago 12, Melborne City", `alt=""` vazios em imagens de conteúdo) deve ser
  substituído ou preenchido — não pode sobrar texto de placeholder do template original.

---

## 7. Checklist de aceite

- [ ] Nenhuma mudança em grid/flex/ordem de seções/número de cards — só CSS de cor/fonte + textos.
- [ ] `--theme-color`, `--theme-color-2`, `--secondary-color`, `--text-color`, `--title-color` em
      `style.css` usando a paleta Crivo.
- [ ] Hex hardcoded remanescentes nos `module-css/*.css` revisados e alinhados à paleta Crivo.
- [ ] Fonte Unbounded carregando via Google Fonts e aplicada em `--title-font` e `--text-font`.
- [ ] Logo Crivo em todos os pontos (header, sticky-header, menu mobile, footer).
- [ ] Nenhum texto genérico do template (Jon Kabir, Lorem, rakabir.com...) restante.
- [ ] Todo texto novo em português, condizente com o PDF da Crivo.
- [ ] Onde faltou dado real (telefone, endereço, redes sociais, fotos, logos de clientes), há
      `[PLACEHOLDER]` visível — nada foi inventado, e o trabalho não ficou bloqueado por isso.
- [ ] Site testado visualmente no navegador (desktop e mobile) sem erros de console.

---

## 8. Pendências conhecidas (usuário vai enviar depois)

Estes itens já estão cientes e **não devem gerar perguntas** — só usar placeholder e seguir:

- [ ] Logos reais de Grupo Fleury, Assaí e Ajinomoto Brasil (seção clients).
- [ ] Fotos reais dos 3 depoimentos: Letícia Mendes Morais Leite, André Gervásio, Normando Filho
      (seção testimonial).
- [ ] Telefone e e-mail de contato reais da Crivo (banner e seção contact).
- [ ] Endereço (se aplicável) e perfis reais de redes sociais (footer e menu mobile).
- [ ] Eventualmente, uma versão em resolução maior/vetor da logo (hoje só há a de 128×59px).

Quando o usuário mandar esses arquivos/dados, é só substituir os placeholders marcados nas seções 5.6,
5.7, 5.9, 5.10 e 4.
