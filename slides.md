---
theme: default
title: GitHub Actions · Del cambio a la publicación
info: |
  Automatización e integración continua con una demostración real en EXPOGIT.
class: hero
transition: fade
colorSchema: dark
aspectRatio: 16/9
canvasWidth: 1200
fonts:
  sans: Segoe UI
  mono: Consolas
drawings:
  persist: false
---

<div class="eyebrow">AUTOMATIZACIÓN E INTEGRACIÓN CONTINUA</div>

# GitHub<br>Actions

<div class="hero-sub">El trabajo que ocurre después de un cambio</div>
<div class="hero-line">Una presentación</div>
<div class="authors">Antony Guallasamin</div>
<div class="hero-aside">CAMBIAR<br><span>COMPROBAR</span><br>PUBLICAR</div>

<!--
Saludo: hoy vamos a explicar GitHub Actions con un proyecto que ya está funcionando. Esta misma presentación vive en un repositorio: cuando modificamos su contenido, GitHub la compila y después la publica. Primero veremos cómo funciona y luego haremos un cambio en vivo.
-->

---

<div class="eyebrow">LA IDEA</div>

# Una entrega de clase,<br>pero automática

<div class="sequence">
<div><b>01</b><h2>Cambio</h2><p>Un compañero modifica<br>el trabajo compartido.</p></div>
<div><b>02</b><h2>Revisión</h2><p>El equipo comprueba<br>que sigue funcionando.</p></div>
<div><b>03</b><h2>Entrega</h2><p>La versión revisada<br>llega al profesor.</p></div>
</div>

<div class="takeaway">En nuestro proyecto: editar → compilar → publicar.</div>

<!--
La analogía es una entrega grupal. No basta con recibir cambios: alguien debe revisarlos antes de entregar. Actions permite escribir las instrucciones de esa revisión y ejecutarlas automáticamente. La máquina revisa solo lo que le hemos pedido, no entiende por sí sola si la exposición es buena.
-->

---

<div class="eyebrow">CONCEPTOS</div>

# CI y CD

<div class="comparison">
<section><div class="big-label">CI</div><h2>Integración continua</h2><p>Comprueba los cambios<br>con compilación y pruebas.</p><small>En EXPOGIT: <code>npm run build</code></small></section>
<section><div class="big-label accent">CD</div><h2>Entrega continua</h2><p>Deja una versión lista<br>para publicar.</p><small>Puede esperar aprobación humana.</small></section>
<section><div class="big-label accent">CD</div><h2>Despliegue continuo</h2><p>Publica automáticamente<br>si pasan los controles.</p><small>En EXPOGIT: GitHub Pages</small></section>
</div>

<div class="takeaway">Entrega continua puede incluir aprobación; despliegue continuo publica automáticamente.</div>

<!--
CI significa integración continua. Nuestro ejemplo comprueba que la presentación compile; no tenemos pruebas unitarias configuradas. CD tiene dos usos: continuous delivery deja la versión preparada, y continuous deployment la publica automáticamente al superar los controles. Nuestro workflow de Pages es un ejemplo de despliegue automático.
Fuente: https://docs.github.com/en/actions/get-started/understand-github-actions
-->

---

<div class="eyebrow">LA CONFIGURACIÓN</div>

# Un workflow real dentro de GitHub

<div class="image-split">
<div><h2><code>.github/<br>workflows/<br>ci.yml</code></h2><p>YAML describe cuándo<br>y cómo ejecutar<br>la automatización.</p><a href="https://github.com/Anyxg12/github-actions-live-lab/blob/main/.github/workflows/ci.yml" target="_blank" rel="noopener">Ver nuestro archivo ↗</a></div>
<img src="/images/workflow-live.png" alt="Captura real de un archivo YAML de workflow en GitHub">
</div>

<!--
Esta captura muestra un ejemplo de GitHub, obtenido el 19 de septiembre de 2026. El enlace abre nuestro ci.yml real. Los workflows son archivos de texto guardados junto al código, por eso también tienen historial de cambios. La indentación de YAML expresa qué parte pertenece a cada sección.
Fuente: https://docs.github.com/en/actions/concepts/workflows-and-actions/workflows
-->

---

<div class="eyebrow">NUESTRO PROYECTO</div>

# Una presentación que<br>explica su propia publicación

