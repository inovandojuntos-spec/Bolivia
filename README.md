# DSANT · Sistema de ventas + Landing

## Qué hay aquí

- `index.html` — Landing de venta (blanco / dorado / rosado). Catálogo en vivo desde Supabase, raspadita de descuento (5/10/15%), carrito y pedido por WhatsApp.
- `admin.html` — Panel de ventas: pedidos con estados, edición de stock y raspaditas generadas.
- `images/` — Fotos de productos optimizadas para web.

## Base de datos (Supabase, proyecto `dsant`)

- URL: `https://lrdefhubzhflcrshonhx.supabase.co` (región São Paulo)
- Tablas: `products`, `variants` (color/talla/stock), `orders`, `discount_codes`
- Funciones seguras (RPC): `scratch_discount()` genera el premio en el servidor (no manipulable) y `place_order(...)` valida stock, aplica el cupón, descuenta stock y registra el pedido — todo en una transacción.
- RLS: el público solo puede leer catálogo; los pedidos y cupones solo se crean vía funciones. Nadie puede leer pedidos sin la service key.

## Publicar en GitHub Pages

1. Crea un repo y sube la carpeta `web/` (o su contenido en `/docs`).
2. Settings → Pages → Deploy from branch → carpeta correspondiente.
3. Listo: el catálogo y el stock se actualizan solos desde Supabase.

**Nunca subas la service_role key al repo.** La landing solo usa la clave publishable (pública por diseño).

## Panel admin

Abre `admin.html` (localmente o publicado) y pega tu **service_role key**:
supabase.com → proyecto **dsant** → Project Settings → API Keys. Queda guardada solo en tu navegador.

## Datos configurables

En `index.html` (bloque CONFIG al final):
- `WHATSAPP` — número de pedidos (actual: 5562991551720)
- Precio: se cambia en la base (`products.price_bs`) o desde el admin.
- Probabilidades de la raspadita: función `scratch_discount()` en Supabase (50% → 5%, 35% → 10%, 15% → 15%).
