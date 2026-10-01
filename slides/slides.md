---
marp: true
theme: default
paginate: true
header: 'gingaf: Cross-Platform NCL & HTML5 Execution — WebMedia 2026'
style: |
  @import url('https://cdnjs.cloudflare.com/ajax/libs/font-awesome/6.5.1/css/all.min.css');
  img[alt~="center"] {
    display: block;
    margin: 0 auto;
  }
  section.invert {
    text-align: center;
  }
  section.invert {
    text-align: center;
  }
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
.callout-red {
  margin-top: 18px;
  padding: 14px 20px;
  background-color: #ffebe9;
  border-left: 6px solid #cf222e;
  border-radius: 4px;
  color: #cf222e;
  font-weight: 600;
  font-size: 25px;
  line-height: 1.45;
}
</style>

<!-- _paginate: false -->
<!-- _header: "" -->

<div style="display: grid; grid-template-columns: 3fr 1fr; align-items: center;">

<div>

# gingaf: A Cross-Platform Architecture To Execute Ginga-NCL and Ginga-HTML5 Applications

**Alan L. V. Guedes**$^1$, **Paulo Victor Borges**$^2$, **Daniel Moraes**$^2$, **Sergio Colcher**$^2$
$^1$University of Reading, UK | $^2$PUC-Rio, BR

*Anais do Simpósio Brasileiro de Sistemas Multimídia e Web (WebMedia 2026)*
Lavras/MG, BR

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

# O Middleware de DTV Ginga

<div style="display: flex; flex-direction: column; gap: 14px; margin-top: 10px; width: 100%;">
  <div style="display: flex; justify-content: space-between; gap: 24px; width: 100%;">
    <div style="flex: 1 1 0; min-width: 0; display: flex; justify-content: center; align-items: center; height: 215px;">
      <img src="assets/Picture1.png" style="max-height: 215px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 4px 12px rgba(0,0,0,0.12);" />
    </div>
    <div style="flex: 1 1 0; min-width: 0; display: flex; justify-content: center; align-items: center; height: 215px;">
      <img src="assets/Picture2.jpg" style="max-height: 215px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 4px 12px rgba(0,0,0,0.12);" />
    </div>
  </div>
  <div style="display: flex; justify-content: space-between; gap: 24px; width: 100%;">
    <div style="flex: 1 1 0; min-width: 0; display: flex; justify-content: center; align-items: center; height: 215px;">
      <img src="assets/Picture3.png" style="max-height: 215px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 4px 12px rgba(0,0,0,0.12);" />
    </div>
    <div style="flex: 1 1 0; min-width: 0; display: flex; justify-content: center; align-items: center; height: 215px;">
      <img src="assets/Picture4.jpg" style="max-height: 215px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 4px 12px rgba(0,0,0,0.12);" />
    </div>
  </div>
</div>

Definido na serie de normas SBTVD ABNT 15606.

Presente receptores de TV Digital certificados no Brasil e América Latina (>60M telespectadores)

---

# Ecosistema de Desenvolvimento Ginga é limatado

Não existe um ambiente desenvolve fácil acesso, completo e aberto. Por exemple o Mozilla https://developer.mozilla.org/

![center w:500](assets/image.png)

---

# Ecosistema de Desenvolvimento Ginga é limatado

- **Sem Execução Imediata e Setup dicifil**: Ausência de ambiente portátil e "zero-install".
- **Foco Acadêmico**: Foco em pesquisas.

**Desafios Técnicos de Cobertura da Normal**
- Além de Ginga-NCL e NCLua novos componentes HTML5 and Ginga-CC-Websservices increementam complexidade.

![bg right:30% 90%](assets/image-1.png)
![bg vertical right:30% 90%](assets/ginga.png)

---

# Implementações do Ginga na Literatura