<div class="file-list">
<div><code>slides.md</code><span>El contenido de estas diapositivas.</span></div>
<div><code>package.json</code><span>Los comandos y las dependencias.</span></div>
<div><code>package-lock.json</code><span>Las versiones concretas que instalamos.</span></div>
<div><code>.github/workflows/</code><span>Las instrucciones de automatización.</span></div>
</div>

<!--
Slidev transforma un archivo Markdown en una presentación web. Podemos editar texto sin diseñar cada página desde cero. package.json declara el comando build. package-lock registra las versiones que npm ci instalará. GitHub busca los workflows dentro de .github/workflows. Mostrar estos archivos en el editor si hace falta.
-->

---

<div class="eyebrow">DEL EDITOR A GITHUB</div>

# Guardar no es publicar

<div class="sequence">
<div><b>01</b><h2><code>git add</code></h2><p>Prepara los archivos<br>que entrarán al commit.</p></div>
<div><b>02</b><h2><code>git commit</code></h2><p>Guarda una versión<br>en el historial local.</p></div>
<div><b>03</b><h2><code>git push</code></h2><p>Envía los commits<br>al repositorio remoto.</p></div>
</div>

<div class="takeaway">En nuestra configuración, el push a main activa CI.</div>

<!--
Guardar el archivo solo cambia nuestra computadora. add selecciona el cambio; commit guarda la versión en Git local; push la envía a GitHub. El push es el evento que inicia CI. GitHub Pages publica después, si la comprobación y la compilación del sitio salen bien.
-->

---

<div class="eyebrow">EL WORKFLOW</div>

# Las piezas de Actions

<div class="terms">
<div><strong>Evento</strong><p>Lo que activa el proceso.<br>Ejemplo: un push.</p></div>
<div><strong>Job</strong><p>Un trabajo que agrupa<br>varios pasos.</p></div>
<div><strong>Runner</strong><p>La máquina que<br>ejecuta ese trabajo.</p></div>
<div><strong>Step</strong><p>Un comando con <code>run</code><br>o una acción con <code>uses</code>.</p></div>
</div>
<div class="takeaway">Los pasos van en orden. Los jobs pueden depender de otros jobs.</div>

<!--
No hace falta memorizar todo el vocabulario. Evento: cuándo. Job: qué trabajo. Runner: dónde. Step: cada instrucción. En CI tenemos un job de compilación. En Pages hay un job para preparar el sitio y otro para publicarlo.
Fuente: https://docs.github.com/en/actions/get-started/understand-github-actions
-->

---

<div class="eyebrow">CI.YML · FRAGMENTO DEL ARCHIVO</div>

# Cuándo y dónde se ejecuta

<div class="code-split">
<div>

```yaml
on:
  push:
    branches: [main]
  pull_request:
    branches: [main]
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
```

</div>
<div class="explain"><h2>El evento activa el trabajo</h2><p><code>push</code>: cambios enviados a main.</p><p><code>pull_request</code>: propuesta de cambios hacia main.</p><p><code>workflow_dispatch</code>: inicio manual.</p><p><code>ubuntu-latest</code>: runner administrado por GitHub.</p></div>
</div>

<!--
Este es un fragmento, no el archivo completo. Los espacios en YAML definen qué configuración pertenece a cada sección. push filtra la rama main. pull_request permite comprobar una propuesta antes de integrarla. workflow_dispatch ofrece un botón para ejecutar manualmente. ubuntu-latest selecciona una imagen de Ubuntu mantenida por GitHub; su versión cambia con el tiempo.
Fuente: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows
-->

---

<div class="eyebrow">CI.YML · LOS PASOS REALES</div>

# Qué hace la comprobación

<div class="code-split">
<div>

```yaml
steps:
  - uses: actions/checkout@v7
  - uses: actions/setup-node@v7
    with:
      node-version: '24'
      cache: npm
  - run: npm ci
  - run: npm run build
```

</div>
<div class="explain"><p><strong>Checkout</strong><br>Descarga el código del commit.</p><p><strong>Setup Node</strong><br>Prepara Node.js 24.</p><p><strong>npm ci</strong><br>Instala las dependencias del lockfile.</p><p><strong>npm run build</strong><br>Ejecuta <code>slidev build</code>.</p></div>
</div>

<!--
uses reutiliza una acción; run ejecuta un comando. checkout y setup-node ya resuelven tareas comunes. cache npm guarda la caché de descargas; no reutiliza directamente node_modules. npm ci exige un lockfile coherente con package.json. build produce los archivos web en dist. Si compila, conocemos ese resultado; no significa que todos los contenidos o enlaces sean correctos.
Fuente: https://docs.github.com/en/actions/tutorials/build-and-test-code/nodejs
-->

