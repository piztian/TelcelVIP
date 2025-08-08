
# Telcel Planes Libres – Bitrix Site Integration

Este documento explica cómo funciona y qué componentes incluye el módulo de **Planes Telcel Libres** integrado en Bitrix24 Site. Aquí encontrarás detalles del funcionamiento, estructura, y cómo mantenerlo actualizado.

---

## 📦 ¿Qué hace este módulo?

Muestra una **vitrina dinámica tipo carrusel** con los 10 planes "Telcel Libre", incluyendo:

- Nombre del plan (Telcel Libre 1 a VIP)
- Precios abierto y controlado
- GB base y promocionales
- Porcentaje de Cashback
- Íconos de redes sociales incluidas
- Beneficios adicionales (Claro Drive y Claro Video)
- Botón de contacto personalizado

El diseño es responsivo y centrado visualmente.

---

## 🧱 Estructura del código

### HTML

- Cada tarjeta de plan está dentro de un `<div class="swiper-slide">`.
- Contiene la imagen de encabezado del plan, datos, íconos, beneficios y un botón.

### CSS

- Se ajustó la clase `.plan-logo` para que las imágenes de los planes no se distorsionen:
```css
.plan-logo {
  max-width: 180px;
  height: auto;
  display: block;
  margin: 0 auto 15px auto;
}
```

- Se usó SwiperJS para hacer el carrusel horizontal.

### JS (SwiperJS)

```js
const swiper = new Swiper('.mySwiper', {
  slidesPerView: 1,
  spaceBetween: 10,
  navigation: {
    nextEl: '.swiper-button-next',
    prevEl: '.swiper-button-prev',
  },
  breakpoints: {
    768: {
      slidesPerView: 2,
    },
    1024: {
      slidesPerView: 3,
    },
  },
});
```

---

## 🖼️ Imágenes

Las imágenes se alojan en GitHub para mayor estabilidad:
- Logos de cada plan: `https://raw.githubusercontent.com/piztian/TelcelVIP/main/fotos/planestelcel/`
- Redes sociales y beneficios: `https://raw.githubusercontent.com/piztian/TelcelVIP/main/fotos/redessociales/`

### Ejemplo:

```html
<img src="https://raw.githubusercontent.com/piztian/TelcelVIP/main/fotos/planestelcel/LOGO-PLANES-TELCEL-LIBRE_azul-249-1.png" class="plan-logo">
```

---

## 🔁 Cómo actualizar

1. **Agregar un nuevo plan:**
   - Duplicar una tarjeta `<div class="swiper-slide">`.
   - Actualizar texto, precios y rutas de imagen.

2. **Actualizar imagen:**
   - Subir el nuevo archivo a GitHub.
   - Reemplazar la URL en el HTML.

3. **Agregar red social o beneficio:**
   - Subir la imagen a GitHub.
   - Agregar `<img src="...">` en la sección correspondiente.

---

## 🛠️ Dependencias

- SwiperJS (ya está incluido en el HTML)
- Requiere que las imágenes estén disponibles públicamente en GitHub (raw).

---

## ✨ Mejoras futuras

- Agregar campo para “equipos incluidos” si aplica.
- Incorporar tooltip con info sobre promociones.
- Integrar Google Tag Manager o evento a botón de contacto.
- Agregar soporte multilenguaje si Bitrix lo requiere.

---

> Documento generado por ChatGPT para integración en Bitrix24 Site.
