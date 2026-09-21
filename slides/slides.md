---
marp: true
theme: default
paginate: true
header: 'gingaf: Cross-Platform NCL & HTML5 Execution — WebMedia 2026'
---

<style>
.grayscale {
  filter: grayscale(100%);
}
.grid-2x2 {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  grid-gap: 14px 28px;
  width: 100%;
  margin-top: 8px;
}
.grid-3 {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  grid-gap: 18px;
  width: 100%;
  margin-top: 18px;
}
.grid-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
}
.grid-card img {
  width: 100%;
  max-height: 180px;
  object-fit: contain;
  border-radius: 6px;
  border: 1px solid #d0d7de;
  background-color: transparent;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.06);
}
.grid-card p {
  margin: 8px 0 0 0;
  font-size: 20px;
  font-weight: 600;
  line-height: 1.35;
  color: #1f2328;
}
.grid-card a {
  color: #0969da;
  font-weight: 700;
  text-decoration: underline;
}
</style>

<!--
_paginate: false
_header: ""
-->

<div style="display: grid; grid-template-columns: 3fr 1fr; align-items: center;">

<div>

# gingaf: A Cross-Platform Architecture To Execute Ginga-NCL and Ginga-HTML5 Applications

**Alan L. V. Guedes**$^1$, **Paulo Victor Borges**$^2$, **Daniel Moraes**$^2$, **Sergio Colcher**$^2$
$^1$Universidade de Reading, Reino Unido | $^2$PUC-Rio, Brasil

*Anais do Simpósio Brasileiro de Sistemas Multimídia e Web (WebMedia 2026)*
Lavras/MG, Brasil

**Website do Artigo (slides, código, demo)**:
https://alanlivio.github.io/paper-webmedia26-gingaf/

</div>

<div style="display: flex; flex-direction: column; justify-content: center;">

<img src="assets/uor.svg" height="200" class="grayscale" />
<img src="assets/puc-rio.svg" height="120" class="grayscale" />
<img src="assets/qrcode.svg" height="250" />

</div>

</div>

---

# Agenda

- **Contexto e Definição do Problema**
- **Solução Proposta**
- **Funcionalidades e Demo do gingaf**
- **Considerações Finais**

---

<!-- _class: invert -->
<!-- _paginate: skip -->

# Contexto e Definição do Problema

---

# Contexto: O Middleware de DTV Ginga

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Padronização e Alcance**
- Definido pela ITU-T H.761 e SBTVD ABNT 15606.
- Instalado em 100% dos receptores de TV Digital certificados no Brasil e América Latina (>60M telespectadores).

**Evolução dos Subsistemas Ginga**
- **Ginga-NCL**: Sincronização e formatação multimídia declarativa.
- **NCLua**: Programação imperativa e gráficos dinâmicos em canvas.
- **Ginga-HTML5 e CCWS**: Aplicações web com acesso a dados de transmissão (broadcast).

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/ginga.png" />

</div>

</div>

---

# O Problema: Acoplamento à Plataforma

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Reprodutores Pesados em C++**
- Implementações legadas (Ginga v0.13, v1.0 da PUC-Rio) dependem de bibliotecas C++ específicas da plataforma (GTK, GStreamer, FFmpeg).
- Focados em ambientes STB Linux embarcados, impedindo a execução web.

**Apresentação Fortemente Acoplada**
- Avaliações da máquina de estados bloqueiam em chamadas nativas de renderização do SO (`draw()`).
- Objetos de mídia disparam transições NCL diretamente por callbacks de threads do sistema (`onEvent()`).

**Incompatibilidade com a Web**
- Ambientes isolados (sandbox) de navegadores não possuem acesso a sockets brutos nem threads nativas POSIX.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/old_arch.png" />

</div>

</div>

---

<!-- _class: invert -->
<!-- _paginate: skip -->

# Solução Proposta

---

# Arquitetura em Camadas: Desacoplamento de Subsistemas

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Separação Estrita de Subsistemas**
- Componentes de lógica são rigorosamente separados dos componentes de interface (UI).

**Camada de Lógica (Dart Puro)**
- `NCLDocument` (Parser, runtime NCLua) e `CCWS` (HTTPServer, roteador).
- Compila de forma transparente para JavaScript e WebAssembly.