---

<div class="eyebrow">EVENTOS</div>

# Triggers: el momento de empezar

<div class="file-list triggers">
<div><code>push</code><span>Se envían commits o tags al repositorio.</span></div>
<div><code>pull_request</code><span>Se abre o actualiza una propuesta de cambios.</span></div>
<div><code>workflow_dispatch</code><span>Una persona inicia el workflow manualmente.</span></div>
<div><code>schedule</code><span>Una programación activa una tarea periódica.</span></div>
</div>

<div class="takeaway">Nuestro despliegue usa además workflow_run: espera a que termine CI.</div>

<!--
Un trigger es el evento que inicia el workflow. Estos son ejemplos generales; nuestro ci.yml limita push y pull_request a main. schedule no está configurado en EXPOGIT. workflow_run enlaza el final de CI con Pages y permite comprobar su resultado antes de continuar.
Fuente: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows
-->

---

<div class="eyebrow">RUNNERS</div>

# ¿De quién es la máquina?

<div class="comparison">
<section><h2>GitHub-hosted</h2><p>GitHub prepara y mantiene<br>el entorno de ejecución.</p><code>runs-on: ubuntu-latest</code><small>Como usar el laboratorio de la universidad.</small></section>
<section><h2>Self-hosted</h2><p>El equipo instala y mantiene<br>su propia máquina.</p><code>runs-on: self-hosted</code><small>Como trabajar en tu propio laboratorio.</small></section>
</div>
<div class="takeaway">Nuestra demo usa un runner de GitHub: no depende de que esta PC siga encendida.</div>

<!--
Un runner ejecuta el trabajo, no es el repositorio. Con GitHub-hosted tenemos un entorno preparado. Con self-hosted controlamos hardware y software, pero asumimos mantenimiento y seguridad. En esta demo, después del push podemos apagar nuestra PC y GitHub continúa trabajando.
Fuente: https://docs.github.com/en/actions/concepts/runners/github-hosted-runners
-->

---

<div class="eyebrow">ACCIONES REUTILIZABLES</div>

# Marketplace

<div class="image-split">
<div><p>Un catálogo de acciones<br>para tareas comunes.</p><h2>Buscar → revisar → reutilizar</h2><p class="muted">Antes de elegir: autor,<br>documentación y versión.</p><a href="https://github.com/marketplace?type=actions" target="_blank" rel="noopener">Abrir Marketplace ↗</a></div>
<img src="/images/marketplace-live.png" alt="Captura real de GitHub Marketplace con su catálogo de acciones">
</div>

<!--
Marketplace evita reinventar pasos habituales. Pero una acción ejecuta código dentro del workflow, por eso debemos revisar su procedencia y permisos. Abrir el enlace para mostrar el catálogo si hay tiempo. La captura fue obtenida el 19 de septiembre de 2026; el catálogo puede cambiar.
Fuente y captura: https://github.com/marketplace?type=actions
-->

---

<div class="eyebrow">UNA ACCIÓN POR DENTRO</div>

# actions/checkout@v7

<div class="image-split">
<div><div class="file-list compact"><div><code>actions</code><span>Organización.</span></div><div><code>checkout</code><span>Acción que usamos.</span></div><div><code>@v7</code><span>Versión principal.</span></div></div><p class="muted">Descarga el repositorio<br>para que los pasos usen sus archivos.</p></div>
<img src="/images/checkout-live.png" alt="Captura real de la ficha de Checkout en GitHub">
</div>

<!--
Leer la referencia en tres partes ayuda a entender uses. @v7 es una etiqueta de versión principal; para mayor reproducibilidad en proyectos sensibles se puede fijar el SHA de la acción. Aquí usamos la misma versión que funciona en nuestro workflow. Captura del 19 de septiembre de 2026.
Fuente: https://github.com/actions/checkout
-->

---
class: demo-break
---

<div class="eyebrow">DEMOSTRACIÓN EN VIVO</div>

# Un cambio.<br>Un push.<br><span>Una comprobación.</span>

<p>Ahora pasamos del concepto al repositorio.</p>
<a href="https://github.com/Anyxg12/github-actions-live-lab/actions" target="_blank" rel="noopener">Abrir nuestras ejecuciones en Actions ↗</a>