<div style="display: grid; grid-template-columns: repeat(3, 1fr); grid-gap: 24px; align-items: center; position: relative; margin: 8px 0 16px 0;">
  <div style="position: absolute; left: 60px; right: 28px; height: 3px; background: #0969da; top: 50%; transform: translateY(-50%); z-index: 1;"></div>
  <div style="position: absolute; right: 14px; top: 50%; transform: translateY(-50%); width: 0; height: 0; border-top: 7px solid transparent; border-bottom: 7px solid transparent; border-left: 14px solid #0969da; z-index: 1;"></div>
  
  <div style="display: flex; justify-content: center; position: relative; z-index: 2;">
    <span style="background: #ffffff; border: 2.5px solid #0969da; color: #0969da; padding: 4px 22px; border-radius: 20px; font-weight: 700; font-size: 16.5px; box-shadow: 0 2px 6px rgba(0,0,0,0.06);">
      1998
    </span>
  </div>

  <div style="display: flex; justify-content: center; position: relative; z-index: 2;">
    <span style="background: #ffffff; border: 2.5px solid #0969da; color: #0969da; padding: 4px 22px; border-radius: 20px; font-weight: 700; font-size: 16.5px; box-shadow: 0 2px 6px rgba(0,0,0,0.06);">
      2001
    </span>
  </div>

  <div style="display: flex; justify-content: center; position: relative; z-index: 2;">
    <span style="background: #ffffff; border: 2.5px solid #0969da; color: #0969da; padding: 4px 22px; border-radius: 20px; font-weight: 700; font-size: 16.5px; box-shadow: 0 2px 6px rgba(0,0,0,0.06);">
      2010
    </span>
  </div>
</div>

<div style="display: grid; grid-template-columns: repeat(3, 1fr); grid-gap: 24px; align-items: start;">

<div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
<h3 style="margin: 0 0 6px 0; color: #0969da; font-size: 21px; font-weight: 700;">PUC-Rio (Netscape)</h3>
<div style="height: 190px; width: 100%; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/ginga-netscape.png" style="max-height: 190px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Plugin para navegador Netscape no início da WWW.
</p>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 6px 0 0 0; color: #57606a;">
[Rodrigues et al. 1998]
</p>
</div>

<div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
<h3 style="margin: 0 0 6px 0; color: #0969da; font-size: 21px; font-weight: 700;">PUC-Rio (Java AWT)</h3>
<div style="height: 190px; width: 100%; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/ginga-java.png" style="max-height: 190px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Ferramentas de exibição hipermídia sobre Java AWT.
</p>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 6px 0 0 0; color: #57606a;">
[Rodrigues et al. 2001]
</p>
</div>

<div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
<h3 style="margin: 0 0 6px 0; color: #0969da; font-size: 21px; font-weight: 700;">PUC-Rio (C++ &amp; FFmpeg)</h3>
<div style="height: 190px; width: 100%; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/ginga-ffmpeg.png" style="max-height: 190px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Middleware declarativo com backend FFmpeg para IPTV/DTV.
</p>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 6px 0 0 0; color: #57606a;">
[Soares et al. 2010]
</p>
</div>

</div>

---

# Implementações do Ginga  na Literatura

<div style="display: grid; grid-template-columns: repeat(3, 1fr); grid-gap: 24px; align-items: center; position: relative; margin: 8px 0 16px 0;">
  <div style="position: absolute; left: 60px; right: 28px; height: 3px; background: #0969da; top: 50%; transform: translateY(-50%); z-index: 1;"></div>
  <div style="position: absolute; right: 14px; top: 50%; transform: translateY(-50%); width: 0; height: 0; border-top: 7px solid transparent; border-bottom: 7px solid transparent; border-left: 14px solid #0969da; z-index: 1;"></div>
  
  <div style="display: flex; justify-content: center; position: relative; z-index: 2;">
    <span style="background: #ffffff; border: 2.5px solid #0969da; color: #0969da; padding: 4px 22px; border-radius: 20px; font-weight: 700; font-size: 16.5px; box-shadow: 0 2px 6px rgba(0,0,0,0.06);">
      2012
    </span>
  </div>

  <div style="display: flex; justify-content: center; position: relative; z-index: 2;">
    <span style="background: #ffffff; border: 2.5px solid #0969da; color: #0969da; padding: 4px 22px; border-radius: 20px; font-weight: 700; font-size: 16.5px; box-shadow: 0 2px 6px rgba(0,0,0,0.06);">
      2018
    </span>
  </div>

  <div style="display: flex; justify-content: center; position: relative; z-index: 2;">
    <span style="background: #ffffff; border: 2.5px solid #0969da; color: #0969da; padding: 4px 22px; border-radius: 20px; font-weight: 700; font-size: 16.5px; box-shadow: 0 2px 6px rgba(0,0,0,0.06);">
      2018–2020
    </span>
  </div>
