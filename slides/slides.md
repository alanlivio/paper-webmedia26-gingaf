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
</style>

<!--
_paginate: false
_header: ""
-->

<div style="display: grid; grid-template-columns: 3fr 1fr; align-items: center;">

<div>

# gingaf: A Cross-Platform Architecture To Execute Ginga-NCL and Ginga-HTML5 Applications

**Alan L. V. Guedes**$^1$, **Paulo Victor Borges**$^2$, **Daniel Moraes**$^2$, **Sergio Colcher**$^2$
$^1$University of Reading, UK | $^2$PUC-Rio, Brazil

*Proceedings of the Brazilian Symposium on Multimedia and the Web (WebMedia 2026)*
Lavras/MG, Brazil

**Paper Website (slides, code, demo)**:
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

- **Context**
- **Proposed Solution**
- **Results**
- **Final Remarks**

---

# Background: Ginga DTV Middleware

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Standardization & Reach**
- Defined by ITU-T H.761 and SBTVD ABNT 15606.
- Deployed on 100% of certified Digital TV receivers across Brazil and Latin America (>60M viewers).

**Evolution of Ginga Subsystems**
- **Ginga-NCL**: Declarative multimedia synchronization and formatting.
- **NCLua**: Imperative scripting and dynamic canvas graphics.
- **Ginga-HTML5 & CCWS**: Web-based applications with broadcast data access.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/ginga.png" />

</div>

</div>

---

# The Problem: Platform Tethering

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Heavyweight C++ Players**
- Legacy implementations (PUC-Rio Ginga v0.13, v1.0) depend on platform-specific C++ frameworks (GTK, GStreamer, FFmpeg).
- Target embedded Linux STB environments, preventing web deployment.

**Tightly Coupled Presentation**
- State machine evaluations block on native OS rendering calls (`draw()`).
- Media objects trigger NCL transitions directly via system thread callbacks (`onEvent()`).

**Web Incompatibility**
- Sandboxed browser environments lack raw socket access and native POSIX threading.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/old_arch.png" />

</div>

</div>

---

# Layered Architecture: Subsystem Decoupling

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Strict Subsystem Separation**
- Logic components are strictly separated from UI components.

**Logic Layer (Pure Dart)**
- `NCLDocument` (Parser, NCLua runtime) and `CCWS` (HTTPServer, router).
- Compiles seamlessly to JavaScript and WebAssembly.

**Presentation Layer (Flutter)**
- `NCLWidget` (NCLuaWidget, NCLMediaState) and `HTMLWidget` (webview, js-interop).
- High-performance, pixel-perfect rendering across Web, desktop, and mobile.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/layered_arch.png" />

</div>

</div>

---

# Architectural Communication Flow

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Unidirectional Coordination**
- `NCLWidget` drives execution via explicit `tick()` calls.
- No direct reference held between `NCLDocument` and UI rendering widgets.

**Deterministic Synchronization**
- Engine edits internal `Media` states in document order.
- UI queries and synchronizes visual properties on-demand (`syncProperties()`).
- Completely eliminates race conditions and platform threading issues.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/arch.png" />

</div>

</div>

---

# NCL Logic & Document Object Model

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**In-Memory DOM Tree**
- XML document parsed into `Element` and `Node` hierarchy.
- Subclasses manage runtime states: `Media`, `Composition`, `Context`, `Switch`.
- `NCLua` encapsulates the embedded Lua runtime.

**Queue-Based Decoupling**
- `ActionQueue`: Collects deterministic link executions and state changes.
- `UIQueue`: Shares state changes across boundaries without coupling logic to rendering.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/elem_tree.png" />

</div>

</div>

---

# Portable NCLua: Canvas Translation Pipeline

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Pure Dart Lua Engine**
- Embeds `lua_dardo` (pure Dart Lua 5.3 interpreter).
- Runs in-browser without external C dependencies or WebAssembly bridges.

**Command List Abstraction**
- Lua drawing calls (`canvas:drawLine()`) are intercepted by NCLua.
- Serialized command lists are dispatched to `NCLuaWidgetState`.
- Flutter `CustomPainter` renders commands directly to the screen.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/lua_pipeline.png" />

</div>

</div>

---

# Portable NCLua in Practice

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Interactive Procedural Graphics**
- Execution of Lua scripts manipulating shapes, text, and animations in real time.

**Cross-Platform Parity**
- Same visual output across WebGL, Windows desktop, and mobile devices.

**Asynchronous Coroutines**
- Maps Lua coroutines to Dart `Future` and `async/await` paradigms without blocking the main tick.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/playground-lua.png" />

</div>

</div>

---

# Ginga-HTML5 & CCWS Architecture

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Native Clients (a)**
- HTML app runs in native WebView.
- Embedded local `HTTPServer` on port 44642 responds to standard HTTP requests.

**Web Client via Fetch Overloading (b)**
- HTML app runs in a sandboxed `iframe`.
- Injected shim overloads window `fetch()` and `XMLHttpRequest`.
- Intercepts requests and bridges them to Flutter via `postMessage`.
- Resolves promises transparently without requiring an HTTP server or browser extension.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/ccws_intercept.png" />

</div>

</div>

---

# Ginga-HTML5 in Practice

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Full CCWS Virtualization**
- Live discovery of broadcast services, program info, and channel metadata.

**Zero Configuration**
- HTML5 applications run without local web servers or special browser permissions.

**Seamless Integration**
- Broadcast-interactive web content embedded directly alongside declarative NCL compositions.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/playground-html.png" />

</div>

</div>

---

# Validation: GingaPlayground

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

**Browser-Native Workbench**
- Integrates `gingaf` Dart/Flutter web engine with Monaco code editor and live preview.

**Demonstrated Capabilities**
- Declarative NCL synchronization (`video.ncl`).
- Procedural Lua graphics rendering (`lua_canvas.ncl`).
- Ginga-HTML5 application with CCWS service discovery (`current_service.html`).
- Instant interactive execution directly via public URL without installation.

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/playground.png" />

</div>

</div>

---

# Final Remarks

- First cross-platform architecture unifying Ginga-NCL, NCLua, and Ginga-HTML5 across Web and Desktop.
- Portable Lua interpreter with Flutter canvas translation.
- Client-side CCWS network interception through `fetch` overloading.
- Open-source codebase, unit tests, and interactive web playground available openly.

---

<!--
_paginate: false
_header: ""
-->

# Thank You!

<div style="display: grid; grid-template-columns: 3fr 2fr; align-items: start;">

<div>

### Questions & Discussion

- **Repository**: https://github.com/ginga-org-br/gingaf
- **Playground**: https://ginga-org-br.github.io/gingaf/playground/
- **Contact**: `a.guedes@reading.ac.uk` | `danielmoraes@telemidia.puc-rio.br`

</div>

<div style="display: flex; justify-content: center; align-items: flex-start;">

<img src="assets/portal1.png" />

</div>

</div>