**Camada de Apresentação (Flutter)**
- `NCLWidget` (NCLuaWidget, NCLMediaState) e `HTMLWidget` (webview, js-interop).
- Renderização de alto desempenho e precisão de pixels na Web, desktop e dispositivos móveis.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/layered_arch.png" />

</div>

</div>

---

# Fluxo de Comunicação Arquitetural

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Coordenação Unidirecional**
- `NCLWidget` conduz a execução por meio de chamadas explícitas de `tick()`.
- Nenhuma referência direta é mantida entre `NCLDocument` e os widgets de renderização da UI.

**Sincronização Determinística**
- O motor atualiza estados internos de `Media` na ordem do documento.
- A UI consulta e sincroniza propriedades visuais sob demanda (`syncProperties()`).
- Elimina completamente condições de corrida e conflitos de concorrência de threads nativas.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/arch.png" />

</div>

</div>

---

# Lógica NCL e Modelo de Objetos do Documento (DOM)

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Árvore DOM em Memória**
- Documento XML analisado em uma hierarquia de `Element` e `Node`.
- Subclasses gerenciam estados em tempo de execução: `Media`, `Composition`, `Context`, `Switch`.
- `NCLua` encapsula o runtime Lua embutido.

**Desacoplamento Baseado em Filas**
- `ActionQueue`: Coleta execuções determinísticas de links e mudanças de estado.
- `UIQueue`: Compartilha mudanças de estado entre fronteiras sem acoplar a lógica à renderização.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/elem_tree.png" />

</div>

</div>

---

# NCLua Portável: Pipeline de Tradução para Canvas

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Motor Lua em Dart Puro**
- Incorpora o `lua_dardo` (interpretador Lua 5.3 puro em Dart).
- Executa no navegador sem dependências C externas ou pontes WebAssembly.

**Abstração de Lista de Comandos**
- Chamadas de desenho Lua (`canvas:drawLine()`) são interceptadas pelo NCLua.
- Listas de comandos serializados são despachadas para o `NCLuaWidgetState`.
- O `CustomPainter` do Flutter renderiza os comandos diretamente na tela.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/lua_pipeline.png" />

</div>

</div>

---

# NCLua Portável na Prática

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Gráficos Procedurais Interativos**
- Execução de scripts Lua manipulando formas, textos e animações em tempo real.

**Paridade Multiplataforma**
- Mesma saída visual no WebGL, desktop Windows e dispositivos móveis.

**Corrotinas Assíncronas**
- Mapeia corrotinas Lua para os paradigmas de `Future` e `async/await` do Dart sem bloquear o loop principal (`tick`).

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/playground-lua.png" />

</div>

</div>

---

# Arquitetura Ginga-HTML5 e CCWS

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Clientes Nativos (a)**
- A aplicação HTML executa em WebView nativa.
- `HTTPServer` local embutido na porta 44642 responde a requisições HTTP padrão.

**Cliente Web via Sobrecarga de Fetch (b)**
- Aplicação HTML executa em `iframe` com sandbox.
- Shim injetado sobrecarrega `window.fetch()` e `XMLHttpRequest`.
- Intercepta requisições e faz a ponte para o Flutter via `postMessage`.
- Resolve promises de forma transparente, sem servidor HTTP local ou extensões de navegador.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/ccws_intercept.png" />

</div>

</div>

---

# Ginga-HTML5 na Prática

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Virtualização Completa do CCWS**
- Descoberta em tempo real de serviços de transmissão, informações de programação e metadados de canais.

**Configuração Zero**
- Aplicações HTML5 executam sem servidores web locais ou permissões especiais de navegador.

**Integração Transparente**
- Conteúdo web interativo de broadcast embutido diretamente ao lado de composições NCL declarativas.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/playground-html.png" />

</div>

</div>

---

# Validação: GingaPlayground

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Bancada de Testes Nativa no Navegador**
- Integra o motor web Dart/Flutter do `gingaf` com editor de código Monaco e pré-visualização ao vivo.

