Aquí tienes el **.md** para el carrusel de 2 imágenes (VIP primero), listo para pegar en tu repo:

---

# Carrusel Tablas de Planes Telcel (Bitrix-proof)

Carrusel minimalista de **dos imágenes** (tablas de planes), **sin librerías**, compatible con **Bitrix Sites**, **autoplay** y **responsive**. Muestra **primero VIP** y después **1–4**.

---

## ✅ Qué incluye

* 2 slides con imágenes **RAW** de GitHub.
* **Autoplay** cada 7 s (configurable).
* Flechas y **paginación** (puntitos) clicables.
* **Responsive**: relación 16:9 en desktop y 4:5 en móvil.
* IDs únicos (`*-tablas`) para no chocar con otros carruseles.

---

## 📁 Imágenes (RAW GitHub)

Asegúrate de que los archivos existan en el repo y rama correctos.

* VIP:
  `https://raw.githubusercontent.com/piztian/TelcelVIP/main/fotos/tabladeplanes/Manteleta_PTL-5-VP-scaled.jpg`
* 1–4:
  `https://raw.githubusercontent.com/piztian/TelcelVIP/main/fotos/tabladeplanes/Manteleta_PTL-1-4-scaled.jpg`

> Si cambias nombres/carpeta/rama, actualiza las URLs.

---

## 🧩 Código para Bitrix

Pega este bloque en un bloque **HTML** de Bitrix (no requiere CSS/JS externos).

