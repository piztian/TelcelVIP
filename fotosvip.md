Perfecto, vamos a construir este nuevo catálogo dinámico para **equipos VIP** siguiendo el mismo sistema que ya tienes.

---

### ✅ **1. Paso: estructura de Google Sheet**

Asegúrate de que tu pestaña `Datos Equipos` tenga esta estructura y que ya esté publicada al web:

| TELEFONO         | PRECIO | CARACTERISTICAS             | Link Foto       |
| ---------------- | ------ | --------------------------- | --------------- |
| iPhone 16        | 19,999 | PANTALLA 6.1 / 6 GB / 128GB | *(por agregar)* |
| Samsung Z Flip 5 | 19,999 | PANTALLA 6.7 / 12GB / 256GB | *(por agregar)* |

Luego publica en la web la hoja, como ya lo has hecho antes.

---

### ✅ **2. Paso: URLs esperadas de GitHub**

Tus imágenes deberían tener estos links si están en el repo [TelcelVIP/fotos](https://github.com/piztian/TelcelVIP/tree/main/fotos):

```
https://raw.githubusercontent.com/piztian/TelcelVIP/main/fotos/Iphone%2016.jpg
https://raw.githubusercontent.com/piztian/TelcelVIP/main/fotos/Samsung%20Z%20flip%205.jpg
```

**Importante:** asegúrate de que los nombres de las fotos coincidan exactamente con los del campo `TELEFONO`, o crea una nueva columna `"Link Foto"` donde agregues la URL completa.

---

### ✅ **3. Paso: HTML para mostrar catálogo VIP**

Aquí tienes el HTML completo y comentado:

```html
<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8">
  <title>Catálogo VIP - Telcel</title>
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <style>
    body {
      margin: 0;
      font-family: 'Segoe UI', sans-serif;
      background-color: #f4f4f4;
    }
    h1 {
      text-align: center;
      margin: 20px;
    }
    .grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(280px, 1fr));
      gap: 20px;
      padding: 20px;
      max-width: 1200px;
      margin: auto;
    }
    .card {
      position: relative;
      overflow: hidden;
      border-radius: 10px;
      box-shadow: 0 4px 12px rgba(0,0,0,0.15);
      background: white;
    }
    .card img {
      width: 100%;
      height: auto;
      max-height: 250px;
      object-fit: contain;
      padding: 8px;
      background: white;
    }
    .info {
      padding: 15px;
    }
    .modelo {
      font-size: 18px;
      font-weight: bold;
      margin-bottom: 5px;
    }
    .caracteristicas {
      font-size: 14px;
      color: #444;
    }
    .precio {
      background: #e60023;
      color: white;
      font-weight: bold;
      padding: 5px 10px;
      border-radius: 5px;
      font-size: 16px;
      position: absolute;
      top: 10px;
      left: 10px;
    }
  </style>
</head>
<body>

<h1>🌟 Catálogo Telcel VIP</h1>
<div class="grid" id="catalogo"></div>

<script>
// 🔁 Llama a la API de opensheet que convierte la hoja "Datos Equipos" en JSON
fetch("https://opensheet.elk.sh/1H91IAn1suzgIZaZ7VXzpGpM-CWvPf9dKv_hUNoELjFg/Datos%20Equipos")

  // 🔁 Convierte a JSON
  .then(response => response.json())

  // 🔁 Recorre los datos y genera el HTML
  .then(data => {
    const container = document.getElementById("catalogo");

    data.forEach(item => {
      const html = `
        <div class="card">
          <a href="${item['Link Foto']}" target="_blank">
            <img src="${item['Link Foto']}" alt="${item.TELEFONO}">
          </a>
          <div class="precio">$${item.PRECIO}</div>
          <div class="info">
            <div class="modelo">${item.TELEFONO}</div>
            <div class="caracteristicas">${item.CARACTERISTICAS}</div>
          </div>
        </div>
      `;
      container.insertAdjacentHTML("beforeend", html);
    });
  });
</script>

</body>
</html>
```

---

### ✅ ¿Qué sigue?

1. Asegúrate que la hoja de cálculo esté **publicada en la web**
2. Agrega los links de cada imagen en la columna `"Link Foto"` (formato JPG, sin espacios raros)
3. Guarda el HTML y ábrelo en navegador

¿Quieres que te prepare el `README.md` para ese repositorio también?