<!--
Pausa y pasa a Antigravity. Primero muestra el repositorio y Actions. Podemos comenzar con un cambio visible: modificar un título y hacer add, commit y push. No uses un re-run del fallo anterior como corrección: re-run vuelve a ejecutar el mismo commit. El nuevo contenido requiere un nuevo commit. Espera el resultado de CI y después Pages.
-->

---

<div class="eyebrow">PASO 1 · CAMBIO VISIBLE</div>

# Del editor a la pantalla

<div class="code-split">
<div>

```bash
git add slides.md
git commit -m "docs: actualizar título de la demo"
git push origin main
```

</div>
<div class="explain"><p>Editamos un título en <code>slides.md</code>.</p><p>Subimos el cambio y observamos CI.</p><p>Si CI pasa, Pages prepara y publica el sitio.</p><p>Recargamos la página para ver el título nuevo.</p></div>
</div>

<!--
Antes de empezar, comprueba git status. Cambia una frase corta para que el público la identifique. Ejecuta cada comando y explica su función. Mantén abierta la presentación actual mientras GitHub trabaja y recarga cuando Pages finalice. Un cambio de texto sencillo permite mostrar el proceso completo sin provocar un error todavía.
-->

---

<div class="eyebrow">PASO 2 · FALLO CONTROLADO</div>

# Pedimos compilar<br>un archivo inexistente

<div class="code-split">
<div>

```json
"build": "slidev build diapositiva-inexistente.md"
```

```bash
git add package.json
git commit -m "test: provocar fallo controlado"
git push origin main
```

</div>
<div class="explain"><p>El archivo real sigue siendo <code>slides.md</code>.</p><p>CI ejecuta el comando modificado y detecta el fallo.</p><p class="failure">La nueva versión no llega a publicarse.</p></div>
</div>

<!--
Repetimos el fallo ya ensayado. Edita solo el valor del script build en package.json, manteniendo la coma si corresponde. Al no existir el archivo, Slidev termina con error. CI falla y el job de preparación de Pages queda omitido por su condición. La versión publicada anteriormente permanece disponible. No provoques un error en el YAML: queremos mostrar el fallo de la aplicación y sus logs.
-->

---

<div class="eyebrow">EL REGISTRO REAL DE NUESTRA DEMO</div>

# El rojo indica dónde investigar

<div class="evidence">
<img src="/images/fallo-demo.png" alt="Captura de nuestra ejecución fallida en GitHub Actions, con estado Failure y exit code 1">
<div><h2>Failure</h2><p>Un paso terminó con error.</p><h2>Exit code 1</h2><p>Indica fallo; los logs explican la causa.</p><a href="https://github.com/Anyxg12/github-actions-live-lab/actions/runs/36635169354" target="_blank" rel="noopener">Abrir el fallo registrado ↗</a></div>
</div>

<!--
Esta captura pertenece a nuestra ejecución controlada. Muestra el resultado general, no el mensaje detallado del archivo inexistente. Haz clic en Instalar y compilar y abre Compilar presentación. Busca el primer mensaje útil del error, no solo la última línea exit code 1. Distinguir el síntoma y la causa permite explicar por qué vamos a corregir el comando.
Evidencia: https://github.com/Anyxg12/github-actions-live-lab/actions/runs/36635169354
-->

---

<div class="eyebrow">PASO 3 · CORRECCIÓN</div>

# Restaurar, subir,<br>volver a comprobar

<div class="code-split">
<div>

```json
"build": "slidev build"
```

```bash
git add package.json
git commit -m "fix: restaurar compilación"
git push origin main
```

</div>
<div class="explain"><p>Restauramos el comando correcto.</p><p>El nuevo commit activa otra ejecución.</p><p class="success">CI vuelve a verde y habilita el despliegue.</p><p class="muted">El fallo anterior permanece en el historial.</p></div>
</div>

<!--
No borramos la ejecución roja: forma parte de la evidencia. El historial cuenta la historia del cambio y su solución. Ejecutar otra vez el mismo commit defectuoso no lo arregla. Después de corregir, muestra el nuevo commit y su workflow. Verde significa que los pasos configurados terminaron correctamente.
-->

---

<div class="eyebrow">DEPLOY.YML</div>

# De CI a GitHub Pages

<div class="sequence">
<div><b>01</b><h2>CI pasa</h2><p>Pages recibe el resultado<br>del workflow de CI.</p></div>
<div><b>02</b><h2>Build</h2><p>Compila ese commit<br>y empaqueta <code>dist</code>.</p></div>
<div><b>03</b><h2>Deploy</h2><p>Publica el artefacto<br>en GitHub Pages.</p></div>
</div>
<div class="takeaway"><code>needs: build</code> hace que deploy espere a la preparación del sitio.</div>

