---
layout: base.njk
title: Tutorial Python WebAssembly
subtitle: Tutorial python para wasm
---

## Instalación

Este tutorial usa una distribución de Python para el navegador basada en WebAssembly.

**Pyodide** es un port de CPython a WebAssembly/Emscripten.

Gracias a el se puede ejecutar código de Python en el navegador.

<br/>

Para incluir **Pyodide** en tu proyecto puedes utilizar la siguiente URL de CDN y usarla dentro del head:

```
  https://cdn.jsdelivr.net/pyodide/v0.21.0/full/pyodide.js
```

Ejemplo:

```html
  <script src="https://cdn.jsdelivr.net/pyodide/v0.21.0/full/pyodide.js"></script>
```

## Cómo empezar

El archivo pyodide.js define una única función asíncrona llamada **loadPyodide** que configura el entorno de Python y devuelve el top level namespace de Pyodide.

```javascript
async function main() {
  let pyodide = await loadPyodide();
  // Pyodide esta listo para usarse
  console.log(pyodide.runPython(`
    import sys
    sys.version
  `));
};
main();
```

Gracias a esa función ya se puede correr código básico de Python en el navegador.

## Librerías

Pyodide incluye librerías básicas, por lo que si se requiere usar una librería mas avanzada como **Numpy** o **Matplotlib**, se debe importarla manualmente.

En caso de que requieran importar librerías de Python, se puede usar la función **loadPackage** para importar la librería previo a su uso.

```html
<script type="text/javascript">
  async function main() {
    let pyodide = await loadPyodide();
    pyodide.loadPackage('numpy').then(() => {
      pyodide.runPython(`
        from numpy import random
        import numpy as np
      `);
      pyodide.runPython(`
        arr = np.array([1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16])
        print(arr)
        random.shuffle(arr)
        print(arr)
      `);
    });
  }
  main();
</script>
```

En el ejemplo anterior se importo la librería **Numpy** y se ejecutó haciendo uso de su función shuffle para desordenar un arreglo.

Para poder ver el resultado, se debe ver en la consola del navegador.

## Referencias

<a href = "https://pyodide.org/en/stable/" target="_blank">Pyodide</a>