```html
<!-- ====== CARRUSEL TABLAS TELCEL (VIP primero) ====== -->
<div style="--gap:12px; --pad:0; --radius:14px; --b:#e9e9e9; --brand:#0a66c2; font-family:Segoe UI,system-ui,Arial,sans-serif;">
  <div style="max-width:1200px;margin:20px auto;padding:0 16px;position:relative">

    <!-- Flechas de navegación -->
    <button id="prev-tablas" aria-label="Anterior"
      style="position:absolute;left:0;top:50%;transform:translateY(-50%);border:0;background:#fff;border-radius:50%;width:36px;height:36px;box-shadow:0 2px 10px rgba(0,0,0,.15);cursor:pointer;z-index:2">‹</button>
    <button id="next-tablas" aria-label="Siguiente"
      style="position:absolute;right:0;top:50%;transform:translateY(-50%);border:0;background:#fff;border-radius:50%;width:36px;height:36px;box-shadow:0 2px 10px rgba(0,0,0,.15);cursor:pointer;z-index:2">›</button>

    <!-- Riel (contenedor horizontal de slides) -->
    <div id="rail-tablas"
      style="display:flex;gap:var(--gap);overflow:auto;scroll-snap-type:x mandatory;padding:0 48px;scrollbar-width:none;-ms-overflow-style:none">
      <style>
        #rail-tablas::-webkit-scrollbar{display:none}
        .slide-tabla{scroll-snap-align:start;flex:0 0 100%}
        .card-tabla{background:#fff;border:1px solid var(--b);border-radius:var(--radius);padding:var(--pad);box-shadow:0 4px 14px rgba(0,0,0,.06);overflow:hidden}
        .frame-tabla{width:100%;aspect-ratio:16/9;background:#f7f7f7;display:flex;align-items:center;justify-content:center}
        .frame-tabla img{max-width:100%;max-height:100%;object-fit:contain;display:block}
        @media (max-width:768px){.frame-tabla{aspect-ratio:4/5}}
      </style>

      <!-- SLIDE 1 → VIP primero -->
      <div class="slide-tabla">
        <div class="card-tabla">
          <div class="frame-tabla">
            <img loading="lazy" alt="Tabla Planes Telcel VIP"
              src="https://raw.githubusercontent.com/piztian/TelcelVIP/main/fotos/tabladeplanes/Manteleta_PTL-5-VP-scaled.jpg">
          </div>
        </div>
      </div>

      <!-- SLIDE 2 → Planes 1–4 -->
      <div class="slide-tabla">
        <div class="card-tabla">
          <div class="frame-tabla">
            <img loading="lazy" alt="Tabla Planes Telcel 1–4"
              src="https://raw.githubusercontent.com/piztian/TelcelVIP/main/fotos/tabladeplanes/Manteleta_PTL-1-4-scaled.jpg">
          </div>
        </div>
      </div>

    </div><!-- /rail -->

    <!-- Paginación (puntitos) -->
    <div id="dots-tablas" aria-label="paginación"
      style="display:flex;justify-content:center;gap:8px;margin-top:10px"></div>

  </div>
</div>

<script>
(function(){
  const rail = document.getElementById('rail-tablas');
  const prev = document.getElementById('prev-tablas');
  const next = document.getElementById('next-tablas');
  const slides = Array.from(rail.querySelectorAll('.slide-tabla'));
  const dots = document.getElementById('dots-tablas');

  // ===== CONFIG =====
  let AUTOPLAY_MS = 7000; // ⏱ Tiempo de cambio en milisegundos
  const padSide = 48;     // Padding lateral del riel (para scroll preciso)

  // Crear puntitos de navegación
  slides.forEach((_, i)=>{
    const d=document.createElement('span');
    d.style.cssText='width:10px;height:10px;border-radius:50%;background:#cfd8e3;display:inline-block;cursor:pointer';
    d.addEventListener('click',()=> rail.scrollTo({left: slides[i].offsetLeft - padSide, behavior:'smooth'}));
    dots.appendChild(d);
  });

  // Cambiar puntito activo
  const setActive = () => {
    const mid = rail.scrollLeft + rail.clientWidth/2;
    let idx = 0;
    slides.forEach((s,i)=>{ if(s.offsetLeft + s.clientWidth/2 < mid) idx = i; });
    dots.childNodes.forEach((el,j)=> el.style.background = (j===idx?'#0a66c2':'#cfd8e3'));
  };
  rail.addEventListener('scroll', ()=> requestAnimationFrame(setActive));
  setActive();

  // Funciones de navegación
  const step = () => rail.clientWidth; // avanza una pantalla completa
  prev.addEventListener('click', ()=> rail.scrollBy({left: -step(), behavior:'smooth'}));
  next.addEventListener('click', ()=> rail.scrollBy({left: step(), behavior:'smooth'}));

  // Autoplay con pausa al interactuar
  let timer = setInterval(()=> rail.scrollBy({left: step(), behavior:'smooth'}), AUTOPLAY_MS);
  const pause = ()=> clearInterval(timer);
  const play  = ()=> timer = setInterval(()=> rail.scrollBy({left: step(), behavior:'smooth'}), AUTOPLAY_MS);
  rail.addEventListener('pointerenter', pause);
  rail.addEventListener('pointerleave', play);
  window.addEventListener('blur', pause);
  window.addEventListener('focus', play);

  // Ajustar puntito activo en resize
  window.addEventListener('resize', ()=> requestAnimationFrame(setActive));
})();
</script>
<!-- ====== /CARRUSEL TABLAS TELCEL ====== -->
```

---

## 🔧 Cómo personalizar

* **Cambiar orden**: invierte los bloques `.slide-tabla`.
* **Tiempo de autoplay**: edita `AUTOPLAY_MS` (p. ej., `5000` para 5 s).
* **Tamaño**: ajusta `max-width` del contenedor (por defecto `1200px`) y/o `aspect-ratio`:

  * Desktop: `16/9` → más “ancho”.
  * Alternativa: `5/4` → más “alto” (mejor legibilidad).
* **Accesibilidad**: edita los `alt` de las imágenes con descripciones claras.

---

## 🧪 Troubleshooting

* Si una imagen **no carga**:

  1. Revisa la **URL RAW** (nombre exacto, mayúsculas, rama).
  2. Comprueba que el repo sea **público**.
  3. Borra caché / prueba en incógnito.
  4. En DevTools → **Network**: la imagen debe devolver **200** (no 404).

---

## 🗺️ Notas Bitrix

* Pega el bloque completo en un componente **HTML**.
* Evita duplicar IDs si ya tienes otros carruseles; estos usan sufijo `-tablas`.

---

¿Quieres que agregue **lightbox (zoom al tocar)** en una versión opcional? Te la paso como “v2” si te sirve.