**Capacidades Demonstradas**
- Sincronização NCL declarativa (`video.ncl`).
- Renderização gráfica procedural em Lua (`lua_canvas.ncl`).
- Aplicação Ginga-HTML5 com descoberta de serviços CCWS (`current_service.html`).
- Execução interativa instantânea diretamente via URL pública, sem instalação.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/playground.png" />

</div>

</div>

---

<!-- _class: invert -->
<!-- _paginate: skip -->

# Funcionalidades e Demo do gingaf

---

## NCL+links, NCL+grade_de_vídeos, NCL+embNCL e NCL+navegação

<div class="grid-2x2">
  <div class="grid-card">
    <img src="assets/gifs/video.ncl.gif" alt="video.ncl" />
    <p>NCL com links básicos (<a href="https://ginga-org-br.github.io/gingaf/playground/?app=video.ncl">video.ncl</a>)</p>
  </div>
  <div class="grid-card">
    <img src="assets/gifs/video_grid.ncl.gif" alt="video_grid.ncl" />
    <p>NCL com grade de vídeos (<a href="https://ginga-org-br.github.io/gingaf/playground/?app=video_grid.ncl">video_grid.ncl</a>)</p>
  </div>
  <div class="grid-card">
    <img src="assets/gifs/emb_ncl.ncl.gif" alt="emb_ncl.ncl" />
    <p>NCL embutido em NCL (<a href="https://ginga-org-br.github.io/gingaf/playground/?app=emb_ncl.ncl">emb_ncl.ncl</a>)</p>
  </div>
  <div class="grid-card">
    <img src="assets/gifs/focus_nav.ncl.gif" alt="focus_nav.ncl" />
    <p>NCL com navegação de foco e seleção (<a href="https://ginga-org-br.github.io/gingaf/playground/?app=focus_nav.ncl">focus_nav.ncl</a>)</p>
  </div>
</div>

---

## NCLua, HTML+CCWS, NCL+embHTML e NCL+multiusuário

<div class="grid-2x2">
  <div class="grid-card">
    <img src="assets/gifs/lua_canvas.ncl.gif" alt="lua_canvas.ncl" />
    <p>NCL com desenho em tela Lua e teclas (<a href="https://ginga-org-br.github.io/gingaf/playground/?app=lua_canvas.ncl">lua_canvas.ncl</a>)</p>
  </div>
  <div class="grid-card">
    <img src="assets/gifs/current_service.html.gif" alt="current_service.html" />
    <p>HTML com CCWS /current-service/ (<a href="https://ginga-org-br.github.io/gingaf/playground/?app=current_service.html">current_service.html</a>)</p>
  </div>
  <div class="grid-card">
    <img src="assets/gifs/emb_html.ncl.gif" alt="emb_html.ncl" />
    <p>NCL com documento HTML embutido (<a href="https://ginga-org-br.github.io/gingaf/playground/?app=emb_html.ncl">emb_html.ncl</a>)</p>
  </div>
  <div class="grid-card">
    <img src="assets/gifs/multiuser_profile.gif" alt="multiuser_profile/main.ncl" />
    <p>NCL com troca de perfil multiusuário e publicidade direcionada (<a href="https://ginga-org-br.github.io/gingaf/playground/?app=multiuser_profile/main.ncl">multiuser_profile/main.ncl</a>)</p>
  </div>
</div>

---

<!-- _class: invert -->
<!-- _paginate: skip -->

# Considerações Finais

---

# Considerações Finais

- Primeira arquitetura multiplataforma que unifica Ginga-NCL, NCLua e Ginga-HTML5 na Web e no Desktop.
- Interpretador Lua portátil com tradução de canvas para Flutter.
- Interceptação de rede CCWS no lado do cliente por sobrecarga de `fetch`.
- Código-fonte aberto, testes unitários e ambiente interativo web disponibilizados publicamente.

---

<!--
_paginate: false
_header: ""
-->

# Obrigado!

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

### Dúvidas e Discussão

- **Repositório**: https://github.com/ginga-org-br/gingaf
- **Playground**: https://ginga-org-br.github.io/gingaf/playground/
- **Contato**: `a.guedes@reading.ac.uk` | `danielmoraes@telemidia.puc-rio.br`

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/portal1.png" />

</div>

</div>
