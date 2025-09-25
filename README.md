[README.md](https://github.com/user-attachments/files/22548526/README.md)
# Galería interactiva de modelos GLB en Realidad Aumentada

Este repositorio incluye una galería web para visualizar varios modelos `.glb` en 3D y Realidad Aumentada (RA) usando [Google Model Viewer](https://modelviewer.dev/). Puedes activar/desactivar la visualización de cada modelo para explorar su comportamiento de manera individual o grupal.

---

## ¿Cómo funciona la galería?

- **Visualiza todos los modelos a la vez o selecciona cuáles mostrar.**
- **Activa/desactiva la visualización de cada modelo con un solo clic.**
- **Explora los modelos en RA desde dispositivos compatibles.**
- **Galería de miniaturas para seleccionar el modelo que deseas ver.**

---

## Estructura de archivos

Los modelos `.glb` se encuentran en la raíz del repositorio:

```
/
  ├── ARQ.glb
  ├── EST.glb
  ├── HDR.glb
  ├── ELE.glb
  ├── HVAC.glb
  └── RCI.glb
```

---

## Ejemplo de galería interactiva

Guarda el siguiente código como `index.html` en tu repositorio, en la raíz junto a tus modelos `.glb`.

```html
<!DOCTYPE html>
<html>
<head>
  <title>Galería de Modelos 3D y RA</title>
  <script type="module" src="https://unpkg.com/@google/model-viewer/dist/model-viewer.min.js"></script>
  <style>
    body { font-family: Arial, sans-serif; margin: 0; padding: 0; background: #fafafa;}
    h1 { text-align: center; margin-top: 1em; }
    .gallery { display: flex; flex-wrap: wrap; justify-content: center; gap: 1em; margin-bottom: 2em;}
    .gallery-item { text-align: center; }
    .controls { display: flex; justify-content: center; gap: 2em; flex-wrap: wrap; margin-bottom: 2em;}
    .model-container { display: flex; flex-wrap: wrap; justify-content: center; gap: 2em;}
    model-viewer { width: 350px; height: 350px; border-radius: 12px; background: #fff; box-shadow: 0 2px 12px #0001;}
    .toggle-btn { margin-top: 0.5em;}
  </style>
</head>
<body>
  <h1>Galería interactiva de modelos 3D y RA</h1>
  <div class="gallery" id="gallery">
    <!-- Miniaturas de los modelos -->
  </div>
  <div class="controls" id="controls">
    <!-- Botones de activación/desactivación -->
  </div>
  <div class="model-container" id="modelContainer">
    <!-- Modelos visualizados -->
  </div>
  <script>
    // Lista de modelos (puedes personalizar los nombres y archivos)
    const models = [
      { name: 'ARQ', file: 'ARQ.glb', poster: 'ARQ.png' },
      { name: 'EST', file: 'EST.glb', poster: 'EST.png' },
      { name: 'HDR', file: 'HDR.glb', poster: 'HDR.png' },
      { name: 'ELE', file: 'ELE.glb', poster: 'ELE.png' },
      { name: 'HVAC', file: 'HVAC.glb', poster: 'HVAC.png' },
      { name: 'RCI', file: 'RCI.glb', poster: 'RCI.png' },
    ];

    // Estado de visualización de cada modelo
    const activeModels = models.map(() => false);

    // Renderiza la galería de miniaturas
    function renderGallery() {
      const gallery = document.getElementById('gallery');
      gallery.innerHTML = models.map((model, i) => `
        <div class="gallery-item">
          <img src="${model.poster}" alt="${model.name}" width="100" height="100" style="border-radius:8px; box-shadow:0 1px 6px #0001;">
          <div>${model.name}</div>
          <button class="toggle-btn" onclick="toggleModel(${i})">
            ${activeModels[i] ? 'Ocultar' : 'Mostrar'}
          </button>
        </div>
      `).join('');
    }

    // Renderiza los controles de activación/desactivación
    function renderControls() {
      const controls = document.getElementById('controls');
      controls.innerHTML =
        `<button onclick="showAll()">Mostrar todos</button>
         <button onclick="hideAll()">Ocultar todos</button>`;
    }

    // Renderiza los modelos activos
    function renderModels() {
      const container = document.getElementById('modelContainer');
      container.innerHTML = models.map((model, i) =>
        activeModels[i] ? `
          <model-viewer
            src="${model.file}"
            ar
            ar-modes="webxr scene-viewer quick-look"
            camera-controls
            auto-rotate
            poster="${model.poster}"
            alt="${model.name}">
          </model-viewer>
        ` : ''
      ).join('');
    }

    // Funciones de control
    window.toggleModel = function(i) {
      activeModels[i] = !activeModels[i];
      renderGallery();
      renderModels();
    }

    window.showAll = function() {
      activeModels.fill(true);
      renderGallery();
      renderModels();
    }

    window.hideAll = function() {
      activeModels.fill(false);
      renderGallery();
      renderModels();
    }

    // Inicializa la galería
    renderGallery();
    renderControls();
    renderModels();
  </script>
</body>
</html>
```

- Cambia las rutas de las imágenes (`ARQ.png`, `EST.png`, etc.) si tienes miniaturas, o elimina el atributo `poster` si no tienes imágenes.
- Los modelos se cargarán directamente desde la raíz del repositorio.

---

## ¿Cómo agregar más modelos o imágenes?

1. Coloca tus archivos `.glb` y sus imágenes de miniatura (`.png`) en la raíz del repositorio.
2. Modifica la lista `models` en el HTML para agregar el nombre y las rutas de tus nuevos modelos.

---

## ¿Cómo visualizar en Realidad Aumentada?

- Haz clic en el icono de RA de cada modelo (disponible en dispositivos compatibles).
- Puedes activar uno o varios modelos para observar su comportamiento combinado.

---

## Requisitos

- Navegador moderno compatible con [model-viewer](https://modelviewer.dev/).
- Dispositivo móvil para RA (Android/iOS).
- Las imágenes de miniatura son opcionales, pero recomendadas para la galería.

---

## Créditos y contribuciones

Este repositorio está cerrado a nuevas expansiones, pero puedes clonar o adaptar la galería a tus necesidades.