<!--
El workflow de Pages se activa cuando termina CI mediante workflow_run. Comprueba que CI haya sido exitoso y corresponda a un push de nuestro repositorio. Checkout usa el SHA del commit comprobado, no una versión distinta de main. Dentro de Pages, needs build conecta los dos jobs. Build vuelve a compilar con la base de la URL y sube dist; deploy-pages publica el artefacto. El inicio manual también está disponible y compila antes de publicar.
Fuente: https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages
Fuente: https://docs.github.com/en/actions/reference/workflows-and-actions/events-that-trigger-workflows#workflow_run
-->

---

<div class="eyebrow">MÁS APLICACIONES</div>

# El mismo mecanismo,<br>otras tareas

<div class="terms applications">
<div><strong>Pruebas</strong><p>Ejecutar <code>npm test</code><br>cuando el proyecto<br>tiene pruebas configuradas.</p></div>
<div><strong>Seguridad</strong><p>Analizar código<br>con herramientas<br>como CodeQL.</p></div>
<div><strong>Mantenimiento</strong><p>Programar tareas<br>con <code>schedule</code><br>y revisar sus resultados.</p></div>
</div>
<div class="takeaway">Automatizamos instrucciones concretas; seguimos necesitando revisión humana.</div>

<!--
Estas son posibilidades, no funciones que ya estén habilitadas en EXPOGIT. No tenemos npm test ni CodeQL configurados. Actions sirve para varias tareas porque el mecanismo es el mismo: evento, runner y pasos. Una automatización comprueba lo que definimos, por eso no sustituye todas las revisiones.
Fuentes: https://docs.github.com/en/actions/get-started/understand-github-actions y https://docs.github.com/en/code-security/code-scanning/introduction-to-code-scanning/about-code-scanning-with-codeql
-->

---
class: closing
---

<div class="eyebrow">RESULTADO</div>

# Cada cambio deja<br><span>una evidencia.</span>

<p>El commit registra qué cambió.<br>Actions registra qué ocurrió.<br>Pages muestra la versión publicada.</p>

<a href="https://anyxg12.github.io/github-actions-live-lab/" target="_blank" rel="noopener">Ver la presentación publicada ↗</a>

<div class="closing-question">¿Qué tarea repetitiva automatizarías en tu próximo proyecto?</div>

<!--
Cierre: hoy vimos un cambio correcto, un fallo y su corrección. No solo contamos que funciona: dejamos registros que pueden revisarse. La automatización hace repetible el trabajo, pero sus controles deben diseñarse. Invita a una pregunta o plantea qué tarea automatizarían en un proyecto de clase.
-->

---

<div class="eyebrow">REFERENCIAS Y EVIDENCIA</div>

# Para revisar y practicar

<div class="source-list">
<a href="https://docs.github.com/en/actions/get-started/understand-github-actions" target="_blank" rel="noopener">GitHub Docs · Conceptos de Actions</a>
<a href="https://docs.github.com/en/actions/tutorials/build-and-test-code/nodejs" target="_blank" rel="noopener">GitHub Docs · Compilar proyectos Node.js</a>
<a href="https://docs.github.com/en/pages/getting-started-with-github-pages/using-custom-workflows-with-github-pages" target="_blank" rel="noopener">GitHub Docs · Publicación en Pages</a>
<a href="https://github.com/marketplace?type=actions" target="_blank" rel="noopener">Marketplace · Acciones reutilizables</a>
<a href="https://github.com/Anyxg12/github-actions-live-lab" target="_blank" rel="noopener">Nuestro repositorio · Código y workflows</a>
<a href="https://github.com/Anyxg12/github-actions-live-lab/actions" target="_blank" rel="noopener">Nuestras ejecuciones · Éxitos, fallo y corrección</a>
</div>

<p class="source-note">Capturas de Marketplace y Checkout: 19/09/2026.<br>Demostración del repositorio: 29/09/2026.</p>

<!--
Los enlaces son clicables. Las capturas anteriores muestran interfaces reales de GitHub y se reutilizan como referencia visual del material previo. El fallo pertenece a este repositorio. Para ensayar: editor, Actions y presentación publicada en tres pestañas. La explicación oral está en las notas de cada diapositiva.
-->
