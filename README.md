# 🍦 Helados Rica Fruta — App de menú y pedidos

App web instalable (PWA) para **Helados Rica Fruta – Caucasia, Antioquia**.
El cliente arma su pedido desde el celular y lo envía **ya escrito por WhatsApp**, sin apps de terceros, sin comisiones y sin servidor.

**Desarrollada por Vibras Positivas HM — Derechos de Autor Reservados**

---

## Qué hace

| Función | Detalle |
|---|---|
| Menú completo | 7 categorías, más de 80 productos con ingredientes y precios reales del menú impreso |
| Tamaños y sabores | 8/16/24 Oz, jugo en agua o en leche, 19 sabores de helado artesanal, 8 malteadas |
| Carrito | Cantidades, notas por producto ("sin queso"), edición y borrado |
| Pedido por WhatsApp | Mensaje formateado con código de pedido, detalle, totales, dirección y forma de pago |
| Domicilio o recoger | Cobro de domicilio configurable; los campos de dirección aparecen solo si aplica |
| Instalable | Se agrega a la pantalla de inicio como app (Android, iOS y escritorio) |
| Funciona sin datos | El menú queda en caché; el cliente lo consulta aunque se le acabe el plan |
| Buscador | Filtra por producto, ingrediente o sabor |
| Horario en vivo | Muestra "Abierto / Cerrado" con la hora real de Colombia (UTC-5) |
| Habeas Data | Autorización obligatoria, política visible y botón para borrar datos del dispositivo (Ley 1581 de 2012) |

---

## Archivos

```
ricafruta/
├── index.html                 ← la app completa (menú, carrito, WhatsApp)
├── manifest.json              ← identidad de la PWA
├── sw.js                      ← service worker (offline + instalación)
├── icon-192.png
├── icon-512.png
├── icon-maskable-512.png
├── apple-touch-icon.png
├── og-image.jpg               ← imagen que se ve al compartir el enlace (1200×630)
└── README.md
```

---

## Antes de publicar: 3 ajustes

Abre `index.html` y busca el bloque `const CONFIG` (arriba del `<script>`):

```js
const CONFIG = {
  whatsapp: "573117700431",   // ⚠️ CAMBIAR por el WhatsApp de Helados Rica Fruta
  domicilio: 3000,            // valor del domicilio (0 = gratis)
  abre: 10,                   // hora de apertura
  cierra: 21                  // hora de cierre
};
```

1. **WhatsApp del negocio** en formato `57` + número, sin espacios ni `+`.
2. **Valor del domicilio** en Caucasia.
3. **Horario real** de atención.

En las etiquetas Open Graph del `<head>` reemplaza `https://haroldco45.github.io/ricafruta/` por la URL final donde quede publicada.

---

## Publicar en GitHub Pages

```bash
# 1. Crear el repositorio
gh repo create ricafruta --public --source=. --remote=origin

# 2. Subir
git init
git add .
git commit -m "App de pedidos Helados Rica Fruta"
git branch -M main
git push -u origin main
```

Luego: **Settings → Pages → Source: main / (root) → Save**.
Queda en `https://haroldco45.github.io/ricafruta/` en 1–2 minutos.

> La instalación como app requiere **HTTPS**. GitHub Pages, Netlify y Hostinger ya lo traen. Abriendo el archivo con doble clic (`file://`) el menú funciona, pero no se instala.

---

## Cambiar precios o productos

Todo el menú vive en la constante `MENU` dentro de `index.html`. Cada producto es una línea:

```js
{n:'Waffle Especial',
 d:'Banano, fresas, kiwi, queso mozarella, helado de vainilla…',
 t:[T('Porción',22000)],   // T('nombre del tamaño', precio)
 top:1,                     // aparece en "Los más pedidos"
 e:'🧇',                    // emoji de la tarjeta
 sabores:['Naranja','Yogurt']}  // opcional: lista de sabores a elegir
```

Para subir un precio basta cambiar el número. Después de editar, sube el archivo y **sube también el número de versión** en `sw.js` (`ricafruta-v1` → `ricafruta-v2`) para que los clientes reciban el menú nuevo y no la copia en caché.

---

## Cómo llega el pedido

```
*PEDIDO — HELADOS RICA FRUTA* 🍦
Código: RF-48213
──────────────
▪ 2 x Ensalada de Frutas (16 Oz)  $44.000
▪ 1 x Bola de helado artesanal · Maracuyá (1 bola)  $3.600
   ↳ sin piazza
──────────────
Productos: $47.600
Domicilio: $3.000
*TOTAL: $50.600*
──────────────
Cliente: Marleny Rúa
WhatsApp: 3115557788
Entrega: Domicilio
Dirección: Calle 20 #15-30
Barrio: El Bosque
Pago: Efectivo (paga con $60.000)
```

---

## Protección de datos (Ley 1581 de 2012)

- La app **no tiene backend**: no envía ni almacena datos en ningún servidor.
- Nombre, teléfono y dirección se guardan solo en el `localStorage` del propio celular del cliente, para no volver a pedírselos.
- La autorización es obligatoria para enviar el pedido y la política es consultable desde el pie de página.
- Botón "Borrar mis datos de este dispositivo" disponible siempre.

---

## Ideas para la versión 2

- Cupones por código (`RICA10`) y combos armados.
- Programa de puntos: 10 obleas = 1 gratis, con QR.
- Panel del negocio para cambiar precios sin tocar código.
- Pedidos programados para cumpleaños y pedidos recurrentes de pulpas.

---

*Vibras Positivas HM · Caucasia, Antioquia · Colombia*
