---
title: "gingaf: A Cross-Platform Architecture to Execute Ginga-NCL and Ginga-HTML5 Applications"
template: "home.html"
hide:
  - navigation
authors:
  - name: Alan L. V. Guedes
    institution: University of Reading
  - name: Paulo Victor Borges
    institution: PUC-Rio
  - name: Daniel Moraes
    institution: PUC-Rio
  - name: Sergio Colcher
    institution: PUC-Rio
conference: "WebMedia 2026"
links:
  - name: Paper
    url: https://sol.sbc.org.br/index.php/webmedia/article/view/46098
    icon: ri:file-pdf-2-line
  - name: Pre-print
    url: assets/pdfs/main.pdf
    icon: ri:file-pdf-2-line
  - name: Slides
    url: slides/
    icon: ri:slideshow-line
  - name: Software Code
    url: https://github.com/ginga-org-br/gingaf
    icon: ri:github-line
  - name: LaTeX/Website Code
    url: https://github.com/alanlivio/paper-gingaf-webmedia26
    icon: ri:github-line
description: "gingaf: A Cross-Platform Architecture to Execute Ginga-NCL and Ginga-HTML5 Applications. WebMedia 2026."
---

<div class="abstract-container" markdown="1">
<div class="abstract-inner" markdown="1">

## Abstract

The Ginga middleware, alongside its Ginga-NCL and Ginga-HTML5 subsystems, is an international standard for interactive digital television defined by the ITU-T/SBTDVD and used TV in Brazil and several Latin American countries. It reaches over 60 million people. However, traditional Ginga development tools rely on heavy, platform-specific C++ implementations, creating a steep barrier to entry for developers. This paper presents <span style="font-variant: small-caps;">gingaf</span>, a Ginga architecture support running both Ginga-NCL and Ginga-HTML5 applications directly from web browser, mobile or desktop. By decoupling the headless NCL state from the user interface, <span style="font-variant: small-caps;">gingaf</span> allows developers to execute synchronization logic deterministically while rendering seamlessly via pure Web HTML/JS. We present the extended architecture supporting imperative subsystems, including a pure Dart Lua interpreter (lua_dardo) translating canvas instructions, and a cross-platform HTML player that intercepts network requests via fetch overloading for Ginga-CCWebservices. This architecture does not require any native browser plugins, paving the way for web-based Ginga playgrounds and interactive debugging environments.

</div>
</div>

## Playground Demonstrations

The following videos demonstrate the interactive Ginga Playground executing different Ginga applications on the Web:

<div style="display: grid; grid-template-columns: repeat(auto-fit, minmax(400px, 1fr)); gap: 2rem; margin-top: 1rem; margin-bottom: 2rem;">
  <div style="text-align: center;">
    <h3 style="margin-top: 0; font-size: 1.25rem;">Ginga-NCL (video.ncl)</h3>
    <video src="assets/playground-ncl.mp4" controls style="width: 100%; border-radius: 0.5rem;"></video>
  </div>
  <div style="text-align: center;">
    <h3 style="margin-top: 0; font-size: 1.25rem;">Ginga-HTML5 (current_service.html)</h3>
    <video src="assets/playground-html.mp4" controls style="width: 100%; border-radius: 0.5rem;"></video>
  </div>
  <div style="text-align: center;">
    <h3 style="margin-top: 0; font-size: 1.25rem;">Ginga-NCL with Lua (lua.ncl)</h3>
    <video src="assets/playground-lua.mp4" controls style="width: 100%; border-radius: 0.5rem;"></video>
  </div>
</div>

## Citation

```bibtex
@inproceedings{webmedia,
 author = {Alan L. V. Guedes and Paulo Victor Borges and Daniel Moraes and Sergio Colcher},
 title = { gingaf: A Cross-Platform Architecture to Execute Ginga-NCL and Ginga-HTML5 Applications},
 booktitle = {Proceedings of the 32nd Brazilian Symposium on Multimedia and the Web},
 location = {Lavras/MG},
 year = {2026},
 keywords = {},
 issn = {0000-0000},
 pages = {254--261},
 publisher = {SBC},
 address = {Porto Alegre, RS, Brasil},
 doi = {10.5753/webmedia.2026.30538},
 url = {https://sol.sbc.org.br/index.php/webmedia/article/view/46098}
}
```