</div>

<div style="display: grid; grid-template-columns: repeat(3, 1fr); grid-gap: 24px; align-items: start;">

<div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
<h3 style="margin: 0 0 6px 0; color: #0969da; font-size: 21px; font-weight: 700;">UFSCar (WebNCL)</h3>
<div style="height: 190px; width: 100%; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/webncl.png" style="max-height: 190px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Apresentador web puramente em JavaScript (sem Lua).
</p>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 6px 0 0 0; color: #57606a;">
[Melo et al. 2013]
</p>
</div>

<div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
<h3 style="margin: 0 0 6px 0; color: #0969da; font-size: 21px; font-weight: 700;">PUC-Rio (C++ &amp; GStreamer)</h3>
<div style="height: 190px; width: 100%; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/ginga-gst.png" style="max-height: 190px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Reimplementação C++ com <code>tick()</code> e GStreamer.
</p>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 6px 0 0 0; color: #57606a;">
[PUC-Rio / Telemídia]
</p>
</div>

<div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
<h3 style="margin: 0 0 6px 0; color: #0969da; font-size: 21px; font-weight: 700;">Sidia NuGinga (NodeJS)</h3>
<div style="height: 190px; width: 100%; display: flex; gap: 8px; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/nuginga1.png" style="max-height: 190px; max-width: 32%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
  <img src="assets/nuginga2.png" style="max-height: 190px; max-width: 64%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Middleware JS/Android e ferramenta web Playcode.
</p>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 6px 0 0 0; color: #57606a;">
[Braga et al. 2018; Nogueira et al. 2020]
</p>
</div>

</div>

---

# Limitações das Implementações Ginga na Literatura

<div style="display: grid; grid-template-columns: 1fr 1fr; grid-gap: 36px; align-items: start; font-size: 24px; line-height: 1.45; margin-top: 10px;">

<div>

**Acoplamento à Plataforma**
- **Concorrência por Eventos**: Callbacks assíncronos e chamadas bloqueantes de SO.
- **Dependência Nativa**: C++ acoplado a bibliotecas e codecs (FFmpeg, GTK).
- **Sobrecarga de VMs**: Máquinas virtuais pesadas para contornar dependências.

</div>

<div>

**Limitações Web e Código Fechado**
- **Suporte Web Parcial**: WebNCL sem suporte a NCLua nem CCWS.
- **Código Fechado**: NuGinga/Playcode fechados para a comunidade.
- **Fragmentação**: Falta de paridade unificada entre Web e Desktop.

</div>

</div>

<div class="callout-red" style="font-size: 26px; padding: 16px 22px; margin-top: 22px; border-left-width: 6px; line-height: 1.45;">
<strong>Gargalos históricos</strong>: concorrência assíncrona complexa, dependência de codecs nativos, suporte web parcial e falta de código aberto.
</div>

---

<!-- _class: invert -->
<!-- _paginate: skip -->

# Solução Proposta

---

# Solução proposta

<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; height: 180px; margin-top: 10px; visibility: hidden;">
  <div></div>
  <div></div>
  <div></div>
