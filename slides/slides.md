---
marp: true
theme: default
paginate: true
header: 'gingaf: Cross-Platform NCL & HTML5 Execution — WebMedia 2026'
style: |
  @import url('https://cdn.jsdelivr.net/gh/alanlivio/marp-utils@v0.1/marp-utils.css');
  .cols-4 ul {
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
    align-items: end;
    margin-top: 24px !important;
  }
  .contrib-grid ul {
    display: grid !important;
    grid-template-columns: repeat(4, 1fr);
    gap: 14px;
    list-style: none !important;
    padding: 0 !important;
    margin-top: 10px !important;
  }
  .contrib-grid li {
    border: 1.5px solid #d0d7de;
    border-radius: 8px;
    padding: 12px 14px;
    background: #ffffff;
    margin: 0 !important;
    font-size: 20px;
  }
  .contrib-grid li.highlight {
    background: #ddf4ff;
  }
  .contrib-grid li.dimmed {
    background: #f6f8fa;
    opacity: 0.6;
  }
---

<!--
_paginate: false
_header: ""
_class: cols-3-1 vcenter
-->

- # gingaf: A Cross-Platform Architecture To Execute Ginga-NCL and Ginga-HTML5 Applications

  **Alan L. V. Guedes**$^1$, **Paulo Victor Borges**$^2$, **Daniel Moraes**$^2$, **Sergio Colcher**$^2$
  $^1$University of Reading, UK | $^2$PUC-Rio, BR

  *Anais do Simpósio Brasileiro de Sistemas Multimídia e Web (WebMedia 2026)*
  Lavras/MG, BR

  **Website do Artigo (slides, código, demo)**:
  https://alanlivio.github.io/paper-webmedia26-gingaf/

- ![h:160 grayscale](assets/uor.svg)

  ![h:100 grayscale](assets/puc-rio.svg)

  ![h:200](assets/qrcode.svg)

---

# Spoiler Alert!

## Esta apresentação vai para o Guinness Book de 2027 💪

![center w:450](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ2S0TQNZ9hLSSAZlZ4PNTKgmKhCihdzZTAewErSnXD4w&s)

---

<!-- _class: invert -->
<!-- _paginate: skip -->

# Contexto e Definição do Problema

---

<!-- _class: grid-2x2 center -->

# O Middleware de DTV Ginga

- ![h:180](assets/Picture1.png)

- ![h:180](assets/Picture2.jpg)

- ![h:180](assets/Picture3.png)

- ![h:180](assets/Picture4.jpg)

Definido na série de normas SBTVD ABNT 15606. Presente em receptores de TV Digital certificados no Brasil e América Latina (>60M telespectadores).

---

<!-- _class: cols-2 vcenter -->

# Ecossistema de Desenvolvimento Ginga é limitado

