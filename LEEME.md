# Castelli Tools — sitio corregido

## ⚠️ Lo único obligatorio antes de publicar

Abre `castelli-tools.html`, busca el bloque `const CONFIG` (cerca del primer `<script>`)
y reemplaza estos tres valores por los reales:

```js
const CONFIG = {
  waNumber: '521XXXXXXXXXX',      // WhatsApp en formato internacional sin signos: 52 + 1 + 10 dígitos
  phone:    '+525500000000',      // teléfono para el botón "llamar"
  phoneText:'+52 55 0000 0000',   // cómo se muestra el teléfono
  email:    'contacto@castellitools.com'
};
```

Con eso, **todos** los botones de WhatsApp (hero, banner, fichas de producto y chat),
el teléfono y el correo quedan funcionando desde un solo lugar.

## Estructura para subir al hosting

```
castelli-tools.html      ← súbelo como index.html en la raíz
images/                  ← sube la carpeta completa junto al HTML
```

Las imágenes ahora son archivos externos (antes iban incrustadas en el HTML).
Mantén la carpeta `images/` al lado del HTML o las imágenes no cargarán.

## Cómo se envía el formulario de contacto

Por defecto, "Enviar mensaje" valida los campos y abre WhatsApp con los datos
prellenados (es el canal principal del negocio). Si prefieres recibirlo por correo
con un backend, dentro del `<script>` está comentado el bloque alternativo para
**Formspree**: descomenta y pon tu ID de formulario.

## Qué se corrigió

**Performance**
- 38 imágenes base64 → 16 archivos externos (había duplicados). HTML de 1.2 MB a ~104 KB.
- Carga diferida real (`loading="lazy"`), dimensiones explícitas (menos saltos de layout),
  hero con prioridad alta, fuentes recortadas a los pesos usados.

**Funcionalidad / conversión**
- Formulario de contacto ahora funciona (antes la función no existía y no enviaba nada).
- WhatsApp, teléfono y correo centralizados en `CONFIG` (antes el número era un placeholder
  repetido en varios lugares).

**Accesibilidad**
- Fichas del catálogo y burbuja de chat operables con teclado.
- Modal con semántica de diálogo y manejo de foco (Esc para cerrar, foco atrapado).
- Etiquetas asociadas a los campos, foco visible, soporte de "movimiento reducido".

**UX**
- Menú móvil (hamburguesa): antes en celular desaparecía la navegación.
- Buscador en el catálogo + filtros con estado accesible.
- Chatbot alineado al catálogo real (se quitaron productos que no estaban: lijas, taladros).

**SEO**
- Meta descripción, Open Graph/Twitter (para compartir por WhatsApp), favicon, canonical.

## Pendiente — decisión de negocio (no técnica)

La portada se promociona como **ferretería general** (WD-40, DeWALT, herramienta eléctrica
y manual), pero el catálogo es 100% **herramienta de corte industrial**
(Cleveland, Meda, Star USA, Lavallee). Alineé el chatbot al catálogo real, pero el texto
del hero y la marquesina de marcas dependen de qué vende Castelli realmente. Decide el
posicionamiento y ajustamos el copy.