</div>

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 32px; height: 180px; margin-top: 24px;">
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-bottom: 8px;">Native</div>
    <img src="assets/setupbox.png" style="max-height: 110px; max-width: 90%; object-fit: contain;" />
  </div>
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-bottom: 8px;">Browser</div>
    <img src="assets/browsers.png" style="max-height: 80px; max-width: 90%; object-fit: contain; margin-top: 15px;" />
  </div>
</div>

---

<!-- _paginate: hold -->

# Implementações do Ginga na Literatura

<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; height: 180px; margin-top: 10px;">
  <div style="display: flex; align-items: center; justify-content: center;">
    <ul style="margin: 0; padding-left: 20px; font-size: 20px; line-height: 1.7; color: #24292f;">
      <li><strong>PUC-Rio (Java AWT)</strong></li>
      <li><strong>PUC-Rio (C++ &amp; FFmpeg)</strong></li>
      <li><strong>PUC-Rio (C++ &amp; GStreamer)</strong></li>
    </ul>
  </div>
  <div></div>
  <div style="display: flex; align-items: center; justify-content: center;">
    <ul style="margin: 0; padding-left: 20px; font-size: 20px; line-height: 1.7; color: #24292f;">
      <li><strong>PUC-Rio (Netscape)</strong></li>
      <li><strong>UFSCar (WebNCL)</strong></li>
      <li><strong>Sidia NuGinga (NodeJS)</strong></li>
    </ul>
  </div>
</div>

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 32px; height: 180px; margin-top: 24px;">
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-bottom: 8px;">Native</div>
    <img src="assets/setupbox.png" style="max-height: 110px; max-width: 90%; object-fit: contain;" />
  </div>
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-bottom: 8px;">Browser</div>
    <img src="assets/browsers.png" style="max-height: 80px; max-width: 90%; object-fit: contain; margin-top: 15px;" />
  </div>
</div>

---

<!-- _paginate: hold -->

# Implementações do Ginga na Literatura

<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; height: 180px; margin-top: 10px;">
  <div style="display: flex; align-items: center; justify-content: center;">
    <ul style="margin: 0; padding-left: 20px; font-size: 20px; line-height: 1.7; color: #24292f;">
      <li><strong>PUC-Rio (Java AWT)</strong></li>
      <li><strong>PUC-Rio (C++ &amp; FFmpeg)</strong></li>
      <li><strong>PUC-Rio (C++ &amp; GStreamer)</strong></li>
    </ul>
  </div>
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 28px; font-weight: 800; color: #0969da; margin-bottom: 8px;">gingaf (ours)</div>
    <div style="font-size: 19px; font-weight: 600; color: #1f2328; line-height: 1.35; margin-bottom: 8px;">
      Arquitetura Cross-Platform
    </div>
    <div style="font-size: 16px; font-weight: 700; color: #0969da;">
      Ginga-NCL + Ginga-HTML5
    </div>
  </div>
  <div style="display: flex; align-items: center; justify-content: center;">
    <ul style="margin: 0; padding-left: 20px; font-size: 20px; line-height: 1.7; color: #24292f;">
      <li><strong>PUC-Rio (Netscape)</strong></li>
      <li><strong>UFSCar (WebNCL)</strong></li>
      <li><strong>Sidia NuGinga (NodeJS)</strong></li>
    </ul>
  </div>
</div>

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 32px; height: 180px; margin-top: 24px;">
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-bottom: 8px;">Native</div>
    <img src="assets/setupbox.png" style="max-height: 110px; max-width: 90%; object-fit: contain;" />
  </div>
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-bottom: 8px;">Browser</div>
    <img src="assets/browsers.png" style="max-height: 80px; max-width: 90%; object-fit: contain; margin-top: 15px;" />
  </div>
</div>

---

# Solução Proposta: gingaf

### A primeira reformulação arquitetural em mais de 15 anos

<div style="margin-top: 24px; font-size: 26px; line-height: 1.6;">

