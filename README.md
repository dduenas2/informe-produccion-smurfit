# Informe de Producción · ODEMPA

Dashboard interactivo para analizar el **Informe de Producción Consolidado** de planta (proceso de bolsas de papel: Impresora → Tubuladora → Fondeadora).

**Demo en línea:** https://dduenas2.github.io/informe-produccion-smurfit/

Funciona 100% en el navegador: sin servidor, sin instalación y sin enviar datos a internet. El Excel se procesa en memoria local y nunca sale de tu equipo.

## Cómo usarlo

1. Abre la [página publicada](https://dduenas2.github.io/informe-produccion-smurfit/) o haz doble clic en `dashboard.html`.
2. Arrastra el Excel del Informe de Producción sobre la zona de carga (o usa "Seleccionar archivo .xlsx").
3. Por defecto se muestra el mes actual; ajusta el rango con "Desde / Hasta" o el botón "Todo el histórico".
4. Refina con los filtros superiores: Máquina, Turno, Tipo de máquina, Supervisor, Operario y Cliente.

## Pestañas

| Pestaña | Contenido |
|---|---|
| **Resumen** | KPIs ejecutivos, producción por tipo de máquina (Impresora · Tubuladora · Fondeadora) y detalle por fondeadora (producto terminado: 2377, 2360-1, 2360-2). |
| **Desperdicio** | Pareto y treemap de % de desperdicio por dimensión (Operario, Supervisor, Turno, Máquina, Cliente, Material, Día), scatter desperdicio vs producción y evolución mensual con tendencia. |
| **Productividad** | Tiempos (invertido, corrida, cuadre, mantenimiento, paros), velocidad promedio por máquina, evolución mensual de velocidad y subpestaña **Mes a mes** (producción de fondeadoras con línea de tendencia). |
| **Paros** | Evolución mensual de horas de paro (T Paros) y de cuadre (T Cuadre) con tendencia, Pareto de causas (umbral 80%) y tabla de detalle. |
| **Tendencia** | Evolución diaria, semanal y mensual de producción y desperdicio. |
| **Detalle** | Tabla de registros filtrados con búsqueda, ordenamiento y exportación a CSV. |

## Conceptos clave

- **Producto terminado** = unidades producidas solo en **fondeadoras** (producto final que sale de planta).
- **% Desperdicio** = `unidades desperdiciadas / unidades fabricadas` (fórmula unificada en todo el dashboard).
- **Desperdicio total (Kg)** = suma de todas las máquinas: cada etapa genera desperdicio real.
- Todos los tiempos se muestran en **horas**; el Excel los trae en minutos.
- Las gráficas de evolución mensual usan el **histórico completo** (ignoran el filtro de fechas) pero respetan los filtros categóricos.

## Formato del Excel

Hoja única con encabezados en la primera fila. Columnas esperadas:

```
Fecha · Turno · Máquina · Tipo Máquina · Operario · Supervisor · Cliente ·
Material · Ctd · Desperdicio (Kg) · Und. desperdiciadas · T Invertido ·
T Corrida · T Cuadre · T Mtto · T Paros · Vel · Paro 1..10 · Paro N (min)
```

## Stack técnico

- Un solo archivo `dashboard.html` (HTML + CSS + JS inline).
- [ECharts](https://echarts.apache.org/) para las gráficas (con copia local en `lib/` como respaldo del CDN).
- [SheetJS](https://sheetjs.com/) para leer el `.xlsx` en el navegador.
- Publicado con GitHub Pages (`index.html` redirige a `dashboard.html`).

## Versiones

| Versión | Cambios principales |
|---|---|
| v1.0 | Dashboard piloto completo (6 pestañas, filtros, carga de Excel). |
| v1.1 | Pareto en la pestaña Desperdicio. |
| v1.2 | Logo Odempa, velocidad por máquina y desperdicio vs producción. |
| v1.3 | Fórmula de % desperdicio unificada, detalle por fondeadora, subpestaña "Mes a mes" y evolución mensual de paros y cuadres. |
