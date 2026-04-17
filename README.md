# Hoja de cálculo: Losa aligerada (NTP E-060)

Se creó el archivo **`Losa_Aligerada_Momentos_E060.xml`** compatible con Microsoft Excel (SpreadsheetML 2003), con fórmulas enlazadas para:

- Momento último positivo y negativo a partir de carga última seleccionable en **patín** o **alma**.
- Verificación de capacidad a flexión con acero positivo (`As+`) y negativo (`As-`).
- Evaluación de bloque de compresión para sección tipo T (caso `a <= h_f` y `a > h_f`).

## Entradas modificables

En la hoja (celdas amarillas):

- Propiedades de material: `f'c`, `fy`, `Es`, `ϕ`.
- Geometría: `b_f`, `h_f`, `b_w`, `h`, `d+`, `d-`.
- Acero: `As+`, `As-`.
- Cargas y coeficientes: `w_u patín`, `w_u alma`, selección de ubicación de carga, coeficientes de momento positivo/negativo.

## Unidades

Sistema Internacional empleado:

- Longitud: **mm** y **m**.
- Esfuerzo: **MPa**.
- Carga distribuida: **kN/m**.
- Momento: **kN·m**.

## Criterio normativo

La hoja está estructurada con el criterio de diseño por resistencia de la **Norma Técnica Peruana E-060** para flexión en concreto armado. Incluye cálculo de `β1` con reducción por resistencia del concreto y `ϕMn` para comparación con `Mu`.

## Uso

1. Abrir `Losa_Aligerada_Momentos_E060.xml` con Excel.
2. Modificar las entradas amarillas.
3. Revisar resultados en las secciones de `M_u`, `Mn`, `ϕMn` y estado de cumplimiento.
4. Complementar en proyecto real con verificaciones de cuantías mínimas/máximas, corte, deflexión y detalle de armado según E-060.
