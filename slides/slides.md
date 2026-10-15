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
  max-height: 165px;
  object-fit: contain;
  border-radius: 6px;
  border: 1px solid transparent;
  background-color: transparent;
  box-shadow: none;
}
.grid-card p {
  margin: 6px 0 0 0;
  font-size: 18px;
  font-weight: 600;
  line-height: 1.3;
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
section.contrib-slide {
  padding: 34px 60px 24px 60px;
}
section.contrib-slide h1 {
  margin-bottom: 2px;
}
section.contrib-slide h2 {
  margin-top: 6px;
  margin-bottom: 6px;
}
.contrib-subheading {
  font-size: 28px;
  font-weight: 700;
  color: #1f2328;
  margin: 16px 0 10px 0;
}
.contrib-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 14px;
}
.contrib-card {
  border: 1.5px solid #d0d7de;
  border-radius: 8px;
  padding: 14px 16px;
  box-shadow: 0 1px 3px rgba(0,0,0,0.06);
  background: #ffffff;
  display: flex;
  flex-direction: column;
  justify-content: center;
  height: 126px;
  box-sizing: border-box;
  margin: 0 !important;
}
.contrib-card strong {
  display: block;
  font-size: 25px;
  font-weight: 700;
  color: #1f2328;
  margin-bottom: 6px;
  line-height: 1.2;
}
.contrib-card p {
  margin: 0;
  font-size: 22px;
  line-height: 1.35;
  color: #57606a;
}
.contrib-card.highlight {
  background: #ddf4ff;
  margin: 0 !important;
}
.contrib-card.highlight strong {
  color: #0969da;
}
.contrib-card.highlight p {
  color: #1f2328;
}
.contrib-card.dimmed {
  background: #f6f8fa;
  opacity: 0.6;
  margin: 0 !important;
}
.contrib-card.dimmed strong {
  color: #57606a;
}
.contrib-card.dimmed p {
  color: #57606a;
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

# Spoiler Alert!

## Esta apresentação vai para o Guinness Book de 2027 💪

![center w:450](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ2S0TQNZ9hLSSAZlZ4PNTKgmKhCihdzZTAewErSnXD4w&s)

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

Definido na série de normas SBTVD ABNT 15606.

Presente em receptores de TV Digital certificados no Brasil e América Latina (>60M telespectadores)

---

# Ecossistema de Desenvolvimento Ginga é limitado

**Ausência de ambiente portátil e "zero-install"**: de fácil acesso, completo e aberto.
- Podemos comparar o Mozilla https://developer.mozilla.org/ e a Ginga-VM (2010)

<div style="display: flex; justify-content: center; gap: 24px; align-items: center; margin-top: 12px;">
  <img src="assets/image.png" style="width: 500px; object-fit: contain;" />
  <img src="assets/image-1.png" style="width: 500px; object-fit: contain;" />
</div>

---

# Ecossistema de Desenvolvimento Ginga é limitado

**Um fator é a escolha da Engine Gráfica** (e.g., DirectFrameBuffer, FFmpeg, GStreamer, Browsers)

**Outro fator é a complexidade de certos componentes do Ginga**: NCLua (C-based lua engine), Ginga-HTML5 (chromium, webkit) e Ginga-CC-Webservices (HTTP server).

![center w:600](assets/ginga.png)

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
<h3 style="margin: 0 0 2px 0; color: #0969da; font-size: 21px; font-weight: 700;">PUC-Rio (Netscape)</h3>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 0 0 8px 0; color: #0969da;">
[Rodrigues et al. 1998]
</p>
<div style="height: 180px; width: 100%; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/ginga-netscape.png" style="max-height: 180px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Plugin para navegador Netscape no início da WWW.
</p>
<p style="font-size: 14.5px; font-weight: 700; line-height: 1.35; margin: 8px 0 0 0; color: #cf222e;">
browser-only<br>sem Lua
</p>
</div>

<div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
<h3 style="margin: 0 0 2px 0; color: #0969da; font-size: 21px; font-weight: 700;">PUC-Rio (Java AWT)</h3>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 0 0 8px 0; color: #0969da;">
[Rodrigues et al. 2001]
</p>
<div style="height: 180px; width: 100%; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/ginga-java.png" style="max-height: 180px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Ferramentas de exibição hipermídia sobre Java AWT.
</p>
<p style="font-size: 14.5px; font-weight: 700; line-height: 1.35; margin: 8px 0 0 0; color: #cf222e;">
desktop-only<br>sem Lua
</p>
</div>

<div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
<h3 style="margin: 0 0 2px 0; color: #0969da; font-size: 21px; font-weight: 700;">PUC-Rio (C++ &amp; FFmpeg)</h3>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 0 0 8px 0; color: #0969da;">
[Soares et al. 2010]
</p>
<div style="height: 180px; width: 100%; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/ginga-ffmpeg.png" style="max-height: 180px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Middleware declarativo com backend FFmpeg para IPTV/DTV.
</p>
<p style="font-size: 14.5px; font-weight: 700; line-height: 1.25; margin: 8px 0 0 0; color: #cf222e;">
desktop-only
</p>
</div>

</div>

---

# Implementações do Ginga na Literatura

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
<h3 style="margin: 0 0 2px 0; color: #0969da; font-size: 21px; font-weight: 700;">UFSCar (WebNCL)</h3>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 0 0 8px 0; color: #0969da;">
[Melo et al. 2013]
</p>
<div style="height: 180px; width: 100%; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/webncl.png" style="max-height: 180px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Apresentador web puramente em JavaScript.
</p>
<p style="font-size: 14.5px; font-weight: 700; line-height: 1.35; margin: 8px 0 0 0; color: #cf222e;">
browser-only<br>sem Lua
</p>
</div>

<div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
<h3 style="margin: 0 0 2px 0; color: #0969da; font-size: 21px; font-weight: 700;">PUC-Rio (C++ &amp; GStreamer)</h3>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 0 0 8px 0; color: #0969da;">
[PUC-Rio / Telemídia]
</p>
<div style="height: 180px; width: 100%; display: flex; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/ginga-gst.png" style="max-height: 180px; max-width: 100%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Reimplementação C++ com <code>tick()</code> e GStreamer.
</p>
<p style="font-size: 14.5px; font-weight: 700; line-height: 1.35; margin: 8px 0 0 0; color: #cf222e;">
desktop-only<br>sem Ginga-CC-Webservices
</p>
</div>

<div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
<h3 style="margin: 0 0 2px 0; color: #0969da; font-size: 21px; font-weight: 700;">Sidia NuGinga (NodeJS)</h3>
<p style="font-size: 13.5px; font-weight: 600; line-height: 1.2; margin: 0 0 8px 0; color: #0969da;">
[Braga et al. 2018; Nogueira et al. 2020]
</p>
<div style="height: 180px; width: 100%; display: flex; gap: 8px; align-items: center; justify-content: center; margin-bottom: 8px;">
  <img src="assets/nuginga1.png" style="max-height: 180px; max-width: 32%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
  <img src="assets/nuginga2.png" style="max-height: 180px; max-width: 64%; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); background: #fff;" />
</div>
<p style="font-size: 16px; line-height: 1.35; margin: 0; color: #24292f;">
Middleware JS/Android e ferramenta web Playcode.
</p>
<p style="font-size: 14.5px; font-weight: 700; line-height: 1.35; margin: 8px 0 0 0; color: #cf222e;">
browser-only<br>sem Ginga-CC-Webservices
</p>
</div>

</div>

---

# Implementações do Ginga na Literatura

<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; height: 180px; margin-top: 10px;">
  <div style="display: flex; align-items: center; justify-content: center;">
    <ul style="margin: 0; padding: 0; list-style: none; font-size: 20px; line-height: 1.8; color: #24292f; text-align: center;">
      <li><strong>PUC-Rio (Java AWT)</strong></li>
      <li><strong>PUC-Rio (C++ &amp; FFmpeg)</strong></li>
      <li><strong>PUC-Rio (C++ &amp; GStreamer)</strong></li>
    </ul>
  </div>
  <div></div>
  <div style="display: flex; align-items: center; justify-content: center;">
    <ul style="margin: 0; padding: 0; list-style: none; font-size: 20px; line-height: 1.8; color: #24292f; text-align: center;">
      <li><strong>PUC-Rio (Netscape)</strong></li>
      <li><strong>UFSCar (WebNCL)</strong></li>
      <li><strong>Sidia NuGinga (NodeJS)</strong></li>
    </ul>
  </div>
</div>

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 32px; height: 180px; margin-top: 24px;">
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-bottom: 8px;">Native</div>
    <div style="display: flex; align-items: center; justify-content: center; gap: 16px; height: 110px;">
      <img src="assets/setupbox.png" style="max-height: 105px; max-width: 48%; object-fit: contain;" />
      <img src="assets/pc.png" style="max-height: 105px; max-width: 48%; object-fit: contain;" />
    </div>
  </div>
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-bottom: 8px;">Browser</div>
    <img src="assets/browsers.png" style="max-height: 80px; max-width: 90%; object-fit: contain; margin-top: 15px;" />
  </div>
</div>

---
<!-- _class: invert -->
<!-- _paginate: skip -->

# Solução Proposta

---

# Solução Proposta: gingaf

<div style="font-size: 22px; color: #57606a; margin-top: 14px; margin-bottom: 22px; font-weight: 600;">
As principais decisões de design são:
</div>

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 20px;">

<div style="background: #f8fafc; border: 1.5px solid #d0d7de; border-radius: 8px; padding: 20px 22px; box-shadow: 0 2px 8px rgba(0,0,0,0.03);">
  <div style="font-size: 21px; font-weight: 800; color: #1f2328; margin-bottom: 8px;">
    <strong>1. Engine Gráfica Multiplataforma</strong>
  </div>
  <div style="font-size: 17.5px; line-height: 1.45; color: #424a53;">
    Código único em Dart/Flutter para execução consistente na Web, Desktop e Mobile.
  </div>
</div>

<div style="background: #f8fafc; border: 1.5px solid #d0d7de; border-radius: 8px; padding: 20px 22px; box-shadow: 0 2px 8px rgba(0,0,0,0.03);">
  <div style="font-size: 21px; font-weight: 800; color: #1f2328; margin-bottom: 8px;">
    <strong>2. UI e Modelos Desacoplados</strong>
  </div>
  <div style="font-size: 17.5px; line-height: 1.45; color: #424a53;">
    Lógica (<code>NCLDocument</code>) independente e isolada de rendering.
  </div>
</div>

<div style="background: #f8fafc; border: 1.5px solid #d0d7de; border-radius: 8px; padding: 20px 22px; box-shadow: 0 2px 8px rgba(0,0,0,0.03);">
  <div style="font-size: 21px; font-weight: 800; color: #1f2328; margin-bottom: 8px;">
    <strong>3. Relógio Virtual</strong>
  </div>
  <div style="font-size: 17.5px; line-height: 1.45; color: #424a53;">
    Avanço temporal determinístico orquestrado via <code>tick()</code>, eliminando condições de corrida.
  </div>
</div>

<div style="background: #f8fafc; border: 1.5px solid #d0d7de; border-radius: 8px; padding: 20px 22px; box-shadow: 0 2px 8px rgba(0,0,0,0.03);">
  <div style="font-size: 21px; font-weight: 800; color: #1f2328; margin-bottom: 8px;">
    <strong>4. NCLua e CCWS Portáveis</strong>
  </div>
  <div style="font-size: 17.5px; line-height: 1.45; color: #424a53;">
    Runtime Lua puro em Dart e virtualização de rede sem dependências nativas.
  </div>
</div>

</div>

---

<!-- _paginate: hold -->

# 1. Engine Gráfica Multiplataforma

<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 24px; height: 130px; margin-top: 10px;">
  <div style="display: flex; align-items: center; justify-content: center;">
    <ul style="margin: 0; padding: 0; list-style: none; font-size: 20px; line-height: 1.8; color: #24292f; text-align: center;">
      <li><strong>PUC-Rio (Java AWT)</strong></li>
      <li><strong>PUC-Rio (C++ &amp; FFmpeg)</strong></li>
      <li><strong>PUC-Rio (C++ &amp; GStreamer)</strong></li>
    </ul>
  </div>
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 30px; font-weight: 800; color: #0969da; margin-bottom: 6px;">gingaf (ours)</div>
    <div style="font-size: 18px; font-weight: 700; color: #0969da;">
      Ginga-NCL + Ginga-HTML5
    </div>
  </div>
  <div style="display: flex; align-items: center; justify-content: center;">
    <ul style="margin: 0; padding: 0; list-style: none; font-size: 20px; line-height: 1.8; color: #24292f; text-align: center;">
      <li><strong>PUC-Rio (Netscape)</strong></li>
      <li><strong>UFSCar (WebNCL)</strong></li>
      <li><strong>Sidia NuGinga (NodeJS)</strong></li>
    </ul>
  </div>
</div>

<div style="background: #e2e7ee; border: 2px solid #b8c4d1; border-radius: 8px; padding: 10px 0; margin: 16px 0 20px 0; box-shadow: 0 2px 6px rgba(0,0,0,0.05); display: flex; align-items: center; justify-content: center; gap: 24px;">
  <div style="display: flex; align-items: center; gap: 10px;">
    <img src="assets/dart.svg" style="height: 32px; width: 32px; object-fit: contain;" />
    <span style="font-size: 24px; font-weight: 800; color: #1f2328; letter-spacing: 0.5px;">Dart</span>
  </div>
  <span style="font-size: 24px; font-weight: 300; color: #8c959f;">/</span>
  <div style="display: flex; align-items: center; gap: 10px;">
    <img src="assets/flutter.svg" style="height: 32px; width: 32px; object-fit: contain;" />
    <span style="font-size: 24px; font-weight: 800; color: #1f2328; letter-spacing: 0.5px;">Flutter</span>
  </div>
</div>

<div style="display: grid; grid-template-columns: repeat(2, 1fr); gap: 32px; height: 160px; margin-top: 12px;">
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-bottom: 8px;">Native</div>
    <div style="display: flex; align-items: center; justify-content: center; gap: 16px; height: 110px;">
      <img src="assets/setupbox.png" style="max-height: 105px; max-width: 48%; object-fit: contain;" />
      <img src="assets/pc.png" style="max-height: 105px; max-width: 48%; object-fit: contain;" />
    </div>
  </div>
  <div style="display: flex; flex-direction: column; align-items: center; justify-content: center; text-align: center;">
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-bottom: 8px;">Browser</div>
    <img src="assets/browsers.png" style="max-height: 80px; max-width: 90%; object-fit: contain; margin-top: 15px;" />
  </div>
</div>

---

# 1. Engine Gráfica Multiplataforma

<div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 28px; align-items: end; margin-top: 36px;">
  <div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
    <img src="assets/app_clock4.png" style="max-height: 320px; max-width: 100%; object-fit: contain; border-radius: 6px; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" />
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-top: 14px;">Desktop</div>
  </div>

  <div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
    <img src="assets/web.png" style="max-height: 320px; max-width: 100%; object-fit: contain; border-radius: 6px; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" />
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-top: 14px;">Web</div>
  </div>

  <div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
    <img src="assets/android.png" style="max-height: 320px; max-width: 100%; object-fit: contain; border-radius: 6px; box-shadow: 0 4px 12px rgba(0,0,0,0.1);" />
    <div style="font-size: 24px; font-weight: 700; color: #1f2328; margin-top: 14px;">Mobile</div>
  </div>
</div>

---

# 2. UI e Modelos Desacoplados

<div style="display: grid; grid-template-columns: 1.1fr 1fr; gap: 32px; align-items: center;">

<div>

**Camada de Lógica (Dart Puro)**
- `NCLDocument` (Parser, runtime NCLua) e `CCWS`.
- Compila para JavaScript e WebAssembly.

**Camada de Apresentação (Flutter)**
- `NCLWidget` e `HTMLWidget` (webview, js-interop).
- Renderização com precisão de pixels na Web, desktop e mobile.

</div>

<div style="display: flex; justify-content: center; align-items: center; width: 100%;">

<img src="assets/layered_arch.png" style="max-width: 100%; max-height: 410px; width: auto; height: auto; object-fit: contain; margin: 0 auto; display: block;" />

</div>

</div>

---

# 3. Relógio Virtual

## Implementações Anteriores Sem Relógio Virtual

<div style="display: grid; grid-template-columns: 1fr 1.15fr; gap: 32px; align-items: center;">

<div>

- Tempo atrelado ao relógio e threads do SO.
- Máquina de estados bloqueada por chamadas `draw()`.
- Transições disparadas via `onEvent()` nativo.

</div>

<div style="display: flex; justify-content: center; align-items: center; width: 100%;">

<img src="assets/old_arch.png" style="max-width: 100%; max-height: 380px; width: auto; height: auto; object-fit: contain; margin: 0 auto; display: block;" />

</div>

</div>

---

# 3. Relógio Virtual

<div style="display: grid; grid-template-columns: 1.15fr 1fr; gap: 32px; align-items: center;">

<div>

- **Coordenação por `tick()`**: O `NCLWidget` avança o relógio virtual por pulsos explícitos.
- **Desacoplamento de UI**: Sem referência direta entre `NCLDocument` e widgets da UI.
- **Sincronização Determinística**: Estados de `Media` atualizados na ordem do documento.
- **Consulta sob Demanda**: UI obtém propriedades via `syncProperties()`, sem condições de corrida.

</div>

<div style="display: flex; justify-content: center; align-items: center; width: 100%;">

<img src="assets/arch.png" style="max-width: 100%; max-height: 380px; width: auto; height: auto; object-fit: contain; margin: 0 auto; display: block;" />

</div>

</div>

---

# 4. NCLua Portável

<div style="display: grid; grid-template-columns: 1.1fr 1fr; gap: 28px; align-items: center;">

<div>

- **Motor Lua em Dart Puro**: `lua_dardo` (Lua 5.3) na Web sem dependências C ou Wasm.
- **Abstração de Comandos**: Chamadas `canvas` despachadas para o `CustomPainter` do Flutter.
- **Corrotinas Assíncronas**: Mapeadas para `async/await` sem bloquear o `tick()`.
- **Paridade Multiplataforma**: Saída visual idêntica na Web (WebGL), Desktop e Mobile.

</div>

<div style="display: flex; flex-direction: column; gap: 14px; align-items: center; justify-content: center; width: 100%;">

<img src="assets/lua_pipeline.png" style="max-width: 100%; max-height: 185px; width: auto; height: auto; object-fit: contain; margin: 0 auto; display: block;" />

<img src="assets/playground-lua.png" style="max-width: 100%; max-height: 195px; width: auto; height: auto; object-fit: contain; border-radius: 6px; border: 1px solid #d0d7de; box-shadow: 0 3px 10px rgba(0,0,0,0.08); margin: 0 auto; display: block;" />

</div>

</div>

---

# 4. Ginga-CC-WebServices Portável

<div style="display: grid; grid-template-columns: 1.15fr 1fr; gap: 32px; align-items: center;">

<div>

**Nativo (a)**
- Aplicação HTML executa em WebView nativa.
- `HTTPServer` local embutido (porta 44642) atende requisições HTTP.

**Navegador com Sandbox (b)**
- Aplicação HTML executa em `iframe` com sandbox.
- Shim injetado intercepta `window.fetch()` e `XMLHttpRequest`.

</div>

<div style="display: flex; justify-content: center; align-items: center; width: 100%;">

<img src="assets/ccws_intercept.png" style="max-width: 100%; max-height: 400px; width: auto; height: auto; object-fit: contain; margin: 0 auto; display: block;" />

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
    <p>HTML com CCWS /current-service/ (<a href="https://ginga.org.br/gingaf/playground/?app=current_service.html">current_service.html</a>)</p>
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

# Esta apresentação vai para o Guinness Book de 2027?

![center w:450](https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ2S0TQNZ9hLSSAZlZ4PNTKgmKhCihdzZTAewErSnXD4w&s)

---

# Esta apresentação vai para o Guinness Book de 2027?

## Primeiro exemplo de NCL forward na história!

<div style="display: flex; justify-content: center; margin-top: 16px;">
  <img src="assets/gifs/00syncProp.ncl.gif" />
</div>

---

<!-- _class: contrib-slide -->

# Contribuições

<div style="height: 240px; border: 2.5px dashed #d0d7de; border-radius: 8px; background: #f6f8fa; box-sizing: border-box; margin: 18px 0 10px 0;"></div>

<div class="contrib-subheading">Decisões de Arquitetura</div>

<div class="contrib-grid">
  <div class="contrib-card">
    <strong>1. Engine Gráfica</strong>
    <p>Dart/Flutter unificado</p>
  </div>
  <div class="contrib-card">
    <strong>2. UI Desacoplada</strong>
    <p>Lógica headless em memória</p>
  </div>
  <div class="contrib-card">
    <strong>3. Relógio Virtual</strong>
    <p>Avanço via tick()</p>
  </div>
  <div class="contrib-card">
    <strong>4. NCLua &amp; CCWS</strong>
    <p>Lua e CCWS virtualizados</p>
  </div>
</div>

---

<!-- _class: contrib-slide -->

# Contribuições

## Portabilidade Multiplataforma

<div style="display: grid; grid-template-columns: 1fr 1.35fr; gap: 24px; align-items: center; height: 215px;">
  <div>
    <ul style="font-size: 23px; line-height: 1.55; color: #24292f; margin: 0; padding-left: 24px;">
      <li>Suporte a <strong>Desktop</strong>, <strong>Web</strong> e <strong>Android</strong></li>
      <li>Pronto para <strong>dispositivos futuros</strong> (ex.: TVs com suporte a Flutter)</li>
    </ul>
  </div>
  <div style="display: grid; grid-template-columns: repeat(3, 1fr); gap: 10px; align-items: center; justify-items: center;">
    <div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
      <img src="assets/app_clock4.png" style="max-height: 135px; max-width: 100%; object-fit: contain; border-radius: 4px; box-shadow: 0 2px 8px rgba(0,0,0,0.12); border: 1px solid #d0d7de;" />
      <span style="font-size: 20px; font-weight: 700; color: #1f2328; margin-top: 4px;">Desktop</span>
    </div>
    <div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
      <img src="assets/web.png" style="max-height: 135px; max-width: 100%; object-fit: contain; border-radius: 4px; box-shadow: 0 2px 8px rgba(0,0,0,0.12); border: 1px solid #d0d7de;" />
      <span style="font-size: 20px; font-weight: 700; color: #1f2328; margin-top: 4px;">Web</span>
    </div>
    <div style="display: flex; flex-direction: column; align-items: center; text-align: center;">
      <img src="assets/android.png" style="max-height: 135px; max-width: 100%; object-fit: contain; border-radius: 4px; box-shadow: 0 2px 8px rgba(0,0,0,0.12); border: 1px solid #d0d7de;" />
      <span style="font-size: 20px; font-weight: 700; color: #1f2328; margin-top: 4px;">Mobile</span>
    </div>
  </div>
</div>

<div class="contrib-subheading">Decisões de Arquitetura</div>

<div class="contrib-grid">
  <div class="contrib-card highlight">
    <strong>1. Engine Gráfica</strong>
    <p>Dart/Flutter unificado</p>
  </div>
  <div class="contrib-card dimmed">
    <strong>2. UI Desacoplada</strong>
    <p>Lógica headless em memória</p>
  </div>
  <div class="contrib-card dimmed">
    <strong>3. Relógio Virtual</strong>
    <p>Avanço via tick()</p>
  </div>
  <div class="contrib-card highlight">
    <strong>4. NCLua &amp; CCWS</strong>
    <p>Lua e CCWS virtualizados</p>
  </div>
</div>

---

<!-- _class: contrib-slide -->

# Contribuições

## Determinismo

<div style="display: grid; grid-template-columns: 1fr 1.25fr; gap: 24px; align-items: center; height: 215px;">
  <div>
    <ul style="font-size: 23px; line-height: 1.5; color: #24292f; margin: 0; padding-left: 24px;">
      <li>Modo <strong>headless</strong> em memória</li>
      <li>Avanço por <code>tick()</code> orquestrado</li>
      <li><strong>64 testes unitários</strong> em CI</li>
    </ul>
  </div>
  <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <img src="assets/headless_listing.png" style="max-height: 195px; max-width: 100%; object-fit: contain; border-radius: 4px; box-shadow: 0 2px 8px rgba(0,0,0,0.1); border: 1px solid #d0d7de;" />
  </div>
</div>

<div class="contrib-subheading">Decisões de Arquitetura</div>

<div class="contrib-grid">
  <div class="contrib-card dimmed">
    <strong>1. Engine Gráfica</strong>
    <p>Dart/Flutter unificado</p>
  </div>
  <div class="contrib-card highlight">
    <strong>2. UI Desacoplada</strong>
    <p>Lógica headless em memória</p>
  </div>
  <div class="contrib-card highlight">
    <strong>3. Relógio Virtual</strong>
    <p>Avanço via tick()</p>
  </div>
  <div class="contrib-card dimmed">
    <strong>4. NCLua &amp; CCWS</strong>
    <p>Lua e CCWS virtualizados</p>
  </div>
</div>

---

<!-- _class: contrib-slide -->

# Contribuições

## Debug

<div style="display: grid; grid-template-columns: 1fr 1.25fr; gap: 24px; align-items: center; height: 215px;">
  <div>
    <ul style="font-size: 23px; line-height: 1.5; color: #24292f; margin: 0; padding-left: 24px;">
      <li>Extensão <strong>ginga-code</strong> para VS Code</li>
      <li>Inspeção <strong>passo a passo</strong> (step)</li>
      <li>Sem necessidade de hardware STB</li>
    </ul>
  </div>
  <div style="display: flex; justify-content: center; align-items: center; height: 100%;">
    <img src="assets/vscode.png" style="max-height: 195px; max-width: 100%; object-fit: contain; border-radius: 6px; box-shadow: 0 4px 12px rgba(0,0,0,0.12); border: 1px solid #d0d7de;" />
  </div>
</div>

<div class="contrib-subheading">Decisões de Arquitetura</div>

<div class="contrib-grid">
  <div class="contrib-card dimmed">
    <strong>1. Engine Gráfica</strong>
    <p>Dart/Flutter unificado</p>
  </div>
  <div class="contrib-card highlight">
    <strong>2. UI Desacoplada</strong>
    <p>Lógica headless em memória</p>
  </div>
  <div class="contrib-card highlight">
    <strong>3. Relógio Virtual</strong>
    <p>Avanço via tick()</p>
  </div>
  <div class="contrib-card dimmed">
    <strong>4. NCLua &amp; CCWS</strong>
    <p>Lua e CCWS virtualizados</p>
  </div>
</div>

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
