# Contexto del Proyecto: Radios UV-5R Baofeng

## Resumen
Web app para el equipo de comunicaciones que gestiona radios Baofeng UV-5R. Funciona como PWA (Progressive Web App) - se puede instalar en el celular y usar sin internet.

## URL de produccion
- **Repositorio:** https://github.com/Nancyms1012/Guia-rapida
- **Web app (GitHub Pages):** https://nancyms1012.github.io/Guia-rapida/
- Para activar GitHub Pages: Settings > Pages > Source: Deploy from branch > main / root

## Estructura de archivos

| Archivo | Descripcion |
|---------|-------------|
| `index.html` | Web app principal (generada por build-webapp.js) - NO editar directamente |
| `webapp-template.html` | **Template fuente** de la web app - EDITAR ESTE para hacer cambios |
| `build-webapp.js` | Script Node.js que inserta imagenes base64 en el template y genera index.html |
| `guia-rapida-uv5r.html` | Guia rapida standalone (PDF horizontal, 1 pagina) |
| `guia-rapida-uv5r.pdf` | PDF de la guia rapida |
| `boton-bloqueo.png` | Imagen del boton asterisco/candado |
| `icono-candado.png` | Imagen del simbolo de candado en pantalla |
| `perilla-volumen.png` | Imagen de la perilla de volumen |
| `Botones-laterales.png` | Imagen de los 3 botones laterales (PTT-A, PTT-B, SK-1) |
| `Pantalla-canales.png` | Imagen de la pantalla mostrando los 2 canales |

## Como hacer cambios

### Para modificar la web app:
1. Editar `/projects/sandbox/webapp-template.html` (el template)
2. Ejecutar: `node build-webapp.js` (desde /projects/sandbox/)
3. El script lee los archivos .b64 y genera `Guia-rapida/index.html`
4. Hacer commit y push

### Para regenerar los archivos base64 (si cambian las imagenes):
```bash
cd Guia-rapida
base64 -w0 boton-bloqueo.png > ../boton.b64
base64 -w0 icono-candado.png > ../candado.b64
base64 -w0 perilla-volumen.png > ../perilla.b64
base64 -w0 Botones-laterales.png > ../botones-laterales.b64
base64 -w0 Pantalla-canales.png > ../pantalla-canales.b64
```

### Para regenerar el PDF:
```bash
node generate-pdf.js
```

## Arquitectura de la Web App

### 4 Tabs:
1. **Asignaciones** - Formulario rellenable con 10 radios, encargado, canales. Boton "Modificar" alterna entre modo vista y edicion. Datos guardados en localStorage.
2. **Guia Rapida** - 6 pasos con imagenes incrustadas (boton bloqueo, candado, perilla)
3. **Manual Tecnico** - Informacion completa: botones laterales, pantalla canales, menus Radio Set y Program CH
4. **Problemas y Soluciones** - 7 problemas comunes con soluciones

### Tecnologias:
- HTML/CSS/JS puro (sin dependencias externas)
- Imagenes incrustadas en base64 (autocontenido)
- localStorage para persistencia de datos
- Service Worker inline para funcionar offline
- PWA manifest para instalar en celular
- Responsive: bottom-nav para movil, grid de 2 columnas en desktop

### Estilo visual:
- Tema oscuro tipo GitHub
- Variables CSS en :root (--accent: #58a6ff, --bg: #0c1117, etc.)
- Bottom navigation con iconos SVG
- Cards con bordes sutiles
- Animaciones: fadeIn al cambiar tabs

## Informacion del equipo
- **Encargado/Tecnico:** Ivan Wong
- **10 radios** (Radio #10 es del coordinador, con PTTs invertidos)
- **Canal principal:** arriba en pantalla, PTT-A
- **Canal secundario:** abajo en pantalla, PTT-B
- **Configuracion:** Squelch 3, TOT 60s, Trans Power bajo, Busy Lockout on

## Notas importantes
- Radio #10 tiene PTT-A y PTT-B invertidos
- El bloqueo de teclado debe estar SIEMPRE activado
- Esperar 1-2 seg despues de presionar PTT antes de hablar
- Busy Lockout: no desactivar, mejor bajar TOT si alguien bloquea