**Ausência de ambiente portátil e "zero-install"**: de fácil acesso, completo e aberto.
Podemos comparar o Mozilla (https://developer.mozilla.org/) e a Ginga-VM (2010)

- ![w:500](assets/image.png)

- ![w:500](assets/image-1.png)

---

# Ecossistema de Desenvolvimento Ginga é limitado

**Um fator é a escolha da Engine Gráfica** (e.g., DirectFrameBuffer, FFmpeg, GStreamer, Browsers)

**Outro fator é a complexidade de certos componentes do Ginga**: NCLua (C-based lua engine), Ginga-HTML5 (chromium, webkit) e Ginga-CC-Webservices (HTTP server).

![center w:600](assets/ginga.png)

---

<!-- _class: cols-3 center -->

# Implementações do Ginga na Literatura

- **1998 — PUC-Rio (Netscape)**

  [Rodrigues et al. 1998]

  ![h:170](assets/ginga-netscape.png)

  Plugin para navegador Netscape no início da WWW.

  <span style="color: #cf222e; font-weight: 700;">browser-only · sem Lua</span>

- **2001 — PUC-Rio (Java AWT)**

  [Rodrigues et al. 2001]

  ![h:170](assets/ginga-java.png)

  Ferramentas de exibição hipermídia sobre Java AWT.

  <span style="color: #cf222e; font-weight: 700;">desktop-only · sem Lua</span>

- **2010 — PUC-Rio (C++ & FFmpeg)**

  [Soares et al. 2010]

  ![h:170](assets/ginga-ffmpeg.png)

  Middleware declarativo com backend FFmpeg para IPTV/DTV.

  <span style="color: #cf222e; font-weight: 700;">desktop-only</span>

---

<!-- _class: cols-3 center -->

# Implementações do Ginga na Literatura

- **2012 — UFSCar (WebNCL)**

  [Melo et al. 2013]

  ![h:170](assets/webncl.png)

  Apresentador web puramente em JavaScript.

  <span style="color: #cf222e; font-weight: 700;">browser-only · sem Lua</span>

- **2018 — PUC-Rio (C++ & GStreamer)**

  [PUC-Rio / Telemídia]

  ![h:170](assets/ginga-gst.png)

  Reimplementação C++ com `tick()` e GStreamer.

  <span style="color: #cf222e; font-weight: 700;">desktop-only · sem CCWS</span>

- **2018–2020 — Sidia NuGinga (NodeJS)**

  [Braga et al. 2018; Nogueira et al. 2020]

  ![h:85](assets/nuginga1.png) ![h:85](assets/nuginga2.png)

  Middleware JS/Android e ferramenta web Playcode.

  <span style="color: #cf222e; font-weight: 700;">browser-only · sem CCWS</span>

---

# Implementações do Ginga na Literatura

<div class="cols-3 spread vcenter">

- **PUC-Rio (Java AWT)**
  **PUC-Rio (C++, FFmpeg)**
  **PUC-Rio (C++, GStreamer)**

-

- **PUC-Rio (Netscape)**
  **UFSCar (WebNCL)**
  **Sidia NuGinga (NodeJS)**

</div>

<div class="cols-3 spread vcenter">

- **Native**
  ![h:95](assets/setupbox.png) ![h:95](assets/pc.png)

-

- **Browser**
  ![h:75](assets/browsers.png)

</div>

---

<!-- _class: invert -->
<!-- _paginate: skip -->

# Solução Proposta

---

<!-- _class: grid-2x2 -->

# Solução Proposta: gingaf

As principais decisões de design são:

- **1. Engine Gráfica Multiplataforma**
  Código único em Dart/Flutter para execução consistente na Web, Desktop e Mobile.

- **2. UI e Modelos Desacoplados**
  Lógica (`NCLDocument`) independente e isolada de rendering.

- **3. Relógio Virtual**
  Avanço temporal determinístico orquestrado via `tick()`, eliminando condições de corrida.

- **4. NCLua e CCWS Portáveis**
  Runtime Lua puro em Dart e virtualização de rede sem dependências nativas.

---

<!-- _paginate: hold -->

# 1. Engine Gráfica Multiplataforma

<div class="cols-3 spread vcenter">

- **PUC-Rio (Java AWT)**
  **PUC-Rio (C++, FFmpeg)**
  **PUC-Rio (C++, GStreamer)**

- <span style="font-size: 30px; font-weight: 800; color: #0969da;">gingaf (ours)</span>
  <span style="font-size: 18px; font-weight: 700; color: #0969da;">Ginga-NCL + Ginga-HTML5</span>

- **PUC-Rio (Netscape)**
  **UFSCar (WebNCL)**
  **Sidia NuGinga (NodeJS)**

</div>

<div class="banner">

![](assets/dart.svg) **Dart** ![](assets/flutter.svg) **Flutter**

</div>

<div class="cols-3 spread vcenter">

- **Native**
  ![h:95](assets/setupbox.png) ![h:95](assets/pc.png)

-

- **Browser**
  ![h:75](assets/browsers.png)

</div>

---

<!-- _class: cols-4 center -->

# 1. Engine Gráfica Multiplataforma

- ![h:280](assets/gifs/windows.gif)
  **Windows**

- ![h:280](assets/gifs/chrome.gif)
  **Chrome**

- ![h:280](assets/gifs/android.gif)
  **Android**

- ![h:280](assets/gifs/cli.gif)
  **CLI**

---

<!-- _class: cols-2 vcenter -->

# 2. UI e Modelos Desacoplados

- **Camada de Lógica (Dart Puro)**
  `NCLDocument` (Parser, runtime NCLua) e `CCWS`. Compila para JavaScript e WebAssembly.

  **Camada de Apresentação (Flutter)**
  `NCLWidget` e `HTMLWidget` (webview, js-interop). Renderização com precisão de pixels na Web, desktop e mobile.

- ![h:400](assets/layered_arch.png)

---

<!-- _class: cols-2 vcenter -->

# 3. Relógio Virtual

## Implementações Anteriores Sem Relógio Virtual

- **Acoplamento Temporal**
  Tempo atrelado ao relógio e threads do SO.

  **Bloqueio por Renderização**
  Máquina de estados bloqueada por chamadas `draw()`.

  **Eventos Nativos**
  Transições disparadas via `onEvent()` nativo.

- ![h:380](assets/old_arch.png)

---

<!-- _class: cols-2 vcenter -->

# 3. Relógio Virtual

- **Coordenação por `tick()`**
  O `NCLWidget` avança o relógio virtual por pulsos explícitos.

  **Desacoplamento de UI**
  Sem referência direta entre `NCLDocument` e widgets da UI.

  **Sincronização Determinística**
  Estados de `Media` atualizados na ordem do documento, e a UI obtém propriedades via `syncProperties()` sem condições de corrida.

- ![h:380](assets/arch.png)

---

<!-- _class: cols-2 vcenter -->

# 4. NCLua Portável

- **Motor Lua em Dart Puro**
  `lua_dardo` (Lua 5.3) na Web sem dependências C ou Wasm.

  **Abstração de Comandos e Corrotinas**
  Chamadas `canvas` despachadas para o `CustomPainter` do Flutter, e corrotinas mapeadas para `async/await` sem bloquear o `tick()`.

  **Paridade Multiplataforma**
  Saída visual idêntica na Web (WebGL), Desktop e Mobile.

- ![h:185](assets/lua_pipeline.png)

  ![h:195](assets/playground-lua.png)

---

<!-- _class: cols-2 vcenter -->

# 4. Ginga-CC-WebServices Portável

- **Nativo (a)**
  Aplicação HTML executa em WebView nativa, enquanto `HTTPServer` local embutido (porta 44642) atende requisições HTTP.

  **Navegador com Sandbox (b)**
  Aplicação HTML executa em `iframe` com sandbox, com shim injetado que intercepta `window.fetch()` e `XMLHttpRequest`.

- ![h:400](assets/ccws_intercept.png)

---

<!-- _class: invert -->
<!-- _paginate: skip -->

# Funcionalidades e Demo do gingaf

---

<!-- _class: grid-2x2 center -->

## NCL com Links, Grade de Vídeos, NCL Embutido e Navegação

- ![h:155](assets/gifs/video.ncl.gif)
  NCL com links básicos ([video.ncl](https://ginga.org.br/gingaf/playground/?app=video.ncl))

- ![h:155](assets/gifs/video_grid.ncl.gif)
  NCL com grade de vídeos ([video_grid.ncl](https://ginga.org.br/gingaf/playground/?app=video_grid.ncl))

- ![h:155](assets/gifs/emb_ncl.ncl.gif)
  NCL embutido em NCL ([emb_ncl.ncl](https://ginga.org.br/gingaf/playground/?app=emb_ncl.ncl))

- ![h:155](assets/gifs/focus_nav.ncl.gif)
  NCL com navegação de foco e seleção ([focus_nav.ncl](https://ginga.org.br/gingaf/playground/?app=focus_nav.ncl))

---

<!-- _class: grid-2x2 center -->

## NCLua, HTML+CCWS, HTML Embutido e Multiusuário

- ![h:155](assets/gifs/lua_canvas.ncl.gif)
  NCL com desenho em tela Lua e teclas ([lua_canvas.ncl](https://ginga.org.br/gingaf/playground/?app=lua_canvas.ncl))

- ![h:155](assets/gifs/current_service.html.gif)
  HTML com CCWS /current-service/ ([current_service.html](https://ginga.org.br/gingaf/playground/?app=current_service.html))

- ![h:155](assets/gifs/emb_html.ncl.gif)
  NCL com documento HTML embutido ([emb_html.ncl](https://ginga.org.br/gingaf/playground/?app=emb_html.ncl))

- ![h:155](assets/gifs/multiuser_profile.gif)
  NCL com troca de perfil multiusuário ([multiuser_profile/main.ncl](https://ginga.org.br/gingaf/playground/?app=multiuser_profile/main.ncl))

---

# Esta apresentação vai para o Guinness Book de 2027?

![center w:450](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ2S0TQNZ9hLSSAZlZ4PNTKgmKhCihdzZTAewErSnXD4w&s)

---

# Esta apresentação vai para o Guinness Book de 2027?

## Primeiro exemplo de NCL forward na história!

![center w:600](assets/gifs/00syncProp.ncl.gif)

---

# Contribuições

## Portabilidade Multiplataforma

<div class="cols-2 vcenter">

- Suporte a **Desktop**, **Web** e **Android**, pronto para **dispositivos futuros** (ex.: TVs com suporte a Flutter).

- ![h:120](assets/app_clock4.png) ![h:120](assets/web.png) ![h:120](assets/android.png)

</div>

**Decisões de Arquitetura**

<div class="contrib-grid">

- **1. Engine Gráfica**
  Dart/Flutter unificado

- **2. UI Desacoplada**
  Lógica headless em memória

- **3. Relógio Virtual**
  Avanço via `tick()`

- **4. NCLua & CCWS**
  Lua e CCWS virtualizados

</div>

---

# Contribuições

## Determinismo

<div class="cols-2 vcenter">

- Modo **headless** em memória, avanço por `tick()` orquestrado e **64 testes unitários** em CI.

- ![h:195](assets/headless_listing.png)

</div>

**Decisões de Arquitetura**

<div class="contrib-grid">

- **1. Engine Gráfica**
  Dart/Flutter unificado

- **2. UI Desacoplada**
  Lógica headless em memória

- **3. Relógio Virtual**
  Avanço via `tick()`

- **4. NCLua & CCWS**
  Lua e CCWS virtualizados

</div>

---

# Contribuições

## Debug

<div class="cols-2 vcenter">

- Extensão **ginga-code** para VS Code com inspeção **passo a passo** (step) sem necessidade de hardware STB.

- ![h:195](assets/vscode.png)

</div>

**Decisões de Arquitetura**

<div class="contrib-grid">

- **1. Engine Gráfica**
  Dart/Flutter unificado

- **2. UI Desacoplada**
  Lógica headless em memória

- **3. Relógio Virtual**
  Avanço via `tick()`

- **4. NCLua & CCWS**
  Lua e CCWS virtualizados

</div>

---

# Referências

- **[Rodrigues et al. 1998]** Rogério Ferreira Rodrigues, Débora C. Muchaluat-Saade, and Luiz Fernando Gomes Soares. "Composite nodes, contextual links and graphical structural views on the WWW." *Journal of the Brazilian Computer Society*, 5(2), 1998.
- **[Rodrigues et al. 2001]** Rogério Ferreira Rodrigues, Leandro Marques Rodrigues, and Luiz Fernando Gomes Soares. "Desenvolvimento e Integração de Ferramentas de Exibição em Sistemas de Apresentação Hipermídia." *VII Simpósio Brasileiro de Sistemas Multimídia e Hipermídia (SBMídia 2001)*, Florianópolis, SC, 2001.
- **[Soares et al. 2010]** Luiz Fernando Gomes Soares, Carlos de Salles Soares Neto, Rogério Ferreira Rodrigues, and Marcelo Ferreira Moreno. "Ginga-NCL: Declarative middleware for multimedia IPTV services." *IEEE Communications Magazine*, 48(6): 74–81, 2010.
- **[Melo et al. 2013]** Erick Lazaro Melo, Caio César Viel, Cesar A. C. Teixeira, Alexandre Coelho Rondon, and Daniel de Paula Silva. "WebNCL: a web-based presentation machine for multimedia documents." *Proceedings of the 19th Brazilian Symposium on Multimedia and the Web (WebMedia 2013)*, 2013.
- **[Braga et al. 2018]** Rodrigo Braga, Volnei Klehm, Leonardo Santana, Kevin Takano, Lauro Gama, Addison Lima, Vinícius Melo, Taynara Paiva, Diego Gonzalez, Michael Mello, Chak Lee, and Lois Nascimento. "NuGinga: a JavaScript Driven Implementation of Brazilian Digital TV Middleware for Android." *Proceedings of the 24th Brazilian Symposium on Multimedia and the Web (WebMedia 2018)*, Salvador, Brazil, 2018.
- **[Nogueira et al. 2020]** Dina Nogueira, Lois Nascimento, Michael Mello, and Rodrigo Braga. "NuGinga Playcode: A web NCL/NCLua authoring tool for Ginga-NCL digital TV applications." *Proceedings of the 26th Brazilian Symposium on Multimedia and the Web (WebMedia 2020)*, 2020.

---

<!--
_paginate: false
_header: ""
_class: cols-2 vcenter
-->

# Obrigado!

- ### Dúvidas e Discussão

  **Repositório**: https://github.com/ginga-org-br/gingaf

  **Playground**: https://ginga.org.br/gingaf/playground/

  **Contato**: `a.guedes@reading.ac.uk` | `danielmoraes@telemidia.puc-rio.br`

- ![](assets/portal1.png)
