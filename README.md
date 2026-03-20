# Finni — App de Finanzas Personales `v2`

Finni es una aplicación de finanzas personales de uso local, sin registro ni servidor. Funciona directamente desde el navegador como un único archivo HTML. Todos los datos se guardan en el dispositivo usando `localStorage`.

---

## Cómo usar

1. Abre el archivo `index.html` en cualquier navegador moderno (Chrome, Safari, Firefox).
2. La primera vez carga automáticamente datos de ejemplo para explorar la app.
3. Configura tu **presupuesto mensual** en Ajustes para activar el indicador de disponible.
4. Empieza a añadir tus propias transacciones con el botón **⊕** central.

No requiere instalación, conexión a internet ni cuenta.

---

## Pantallas

### ⌂ Inicio
Vista principal con la tarjeta **Disponible este mes** — calcula en tiempo real cuánto puedes gastar basándose en tu presupuesto mensual configurado, los gastos ya realizados y los comprometidos (presupuestos, previsiones y recurrentes pendientes). Incluye barra de progreso con semáforo de color y desglose de Gastado / Comprometido / Base mensual.

Accesos rápidos: Agregar · Previsión · Análisis · **📊 Resumen mensual**

### ◉ Análisis
Gráficos y resúmenes del gasto filtrable por semana, mes, 3 meses o año. Incluye distribución por categoría (donut con % e importe en euros), gráfico de barras de gasto diario/semanal/mensual, y mapa de actividad. Al tocar una categoría en la leyenda o en los chips de filtro, todos los gráficos se actualizan para mostrar solo esa categoría.

### ⊕ Nueva transacción *(botón central)*
Modal para registrar un gasto o ingreso. Campos: importe, descripción, categoría (predefinidas + personalizadas), fecha y nota opcional. Toca cualquier transacción del historial para editarla o eliminarla.

### ◈ Presupuestos
Gestión de presupuestos con **categorías vinculadas** — cada presupuesto puede agrupar varias categorías para un seguimiento preciso (ej: "Gastos Fijos" agrupa Alquiler + Gasolina + Suscripciones). También incluye bolsas de ahorro, metas y previsiones del mes.

### ⚙ Ajustes
Configuración general y gestión de datos:

| Opción | Descripción |
|---|---|
| **Mis Categorías** | Crea categorías personalizadas con nombre, icono y color. Oculta las predefinidas que no uses |
| Ver Historial | Lista completa de transacciones con filtros y búsqueda |
| Nueva Previsión | Planifica cuánto gastar — por categoría o concepto libre con categorías vinculadas |
| Nuevo Presupuesto | Límite de gasto con categorías asociadas opcionales |
| Nueva Bolsa de Ahorro | Fondo separado del disponible diario |
| Nueva Meta | Objetivo de ahorro con seguimiento de progreso |
| Pagos Recurrentes | Suscripciones y cargos fijos automáticos |
| Presupuesto mensual | Base para calcular el disponible en inicio |
| Tema | Alterna entre modo claro y modo oscuro |
| Color de acento | 6 opciones de color para la interfaz |
| Exportar CSV | Descarga las transacciones en formato CSV |
| Exportar copia completa | Backup completo en JSON |
| Importar datos | Carga un CSV o JSON exportado previamente |
| Reiniciar con datos demo | Restaura los datos de ejemplo |
| Borrar todos los datos | Elimina todo el historial permanentemente |

---

## Novedades en v2

**Categorías personalizadas** — crea tus propias categorías con nombre, icono (más de 60 emojis disponibles) y color. Se integran en toda la app: transacciones, previsiones, presupuestos, análisis e importación CSV. Las categorías predefinidas se pueden ocultar individualmente.

**Previsiones con categorías vinculadas** — las previsiones de concepto libre (ej: "Compra semanal") pueden tener múltiples categorías asociadas. Todas las transacciones de esas categorías cuentan automáticamente como gasto de esa previsión.

**Presupuestos con categorías vinculadas** — cada presupuesto puede agrupar varias categorías. Sin categorías vinculadas, el presupuesto sigue contando todos los gastos del período.

**Resumen mensual Previsto vs Real** — modal accesible desde el botón 📊 en inicio. Muestra bloques de Ingresos, Previsiones, Presupuestos, Recurrentes y Ahorros con su importe previsto, real y barra de progreso. Navegable por meses con las flechas ‹ ›.

**Disponible este mes** — sustituye al patrimonio acumulado en la tarjeta principal. Calcula: presupuesto base − gastos reales − comprometidos (margen restante de presupuestos y previsiones + recurrentes pendientes del mes). Se pone en rojo si hay déficit.

**Análisis por categoría** — toca cualquier categoría en el donut o en los chips de filtro para aislarla. El gráfico de barras y el mapa de calor se filtran para mostrar solo los días con gasto en esa categoría.

**Importe en la leyenda del donut** — cada categoría muestra el porcentaje y el importe en euros.

**Parser de importación mejorado** — detecta automáticamente encoding (UTF-8 y Windows-1252), formatos de fecha y separadores de miles vs decimales (`2,134` → 2134 · `2,13` → 2.13 · `2.134,50` → 2134.50).

---

## Formato CSV para importación

```
fecha,concepto,importe,tipo,categoria
2024-03-01,Mercadona,-67.40,expense,food
15/03/2024,Nómina,2800,income,salary
3/1/2026,Alquiler,-600,expense,home
```

- **fecha**: acepta `YYYY-MM-DD`, `DD/MM/YYYY`, `MM/DD/YYYY`, `DD-MM-YYYY`, `DD.MM.YYYY` y año corto
- **importe**: acepta punto o coma decimal, separadores de miles, símbolo € opcional, negativos para gastos
- **tipo**: `expense` / `gasto` o `income` / `ingreso` (también se infiere del signo del importe)
- **categoria**: ID o nombre de cualquier categoría, incluyendo las personalizadas
- **encoding**: UTF-8 y Windows-1252 (exportaciones de Excel en español)

---

## Lógica del Disponible

```
Disponible = Presupuesto mensual
           − Gastos reales del mes
           − Σ (límite presupuesto − ya gastado) para cada presupuesto mensual activo
           − Σ (importe previsión − ya gastado) para cada previsión del mes
           − Σ recurrentes mensuales pendientes (día de cobro > hoy)
```

Si el resultado es negativo se muestra en rojo con `−`. Sin presupuesto configurado muestra `—`.

---

## Datos técnicos

- **Tecnología**: HTML + CSS + JavaScript puro. Sin dependencias externas.
- **Almacenamiento**: `localStorage` bajo la clave `finni_v4`.
- **Privacidad**: ningún dato sale del dispositivo. No hay telemetría ni analítica.
- **Compatibilidad**: cualquier navegador moderno con soporte ES6+.

---

## Estructura del estado interno

```json
{
  "tx": [],            // transacciones
  "accounts": [],      // cuentas con saldo
  "savings": [],       // bolsas de ahorro
  "budgets": [],       // presupuestos (con cats[] opcional)
  "fc": [],            // previsiones (con cats[] para tipo libre)
  "goals": [],         // metas
  "recurring": [],     // pagos recurrentes
  "customCats": [],    // categorías personalizadas del usuario
  "hiddenCats": [],    // IDs de categorías predefinidas ocultas
  "monthlyBudget": 0,  // presupuesto mensual base
  "theme": "light",
  "acc": {}            // color de acento
}
```

---

*Finni v2 — local, sin nube, sin tracking.*
