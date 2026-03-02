# Finni — App de Finanzas Personales

Finni es una aplicación de finanzas personales de uso local, sin registro ni servidor. Funciona directamente desde el navegador como un único archivo HTML. Todos los datos se guardan en el dispositivo usando `localStorage`.

---

## Cómo usar

1. Abre el archivo `index.html` en cualquier navegador moderno (Chrome, Safari, Firefox).
2. La primera vez carga automáticamente datos de ejemplo para explorar la app.
3. Empieza a añadir tus propias transacciones con el botón **⊕** central.

No requiere instalación, conexión a internet ni cuenta.

---

## Pantallas

### ⌂ Inicio
Vista principal con la tarjeta de **Patrimonio Total** — suma de todas tus transacciones más las bolsas de ahorro. Muestra también los ingresos y gastos del mes en curso, y las últimas transacciones recientes.

### ◉ Análisis
Gráficos y resúmenes del gasto por categoría. Filtrable por semana, mes, trimestre o año. Incluye mapa de calor de gastos por día.

### ⊕ Nueva transacción *(botón central)*
Modal para registrar un gasto o ingreso. Campos: importe, descripción, categoría, fecha y nota opcional. Toca cualquier transacción del historial para editarla o eliminarla.

### ◈ Presupuestos
Gestión de presupuestos mensuales o anuales por categoría. También incluye las **bolsas de ahorro** (fondos separados del patrimonio principal) y las **metas de ahorro** con seguimiento de progreso.

### ⚙ Ajustes
Configuración general y gestión de datos:

| Opción | Descripción |
|---|---|
| Ver Historial | Lista completa de transacciones con filtros y búsqueda |
| Nueva Previsión | Planifica cuánto quieres gastar en una categoría |
| Nuevo Presupuesto | Establece un límite de gasto |
| Nueva Bolsa de Ahorro | Fondo separado del patrimonio diario |
| Nueva Meta | Objetivo de ahorro con seguimiento |
| Pagos Recurrentes | Suscripciones y cargos fijos automáticos |
| Tema | Alterna entre modo claro y modo oscuro |
| Color de acento | 6 opciones de color para la interfaz |
| Exportar CSV | Descarga las transacciones en formato CSV |
| Exportar copia completa | Backup completo en JSON (transacciones, ahorros, metas…) |
| Importar datos | Carga un CSV o JSON exportado previamente |
| Reiniciar con datos demo | Restaura los datos de ejemplo |
| Borrar todos los datos | Elimina todo el historial permanentemente |

---

## Categorías disponibles

🍔 Alimentación · 🚗 Transporte · 🛍 Compras · 💊 Salud · 🏠 Hogar · 🎬 Ocio · 📚 Educación · 💼 Salario · 📈 Inversión · ⚡ Otro

---

## Formato CSV para importación

El importador acepta archivos CSV con las siguientes columnas:

```
fecha,concepto,importe,tipo,categoria
2024-03-01,Mercadona,-67.40,expense,food
2024-03-01,Nómina,2800,income,salary
```

- **fecha**: formato `YYYY-MM-DD`
- **importe**: número con punto decimal (negativo para gastos, positivo para ingresos)
- **tipo**: `expense` o `income`
- **categoria**: uno de los IDs de categoría (`food`, `transport`, `shopping`, `health`, `home`, `entertain`, `education`, `salary`, `invest`, `other`)

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
  "tx": [],          // transacciones
  "accounts": [],    // cuentas con saldo
  "savings": [],     // bolsas de ahorro
  "budgets": [],     // presupuestos
  "fc": [],          // previsiones
  "goals": [],       // metas
  "recurring": [],   // pagos recurrentes
  "theme": "light",
  "acc": {}          // color de acento
}
```

---

*Finni — versión local, sin nube, sin tracking.*