- **Suporte Multiplataforma**: Execução consistente na Web (Wasm/CanvasKit), Desktop e Mobile a partir de um código-fonte único em Dart/Flutter.
- **UI e Modelos Desacoplados**: A máquina de estados lógica (`NCLDocument`) opera de forma independente, sem acoplamento a widgets ou contextos de desenho.
- **Relógio Virtual Determinístico**: O avanço temporal é orquestrado por chamadas explícitas de `tick()`, permitindo testes em milissegundos e eliminando condições de corrida.

</div>

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

<div >

<img src="assets/old_arch.png"/>

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

**Cliente Web via Interceptação de Fetch (b)**
- Aplicação HTML executa em `iframe` com sandbox.
- Shim injetado intercepta e sobrescreve `window.fetch()` e `XMLHttpRequest`.
- Faz a ponte para o Flutter via `postMessage`.
- Virtualização de rede client-side do CCWS: sem servidor HTTP local ou dependências nativas.

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

## NCL com Links, Grade de Vídeos, NCL Embutido e Navegação

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

## NCLua, HTML+CCWS, HTML Embutido e Multiusuário

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

- **Primeira reformulação arquitetural da PUC-Rio em mais de 15 anos**
- **Multiplataforma Unificado**: Execução nativa de Ginga-NCL, NCLua e Ginga-HTML5/CCWS no navegador (Wasm), Desktop e Dispositivos Móveis.
- **Gráficos a 60 FPS**: Pipeline intermediário de lista de comandos Lua com renderização fluida no Flutter.
- **Virtualização Client-Side de CCWS**: Interceptação transparente de requisições de rede sem necessidade de servidores locais.
- **GingaPlayground**  disponivel em http://ginga.org.br/gingaf/playground.

---

# Referências

<div style="font-size: 13.5px; line-height: 1.4; margin-top: 8px;">

- **[Rodrigues et al. 1998]** Rogério Ferreira Rodrigues, Débora C. Muchaluat-Saade, and Luiz Fernando Gomes Soares. "Composite nodes, contextual links and graphical structural views on the WWW." *Journal of the Brazilian Computer Society*, 5(2), 1998.
- **[Rodrigues et al. 2001]** Rogério Ferreira Rodrigues, Leandro Marques Rodrigues, and Luiz Fernando Gomes Soares. "Desenvolvimento e Integração de Ferramentas de Exibição em Sistemas de Apresentação Hipermídia." *VII Simpósio Brasileiro de Sistemas Multimídia e Hipermídia (SBMídia 2001)*, Florianópolis, SC, 2001.
- **[Soares et al. 2010]** Luiz Fernando Gomes Soares, Carlos de Salles Soares Neto, Rogério Ferreira Rodrigues, and Marcelo Ferreira Moreno. "Ginga-NCL: Declarative middleware for multimedia IPTV services." *IEEE Communications Magazine*, 48(6): 74–81, 2010.
- **[Melo et al. 2013]** Erick Lazaro Melo, Caio César Viel, Cesar A. C. Teixeira, Alexandre Coelho Rondon, and Daniel de Paula Silva. "WebNCL: a web-based presentation machine for multimedia documents." *Proceedings of the 19th Brazilian Symposium on Multimedia and the Web (WebMedia 2013)*, 2013.
- **[Braga et al. 2018]** Rodrigo Braga, Volnei Klehm, Leonardo Santana, Kevin Takano, Lauro Gama, Addison Lima, Vinícius Melo, Taynara Paiva, Diego Gonzalez, Michael Mello, Chak Lee, and Lois Nascimento. "NuGinga: a JavaScript Driven Implementation of Brazilian Digital TV Middleware for Android." *Proceedings of the 24th Brazilian Symposium on Multimedia and the Web (WebMedia 2018)*, Salvador, Brazil, 2018.
- **[Nogueira et al. 2020]** Dina Nogueira, Lois Nascimento, Michael Mello, and Rodrigo Braga. "NuGinga Playcode: A web NCL/NCLua authoring tool for Ginga-NCL digital TV applications." *Proceedings of the 26th Brazilian Symposium on Multimedia and the Web (WebMedia 2020)*, 2020.

</div>

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
