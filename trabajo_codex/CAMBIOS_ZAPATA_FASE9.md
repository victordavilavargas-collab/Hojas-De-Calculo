# Fase 9: acción vertical y escalamiento mínimo E.030

Base: `Diseño de zapata aislada_CORREGIDA_FASE8.xlsx`, commit `aae4c66557401d2a5b4dddad8fca4009fa91abc3`. Se conserva la base y se entrega una copia independiente. No se optimizaron Bx, By, h, qadm, materiales, barras, separaciones ni cargas para obtener CUMPLE. Las fuerzas se expresan en tf, momentos en tf·m, cotas en m, masas modales en kg y el resto de dimensiones conserva m/cm del libro.

## Corrección del escalamiento

`FUENTES_E030` mantiene Vest, Vdin previo, factor de fuente y Vdin final por X/Y. R/W calculan `MAX(1, límite*Vest/Vdin_pre)` con límite 0.80 para regular y 0.90 para irregular. X admite NO REQUERIDO, APLICADO y REQUIERE DEFINIR. AF documenta los cortantes que fundamentan la clasificación. El factor es una auditoría de las acciones finales importadas, nunca una segunda multiplicación de las fuerzas de zapata.

Si ambos factores mínimos son 1 y ambos aplicados son 1, NO REQUERIDO es válido sin exigir una falsa declaración de aplicación. Si algún factor mínimo supera 1, se exige APLICADO, referencia Y, factor suficiente y cortante final suficiente. Una escala superior al mínimo se conserva. AD identifica ESCALAMIENTO CONSERVADOR ADICIONAL si el exceso relativo supera 0.1%, tolerancia visible en `CONTROL_E030_F8!B32`; AE exige justificación. La tolerancia numérica de comparación del mínimo es 1E-10 y no reemplaza esa tolerancia de aviso.

`DEMANDAS_E030!AD` enlaza la sobrescala de la fuente de cada demanda activa. `ENVOLVENTES!B156` y `RESUMEN!B179` muestran el aviso. Si el estado técnico es NO CUMPLE y existen demandas activas con sobrescala, el estado principal lo indica. Esto informa la existencia de demandas superiores al mínimo, sin afirmar que la sobrescala sea la causa única de todos los incumplimientos.

## Acción vertical

`VERTICAL_F9` usa filas 8:67 para últimos y 68:127 para servicio, manteniendo los 60 padres U/60 S. B selecciona:

| Método | Tratamiento |
|---|---|
| A. ESTÁTICA ART.38.1 | Vector firmado de caso externo aplicado con coeficiente 2/3·Z·U·S. No distribuye el peso sísmico del edificio entre columnas. |
| B. ESPECTRO VERTICAL ART.41.2 | Procedimiento estadístico F8; amplitudes finales SZ en ESPECTROS_U/S. No representa un instante físico. |
| C. RESULTADO EXTERNO DOCUMENTADO | Vector final ya combinado, con ID, modelo, norma, interfaz, signos y evidencia de simultaneidad y sentidos adversos. Requiere el modo de demanda externo de COMBOS. |
| D. NO APLICA | Se rechaza cuando la columna u otra clasificación hace obligatoria la vertical. |
| E. REQUIERE DEFINIR | Mantiene pendiente la demanda sísmica hasta completar la selección. |

C/D identifican caso y fuente. E:H registran Z/U/S y 2/3. I contiene referencia normativa y aplicación del peso en la fuente. J/K deben coincidir con plano y cota de la interfaz del padre, con tolerancia 1E-8 m. L confirma la convención de ejes/signos y M documenta simultaneidad y sentidos adversos. N/O documentan modalidad, tratamiento estadístico y escala del resultado dinámico, ya aplicada en fuente. P acredita análisis dinámico externo equivalente para gran luz/voladizo. S:X reciben Pv/Fxv/Fyv/Mxv/Myv/Mzv con signos físicos para A/C. Para B, se usan las amplitudes no negativas AC:AH de ESPECTROS y se exige que el ID coincida con su caso SZ.

AB muestra el coeficiente estático 2/3·Z·U·S para auditar la definición del caso en fuente. El vector Ev importado ya debe proceder de esa aplicación; el motor no vuelve a multiplicarlo por AB. Sólo aplica el factor de servicio que corresponda. Tampoco vuelve a aplicar la escala O de la fuente vertical dinámica.

La columna definida obliga a considerar vertical en las demandas sísmicas. La selección de A es admisible para una columna ordinaria. Gran luz y voladizo/saliente rechazan A y requieren B o C con análisis dinámico equivalente documentado. Los antiguos campos O/P de DEMANDAS se conservan para trazabilidad, pero W ahora enlaza la validez del método y vector en VERTICAL_F9; una etiqueta «vertical incluida» resulta insuficiente.

Y distingue el vector vertical separado del ya incorporado en una combinación externa. A con Y=NO genera ambos sentidos internos. A con Y=SI conserva un vector externo firmado documentado; si el padre usa un espectro horizontal interno, se exige separar Ev o usar el resultado externo ya combinado. Así se evita agregar Ev dos veces o presentar una sola base espectral como evidencia de ambos sentidos.

## Combinación de acciones y estados

Para horizontal espectral más A separado, se evalúan `Base + H_estado + Ev` y `Base + H_estado - Ev`. Los seis componentes de Ev cambian juntos de sentido. La caja horizontal conserva los 64 signos y las dos ramas X100/Y100 de F8; A añade únicamente dos sentidos verticales, dando 256 estados por padre. B conserva 128 estados. Un horizontal estático firmado con A separado usa sólo dos estados activos.

La activación interna de A separado exige una demanda sísmica identificada en COMBOS; una fila de gravedad no recibe Ev por llenar accidentalmente campos verticales. El resumen distingue la horizontal firmada de la caja espectral. El visor expone el método y el sentido vertical en las filas 28/29, además del ID del estado.

En los estados firmados con A interno, D identifica el caso horizontal del padre, E queda vacío y H indica HORIZONTAL FIRMADA EN INTERFAZ; los coeficientes históricos I/J no intervienen en esa rama. Para todo A interno, F identifica el caso Ev de VERTICAL_F9!C, en lugar del caso SZ espectral no utilizado. En las ramas espectrales se conservan los casos SX/SY y sus criterios anteriores. La combinación estática usa las seis acciones globales normalizadas del padre, tal como muestra la fórmula, y no vuelve a recombinarlas mediante I/J.

Para A separado, el vector del padre sin Ev permanece visible como dato de fuente, pero se excluyen de TOTAL_F7 sus resultados numéricos y estados técnicos. Sólo H+Ev y H−Ev participan como candidatos de diseño. Así, un resultado del padre que omite Ev no puede gobernar indebidamente una verificación ni introducir un estado pendiente ajeno a los dos sentidos requeridos. La delegación sólo afecta A interno; los candidatos F8 sin esa selección conservan sus resultados.

Los estados +Ev mantienen el orden de F8 en DERIVADOS_U/S y agregan el sufijo +Ev. Los estados -Ev se registran en DER_EV_U/S y también se enlazan al tramo 7688:15367 de DERIVADOS_U/S con sufijo -Ev. AW identifica el método y AX el sentido vertical. `VISTA_DERIVADO` admite índices 1:15360, de modo que ambas ramas se pueden inspeccionar. Los registros normales TOTAL_F7 se amplían de 1020 a 1980 filas de resultados para que la rama -Ev participe en las envolventes y sus gobernantes.

El ranking HW de TOTAL_F7_U compara los 1980 candidatos en un solo rango y utiliza la fila real de cada registro para desempatar. La rama -Ev no hereda el número de fila del tramo +Ev. Así el listado de combinaciones críticas obtiene rangos únicos y puede mostrar el segundo candidato incluso cuando sólo existen los dos estados físicos ±Ev. Se repiten todas las pruebas nuevas después de esta corrección, junto con los escenarios previos representativos del ranking. En los demás fixtures F8, -Ev permanece inactivo y su GN es vacío: ampliar el rango no agrega valores a COUNTIF ni cambia el ranking anterior.

TOTAL_F7_U!JD/JE y TOTAL_F7_S!BT/BU registran fallo técnico y naturaleza horizontal por candidato. B154 incluye las ramas físicas de horizontal firmada ±Ev, además de los resultados firmados/externos previos. B155 conserva la advertencia de caja cuando el fallo corresponde únicamente a la envolvente estadística; un fallo físico ±Ev no recibe esa etiqueta. Se verifica por regresión y por una inyección de estado sintético destinada exclusivamente a probar esa clasificación.

DU_EV_MENOS/DS_EV_MENOS, MOTOR_EV_U/S y MOTOR_HEV_U/S contienen la segunda rama. CONEXION_EV_MENOS y BARRAS_EV_MENOS conservan la necesidad de resultados externos de conexión/barra para las acciones de esa rama; no se deducen las fuerzas por barra de P-Mx-My. Los estados y máximos espectrales no se declaran concurrentes. La caja conservadora y la combinación física ±Ev se identifican por separado.

La reutilización exacta de F8 se mantiene donde continúa siendo válida. Las entradas de acciones afectadas y sus activaciones se ajustan porque un estado estático activo ya no equivale a todos los estados del padre. No se hizo una nueva compactación masiva. La segunda rama aumenta almacenamiento y cálculo potencial; no se afirma una mejora de rendimiento.

El control de torsión en planta de DERIVADOS_U/S y DER_EV_U/S se evalúa sólo cuando el estado está activo. Una rama inactiva devuelve vacío antes de evaluar ABS(Mz); esto evita errores por su vector deliberadamente vacío. Los escenarios capturados antes de esta corrección se repiten y sustituyen por su comprobación final, conservando la evidencia de la primera ejecución en el directorio de auditoría.

Las seis acciones del cuerpo están en L:Q para DU_INPUT/DU_EV_MENOS y Q:V para DS_INPUT/DS_EV_MENOS. El campo L del registro raíz de servicio por padre conserva 1 como factor interno porque sus acciones globales ya incorporan la reducción pertinente. Los demás registros conservan el plegado exacto de F8 y reutilizan ese dato raíz; sus celdas redundantes pueden estar vacías. Se comparan las seis acciones del cuerpo contra el estado derivado del mismo ID y se comprueba la equivalencia entre reducción adicional y previa.

## Servicio y reducción 0.80

Q/R de VERTICAL_F9 registran reducción previa y referencia. Debe coincidir con la declaración del padre COMBOS_SERVICIO!AI. Para 2026: contribución no reducida usa factor adicional 0.80; contribución ya reducida usa 1.00 y referencia. AD enlaza ese factor, aplicado a todo Ev y a toda contribución horizontal espectral, dejando intacta la base no sísmica. La auditoría Art.44 y la autorización independiente de qadm+30% no sustituyen la reducción.

Si el horizontal es estático firmado y todavía no reducido, se exige separar el vector de base no sísmica en los campos existentes COMBOS_SERVICIO!W:AB y documentarlo en AC. VERTICAL_F9!AG:AL y AM enlazan esa base y referencia, sin solicitar una segunda entrada. Se calcula `Base_no_sísmica + factor*(Vector_importado - Base_no_sísmica ± Ev)`. Así no se reduce inadvertidamente la gravedad al aplicar 0.80 al sismo. Si la fuente ya redujo la contribución completa, el factor es 1 y no se exige esa separación adicional para recombinar Ev ya reducido.

La rama estática de servicio exige también que COMBOS_SERVICIO!O sea OK antes de usar el vector global Q:V. Si la validación original del vector o de la separación de gravedad está pendiente, ESPECTROS_S!AI conserva ese estado y devuelve demandas vacías, evitando operaciones con acciones no disponibles. No se omiten los controles previos de concurrencia, plano de corte, pesos o reducción.

## Fuentes normativas y régimen

La [RM 183-2026-VIVIENDA](https://www.gob.pe/institucion/vivienda/normas-legales/8081915-183-2026-vivienda) modifica E.030. Se contrastó el [texto oficial E.030-2026](https://epdoc2.elperuano.pe/EpPo/DescargaIN.asp?Referencias=MjUxMTI1OF8xMjAyNjA1MDM=), artículos 28.4/28.5, 38.1/38.2, 41.2 y 44.1/44.2. El escalamiento sólo se exige cuando no se alcanza el cortante mínimo; la vertical estática y la dinámica tienen alcances distintos.

La [RM 217-2026-VIVIENDA](https://busquedas.elperuano.pe/dispositivo/NL/2521423-1) permite mantener el régimen anterior en los proyectos incluidos en su disposición transitoria. La selección y evidencia de CONTROL_FASE7 siguen siendo necesarias. Para el [texto anterior E.030](https://cdn.www.gob.pe/uploads/document/file/2366641/51%20E.030%20DISE%C3%91O%20SISMORRESISTENTE%20RM-043-2019-VIVIENDA.pdf?v=1677250657), las referencias verticales son 28.6.1/28.6.2 y 29.2.2, y el mínimo dinámico corresponde a 29.4.1/29.4.2. Los nombres del menú A/B identifican las opciones 2026; AE muestra la referencia efectiva del régimen seleccionado y los mensajes dinámicos distinguen el artículo anterior. No se elige el régimen automáticamente por fecha.

Se mantienen los controles de [E.060](https://cdn.www.gob.pe/uploads/document/file/2686419/E.060%20Concreto%20Armado%20DS%20N%C2%B0%20010-2009.pdf) y [E.050](https://cdn.www.gob.pe/uploads/document/file/2366655/54%20E.050%20SUELOS%20Y%20CIMENTACIONES%20RM%20N%C2%B0%20406-2018-VIVIENDA.pdf) de las fases previas, incluidos conexión, pesos reales, plano de corte y control de contacto. Permanecen fuera del alcance Capítulo 21, contacto parcial, borde/esquina, solver Mz, pedestal localizado mayor que columna y solver interno P-Mx-My.

## Verificación y cierre

Los resultados de ejecución nativa, regresión, integridad y persistencia figuran a continuación.

Se ejecutaron **88 escenarios de F8 y 44 pruebas nuevas**, 132 en total, con **500364 comprobaciones**, tolerancia absoluta/relativa 2E-8 y cero fallos numéricos o de aceptación. Las pruebas nuevas incluyen las 25 solicitadas, pérdida de trazabilidad, sobrescala sin justificar, tolerancia, plano distinto, Mz vertical firmado, separación de gravedad en servicio y participación de la rama -Ev en barras. Las declaraciones añadidas a los fixtures de regresión son evidencia sintética de prueba, no documentos del proyecto. Para preservar sus números, los casos espectrales previos seleccionan B con sus amplitudes SZ originales; los casos firmados/exteriores registran A ya incluido con Ev adicional cero.

Las comprobaciones independientes evalúan los seis componentes de cada estado horizontal en ambas ramas ±Ev, la invariancia ante cambios de factores Art.44 de auditoría, la igualdad entre reducción 0.80 adicional y reducción previa en fuente y el vector de servicio estático con gravedad separada. Los estados estáticos deben activar sólo uno por rama. Se contrasta además el vector del cuerpo contra el estado derivado del mismo ID y se verifica el factor interno 1 en servicio. La prueba 37 inyecta resultados de barra sintéticos en los motores exclusivamente para verificar el enlace de la envolvente y su gobernante; no acredita un cálculo físico de fuerzas por barra. La prueba 42 inyecta un estado técnico para verificar la clasificación física frente a caja espectral. Los fixtures y esas inyecciones se restauraron antes de guardar.

### Resultados de las pruebas nuevas

| Prueba | Resultados esperados y verificados |
|---|---|
| F9 01 Regular 0.95Vest | FUENTES_E030!AB8: OK; FUENTES_E030!R8: 1; FUENTES_E030!Q8: 95 |
| F9 02 Regular 0.80Vest | FUENTES_E030!AB8: OK |
| F9 03 Regular 0.79Vest requiere | FUENTES_E030!AB8: REQUIERE ESCALAMIENTO E.030 |
| F9 04 Irregular 0.90Vest | FUENTES_E030!AB8: OK; FUENTES_E030!R8: 1 |
| F9 05 Irregular 0.89Vest requiere | FUENTES_E030!AB8: REQUIERE ESCALAMIENTO E.030 |
| F9 06 Factor exacto requerido | FUENTES_E030!AB8: OK; FUENTES_E030!Q8: 80 |
| F9 07 Sobrescala justificada | FUENTES_E030!AB8: OK; FUENTES_E030!AD8: ESCALAMIENTO CONSERVADOR ADICIONAL |
| F9 08 Factor inferior | FUENTES_E030!AB8: REQUIERE ESCALAMIENTO E.030 |
| F9 09 Requerido sin referencia | FUENTES_E030!AB8: REQUIERE DEFINIR ESTADO ART.44 |
| F9 10 No requerido sin aplicado | FUENTES_E030!AB8: OK |
| F9 26 Sobrescala sin justificación | FUENTES_E030!AB8: REQUIERE JUSTIFICACIÓN SOBRESCALA |
| F9 27 Sin trazabilidad Vest Vdin | FUENTES_E030!AB8: REQUIERE TRAZABILIDAD VEST / VDIN |
| F9 28 No requerido con factor 1.1 | FUENTES_E030!AB8: REQUIERE DEFINIR ESTADO ART.44 |
| F9 29 Tol sobrescala 0.05% | FUENTES_E030!AB8: OK; FUENTES_E030!AD8: SIN SOBRESCALA SIGNIFICATIVA |
| F9 11 Columna sismo vertical estática | VERTICAL_F9!AA8: OK; DEMANDAS_E030!W8: OK; ENVOLVENTES!B157: HORIZONTAL FIRMADA; VERTICAL ESTÁTICA: +Ev / -Ev; TOTAL_F7_U!A8: NO; TOTAL_F7_U!GM8: NO APLICA |
| F9 12 Horizontal espectral vertical estática | VERTICAL_F9!AA8: OK; ESPECTROS_U!AI8: OK; ENVOLVENTES!B157: HORIZONTAL ESPECTRAL: CAJA DE SIGNOS; VERTICAL ESTÁTICA: +Ev / -Ev; VER CADA DEMANDA |
| F9 13 +Ev vector firmado | VERTICAL_F9!AA8: OK; VISTA_DERIVADO!B28: A. ESTÁTICA ART.38.1; VISTA_DERIVADO!B29: 1 |
| F9 14 -Ev vector firmado | VERTICAL_F9!AA8: OK; VISTA_DERIVADO!B28: A. ESTÁTICA ART.38.1; VISTA_DERIVADO!B29: -1 |
| F9 15 Columna espectro vertical | VERTICAL_F9!AA8: OK |
| F9 16 Vertical requerida faltante | DEMANDAS_E030!W8: REQUIERE DEFINIR MÉTODO VERTICAL |
| F9 17 Gran luz estática insuficiente | VERTICAL_F9!AA8: REQUIERE VERTICAL DINÁMICA ART.38.2 |
| F9 18 Gran luz espectro | VERTICAL_F9!AA8: OK |
| F9 19 Voladizo espectro | VERTICAL_F9!AA8: OK |
| F9 20 Externo documentado | VERTICAL_F9!AA8: OK |
| F9 21 Servicio H + Ev reducción completa | VERTICAL_F9!AA68: OK; DEMANDAS_E030!X68: OK |
| F9 22 Vector ya reducido 0.80 | VERTICAL_F9!AA68: OK; DEMANDAS_E030!X68: OK |
| F9 23 Doble reducción | VERTICAL_F9!AA68: DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 |
| F9 24 Régimen anterior | VERTICAL_F9!AA8: OK |
| F9 25 Régimen 2026 | VERTICAL_F9!AA8: OK |
| F9 30 Plano vertical distinto | VERTICAL_F9!AA8: REQUIERE TRAZABILIDAD VERTICAL / INTERFAZ |
| F9 31 Externo solo etiqueta | VERTICAL_F9!AA8: REQUIERE COMBINACIÓN VERTICAL EXTERNA DOCUMENTADA |
| F9 32 Servicio vertical reducción distinta | VERTICAL_F9!AA68: DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 |
| F9 33 Vector vertical con Mz firmado | VERTICAL_F9!AA8: OK |
| F9 34 Servicio H estático base separada | VERTICAL_F9!AA68: OK; DEMANDAS_E030!X68: OK |
| F9 35 Servicio estático base faltante | VERTICAL_F9!AA68: REQUIERE VECTOR ESTÁTICO ART.38.1 |
| F9 36 Ev incluido en base RS sin externo | VERTICAL_F9!AA8: REQUIERE VECTOR ESTÁTICO ART.38.1 |
| F9 37 Envolvente barra gobernada por -Ev (inyección de resultados sintéticos) | ENV_BARRAS!AF8: 250; ENV_BARRAS!AE8: U1-X01-Ev; ENV_BARRAS!AC8: NO CUMPLE; ENV_BARRAS!AD8: NO CUMPLE |
| F9 38 Sobrescala y fallo conservador | ENVOLVENTES!B156: ESCALAMIENTO CONSERVADOR ADICIONAL — DEMANDA SUPERIOR AL MÍNIMO NORMATIVO; ENVOLVENTES!B5: NO CUMPLE ENVOLVENTE CONSERVADORA — VERIFICAR INTERACCIÓN EXTERNA — DEMANDAS CON ESCALAMIENTO SUPERIOR AL MÍNIMO NORMATIVO |
| F9 39 Anterior vector estático incompleto | VERTICAL_F9!AA8: REQUIERE VECTOR ESTÁTICO ART.28.6.1 ANTERIOR |
| F9 40 Anterior gran luz estática insuficiente | VERTICAL_F9!AA8: REQUIERE VERTICAL DINÁMICA ART.28.6.2 ANTERIOR |
| F9 41 Combinación no sísmica no agrega Ev | DEMANDAS_E030!AC8: NO; ESPECTROS_U!A8: NO |
| F9 42 Fallo físico +/-Ev no es fallo de caja (inyección de estado sintético) | ENVOLVENTES!B153: NO CUMPLE; ENVOLVENTES!B154: NO CUMPLE; ENVOLVENTES!B155: False; ENVOLVENTES!B5: NO CUMPLE |
| F9 43 Servicio estático fuente de acciones incompleta | ESPECTROS_S!AI8: REQUIERE DATOS |
| F9 44 Horizontal estático componente faltante | VERTICAL_F9!AA8: OK; ESPECTROS_U!AI8: distinto de OK |

### Diferencias legítimas de regresión

Se revisan todas las diferencias textuales por escenario: control AD vacío sólo en estados inactivos en ambas fases, ampliación del visor y cuatro transiciones exactas de mensajes en cinco escenarios. En las tres pruebas de reducción 0.80 la demanda sigue inválida; el control vertical específico tiene prioridad sobre el de suelo. En el método B se exige el espectro vertical documentado. Para Art.44 se exige definir el estado de escalamiento de la fuente. No se admite ningún cambio numérico de diseño por esta clasificación. El control de validez Z y los controles generales permanecen disponibles.

- Visor ampliado a las dos ramas verticales: 88 celdas.
- Control AD vacío en estado derivado inactivo: 16384 celdas.
- Validación vertical 0.80 previa al control de suelo; demanda sigue inválida: 1576 celdas.
- Doble reducción vertical rechazada por el control específico: 788 celdas.
- Método B exige evidencia del espectro vertical: 1013 celdas.
- Art.44 exige definir el estado de escalamiento de la fuente: 1013 celdas.

| Escenario | Grupo de celdas registrado | Cambio textual revisado | Cantidad |
|---|---|---|---|
| F7 01 Linear Static | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 01 Linear Static | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 01 Linear Static | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 02 Response Spectrum puro | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 02 Response Spectrum puro | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 03 D + Response Spectrum | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 03 D + Response Spectrum | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 04 Linear Add estático | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 04 Linear Add estático | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 04 Linear Add estático | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 05 Linear Add contiene RS declarado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 05 Linear Add contiene RS declarado | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 06 Envelope estático correspondence | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 06 Envelope estático correspondence | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 06 Envelope estático correspondence | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 07 RS con correspondence | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 07 RS con correspondence | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 08 Time History mismo step | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 08 Time History mismo step | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 08 Time History mismo step | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 09 Time History Envelope rechazado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 09 Time History Envelope rechazado | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 09 Time History Envelope rechazado | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 10 E030 anterior | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 10 E030 anterior | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 11 E030 2026 | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 11 E030 2026 | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 12 E030 sin definir | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 12 E030 sin definir | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 13 FRAME interfaz | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 13 FRAME interfaz | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 13 FRAME interfaz | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 14 FRAME 0.30m encima | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 14 FRAME 0.30m encima | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 14 FRAME 0.30m encima | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 15 End offset activo | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 15 End offset activo | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 15 End offset activo | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 16 FRAME normal pesos incluidos rechazado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 16 FRAME normal pesos incluidos rechazado | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 16 FRAME normal pesos incluidos rechazado | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 17 FRAME especial documentado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 17 FRAME especial documentado | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 17 FRAME especial documentado | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 18 JOINT cimentación modelada | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 18 JOINT cimentación modelada | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 18 JOINT cimentación modelada | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 19 BASE edificio completo | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 19 BASE edificio completo | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 19 BASE edificio completo | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 20 BASE única válida | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 20 BASE única válida | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 20 BASE única válida | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 21 Relleno sin pedestal | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 21 Relleno sin pedestal | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 21 Relleno sin pedestal | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 22 Relleno columna rectangular | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 22 Relleno columna rectangular | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 22 Relleno columna rectangular | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 23 Relleno con pedestal | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 23 Relleno con pedestal | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 23 Relleno con pedestal | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 24 Pedestal incluido en P | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 24 Pedestal incluido en P | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 24 Pedestal incluido en P | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 25 Pedestal sumado manual | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 25 Pedestal sumado manual | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 25 Pedestal sumado manual | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 26 Gamma tres pesos iguales | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 26 Gamma tres pesos iguales | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 26 Gamma tres pesos iguales | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 27 Gamma diferentes sin justificar | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 27 Gamma diferentes sin justificar | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 27 Gamma diferentes sin justificar | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 28 Gamma diferentes documentados | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 28 Gamma diferentes documentados | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 28 Gamma diferentes documentados | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 29 Mz cero | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 29 Mz cero | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 29 Mz cero | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 30 Mz significativo | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 30 Mz significativo | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 30 Mz significativo | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 31 Servicio espectral reducción única 0.8 | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 31 Servicio espectral reducción única 0.8 | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 32 Espectral SZ adverso | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 32 Espectral SZ adverso | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 33 RS en plano distinto bloqueado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 33 RS en plano distinto bloqueado | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 34 RS base sin ejes documentados | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 34 RS base sin ejes documentados | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 35 Pedestal circular en dominio | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 35 Pedestal circular en dominio | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 35 Pedestal circular en dominio | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 36 Geometría manual bruto y bloqueo cuerpo | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 36 Geometría manual bruto y bloqueo cuerpo | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 36 Geometría manual bruto y bloqueo cuerpo | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 37 Pedestal rebasa cara columna | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 37 Pedestal rebasa cara columna | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 37 Pedestal rebasa cara columna | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 38 Relleno y pedestal excéntricos | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 38 Relleno y pedestal excéntricos | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 38 Relleno y pedestal excéntricos | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 39 Invariancia VISTA eta | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 39 Invariancia VISTA eta | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 40 Mz ruido | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 40 Mz ruido | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 40 Mz ruido | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 41 Cancelación Mz por signo propio | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 41 Cancelación Mz por signo propio | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 42 Constituyente RS detectado automáticamente | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 42 Constituyente RS detectado automáticamente | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 43 Externo combinado documentado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 43 Externo combinado documentado | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 43 Externo combinado documentado | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 44 Externo combinado sin procedimiento | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 44 Externo combinado sin procedimiento | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 44 Externo combinado sin procedimiento | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 45 CSI Frame I original | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 45 CSI Frame I original | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 45 CSI Frame I original | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 46 CSI Frame J original | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 46 CSI Frame J original | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 46 CSI Frame J original | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 47 Rotación local 37 grados | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 47 Rotación local 37 grados | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 47 Rotación local 37 grados | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F7 48 Norma indefinida gravedad intacta | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F7 48 Norma indefinida gravedad intacta | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F7 48 Norma indefinida gravedad intacta | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 01 Regular y ejes paralelos | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 01 Regular y ejes paralelos | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 02 Irregular y ejes paralelos | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 02 Irregular y ejes paralelos | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 03 Sistemas no paralelos | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 03 Sistemas no paralelos | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 04 Estático admisible art.33.2 | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 04 Estático admisible art.33.2 | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 04 Estático admisible art.33.2 | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 05 Estático no admisible | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 05 Estático no admisible | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 05 Estático no admisible | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 06 EX simple sin 30% | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 06 EX simple sin 30% | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 06 EX simple sin 30% | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 07 100/30 estático documentado | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 07 100/30 estático documentado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 07 100/30 estático documentado | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 08 Excentricidad X100 documentada | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 08 Excentricidad X100 documentada | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 09 Excentricidad X100 faltante | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 09 Excentricidad X100 faltante | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 10 Excentricidad Y100 documentada | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 10 Excentricidad Y100 documentada | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 11 Masa X 89% | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 11 Masa X 89% | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 12 Masa X 90% | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 12 Masa X 90% | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 13 Masa Y 89% | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 13 Masa Y 89% | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 14 Dos modos predominantes | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 14 Dos modos predominantes | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 15 Tres modos predominantes | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 15 Tres modos predominantes | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 16 CQC documentado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 16 CQC documentado | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 17 Alternativo art.42.3 documentado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 17 Alternativo art.42.3 documentado | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 18 Vdin regular 0.79Vest | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 18 Vdin regular 0.79Vest | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 19 Escala regular a 0.80Vest | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 19 Escala regular a 0.80Vest | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 20 Vdin irregular 0.89Vest | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 20 Vdin irregular 0.89Vest | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 21 Escala irregular a 0.90Vest | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 21 Escala irregular a 0.90Vest | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 22 Servicio no reducido factor 1 | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 22 Servicio no reducido factor 1 | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 22 Servicio no reducido factor 1 | S | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 17 |
| F8 22 Servicio no reducido factor 1 | engineS | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 256 |
| F8 22 Servicio no reducido factor 1 | DS | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 512 |
| F8 22 Servicio no reducido factor 1 | checks.ENVOLVENTES!B6 | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 1 |
| F8 22 Servicio no reducido factor 1 | checks.ESPECTROS_S!AI8 | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 1 |
| F8 22 Servicio no reducido factor 1 | global | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 1 |
| F8 23 Servicio no reducido factor 0.80 | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 23 Servicio no reducido factor 0.80 | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 24 Servicio ya reducido factor 1 | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 24 Servicio ya reducido factor 1 | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 25 Doble reducción | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 25 Doble reducción | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 25 Doble reducción | S | DATOS INVÁLIDOS — DOBLE REDUCCIÓN O REFERENCIA 0.80 FALTANTE → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 17 |
| F8 25 Doble reducción | engineS | DATOS INVÁLIDOS — DOBLE REDUCCIÓN O REFERENCIA 0.80 FALTANTE → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 256 |
| F8 25 Doble reducción | DS | DATOS INVÁLIDOS — DOBLE REDUCCIÓN O REFERENCIA 0.80 FALTANTE → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 512 |
| F8 25 Doble reducción | checks.ENVOLVENTES!B6 | DATOS INVÁLIDOS — DOBLE REDUCCIÓN O REFERENCIA 0.80 FALTANTE → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 1 |
| F8 25 Doble reducción | checks.ESPECTROS_S!AI8 | DATOS INVÁLIDOS — DOBLE REDUCCIÓN O REFERENCIA 0.80 FALTANTE → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 1 |
| F8 25 Doble reducción | global | DATOS INVÁLIDOS — DOBLE REDUCCIÓN O REFERENCIA 0.80 FALTANTE → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 1 |
| F8 26 qadm +30% desactivado | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 26 qadm +30% desactivado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 27 qadm +30% documentado | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 27 qadm +30% documentado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 28 Caja gobierna | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 28 Caja gobierna | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 29 Externo menos conservador documentado | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 29 Externo menos conservador documentado | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 29 Externo menos conservador documentado | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 30 Norma E030 indefinida | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 30 Norma E030 indefinida | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 31 Excentricidad -e Y faltante | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 31 Excentricidad -e Y faltante | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 32 CQC sin referencia | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 32 CQC sin referencia | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 33 Fuente repetida | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 33 Fuente repetida | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 34 Elemento vertical NO prohibido | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 34 Elemento vertical NO prohibido | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 35 Vertical disponible sin espectro | DU | REQUIERE COMPONENTE VERTICAL DOCUMENTADA → REQUIERE ESPECTRO VERTICAL DOCUMENTADO | 512 |
| F8 35 Vertical disponible sin espectro | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 35 Vertical disponible sin espectro | derivedView | REQUIERE COMPONENTE VERTICAL DOCUMENTADA → REQUIERE ESPECTRO VERTICAL DOCUMENTADO | 3 |
| F8 35 Vertical disponible sin espectro | U | REQUIERE COMPONENTE VERTICAL DOCUMENTADA → REQUIERE ESPECTRO VERTICAL DOCUMENTADO | 30 |
| F8 35 Vertical disponible sin espectro | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 35 Vertical disponible sin espectro | checks.MU_PRESION!D20 | REQUIERE COMPONENTE VERTICAL DOCUMENTADA → REQUIERE ESPECTRO VERTICAL DOCUMENTADO | 1 |
| F8 35 Vertical disponible sin espectro | checks.ENVOLVENTES!B6 | REQUIERE COMPONENTE VERTICAL DOCUMENTADA → REQUIERE ESPECTRO VERTICAL DOCUMENTADO | 1 |
| F8 35 Vertical disponible sin espectro | checks.ESPECTROS_U!AI8 | REQUIERE COMPONENTE VERTICAL DOCUMENTADA → REQUIERE ESPECTRO VERTICAL DOCUMENTADO | 1 |
| F8 35 Vertical disponible sin espectro | global | REQUIERE COMPONENTE VERTICAL DOCUMENTADA → REQUIERE ESPECTRO VERTICAL DOCUMENTADO | 1 |
| F8 35 Vertical disponible sin espectro | engineU | REQUIERE COMPONENTE VERTICAL DOCUMENTADA → REQUIERE ESPECTRO VERTICAL DOCUMENTADO | 464 |
| F8 36 Vertical requerido sin confirmar | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 36 Vertical requerido sin confirmar | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 37 No paralelo externo | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 37 No paralelo externo | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 37 No paralelo externo | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 38 Fuente no escalada declarada | DU | REQUIERE ESCALAMIENTO E.030 → REQUIERE DEFINIR ESTADO ART.44 | 512 |
| F8 38 Fuente no escalada declarada | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 38 Fuente no escalada declarada | derivedView | REQUIERE ESCALAMIENTO E.030 → REQUIERE DEFINIR ESTADO ART.44 | 3 |
| F8 38 Fuente no escalada declarada | U | REQUIERE ESCALAMIENTO E.030 → REQUIERE DEFINIR ESTADO ART.44 | 30 |
| F8 38 Fuente no escalada declarada | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 38 Fuente no escalada declarada | checks.MU_PRESION!D20 | REQUIERE ESCALAMIENTO E.030 → REQUIERE DEFINIR ESTADO ART.44 | 1 |
| F8 38 Fuente no escalada declarada | checks.ENVOLVENTES!B6 | REQUIERE ESCALAMIENTO E.030 → REQUIERE DEFINIR ESTADO ART.44 | 1 |
| F8 38 Fuente no escalada declarada | checks.ESPECTROS_U!AI8 | REQUIERE ESCALAMIENTO E.030 → REQUIERE DEFINIR ESTADO ART.44 | 1 |
| F8 38 Fuente no escalada declarada | global | REQUIERE ESCALAMIENTO E.030 → REQUIERE DEFINIR ESTADO ART.44 | 1 |
| F8 38 Fuente no escalada declarada | engineU | REQUIERE ESCALAMIENTO E.030 → REQUIERE DEFINIR ESTADO ART.44 | 464 |
| F8 39 Modos fraccionarios inválidos | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 39 Modos fraccionarios inválidos | DS!AD8:AD135 | DATOS INVÁLIDOS → vacío | 128 |
| F8 40 0.80 no sustituido por qadm+30% | DU!AD8:AD135 | NO APLICA → vacío | 128 |
| F8 40 0.80 no sustituido por qadm+30% | VISTA_DERIVADO!A8 | 1–7680 → 1–15360 | 1 |
| F8 40 0.80 no sustituido por qadm+30% | S | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 17 |
| F8 40 0.80 no sustituido por qadm+30% | engineS | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 256 |
| F8 40 0.80 no sustituido por qadm+30% | DS | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 512 |
| F8 40 0.80 no sustituido por qadm+30% | checks.ENVOLVENTES!B6 | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 1 |
| F8 40 0.80 no sustituido por qadm+30% | checks.ESPECTROS_S!AI8 | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 1 |
| F8 40 0.80 no sustituido por qadm+30% | global | DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO → DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 1 |

Se conserva el inventario completo de diferencias textuales en la evidencia de pruebas. No se permitió ocultar diferencias numéricas mediante esta clasificación.

Se documentan además 512 cambios numéricos de metadatos: exclusivamente el indicador SZ de la columna K de estados derivados inactivos pasa de 1 a 0 cuando la selección vertical es A/C. Se exige que el estado esté inactivo tanto en F8 como en F9. Esta excepción se limita a ese indicador; las seis acciones, geometría, demandas, capacidades y resultados de diseño se comparan sin excepción.
- F7 43 Externo combinado documentado: 128 indicadores inactivos; método A. ESTÁTICA ART.38.1.
- F7 44 Externo combinado sin procedimiento: 128 indicadores inactivos; método A. ESTÁTICA ART.38.1.
- F8 29 Externo menos conservador documentado: 128 indicadores inactivos; método A. ESTÁTICA ART.38.1.
- F8 37 No paralelo externo: 128 indicadores inactivos; método A. ESTÁTICA ART.38.1.

La prueba F7 42 detecta RESPONSE SPECTRUM en los constituyentes CSI sin necesitar la declaración manual. Su fixture selecciona B a partir de esa clasificación real y se repite después de corregir la preparación inicial. No se altera el motor para admitir una selección vertical incoherente.

### Regresión de los 88 escenarios F8

| Escenario | Estado técnico F9 | Validez F9 | Errores/circularidad |
|---|---|---|---|
| F7 01 Linear Static | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 02 Response Spectrum puro | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 03 D + Response Spectrum | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 04 Linear Add estático | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 05 Linear Add contiene RS declarado | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 06 Envelope estático correspondence | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 07 RS con correspondence | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 08 Time History mismo step | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 09 Time History Envelope rechazado | NO CUMPLE | REQUIERE DATOS / REVISAR ENTRADAS FASE 7 | 0/False |
| F7 10 E030 anterior | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 11 E030 2026 | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 12 E030 sin definir | NO CUMPLE | REQUIERE DEFINIR NORMA E.030 APLICABLE | 0/False |
| F7 13 FRAME interfaz | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 14 FRAME 0.30m encima | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 15 End offset activo | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 16 FRAME normal pesos incluidos rechazado | NO CUMPLE | REQUIERE DATOS / REVISAR ENTRADAS FASE 7 | 0/False |
| F7 17 FRAME especial documentado | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 18 JOINT cimentación modelada | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 19 BASE edificio completo | NO CUMPLE | REQUIERE DATOS / REVISAR ENTRADAS FASE 7 | 0/False |
| F7 20 BASE única válida | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 21 Relleno sin pedestal | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 22 Relleno columna rectangular | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 23 Relleno con pedestal | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 24 Pedestal incluido en P | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 25 Pedestal sumado manual | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 26 Gamma tres pesos iguales | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 27 Gamma diferentes sin justificar | NO CUMPLE | REQUIERE DATOS / REVISAR ENTRADAS FASE 7 | 0/False |
| F7 28 Gamma diferentes documentados | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 29 Mz cero | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 30 Mz significativo | NO CUMPLE | REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA | 0/False |
| F7 31 Servicio espectral reducción única 0.8 | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 32 Espectral SZ adverso | NO CUMPLE | REQUIERE ANÁLISIS ESPECIAL | 0/False |
| F7 33 RS en plano distinto bloqueado | NO CUMPLE | REQUIERE DATOS — ESTADOS ESPECTRALES | 0/False |
| F7 34 RS base sin ejes documentados | NO CUMPLE | REQUIERE DATOS — ESTADOS ESPECTRALES | 0/False |
| F7 35 Pedestal circular en dominio | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 36 Geometría manual bruto y bloqueo cuerpo | NO CUMPLE | REQUIERE ANÁLISIS GEOMETRÍA LOCALIZADA | 0/False |
| F7 37 Pedestal rebasa cara columna | NO CUMPLE | REQUIERE ANÁLISIS GEOMETRÍA LOCALIZADA | 0/False |
| F7 38 Relleno y pedestal excéntricos | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 39 Invariancia VISTA eta | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 40 Mz ruido | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 41 Cancelación Mz por signo propio | NO CUMPLE | REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA | 0/False |
| F7 42 Constituyente RS detectado automáticamente | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 43 Externo combinado documentado | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 44 Externo combinado sin procedimiento | NO CUMPLE | REQUIERE DATOS / REVISAR ENTRADAS FASE 7 | 0/False |
| F7 45 CSI Frame I original | NO CUMPLE | REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA | 0/False |
| F7 46 CSI Frame J original | NO CUMPLE | REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA | 0/False |
| F7 47 Rotación local 37 grados | NO CUMPLE | REQUIERE DATOS | 0/False |
| F7 48 Norma indefinida gravedad intacta | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 01 Regular y ejes paralelos | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 02 Irregular y ejes paralelos | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 03 Sistemas no paralelos | NO CUMPLE | REQUIERE EJES NO PARALELOS — PROCEDIMIENTO EXTERNO | 0/False |
| F8 04 Estático admisible art.33.2 | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 05 Estático no admisible | NO CUMPLE | REQUIERE MÉTODO ESTÁTICO ADMISIBLE ART.33.2 | 0/False |
| F8 06 EX simple sin 30% | NO CUMPLE | REQUIERE COMBINACIÓN DIRECCIONAL ESTÁTICA | 0/False |
| F8 07 100/30 estático documentado | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 08 Excentricidad X100 documentada | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 09 Excentricidad X100 faltante | NO CUMPLE | REQUIERE PROCEDIMIENTO EXTERNO DOCUMENTADO — EXCENTRICIDAD X100/Y100 | 0/False |
| F8 10 Excentricidad Y100 documentada | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 11 Masa X 89% | NO CUMPLE | NO CUMPLE FUENTE E.030 | 0/False |
| F8 12 Masa X 90% | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 13 Masa Y 89% | NO CUMPLE | NO CUMPLE FUENTE E.030 | 0/False |
| F8 14 Dos modos predominantes | NO CUMPLE | NO CUMPLE FUENTE E.030 | 0/False |
| F8 15 Tres modos predominantes | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 16 CQC documentado | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 17 Alternativo art.42.3 documentado | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 18 Vdin regular 0.79Vest | NO CUMPLE | REQUIERE ESCALAMIENTO E.030 | 0/False |
| F8 19 Escala regular a 0.80Vest | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 20 Vdin irregular 0.89Vest | NO CUMPLE | REQUIERE ESCALAMIENTO E.030 | 0/False |
| F8 21 Escala irregular a 0.90Vest | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 22 Servicio no reducido factor 1 | NO CUMPLE | DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 0/False |
| F8 23 Servicio no reducido factor 0.80 | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 24 Servicio ya reducido factor 1 | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 25 Doble reducción | NO CUMPLE | DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 0/False |
| F8 26 qadm +30% desactivado | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 27 qadm +30% documentado | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 28 Caja gobierna | NO CUMPLE ENVOLVENTE CONSERVADORA — VERIFICAR INTERACCIÓN EXTERNA | REQUIERE ANÁLISIS ESPECIAL | 0/False |
| F8 29 Externo menos conservador documentado | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 30 Norma E030 indefinida | NO CUMPLE | REQUIERE DEFINIR NORMA E.030 APLICABLE | 0/False |
| F8 31 Excentricidad -e Y faltante | NO CUMPLE | REQUIERE PROCEDIMIENTO EXTERNO DOCUMENTADO — EXCENTRICIDAD X100/Y100 | 0/False |
| F8 32 CQC sin referencia | NO CUMPLE | REQUIERE COMBINACIÓN MODAL DOCUMENTADA | 0/False |
| F8 33 Fuente repetida | NO CUMPLE | REQUIERE FUENTE MODAL ÚNICA | 0/False |
| F8 34 Elemento vertical NO prohibido | NO CUMPLE | REQUIERE COMPONENTE VERTICAL OBLIGATORIA | 0/False |
| F8 35 Vertical disponible sin espectro | NO CUMPLE | REQUIERE ESPECTRO VERTICAL DOCUMENTADO | 0/False |
| F8 36 Vertical requerido sin confirmar | NO CUMPLE | REQUIERE COMPONENTE VERTICAL OBLIGATORIA | 0/False |
| F8 37 No paralelo externo | NO CUMPLE | REQUIERE DATOS | 0/False |
| F8 38 Fuente no escalada declarada | NO CUMPLE | REQUIERE DEFINIR ESTADO ART.44 | 0/False |
| F8 39 Modos fraccionarios inválidos | NO CUMPLE | DATOS INVÁLIDOS MASA MODAL | 0/False |
| F8 40 0.80 no sustituido por qadm+30% | NO CUMPLE | DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80 | 0/False |

## Integridad y cierre nativo

Excel 16.0, build 14332.0, idioma UI 3082. La instalación disponible es Office 2021 x64, español; no hay una instalación de Office 2016. Se verificaron funciones y sintaxis compatibles con Excel español 2016, incluida la fórmula local con SI y separador punto y coma. No se afirma una prueba nativa sobre Office 2016.

Se ejecutó CalculateFullRebuild, guardado, cierre, normalización exclusiva de los nombres reservados de impresión y del modo de cálculo, reapertura sin reparación y otro CalculateFullRebuild. La persistencia superó 3378 comparaciones sin diferencias. Apertura de cierre: 240.973 s; recálculo de cierre: 193.140 s; apertura fría: 280.790 s; recálculo frío: 208.668 s. Son mediciones de esta máquina sin aislamiento de otros procesos. Se revisaron las vistas PDF exportadas por Excel.

El libro final contiene 89 hojas, 24 gráficos y 6691620 celdas con fórmula; ocupa 145811789 bytes. Las hojas adicionales permiten evaluar la rama -Ev con el motor y controles de F8. No se realizó una compactación masiva ni se acredita una mejora de rendimiento.

Cero errores de fórmula nativos/cacheados, circularidad, vínculos externos, VBA, _xlfn, _xludf, referencias #REF! o grupos de fórmulas compartidas huérfanos. Se conservaron 3622 constantes originales de las hojas físicas de entrada, combos, espectros, cargas, barras y acero. Todos los 17 archivos originales F1–F8 mantienen su SHA-256.

El proyecto entregado conserva el estado **NO CUMPLE** y validez **REQUIERE DATOS**. Las fuentes del proyecto, método vertical y referencias pendientes deben completarse antes de acreditar la demanda. No se cambió geometría, qadm, materiales, barras, separaciones o cargas para obtener CUMPLE.

Funciones del libro final: `ABS`, `AND`, `CHOOSE`, `COS`, `COUNT`, `COUNTA`, `COUNTBLANK`, `COUNTIF`, `COUNTIFS`, `EXACT`, `IF`, `IFERROR`, `INDEX`, `INT`, `ISBLANK`, `ISNUMBER`, `ISTEXT`, `LEN`, `MATCH`, `MAX`, `MIN`, `MOD`, `NOT`, `OR`, `PI`, `RADIANS`, `ROUND`, `ROW`, `SIN`, `SQRT`, `SUM`, `SUMIF`, `SUMPRODUCT`, `TEXT`.

SHA-256 del XLSX final: `798728e514ab96de6fbae13a40bb9c6a6dd9d92340531f51dd98f3293a7a02d7`.

## FORMULAS_CRITICAS_AUDITABLES

Texto literal de la copia final, en sintaxis OOXML inglesa con coma. Excel español presenta la traducción y punto y coma; este bloque no debe pegarse como fórmula local. Se mantienen las direcciones críticas de F8 y se añaden las de F9. Los ejemplos compartidos se expanden desde su definición nativa. Filas 8/68: primer padre U/S; mismo patrón para los restantes 59.

### Nombres definidos

| Nombre | Referencia final |
|---|---|
| `inp_adopt_local` | `CONEXION_COLUMNA_ZAPATA!$B$102` |
| `inp_agg` | `INGRESO_DATOS!$C$91` |
| `inp_avf` | `INGRESO_DATOS!$C$121` |
| `inp_avf_anchor` | `INGRESO_DATOS!$C$122` |
| `inp_bar_col` | `INGRESO_DATOS!$C$110` |
| `inp_bar_dowel` | `INGRESO_DATOS!$C$113` |
| `inp_bar_inf_x` | `INGRESO_DATOS!$C$54` |
| `inp_bar_inf_y` | `INGRESO_DATOS!$C$55` |
| `inp_bar_sup_x` | `INGRESO_DATOS!$C$56` |
| `inp_bar_sup_y` | `INGRESO_DATOS!$C$57` |
| `inp_bottom_exposure` | `INGRESO_DATOS!$C$151` |
| `inp_bx` | `INGRESO_DATOS!$C$30` |
| `inp_by` | `INGRESO_DATOS!$C$31` |
| `inp_case` | `VISTA_COMBO!$B$10` |
| `inp_col_system` | `INGRESO_DATOS!$C$107` |
| `inp_col_type` | `INGRESO_DATOS!$C$66` |
| `inp_concrete_type` | `INGRESO_DATOS!$C$85` |
| `inp_convert_p` | `INGRESO_DATOS!$C$50` |
| `inp_cx` | `INGRESO_DATOS!$C$42` |
| `inp_cy` | `INGRESO_DATOS!$C$43` |
| `inp_df` | `INGRESO_DATOS!$C$33` |
| `inp_edge_dir` | `INGRESO_DATOS!$C$81` |
| `inp_ems_incl` | `INGRESO_DATOS!$C$79` |
| `inp_ems_ref` | `INGRESO_DATOS!$C$80` |
| `inp_end_col` | `INGRESO_DATOS!$C$119` |
| `inp_end_inf` | `INGRESO_DATOS!$C$87` |
| `inp_end_sup` | `INGRESO_DATOS!$C$90` |
| `inp_epoxy` | `INGRESO_DATOS!$C$88` |
| `inp_eq_factor` | `INGRESO_DATOS!$C$76` |
| `inp_eta_x` | `INGRESO_DATOS!$C$170` |
| `inp_eta_y` | `INGRESO_DATOS!$C$171` |
| `inp_fc` | `INGRESO_DATOS!$C$14` |
| `inp_fc_col` | `INGRESO_DATOS!$C$108` |
| `inp_fs_over` | `INGRESO_DATOS!$C$131` |
| `inp_fs_over_ref` | `INGRESO_DATOS!$C$132` |
| `inp_fs_slide` | `INGRESO_DATOS!$C$126` |
| `inp_fs_slide_ref` | `INGRESO_DATOS!$C$127` |
| `inp_fws_u` | `INGRESO_DATOS!$C$70` |
| `inp_fwz_u` | `INGRESO_DATOS!$C$69` |
| `inp_fy` | `INGRESO_DATOS!$C$15` |
| `inp_fy_col` | `INGRESO_DATOS!$C$109` |
| `inp_fy_nom` | `INGRESO_DATOS!$C$161` |
| `inp_gamma_c` | `INGRESO_DATOS!$C$16` |
| `inp_gamma_s` | `INGRESO_DATOS!$C$17` |
| `inp_grade` | `INGRESO_DATOS!$C$160` |
| `inp_h` | `INGRESO_DATOS!$C$32` |
| `inp_hs` | `INGRESO_DATOS!$C$36` |
| `inp_joint` | `INGRESO_DATOS!$C$120` |
| `inp_joint_ref` | `INGRESO_DATOS!$C$123` |
| `inp_lcol_above` | `INGRESO_DATOS!$C$116` |
| `inp_lcol_foot` | `INGRESO_DATOS!$C$115` |
| `inp_ldow_above` | `INGRESO_DATOS!$C$118` |
| `inp_ldow_foot` | `INGRESO_DATOS!$C$117` |
| `inp_ll_ix_m` | `INGRESO_DATOS!$C$97` |
| `inp_ll_ix_p` | `INGRESO_DATOS!$C$98` |
| `inp_ll_iy_m` | `INGRESO_DATOS!$C$99` |
| `inp_ll_iy_p` | `INGRESO_DATOS!$C$100` |
| `inp_ll_sx_m` | `INGRESO_DATOS!$C$101` |
| `inp_ll_sx_p` | `INGRESO_DATOS!$C$102` |
| `inp_ll_sy_m` | `INGRESO_DATOS!$C$103` |
| `inp_ll_sy_p` | `INGRESO_DATOS!$C$104` |
| `inp_local_combo` | `CONEXION_COLUMNA_ZAPATA!$B$103` |
| `inp_local_detail` | `INGRESO_DATOS!$C$92` |
| `inp_min_face` | `INGRESO_DATOS!$C$166` |
| `inp_min_frac` | `INGRESO_DATOS!$C$167` |
| `inp_min_scheme` | `INGRESO_DATOS!$C$165` |
| `inp_mu` | `INGRESO_DATOS!$C$19` |
| `inp_n_col` | `INGRESO_DATOS!$C$111` |
| `inp_n_continue` | `INGRESO_DATOS!$C$112` |
| `inp_n_div_x` | `INGRESO_DATOS!$C$37` |
| `inp_n_div_y` | `INGRESO_DATOS!$C$38` |
| `inp_n_dowel` | `INGRESO_DATOS!$C$114` |
| `inp_nc_sx` | `INGRESO_DATOS!$C$179` |
| `inp_nc_sy` | `INGRESO_DATOS!$C$185` |
| `inp_ncx` | `INGRESO_DATOS!$C$137` |
| `inp_ncy` | `INGRESO_DATOS!$C$141` |
| `inp_nloc_ix` | `INGRESO_DATOS!$C$93` |
| `inp_nloc_iy` | `INGRESO_DATOS!$C$94` |
| `inp_nloc_sx` | `INGRESO_DATOS!$C$95` |
| `inp_nloc_sy` | `INGRESO_DATOS!$C$96` |
| `inp_no_sx` | `INGRESO_DATOS!$C$180` |
| `inp_no_sx_minus` | `INGRESO_DATOS!$C$181` |
| `inp_no_sx_plus` | `INGRESO_DATOS!$C$182` |
| `inp_no_sy` | `INGRESO_DATOS!$C$186` |
| `inp_no_sy_minus` | `INGRESO_DATOS!$C$187` |
| `inp_no_sy_plus` | `INGRESO_DATOS!$C$188` |
| `inp_nox` | `INGRESO_DATOS!$C$138` |
| `inp_nox_minus` | `INGRESO_DATOS!$C$145` |
| `inp_nox_plus` | `INGRESO_DATOS!$C$146` |
| `inp_noy` | `INGRESO_DATOS!$C$142` |
| `inp_noy_minus` | `INGRESO_DATOS!$C$147` |
| `inp_noy_plus` | `INGRESO_DATOS!$C$148` |
| `inp_order_inf` | `INGRESO_DATOS!$C$65` |
| `inp_order_sup` | `INGRESO_DATOS!$C$68` |
| `inp_passive` | `INGRESO_DATOS!$C$128` |
| `inp_peak` | `INGRESO_DATOS!$C$156` |
| `inp_peak_ref` | `INGRESO_DATOS!$C$157` |
| `inp_peso_suelo` | `INGRESO_DATOS!$C$35` |
| `inp_peso_zapata` | `INGRESO_DATOS!$C$34` |
| `inp_phi_f` | `INGRESO_DATOS!$C$22` |
| `inp_phi_p` | `INGRESO_DATOS!$C$24` |
| `inp_phi_v` | `INGRESO_DATOS!$C$23` |
| `inp_qadm` | `INGRESO_DATOS!$C$18` |
| `inp_qadm_basis` | `INGRESO_DATOS!$C$77` |
| `inp_qadm_inc` | `INGRESO_DATOS!$C$75` |
| `inp_rebar_type` | `INGRESO_DATOS!$C$84` |
| `inp_rec_inf` | `INGRESO_DATOS!$C$20` |
| `inp_rec_lat` | `INGRESO_DATOS!$C$86` |
| `inp_rec_sup` | `INGRESO_DATOS!$C$21` |
| `inp_repartition_ok` | `INGRESO_DATOS!$C$173` |
| `inp_repartition_ref` | `INGRESO_DATOS!$C$172` |
| `inp_rho_min` | `INGRESO_DATOS!$C$25` |
| `inp_rpassive` | `INGRESO_DATOS!$C$129` |
| `inp_rpassive_ref` | `INGRESO_DATOS!$C$130` |
| `inp_sc_sx` | `INGRESO_DATOS!$C$177` |
| `inp_sc_sy` | `INGRESO_DATOS!$C$183` |
| `inp_scx` | `INGRESO_DATOS!$C$135` |
| `inp_scy` | `INGRESO_DATOS!$C$139` |
| `inp_sep_inf_x` | `INGRESO_DATOS!$C$58` |
| `inp_sep_inf_y` | `INGRESO_DATOS!$C$59` |
| `inp_sep_max_usuario` | `INGRESO_DATOS!$C$26` |
| `inp_sep_sup_x` | `INGRESO_DATOS!$C$60` |
| `inp_sep_sup_y` | `INGRESO_DATOS!$C$61` |
| `inp_side_exposure` | `INGRESO_DATOS!$C$89` |
| `inp_sigma0` | `INGRESO_DATOS!$C$78` |
| `inp_sign_mx_fy` | `INGRESO_DATOS!$C$48` |
| `inp_sign_my_fx` | `INGRESO_DATOS!$C$49` |
| `inp_sign_p` | `INGRESO_DATOS!$C$50` |
| `inp_so_sx` | `INGRESO_DATOS!$C$178` |
| `inp_so_sy` | `INGRESO_DATOS!$C$184` |
| `inp_sox` | `INGRESO_DATOS!$C$136` |
| `inp_soy` | `INGRESO_DATOS!$C$140` |
| `inp_srv_type` | `INGRESO_DATOS!$C$74` |
| `inp_top_exposure` | `INGRESO_DATOS!$C$152` |
| `inp_traslado` | `INGRESO_DATOS!$C$47` |
| `inp_xc` | `INGRESO_DATOS!$C$44` |
| `inp_yc` | `INGRESO_DATOS!$C$45` |
| `inp_zh` | `INGRESO_DATOS!$C$46` |
| `zap7_as_xneg_inf` | `RESULTADOS_ULTIMOS!$BW$8` |
| `zap7_as_xneg_sup` | `RESULTADOS_ULTIMOS!$CF$8` |
| `zap7_as_xpos_inf` | `RESULTADOS_ULTIMOS!$CP$8` |
| `zap7_as_xpos_sup` | `RESULTADOS_ULTIMOS!$CY$8` |
| `zap7_as_yneg_inf` | `RESULTADOS_ULTIMOS!$DI$8` |
| `zap7_as_yneg_sup` | `RESULTADOS_ULTIMOS!$DR$8` |
| `zap7_as_ypos_inf` | `RESULTADOS_ULTIMOS!$EB$8` |
| `zap7_as_ypos_sup` | `RESULTADOS_ULTIMOS!$EK$8` |
| `zap7_dc_punz_u` | `RESULTADOS_ULTIMOS!$AO$8` |
| `zap7_det_t_u` | `COMBOS_ULTIMOS!$BF$8` |
| `zap7_dz_u` | `COMBOS_ULTIMOS!$CR$8` |
| `zap7_error_t_u` | `COMBOS_ULTIMOS!$BG$8` |
| `zap7_estado_cobertura` | `ENVOLVENTES!$B$54` |
| `zap7_estado_tecnico` | `ENVOLVENTES!$B$5` |
| `zap7_estado_validez` | `ENVOLVENTES!$B$6` |
| `zap7_fx_csi_u` | `RESULTADOS_ULTIMOS!$E$8` |
| `zap7_fy_csi_u` | `RESULTADOS_ULTIMOS!$F$8` |
| `zap7_gamma_wped_u` | `COMBOS_ULTIMOS!$CM$8` |
| `zap7_gamma_ws_u` | `COMBOS_ULTIMOS!$CO$8` |
| `zap7_gamma_wz_u` | `COMBOS_ULTIMOS!$CN$8` |
| `zap7_geometria_estado` | `CONTROL_FASE7!$B$41` |
| `zap7_gob_punz` | `ENVOLVENTES!$B$8` |
| `zap7_gob_servicio` | `ENVOLVENTES!$B$48` |
| `zap7_gx_neta_u` | `MU_PRESION!$D$24` |
| `zap7_gy_neta_u` | `MU_PRESION!$D$25` |
| `zap7_mx_csi_u` | `RESULTADOS_ULTIMOS!$G$8` |
| `zap7_mx_cuerpo_u` | `MU_CARGAS!$E$28` |
| `zap7_my_csi_u` | `RESULTADOS_ULTIMOS!$H$8` |
| `zap7_my_cuerpo_u` | `MU_CARGAS!$E$29` |
| `zap7_mz_csi_u` | `RESULTADOS_ULTIMOS!$I$8` |
| `zap7_mz_tol` | `CONTROL_FASE7!$B$44` |
| `zap7_naturaleza_u` | `COMBOS_ULTIMOS!$CQ$8` |
| `zap7_norma` | `CONTROL_FASE7!$B$7` |
| `zap7_norma_estado` | `CONTROL_FASE7!$B$10` |
| `zap7_p_csi_u` | `RESULTADOS_ULTIMOS!$D$8` |
| `zap7_p_cuerpo_u` | `MU_CARGAS!$E$27` |
| `zap7_q0_neta_u` | `MU_PRESION!$D$23` |
| `zap7_qmax_bruta_u` | `RESULTADOS_ULTIMOS!$S$8` |
| `zap7_qmin_bruta_u` | `RESULTADOS_ULTIMOS!$T$8` |
| `zap7_t11_u` | `COMBOS_ULTIMOS!$BB$8` |
| `zap7_t12_u` | `COMBOS_ULTIMOS!$BC$8` |
| `zap7_t21_u` | `COMBOS_ULTIMOS!$BD$8` |
| `zap7_t22_u` | `COMBOS_ULTIMOS!$BE$8` |
| `zap7_vu_punz_u` | `RESULTADOS_ULTIMOS!$Y$8` |
| `zap7_vu_xneg` | `RESULTADOS_ULTIMOS!$AT$8` |
| `zap7_vu_xpos` | `RESULTADOS_ULTIMOS!$AZ$8` |
| `zap7_vu_yneg` | `RESULTADOS_ULTIMOS!$BF$8` |
| `zap7_vu_ypos` | `RESULTADOS_ULTIMOS!$BL$8` |
| `zap7_wped` | `CONTROL_FASE7!$B$35` |
| `zap7_ws` | `CONTROL_FASE7!$B$36` |
| `zap7_ws_prisma` | `CONTROL_FASE7!$B$38` |
| `zap7_ws_void` | `CONTROL_FASE7!$B$37` |
| `zap7_wz` | `CONTROL_FASE7!$B$34` |
| `zap8_caja_exclusiva` | `ENVOLVENTES!$B$155` |
| `zap8_demanda_u` | `DEMANDAS_E030!$Y$8` |
| `zap8_fuente_modal` | `FUENTES_E030!$AC$8` |
| `zap8_no_paralelos` | `CONTROL_E030_F8!$B$9` |
| `zap8_regularidad` | `CONTROL_E030_F8!$B$7` |
| `zap8_suelo_080` | `DEMANDAS_E030!$X$68` |

### Fórmulas por celda

**ENVOLVENTES!B5**

```excel
=IF(B155,"NO CUMPLE ENVOLVENTE CONSERVADORA — VERIFICAR INTERACCIÓN EXTERNA",B153)&IF(AND(B153="NO CUMPLE",COUNTIF(DEMANDAS_E030!AD8:AD127,"ESCALAMIENTO CONSERVADOR ADICIONAL")>0)," — DEMANDAS CON ESCALAMIENTO SUPERIOR AL MÍNIMO NORMATIVO","")
```

**ENVOLVENTES!B6**

```excel
=IF(COUNTIFS(DEMANDAS_E030!A8:A127,"SI",DEMANDAS_E030!Y8:Y127,"<>OK",DEMANDAS_E030!Y8:Y127,"<>NO APLICA")>0,INDEX(DEMANDAS_E030!Y8:Y127,MATCH(1,INDEX((DEMANDAS_E030!A8:A127="SI")*(DEMANDAS_E030!Y8:Y127<>"OK")*(DEMANDAS_E030!Y8:Y127<>"NO APLICA"),0),0)),IF(SUM(COUNTIF(COMBOS_ULTIMOS!CT8:CT67,"REQUIERE DEFINIR NORMA E.030 APLICABLE"),COUNTIF(COMBOS_SERVICIO!DM8:DM67,"REQUIERE DEFINIR NORMA E.030 APLICABLE"))>0,"REQUIERE DEFINIR NORMA E.030 APLICABLE",IF(COUNTIF(TOTAL_F7_U!ET8:ET1987,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA")+COUNTIF(TOTAL_F7_S!AJ8:AJ1987,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA")>0,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",IF(COUNTIFS(ESPECTROS_U!A8:A67,"SI",ESPECTROS_U!AI8:AI67,"<>OK")+COUNTIFS(ESPECTROS_S!A8:A67,"SI",ESPECTROS_S!AI8:AI67,"<>OK")>0,"REQUIERE DATOS — ESTADOS ESPECTRALES",IF(CONTROL_FASE7!B41<>"OK",CONTROL_FASE7!B41,IF(COUNTIFS(COMBOS_ULTIMOS!A8:A67,"SI",COMBOS_ULTIMOS!K8:K67,"<>OK",COMBOS_ULTIMOS!K8:K67,"<>ESPECTRAL — USAR ESTADOS DERIVADOS")+COUNTIFS(COMBOS_SERVICIO!A8:A67,"SI",COMBOS_SERVICIO!O8:O67,"<>OK",COMBOS_SERVICIO!O8:O67,"<>ESPECTRAL — USAR ESTADOS DERIVADOS")>0,"REQUIERE DATOS / REVISAR ENTRADAS FASE 7",IF(COUNTIF(TOTAL_F7_U!GM8:GM1987,"DATOS INVÁLIDOS")+COUNTIF(TOTAL_F7_S!BC8:BC1987,"DATOS INVÁLIDOS")+COUNTIF(ENV_BARRAS!Y8:AA67,"DATOS INVÁLIDOS")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"DATOS INVÁLIDOS")+COUNTIF(COMBOS_ULTIMOS!K8:K67,"DATOS NO CONCURRENTES — NO USAR COMO COMBO")+COUNTIF(COMBOS_SERVICIO!O8:O67,"DATOS NO CONCURRENTES — NO USAR COMO COMBO")>0,"DATOS INVÁLIDOS",IF(COUNTIF(TOTAL_F7_U!GM8:GM1987,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(TOTAL_F7_S!BC8:BC1987,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(ENV_BARRAS!Y8:AA67,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE",IF(COUNTIF(TOTAL_F7_U!GM8:GM1987,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(TOTAL_F7_S!BC8:BC1987,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(ENV_BARRAS!Y8:AA67,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")>0,"REQUIERE CONTACTO PARCIAL",IF(COUNTIF(TOTAL_F7_U!GM8:GM1987,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(TOTAL_F7_S!BC8:BC1987,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(ENV_BARRAS!Y8:AA67,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(TOTAL_F7_U!GM8:GM1987,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(TOTAL_F7_S!BC8:BC1987,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(ENV_BARRAS!Y8:AA67,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(OR(CONTROL_MULTICOMBO!$B$33<>"COMPLETO",CONTROL_MULTICOMBO!$B$35<>"OK",COUNTIF(COMBOS_ULTIMOS!V8:V67,"REQUIERE DATOS")>0,COUNTIF(COMBOS_ULTIMOS!A8:A67,"SI")=0,COUNTIF(COMBOS_SERVICIO!A8:A67,"SI")=0,COUNTIF(TOTAL_F7_U!GM8:GM1987,"REQUIERE DATOS")+COUNTIF(TOTAL_F7_S!BC8:BC1987,"REQUIERE DATOS")+COUNTIF(ENV_BARRAS!Y8:AA67,"REQUIERE DATOS")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"REQUIERE DATOS")>0),"REQUIERE DATOS","COMPLETO")))))))))))
```

**ENVOLVENTES!B8**

```excel
=IF(ISNUMBER(H8),INDEX(TOTAL_F7_U!B1:B1987,H8),"")
```

**ENVOLVENTES!G8**

```excel
=IF(J8>0,MAX(TOTAL_F7_U!$GN$8:$GN$1987),"")
```

**ENVOLVENTES!H8**

```excel
=IF(J8>0,MATCH(G8,TOTAL_F7_U!$GN$8:$GN$1987,0)+7,"")
```

**ENVOLVENTES!B48**

```excel
=IF(ISNUMBER(H48),INDEX(TOTAL_F7_S!B1:B1987,H48),"")
```

**ENVOLVENTES!G48**

```excel
=IF(J48>0,MAX(TOTAL_F7_S!$BN$8:$BN$1987),"")
```

**ENVOLVENTES!H48**

```excel
=IF(J48>0,MATCH(G48,TOTAL_F7_S!$BN$8:$BN$1987,0)+7,"")
```

**ENVOLVENTES!B54**

```excel
=CONTROL_MULTICOMBO!$B$33
```

**ENVOLVENTES!B56**

```excel
=IF(COUNT(TOTAL_F7_U!HW8:HW1987)>=2,INDEX(TOTAL_F7_U!B8:B1987,MATCH(2,TOTAL_F7_U!HW8:HW1987,0)),"")
```

**ENVOLVENTES!E56**

```excel
=IF(COUNT(TOTAL_F7_U!HW8:HW1987)>=2,INDEX(TOTAL_F7_U!AQ8:AQ1987,MATCH(2,TOTAL_F7_U!HW8:HW1987,0)),"")
```

**ENVOLVENTES!B57**

```excel
=IF(COUNT(TOTAL_F7_U!HW8:HW1987)>=3,INDEX(TOTAL_F7_U!B8:B1987,MATCH(3,TOTAL_F7_U!HW8:HW1987,0)),"")
```

**ENVOLVENTES!E57**

```excel
=IF(COUNT(TOTAL_F7_U!HW8:HW1987)>=3,INDEX(TOTAL_F7_U!AQ8:AQ1987,MATCH(3,TOTAL_F7_U!HW8:HW1987,0)),"")
```

**ENVOLVENTES!B145**

```excel
=CONTROL_FASE7!B7
```

**ENVOLVENTES!B146**

```excel
=IF(COUNTIF(ESPECTROS_U!A8:A67,"SI")+COUNTIF(ESPECTROS_S!A8:A67,"SI")>0,"ESPECTRAL / ESTADÍSTICO ESPECTRAL","VER TIPO Y NATURALEZA EN CADA COMBO")
```

**ENVOLVENTES!B147**

```excel
=CONTROL_FASE7!B16
```

**ENVOLVENTES!B148**

```excel
=CONTROL_FASE7!B10
```

**ENVOLVENTES!B150**

```excel
=CONTROL_E030_F8!B19
```

**ENVOLVENTES!B151**

```excel
=CONTROL_E030_F8!B20
```

**ENVOLVENTES!B152**

```excel
=B6
```

**ENVOLVENTES!B153**

```excel
=IF(COUNTIF(TOTAL_F7_U!AP8:AR1987,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!AT8:BQ1987,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!EQ8:ES1987,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!FQ8:GK1987,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!IV8:JC1987,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!EU8:FP1987,"NO CUMPLE")+COUNTIF(TOTAL_F7_S!AF8:BA1987,"NO CUMPLE")+COUNTIF(ENV_BARRAS!Y8:AA67,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!CA8:EO1987,"NO FACTIBLE")+COUNTIF(CALC_ENV_BARRAS!C8:BJ522,"NO CUMPLE")>0,"NO CUMPLE",IF(B6="COMPLETO","CUMPLE","SIN RESULTADO COMPLETO"))
```

**ENVOLVENTES!B154**

```excel
=IF(SUMPRODUCT(TOTAL_F7_U!JD8:JD1987*(TOTAL_F7_U!JE8:JE1987<>"ENVOLVENTE CONSERVADORA DE SIGNOS"))+SUMPRODUCT(TOTAL_F7_S!BT8:BT1987*(TOTAL_F7_S!BU8:BU1987<>"ENVOLVENTE CONSERVADORA DE SIGNOS"))+COUNTIF(CALC_ENV_BARRAS!C8:BJ522,"NO CUMPLE")>0,"NO CUMPLE",IF(B6="COMPLETO","CUMPLE","SIN RESULTADO COMPLETO"))
```

**ENVOLVENTES!B155**

```excel
=AND(B153="NO CUMPLE",B154<>"NO CUMPLE",COUNTIFS(DERIVADOS_U!A8:A15367,"SI",DERIVADOS_U!Z8:Z15367,"OK")+COUNTIFS(DERIVADOS_S!A8:A15367,"SI",DERIVADOS_S!Z8:Z15367,"OK")>0)
```

**ENVOLVENTES!B156**

```excel
=IF(COUNTIF(DEMANDAS_E030!AD8:AD127,"ESCALAMIENTO CONSERVADOR ADICIONAL")>0,"ESCALAMIENTO CONSERVADOR ADICIONAL — DEMANDA SUPERIOR AL MÍNIMO NORMATIVO","SIN SOBRESCALA SIGNIFICATIVA EN DEMANDAS ACTIVAS")
```

**ENVOLVENTES!B157**

```excel
=IF(COUNTIFS(DEMANDAS_E030!A8:A127,"SI",DEMANDAS_E030!AC8:AC127,"SI")=0,"MÉTODO VERTICAL POR DEMANDA: VER VERTICAL_F9",IF(COUNTIFS(DEMANDAS_E030!A8:A127,"SI",DEMANDAS_E030!AC8:AC127,"SI",DEMANDAS_E030!AA8:AA127,"ENVOLVENTE CONSERVADORA DE SIGNOS")>0,"HORIZONTAL ESPECTRAL: CAJA DE SIGNOS; VERTICAL ESTÁTICA: +Ev / -Ev; VER CADA DEMANDA","HORIZONTAL FIRMADA; VERTICAL ESTÁTICA: +Ev / -Ev"))
```

**CONTROL_FASE7!B10**

```excel
=IF(OR(B7="REQUIERE DEFINIR",LEN(B8)=0,LEN(B9)=0),"REQUIERE DEFINIR NORMA E.030 APLICABLE",IF(OR(B7="E.030 ANTERIOR A RM 183-2026",B7="E.030 MODIFICADA RM 183-2026"),"OK","DATOS INVÁLIDOS"))
```

**CONTROL_FASE7!B16**

```excel
=IF(B10<>"OK",B10,IF(CONTROL_E030_F8!B12<>"OK",CONTROL_E030_F8!B12,IF(B7="E.030 MODIFICADA RM 183-2026",IF(CONTROL_E030_F8!B9="SI","REQUIERE EJES NO PARALELOS / PROCEDIMIENTO EXTERNO","SRSS 100/30 E.030 ART.43"),IF(B12="REGULAR","E.030 ANTERIOR — DIRECCIONES INDEPENDIENTES","REQUIERE DIRECCIÓN DESFAVORABLE EXTERNA"))))
```

**CONTROL_FASE7!B30**

```excel
=inp_bx*inp_by*inp_hs
```

**CONTROL_FASE7!B31**

```excel
=IF(B20="COLUMNA DIRECTA",0,IF(B20="PEDESTAL RECTANGULAR",B21*B22,IF(B20="PEDESTAL CIRCULAR",PI()*B23^2/4,0)))
```

**CONTROL_FASE7!B32**

```excel
=IF(B20="COLUMNA DIRECTA",inp_cx*inp_cy*inp_hs,IF(B20="GEOMETRÍA MANUAL",IF(ISNUMBER(B25),B25,0),B31*MIN(B24,inp_hs)+inp_cx*inp_cy*MAX(0,inp_hs-B24)))
```

**CONTROL_FASE7!B33**

```excel
=IF(B40="OK",B30-B32,"")
```

**CONTROL_FASE7!B34**

```excel
=inp_bx*inp_by*inp_h*inp_gamma_c
```

**CONTROL_FASE7!B35**

```excel
=IF(B20="COLUMNA DIRECTA",0,IF(B20="GEOMETRÍA MANUAL",IF(ISNUMBER(B26),B26,0),B31*B24))*inp_gamma_c
```

**CONTROL_FASE7!B36**

```excel
=IF(B40="OK",B33*inp_gamma_s,"")
```

**CONTROL_FASE7!B37**

```excel
=IF(B40="OK",B32*inp_gamma_s,"")
```

**CONTROL_FASE7!B38**

```excel
=B30*inp_gamma_s
```

**CONTROL_FASE7!B40**

```excel
=IF(NOT(OR(B20="COLUMNA DIRECTA",B20="PEDESTAL RECTANGULAR",B20="PEDESTAL CIRCULAR",B20="GEOMETRÍA MANUAL")),"DATOS INVÁLIDOS",IF(AND(B20="PEDESTAL RECTANGULAR",OR(COUNT(B21:B22,B24)<>3,MIN(B21:B22)<=0,B24<0)),"REQUIERE DATOS",IF(AND(B20="PEDESTAL CIRCULAR",OR(COUNT(B23:B24)<>2,B23<=0,B24<0)),"REQUIERE DATOS",IF(AND(B20="GEOMETRÍA MANUAL",OR(COUNT(B25:B26)<>2,LEN(B27)=0,MIN(B25:B26)<0)),"REQUIERE DATOS",IF(OR(B32<0,B32>B30,NOT(OR(B28="SI",B28="NO"))),"DATOS INVÁLIDOS",IF(AND(B35>0,B28="SI",LEN(B29)=0),"REQUIERE DATOS","OK"))))))
```

**CONTROL_FASE7!B41**

```excel
=IF(B40<>"OK",B40,IF(OR(AND(B20="PEDESTAL RECTANGULAR",OR(B21>inp_cx,B22>inp_cy)),AND(B20="PEDESTAL CIRCULAR",B23>MIN(inp_cx,inp_cy)),B20="GEOMETRÍA MANUAL"),"REQUIERE ANÁLISIS GEOMETRÍA LOCALIZADA","OK"))
```

**RESUMEN!B168**

```excel
=CONTROL_FASE7!B7
```

**RESUMEN!B169**

```excel
=ENVOLVENTES!B146
```

**RESUMEN!B170**

```excel
=CONTROL_FASE7!B16
```

**RESUMEN!B171**

```excel
=ENVOLVENTES!B148
```

**RESUMEN!B172**

```excel
=ENVOLVENTES!B8
```

**RESUMEN!B173**

```excel
=ENVOLVENTES!B48
```

**RESUMEN!B174**

```excel
=IF(COUNTIF(ESPECTROS_U!A8:A67,"SI")+COUNTIF(ESPECTROS_S!A8:A67,"SI")>0,"ESTADÍSTICO ESPECTRAL; no instante físico","VER NATURALEZA POR COMBO")
```

**RESUMEN!B176**

```excel
=ENVOLVENTES!B150
```

**RESUMEN!B177**

```excel
=ENVOLVENTES!B151
```

**RESUMEN!B178**

```excel
=ENVOLVENTES!B152
```

**COMBOS_ULTIMOS!K8**

```excel
=IF(AND(A8="SI",DEMANDAS_E030!Y8<>"OK"),DEMANDAS_E030!Y8,IF(AND(BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(BU8)=0),"REQUIERE DATOS",IF(OR(BP8="MODAL",COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"U",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$F$8:$F$1447,"MODAL")>0),"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"U",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$I$8:$I$1447,"<>OK")>0,"REQUIERE DATOS — INVENTARIO CSI",IF(AND(AND(BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(BU8)>0,zap7_norma_estado="OK"),CS8="OK"),CZ8,IF(A8="NO","NO APLICA",IF(CS8<>"OK",CS8,IF(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA"),CT8,IF(CT8<>"NO APLICA",IF(CT8="OK",CZ8,CT8),CZ8)))))))))
```

**COMBOS_ULTIMOS!L8**

```excel
=IF(K8="OK",IF(AND(AK8="CSI ORIGINAL",W8="FRAME FORCE"),-IF(Z8="J",-1,1)*IF(AJ8="-Z",-1,1)*D8,IF(AND(AK8="CSI ORIGINAL",OR(W8="JOINT REACTION",W8="BASE REACTION")),F8,D8)),"")
```

**COMBOS_ULTIMOS!M8**

```excel
=IF(K8="OK",IF(AND(AK8="CSI ORIGINAL",W8="FRAME FORCE"),IF(Z8="J",-1,1)*(BB8*E8+BC8*F8),IF(AND(AK8="CSI ORIGINAL",OR(W8="JOINT REACTION",W8="BASE REACTION")),-D8,BB8*E8+BC8*F8)),"")
```

**COMBOS_ULTIMOS!N8**

```excel
=IF(K8="OK",IF(AND(AK8="CSI ORIGINAL",W8="FRAME FORCE"),IF(Z8="J",-1,1)*(BD8*E8+BE8*F8),IF(AND(AK8="CSI ORIGINAL",OR(W8="JOINT REACTION",W8="BASE REACTION")),-E8,BD8*E8+BE8*F8)),"")
```

**COMBOS_ULTIMOS!O8**

```excel
=IF(K8="OK",IF(AND(AK8="CSI ORIGINAL",W8="FRAME FORCE"),IF(Z8="J",-1,1)*(-BB8*H8+BC8*I8),IF(AND(AK8="CSI ORIGINAL",OR(W8="JOINT REACTION",W8="BASE REACTION")),-G8,BB8*G8+BC8*H8)),"")
```

**COMBOS_ULTIMOS!P8**

```excel
=IF(K8="OK",IF(AND(AK8="CSI ORIGINAL",W8="FRAME FORCE"),IF(Z8="J",-1,1)*(-BD8*H8+BE8*I8),IF(AND(AK8="CSI ORIGINAL",OR(W8="JOINT REACTION",W8="BASE REACTION")),-H8,BD8*G8+BE8*H8)),"")
```

**COMBOS_ULTIMOS!Q8**

```excel
=IF(K8="OK",IF(AND(AK8="CSI ORIGINAL",W8="FRAME FORCE"),IF(Z8="J",-1,1)*IF(AJ8="-Z",-1,1)*G8,IF(AND(AK8="CSI ORIGINAL",OR(W8="JOINT REACTION",W8="BASE REACTION")),-I8,I8)),"")
```

**COMBOS_ULTIMOS!BB8**

```excel
=IFERROR(IF(AB8="GLOBAL",1,IF(AB8="MATRIZ DE TRANSFORMACIÓN",IF(ISNUMBER(AD8),AD8,""),IF(ISNUMBER(AC8),COS(RADIANS(AC8)),""))),"")
```

**COMBOS_ULTIMOS!BC8**

```excel
=IFERROR(IF(AB8="GLOBAL",0,IF(AB8="MATRIZ DE TRANSFORMACIÓN",IF(ISNUMBER(AE8),AE8,""),IF(ISNUMBER(AC8),-IF(AJ8="-Z",-1,1)*SIN(RADIANS(AC8)),""))),"")
```

**COMBOS_ULTIMOS!BD8**

```excel
=IFERROR(IF(AB8="GLOBAL",0,IF(AB8="MATRIZ DE TRANSFORMACIÓN",IF(ISNUMBER(AF8),AF8,""),IF(ISNUMBER(AC8),SIN(RADIANS(AC8)),""))),"")
```

**COMBOS_ULTIMOS!BE8**

```excel
=IFERROR(IF(AB8="GLOBAL",1,IF(AB8="MATRIZ DE TRANSFORMACIÓN",IF(ISNUMBER(AG8),AG8,""),IF(ISNUMBER(AC8),IF(AJ8="-Z",-1,1)*COS(RADIANS(AC8)),""))),"")
```

**COMBOS_ULTIMOS!BF8**

```excel
=IF(COUNT(BB8:BE8)=4,BB8*BE8-BC8*BD8,"")
```

**COMBOS_ULTIMOS!BG8**

```excel
=IF(COUNT(BB8:BE8)=4,MAX(ABS(BB8^2+BC8^2-1),ABS(BD8^2+BE8^2-1),ABS(BB8*BD8+BC8*BE8)),"")
```

**COMBOS_ULTIMOS!BH8**

```excel
=AQ8&"|"&AR8&"|"&IF(AT8="SI",AS8,"")
```

**COMBOS_ULTIMOS!BI8**

```excel
=IF(A8="NO","NO APLICA",IF(OR(LEN(W8)=0,LEN(X8)=0,LEN(AA8)=0,LEN(AB8)=0,LEN(AH8)=0,LEN(AK8)=0),"REQUIERE DATOS",IF(NOT(OR(W8="FRAME FORCE",W8="JOINT REACTION",W8="BASE REACTION",W8="GLOBAL MANUAL",W8="OTRO")),"DATOS INVÁLIDOS",IF(NOT(OR(AK8="CSI ORIGINAL",AK8="ACCIONES DEL LIBRO")),"DATOS INVÁLIDOS",IF(AND(AK8="CSI ORIGINAL",NOT(OR(W8="FRAME FORCE",OR(W8="JOINT REACTION",W8="BASE REACTION")))),"DATOS INVÁLIDOS",IF(AND(W8="FRAME FORCE",OR(NOT(ISNUMBER(Y8)),LEN(Z8)=0)),"REQUIERE DATOS",IF(AND(W8="FRAME FORCE",OR(Y8<0,NOT(OR(Z8="I",Z8="J")))),"DATOS INVÁLIDOS",IF(AND(AK8="CSI ORIGINAL",W8="FRAME FORCE",OR(AB8="GLOBAL",AI8<>"SI")),"FUERA DEL ALCANCE IMPLEMENTADO",IF(AND(AK8="CSI ORIGINAL",OR(W8="JOINT REACTION",W8="BASE REACTION"),NOT(AB8="GLOBAL")),"FUERA DEL ALCANCE IMPLEMENTADO",IF(AND(NOT(AB8="GLOBAL"),AI8<>"SI"),"FUERA DEL ALCANCE IMPLEMENTADO",IF(NOT(OR(AB8="GLOBAL",AB8="LOCAL ORTOGONAL PRESET",AB8="LOCAL ANGULO",AB8="MATRIZ DE TRANSFORMACIÓN")),"DATOS INVÁLIDOS",IF(AND(NOT(AB8="GLOBAL"),NOT(OR(AJ8="+Z",AJ8="-Z"))),"REQUIERE DATOS",IF(COUNT(BB8:BE8)<>4,"REQUIERE DATOS",IF(AND(AB8="LOCAL ORTOGONAL PRESET",NOT(OR(AC8=0,AC8=90,AC8=180,AC8=270))),"DATOS INVÁLIDOS",IF(OR(BG8>0.00000001,ABS(BF8-IF(AB8="GLOBAL",1,IF(AJ8="-Z",-1,1)))>0.00000001),"DATOS INVÁLIDOS","OK")))))))))))))))
```

**COMBOS_ULTIMOS!BJ8**

```excel
=IF(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA"),"ESTADÍSTICO ESPECTRAL",IF(AND(OR(BP8="LINEAR TIME HISTORY",BP8="NONLINEAR TIME HISTORY"),OR(AM8<>"SI",AT8<>"SI",NOT(ISNUMBER(AS8)),NOT(OR(AR8="Time",AR8="Step")))),"DATOS NO CONCURRENTES — NO USAR COMO COMBO",CY8))
```

**COMBOS_ULTIMOS!BK8**

```excel
=IF(AND(BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(BU8)>0,zap7_norma_estado="OK"),IF(A8="NO","NO APLICA",IF(BI8<>"OK",BI8,IF(OR(COUNT(D8:I8)<>6,LEN(B8)=0,COUNTIFS($A$8:$A$67,"SI",$B$8:$B$67,B8)<>1),"DATOS INVÁLIDOS","OK"))),IF(A8="NO","NO APLICA",IF(A8<>"SI","DATOS INVÁLIDOS",IF(OR(LEN(B8)=0,LEN(C8)=0),"REQUIERE DATOS",IF(COUNTIFS($A$8:$A$67,"SI",$B$8:$B$67,B8)<>1,"DATOS INVÁLIDOS",IF(NOT(OR(C8="MANUAL",C8="OTRO",C8="ETABS",C8="SAP2000")),"DATOS INVÁLIDOS",IF(COUNTBLANK(D8:I8)>0,"REQUIERE DATOS",IF(COUNT(D8:I8)<>6,"DATOS INVÁLIDOS",IF(BI8<>"OK",BI8,IF(BJ8<>"OK",BJ8,IF(CONTROL_MULTICOMBO!$B$31<>"OK",CONTROL_MULTICOMBO!$B$31,"OK")))))))))))
```

**COMBOS_ULTIMOS!BL8**

```excel
=IF(K8="OK",IF(OR(CONTROL_MULTICOMBO!$B$7="SI",CONTROL_MULTICOMBO!$B$9="SI"),CONTROL_FASE7!$B$34*CN8,0),"")
```

**COMBOS_ULTIMOS!BM8**

```excel
=IF(K8="OK",IF(OR(CONTROL_MULTICOMBO!$B$8="SI",CONTROL_MULTICOMBO!$B$10="SI"),CONTROL_FASE7!$B$36*CO8,0),"")
```

**COMBOS_ULTIMOS!BN8**

```excel
=IF(K8="OK",IF(CONTROL_MULTICOMBO!$B$7="SI",BL8,0)+IF(CONTROL_MULTICOMBO!$B$8="SI",BM8,0),"")
```

**COMBOS_ULTIMOS!BO8**

```excel
=IF(COUNTBLANK(R8:S8)>0,"REQUIERE DATOS",IF(OR(COUNT(R8:S8)<>2,MIN(R8:S8)<0,NOT(OR(U8="SI",U8="NO"))),"DATOS INVÁLIDOS","OK"))
```

**COMBOS_ULTIMOS!BR8**

```excel
=IF(OR(BP8="RESPONSE SPECTRUM",COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"U",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$F$8:$F$1447,"RESPONSE SPECTRUM")>0),"SI","NO")
```

**COMBOS_ULTIMOS!CM8**

```excel
=CN8
```

**COMBOS_ULTIMOS!CN8**

```excel
=R8
```

**COMBOS_ULTIMOS!CO8**

```excel
=S8
```

**COMBOS_ULTIMOS!CQ8**

```excel
=IF(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA"),"ESTADÍSTICO ESPECTRAL",IF(OR(BP8="LINEAR TIME HISTORY",BP8="NONLINEAR TIME HISTORY"),"STEP DE HISTORIA",IF(AN8="SI","CORRESPONDENCE DE COMBO",IF(W8="GLOBAL MANUAL","MANUAL DOCUMENTADO","CONCURRENTE"))))
```

**COMBOS_ULTIMOS!CR8**

```excel
=IF(COUNT(BW8:BX8)=2,BX8-BW8,"")
```

**COMBOS_ULTIMOS!CS8**

```excel
=IF(AND(OR(W8="JOINT REACTION",W8="BASE REACTION"),OR(CONTROL_MULTICOMBO!$B$7="SI",CONTROL_MULTICOMBO!$B$8="SI",AND(CONTROL_FASE7!$B$35>0,CONTROL_FASE7!$B$28="SI")),OR(CE8<>"SI",CF8<>"SI",NOT(ISNUMBER(CG8)),CG8>=BX8,LEN(CH8)=0,LEN(CC8)=0)),"REQUIERE DATOS — PESOS SOBRE APOYO",IF(AND(W8="BASE REACTION",NOT(OR(CI8="ÚNICO APOYO",CI8="GRUPO EXCLUSIVO ZAPATA"))),"FUERA DEL ALCANCE / RESULTADO NO LOCALIZABLE",IF(AND(W8="BASE REACTION",LEN(CJ8)=0),"REQUIERE DATOS",IF(AND(W8="FRAME FORCE",OR(LEN(BV8)=0,COUNT(BW8:BX8)<>2,NOT(OR(BY8="SI",BY8="NO")))),"REQUIERE DATOS",IF(AND(BV8="INTERFAZ COLUMNA-ZAPATA",ISNUMBER(CR8),ABS(CR8)>0.00000001),"DATOS INVÁLIDOS",IF(AND(W8="FRAME FORCE",BY8="SI",OR(NOT(ISNUMBER(BZ8)),BZ8<0,LEN(CA8)=0)),"REQUIERE DATOS",IF(AND(W8="FRAME FORCE",OR(CONTROL_MULTICOMBO!$B$7="SI",CONTROL_MULTICOMBO!$B$8="SI"),NOT(AND(CB8="ESPECIAL DOCUMENTADO",LEN(CC8)>0,LEN(CD8)>0))),"DATOS INVÁLIDOS — PESOS FUERA DEL CORTE FRAME",IF(AND(W8="JOINT REACTION",OR(CONTROL_MULTICOMBO!$B$7="SI",CONTROL_MULTICOMBO!$B$8="SI"),NOT(AND(CE8="SI",CF8="SI",ISNUMBER(CG8),LEN(CH8)>0,LEN(CC8)>0))),"REQUIERE DATOS — PESOS SOBRE APOYO",IF(AND(CONTROL_FASE7!$B$35>0,CONTROL_FASE7!$B$28="SI",W8="FRAME FORCE",NOT(AND(CB8="ESPECIAL DOCUMENTADO",LEN(CC8)>0,LEN(CD8)>0))),"REQUIERE DATOS — PEDESTAL FUERA DEL CORTE",IF(OR(COUNT(CM8:CO8)<>3,MIN(CM8:CO8)<0),"DATOS INVÁLIDOS",IF(AND(MAX(CM8:CO8)-MIN(CM8:CO8)>0.00000001,LEN(CP8)=0),"REQUIERE JUSTIFICACIÓN FACTORES DE PESOS",IF(CONTROL_FASE7!$B$40<>"OK",CONTROL_FASE7!$B$40,"OK"))))))))))))
```

**COMBOS_ULTIMOS!CT8**

```excel
=IF(AND(A8="SI",DEMANDAS_E030!Y8<>"OK"),DEMANDAS_E030!Y8,IF(AND(BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(BU8)>0,zap7_norma_estado="OK"),"OK",IF(AND(NOT(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA")),BT8="NO"),"NO APLICA",IF(CONTROL_FASE7!$B$10<>"OK",CONTROL_FASE7!$B$10,IF(OR(LEN(BP8)=0,LEN(BQ8)=0,NOT(OR(BR8="SI",BR8="NO"))),"REQUIERE DATOS",IF(AND(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA"),BS8<>"B. ESPECTRO DE RESPUESTA"),"REQUIERE TRATAMIENTO ESPECTRAL",IF(AND(BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(BU8)=0),"REQUIERE DATOS",IF(AND(NOT(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA")),CY8<>"OK"),CY8,IF(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA"),"ESPECTRAL — USAR ESTADOS DERIVADOS","OK")))))))))
```

**COMBOS_ULTIMOS!CU8**

```excel
=IF(A8="NO","NO APLICA",IF(ISNUMBER(Q8),IF(ABS(Q8)>CONTROL_FASE7!$B$44,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA","OK"),"REQUIERE DATOS"))
```

**COMBOS_ULTIMOS!CV8**

```excel
=IF(AND(CS8="OK",CONTROL_FASE7!$B$28="NO"),CONTROL_FASE7!$B$35*CM8,0)
```

**COMBOS_ULTIMOS!CW8**

```excel
=IF(AND(CS8="OK",OR(CONTROL_MULTICOMBO!$B$8="SI",CONTROL_MULTICOMBO!$B$10="SI")),CONTROL_FASE7!$B$37*CO8,0)
```

**COMBOS_ULTIMOS!CX8**

```excel
=IF(AND(CS8="OK",OR(CONTROL_MULTICOMBO!$B$8="SI",CONTROL_MULTICOMBO!$B$10="SI")),CONTROL_FASE7!$B$38*CO8,0)
```

**COMBOS_ULTIMOS!CY8**

```excel
=IF(A8="NO","NO APLICA",IF(AND(OR(AR8="Time",AR8="Step",AR8="Mode",AR8="Frequency"),AT8<>"SI"),"REQUIERE DATOS",IF(OR(LEN(AL8)=0,LEN(BA8)=0),"REQUIERE DATOS",IF(NOT(OR(AL8="LINEAR ADD",AL8="SINGLE CASE / SINGLE STEP",AL8="ENVELOPE",AL8="ABSOLUTE ADD",AL8="SRSS",AL8="RANGE ADD",AL8="MULTISTEP",AL8="OTRO")),"DATOS INVÁLIDOS",IF(AND(NOT(OR(AL8="LINEAR ADD",AL8="SINGLE CASE / SINGLE STEP")),AN8<>"SI"),"DATOS NO CONCURRENTES — NO USAR COMO COMBO",IF(AND(OR(AL8="LINEAR ADD",AL8="SINGLE CASE / SINGLE STEP"),AM8<>"SI"),"DATOS NO CONCURRENTES — NO USAR COMO COMBO",IF(OR(BA8<>"SI",LEN(AQ8)=0,LEN(AR8)=0,NOT(OR(AT8="SI",AT8="NO")),AND(AT8="SI",NOT(ISNUMBER(AS8)))),"REQUIERE DATOS",IF(AND(NOT(OR(AL8="LINEAR ADD",AL8="SINGLE CASE / SINGLE STEP")),OR(LEN(AO8)=0,NOT(OR(AP8="Max",AP8="Min")))),"REQUIERE DATOS",IF(COUNTBLANK(AU8:AZ8)>0,"REQUIERE DATOS",IF(NOT(AND(EXACT(AU8,BH8),EXACT(AV8,BH8),EXACT(AW8,BH8),EXACT(AX8,BH8),EXACT(AY8,BH8),EXACT(AZ8,BH8))),"DATOS NO CONCURRENTES — NO USAR COMO COMBO","OK"))))))))))
```

**COMBOS_ULTIMOS!CZ8**

```excel
=IF(BK8<>"OK",BK8,IF(BO8<>"OK",BO8,"OK"))
```

**COMBOS_SERVICIO!K8**

```excel
=IF(AE8="SI",IF(ISNUMBER(AF8),AF8,""),CONTROL_MULTICOMBO!$B$14)
```

**COMBOS_SERVICIO!O8**

```excel
=IF(AND(A8="SI",DEMANDAS_E030!Y68<>"OK"),DEMANDAS_E030!Y68,IF(AND(CL8="D. RESULTADO EXTERNO YA COMBINADO",LEN(CN8)=0),"REQUIERE DATOS",IF(OR(CI8="MODAL",COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"S",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$F$8:$F$1447,"MODAL")>0),"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"S",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$I$8:$I$1447,"<>OK")>0,"REQUIERE DATOS — INVENTARIO CSI",IF(AND(AND(CL8="D. RESULTADO EXTERNO YA COMBINADO",LEN(CN8)>0,zap7_norma_estado="OK"),DL8="OK"),DS8,IF(A8="NO","NO APLICA",IF(DL8<>"OK",DL8,IF(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA"),DM8,IF(DM8<>"NO APLICA",IF(DM8="OK",DS8,DM8),DS8)))))))))
```

**COMBOS_SERVICIO!Q8**

```excel
=IF(O8="OK",IF(AND(AX8="CSI ORIGINAL",AJ8="FRAME FORCE"),-IF(AM8="J",-1,1)*IF(AW8="-Z",-1,1)*E8,IF(AND(AX8="CSI ORIGINAL",OR(AJ8="JOINT REACTION",AJ8="BASE REACTION")),G8,E8)),"")
```

**COMBOS_SERVICIO!CK8**

```excel
=IF(OR(CI8="RESPONSE SPECTRUM",COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"S",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$F$8:$F$1447,"RESPONSE SPECTRUM")>0),"SI","NO")
```

**COMBOS_SERVICIO!CM8**

```excel
=IF(C8="SISMO","SI","NO")
```

**COMBOS_SERVICIO!DF8**

```excel
=DG8
```

**COMBOS_SERVICIO!DG8**

```excel
=1
```

**COMBOS_SERVICIO!DH8**

```excel
=1
```

**COMBOS_SERVICIO!DJ8**

```excel
=IF(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA"),"ESTADÍSTICO ESPECTRAL",IF(OR(CI8="LINEAR TIME HISTORY",CI8="NONLINEAR TIME HISTORY"),"STEP DE HISTORIA",IF(BA8="SI","CORRESPONDENCE DE COMBO",IF(AJ8="GLOBAL MANUAL","MANUAL DOCUMENTADO","CONCURRENTE"))))
```

**COMBOS_SERVICIO!DK8**

```excel
=IF(COUNT(CP8:CQ8)=2,CQ8-CP8,"")
```

**COMBOS_SERVICIO!DL8**

```excel
=IF(AND(OR(AJ8="JOINT REACTION",AJ8="BASE REACTION"),OR(CONTROL_MULTICOMBO!$B$7="SI",CONTROL_MULTICOMBO!$B$8="SI",AND(CONTROL_FASE7!$B$35>0,CONTROL_FASE7!$B$28="SI")),OR(CX8<>"SI",CY8<>"SI",NOT(ISNUMBER(CZ8)),CZ8>=CQ8,LEN(DA8)=0,LEN(CV8)=0)),"REQUIERE DATOS — PESOS SOBRE APOYO",IF(AND(AJ8="BASE REACTION",NOT(OR(DB8="ÚNICO APOYO",DB8="GRUPO EXCLUSIVO ZAPATA"))),"FUERA DEL ALCANCE / RESULTADO NO LOCALIZABLE",IF(AND(AJ8="BASE REACTION",LEN(DC8)=0),"REQUIERE DATOS",IF(AND(AJ8="FRAME FORCE",OR(LEN(CO8)=0,COUNT(CP8:CQ8)<>2,NOT(OR(CR8="SI",CR8="NO")))),"REQUIERE DATOS",IF(AND(CO8="INTERFAZ COLUMNA-ZAPATA",ISNUMBER(DK8),ABS(DK8)>0.00000001),"DATOS INVÁLIDOS",IF(AND(AJ8="FRAME FORCE",CR8="SI",OR(NOT(ISNUMBER(CS8)),CS8<0,LEN(CT8)=0)),"REQUIERE DATOS",IF(AND(AJ8="FRAME FORCE",OR(CONTROL_MULTICOMBO!$B$7="SI",CONTROL_MULTICOMBO!$B$8="SI"),NOT(AND(CU8="ESPECIAL DOCUMENTADO",LEN(CV8)>0,LEN(CW8)>0))),"DATOS INVÁLIDOS — PESOS FUERA DEL CORTE FRAME",IF(AND(AJ8="JOINT REACTION",OR(CONTROL_MULTICOMBO!$B$7="SI",CONTROL_MULTICOMBO!$B$8="SI"),NOT(AND(CX8="SI",CY8="SI",ISNUMBER(CZ8),LEN(DA8)>0,LEN(CV8)>0))),"REQUIERE DATOS — PESOS SOBRE APOYO",IF(AND(CONTROL_FASE7!$B$35>0,CONTROL_FASE7!$B$28="SI",AJ8="FRAME FORCE",NOT(AND(CU8="ESPECIAL DOCUMENTADO",LEN(CV8)>0,LEN(CW8)>0))),"REQUIERE DATOS — PEDESTAL FUERA DEL CORTE",IF(OR(COUNT(DF8:DH8)<>3,MIN(DF8:DH8)<0),"DATOS INVÁLIDOS",IF(AND(MAX(DF8:DH8)-MIN(DF8:DH8)>0.00000001,LEN(DI8)=0),"REQUIERE JUSTIFICACIÓN FACTORES DE PESOS",IF(CONTROL_FASE7!$B$40<>"OK",CONTROL_FASE7!$B$40,"OK"))))))))))))
```

**COMBOS_SERVICIO!DM8**

```excel
=IF(AND(A8="SI",DEMANDAS_E030!Y68<>"OK"),DEMANDAS_E030!Y68,IF(AND(CL8="D. RESULTADO EXTERNO YA COMBINADO",LEN(CN8)>0,zap7_norma_estado="OK"),"OK",IF(AND(NOT(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA")),CM8="NO"),"NO APLICA",IF(CONTROL_FASE7!$B$10<>"OK",CONTROL_FASE7!$B$10,IF(OR(LEN(CI8)=0,LEN(CJ8)=0,NOT(OR(CK8="SI",CK8="NO"))),"REQUIERE DATOS",IF(AND(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA"),CL8<>"B. ESPECTRO DE RESPUESTA"),"REQUIERE TRATAMIENTO ESPECTRAL",IF(AND(CL8="D. RESULTADO EXTERNO YA COMBINADO",LEN(CN8)=0),"REQUIERE DATOS",IF(AND(NOT(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA")),DR8<>"OK"),DR8,IF(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA"),"ESPECTRAL — USAR ESTADOS DERIVADOS","OK")))))))))
```

**COMBOS_SERVICIO!DN8**

```excel
=IF(A8="NO","NO APLICA",IF(ISNUMBER(V8),IF(ABS(V8)>CONTROL_FASE7!$B$44,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA","OK"),"REQUIERE DATOS"))
```

**COMBOS_SERVICIO!DO8**

```excel
=IF(AND(DL8="OK",CONTROL_FASE7!$B$28="NO"),CONTROL_FASE7!$B$35*DF8,0)
```

**COMBOS_SERVICIO!DP8**

```excel
=IF(AND(DL8="OK",OR(CONTROL_MULTICOMBO!$B$8="SI",CONTROL_MULTICOMBO!$B$10="SI")),CONTROL_FASE7!$B$37*DH8,0)
```

**COMBOS_SERVICIO!DQ8**

```excel
=IF(AND(DL8="OK",OR(CONTROL_MULTICOMBO!$B$8="SI",CONTROL_MULTICOMBO!$B$10="SI")),CONTROL_FASE7!$B$38*DH8,0)
```

**COMBOS_SERVICIO!DR8**

```excel
=IF(A8="NO","NO APLICA",IF(AND(OR(BE8="Time",BE8="Step",BE8="Mode",BE8="Frequency"),BG8<>"SI"),"REQUIERE DATOS",IF(OR(LEN(AY8)=0,LEN(BN8)=0),"REQUIERE DATOS",IF(NOT(OR(AY8="LINEAR ADD",AY8="SINGLE CASE / SINGLE STEP",AY8="ENVELOPE",AY8="ABSOLUTE ADD",AY8="SRSS",AY8="RANGE ADD",AY8="MULTISTEP",AY8="OTRO")),"DATOS INVÁLIDOS",IF(AND(NOT(OR(AY8="LINEAR ADD",AY8="SINGLE CASE / SINGLE STEP")),BA8<>"SI"),"DATOS NO CONCURRENTES — NO USAR COMO COMBO",IF(AND(OR(AY8="LINEAR ADD",AY8="SINGLE CASE / SINGLE STEP"),AZ8<>"SI"),"DATOS NO CONCURRENTES — NO USAR COMO COMBO",IF(OR(BN8<>"SI",LEN(BD8)=0,LEN(BE8)=0,NOT(OR(BG8="SI",BG8="NO")),AND(BG8="SI",NOT(ISNUMBER(BF8)))),"REQUIERE DATOS",IF(AND(NOT(OR(AY8="LINEAR ADD",AY8="SINGLE CASE / SINGLE STEP")),OR(LEN(BB8)=0,NOT(OR(BC8="Max",BC8="Min")))),"REQUIERE DATOS",IF(COUNTBLANK(BH8:BM8)>0,"REQUIERE DATOS",IF(NOT(AND(EXACT(BH8,BU8),EXACT(BI8,BU8),EXACT(BJ8,BU8),EXACT(BK8,BU8),EXACT(BL8,BU8),EXACT(BM8,BU8))),"DATOS NO CONCURRENTES — NO USAR COMO COMBO","OK"))))))))))
```

**COMBOS_SERVICIO!DS8**

```excel
=IF(AD8<>"OK",AD8,IF(OR(LEN(C8)=0,LEN(L8)=0,LEN(M8)=0),"REQUIERE DATOS",IF(OR(NOT(OR(C8="GRAVEDAD",C8="SISMO",C8="VIENTO",C8="OTRO")),COUNT(K8:L8)<>2,K8<=0,NOT(OR(L8=1,L8=0.8)),NOT(OR(M8="SI",M8="NO")),AND(L8=0.8,C8<>"SISMO"),AND(M8="SI",NOT(OR(C8="SISMO",C8="VIENTO"))),NOT(OR(AE8="SI",AE8="NO")),NOT(OR(AI8="SI",AI8="NO")),AND(AI8="SI",L8<>1)),"DATOS INVÁLIDOS",IF(AND(AE8="SI",OR(LEN(AG8)=0,LEN(AH8)=0)),"REQUIERE DATOS",IF(AND(OR(L8=0.8,M8="SI"),LEN(AC8)=0),"REQUIERE DATOS",IF(AND(L8=0.8,COUNTBLANK(W8:AB8)>0),"REQUIERE DATOS",IF(AND(L8=0.8,COUNT(W8:AB8)<>6),"DATOS INVÁLIDOS","OK")))))))
```

**RESULTADOS_ULTIMOS!Y8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(LEN(MU_PUNZ!B17)=0,"",MU_PUNZ!B17))
```

**RESULTADOS_ULTIMOS!AO8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(LEN(MU_PUNZ!B20)=0,"",MU_PUNZ!B20))
```

**RESULTADOS_ULTIMOS!AT8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(LEN(MU_CORT!F8)=0,"",MU_CORT!F8))
```

**RESULTADOS_ULTIMOS!AZ8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(LEN(MU_CORT!F9)=0,"",MU_CORT!F9))
```

**RESULTADOS_ULTIMOS!BF8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(LEN(MU_CORT!F10)=0,"",MU_CORT!F10))
```

**RESULTADOS_ULTIMOS!BL8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(LEN(MU_CORT!F11)=0,"",MU_CORT!F11))
```

**RESULTADOS_ULTIMOS!BW8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(COUNT(BU8,BV8)=2,MAX(BU8,BV8),""))
```

**RESULTADOS_ULTIMOS!CF8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(COUNT(CD8,CE8)=2,MAX(CD8,CE8),""))
```

**RESULTADOS_ULTIMOS!CP8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(COUNT(CN8,CO8)=2,MAX(CN8,CO8),""))
```

**RESULTADOS_ULTIMOS!CY8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(COUNT(CW8,CX8)=2,MAX(CW8,CX8),""))
```

**RESULTADOS_ULTIMOS!DI8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(COUNT(DG8,DH8)=2,MAX(DG8,DH8),""))
```

**RESULTADOS_ULTIMOS!DR8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(COUNT(DP8,DQ8)=2,MAX(DP8,DQ8),""))
```

**RESULTADOS_ULTIMOS!EB8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(COUNT(DZ8,EA8)=2,MAX(DZ8,EA8),""))
```

**RESULTADOS_ULTIMOS!EK8**

```excel
=IF(COMBOS_ULTIMOS!A8="NO","",IF(COUNT(EI8,EJ8)=2,MAX(EI8,EJ8),""))
```

**ENV_BARRAS!AC8**

```excel
=IF((COUNTIF(MOTOR_ESPECTRAL_U!XB8:XB967,"NO CUMPLE")+COUNTIF(MOTOR_EV_U!XB8:XB967,"NO CUMPLE"))>0,"NO CUMPLE",IF((COUNTIF(MOTOR_ESPECTRAL_U!XB8:XB967,"DATOS INVÁLIDOS")+COUNTIF(MOTOR_EV_U!XB8:XB967,"DATOS INVÁLIDOS"))>0,"DATOS INVÁLIDOS",IF((COUNTIF(MOTOR_ESPECTRAL_U!XB8:XB967,"REQUIERE DATOS")+COUNTIF(MOTOR_EV_U!XB8:XB967,"REQUIERE DATOS"))>0,"REQUIERE DATOS",IF((COUNTIF(MOTOR_ESPECTRAL_U!XB8:XB967,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(MOTOR_EV_U!XB8:XB967,"FUERA DEL ALCANCE IMPLEMENTADO"))>0,"FUERA DEL ALCANCE IMPLEMENTADO","CUMPLE"))))
```

**ENV_BARRAS!AD8**

```excel
=IF((COUNTIF(MOTOR_ESPECTRAL_U!UT8:UT967,"NO CUMPLE")+COUNTIF(MOTOR_EV_U!UT8:UT967,"NO CUMPLE"))>0,"NO CUMPLE",IF((COUNTIF(MOTOR_ESPECTRAL_U!UT8:UT967,"DATOS INVÁLIDOS")+COUNTIF(MOTOR_EV_U!UT8:UT967,"DATOS INVÁLIDOS"))>0,"DATOS INVÁLIDOS",IF((COUNTIF(MOTOR_ESPECTRAL_U!UT8:UT967,"REQUIERE DATOS")+COUNTIF(MOTOR_EV_U!UT8:UT967,"REQUIERE DATOS"))>0,"REQUIERE DATOS",IF((COUNTIF(MOTOR_ESPECTRAL_U!UT8:UT967,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(MOTOR_EV_U!UT8:UT967,"FUERA DEL ALCANCE IMPLEMENTADO"))>0,"FUERA DEL ALCANCE IMPLEMENTADO","CUMPLE"))))
```

**ENV_BARRAS!AE8**

```excel
=IF(COUNTIF(MOTOR_ESPECTRAL_U!EP8:EP967,AF8)+COUNTIF(MOTOR_ESPECTRAL_U!EP8:EP967,-AF8)>0,IF(AF8>0,IFERROR(INDEX(MOTOR_ESPECTRAL_U!ARZ8:ARZ967,MATCH(AF8,MOTOR_ESPECTRAL_U!EP8:EP967,0)),INDEX(MOTOR_ESPECTRAL_U!ARZ8:ARZ967,MATCH(-AF8,MOTOR_ESPECTRAL_U!EP8:EP967,0))),""),IF(AF8>0,IFERROR(INDEX(MOTOR_EV_U!ARZ8:ARZ967,MATCH(AF8,MOTOR_EV_U!EP8:EP967,0)),INDEX(MOTOR_EV_U!ARZ8:ARZ967,MATCH(-AF8,MOTOR_EV_U!EP8:EP967,0))),""))
```

**ENV_BARRAS!AF8**

```excel
=MAX(MAX(MOTOR_ESPECTRAL_U!EP8:EP967,MOTOR_EV_U!EP8:EP967),-MIN(MOTOR_ESPECTRAL_U!EP8:EP967,MOTOR_EV_U!EP8:EP967))
```

**MU_CARGAS!E27**

```excel
=IF(COMBOS_ULTIMOS!K8="OK",MU_CARGAS!C27-COMBOS_ULTIMOS!BN8+COMBOS_ULTIMOS!CV8,"")
```

**MU_CARGAS!E28**

```excel
=IF(COMBOS_ULTIMOS!K8="OK",MU_CARGAS!C28-MU_CARGAS!E26*COMBOS_ULTIMOS!CR8-COMBOS_ULTIMOS!BN8*inp_yc,"")
```

**MU_CARGAS!E29**

```excel
=IF(COMBOS_ULTIMOS!K8="OK",MU_CARGAS!C29+MU_CARGAS!E25*COMBOS_ULTIMOS!CR8+COMBOS_ULTIMOS!BN8*inp_xc,"")
```

**MU_CARGAS!E30**

```excel
=IF(COUNT(MU_CARGAS!C25:C30)=6,MU_CARGAS!C30,"")
```

**MU_CONEXION!B29**

```excel
=IF(COMBOS_ULTIMOS!K8="OK",COMBOS_ULTIMOS!L8-COMBOS_ULTIMOS!BN8-IF(CONTROL_FASE7!$B$28="SI",CONTROL_FASE7!$B$35*COMBOS_ULTIMOS!CM8,0),"")
```

**MU_CONEXION!B40**

```excel
=IF(COMBOS_ULTIMOS!CU8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",COMBOS_ULTIMOS!CU8,IF(CONEXION_COMBOS!M8<>"OK",CONEXION_COMBOS!M8,IF(CONEXION_COLUMNA_ZAPATA!B30<>"OK",CONEXION_COLUMNA_ZAPATA!B30,IF(MU_PRESION!B28<>"OK",MU_PRESION!B28,IF(CONEXION_COLUMNA_ZAPATA!B7<>"EXTERNO","FUERA DEL ALCANCE IMPLEMENTADO",IF(ABS(MU_CARGAS!E30)>0.000001,"REQUIERE ANÁLISIS ESPECIAL",IF(OR(NOT(ISTEXT(MU_CONEXION!B11)),LEN(MU_CONEXION!B11)=0,NOT(ISTEXT(MU_CONEXION!B12)),LEN(MU_CONEXION!B12)=0,NOT(ISTEXT(CONEXION_COLUMNA_ZAPATA!B18)),LEN(CONEXION_COLUMNA_ZAPATA!B18)=0,NOT(ISTEXT(CONEXION_COLUMNA_ZAPATA!B22)),LEN(CONEXION_COLUMNA_ZAPATA!B22)=0,LEN(CONEXION_COLUMNA_ZAPATA!B10)=0),"REQUIERE DATOS",IF(OR(MU_CONEXION!B12<>MU_DATOS!C70,CONEXION_COLUMNA_ZAPATA!B10<>"ACCIONES AMPLIFICADAS"),"DATOS INVÁLIDOS",IF(COUNT(MU_CONEXION!B14,MU_CONEXION!B15,MU_CONEXION!B16,MU_CONEXION!B17,MU_CONEXION!B18,MU_CONEXION!B19,MU_CONEXION!B20)<>7,"REQUIERE DATOS",IF(OR(MU_CONEXION!B14<0,MU_CONEXION!B16<0,MU_CONEXION!B19<0,MU_CONEXION!B19>CONEXION_COLUMNA_ZAPATA!B29,MU_CONEXION!B20<0,ABS(MU_CONEXION!B17)>INGRESO_DATOS!C42*50,ABS(MU_CONEXION!B18)>INGRESO_DATOS!C43*50,MU_CONEXION!B15<=0,MU_CONEXION!B15>1),"DATOS INVÁLIDOS",IF(CONEXION_COMBOS!M8<>"OK",CONEXION_COMBOS!M8,IF(MU_CONEXION!B16=0,IF(AND(MU_CONEXION!B19=0,MU_CONEXION!B20=0,MU_CONEXION!B17=0,MU_CONEXION!B18=0),"OK","DATOS INVÁLIDOS"),IF(MU_CONEXION!B19<=0,"DATOS INVÁLIDOS",IF(MU_CONEXION!B20+0.00000001>=MU_CONEXION!B16*1000/MU_CONEXION!B19,"OK","DATOS INVÁLIDOS"))))))))))))))
```

**MU_CONEXION!B82**

```excel
=IF(COMBOS_ULTIMOS!CU8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",COMBOS_ULTIMOS!CU8,IF(MU_PRESION!B28<>"OK",MU_PRESION!B28,IF(MU_CONEXION!B76<=0.000000001,"NO APLICA",IF(CONEXION_COLUMNA_ZAPATA!B30<>"OK",CONEXION_COLUMNA_ZAPATA!B30,IF(OR(NOT(ISNUMBER(CONEXION_COLUMNA_ZAPATA!B74)),COUNT(INGRESO_DATOS!C121)<>1,LEN(INGRESO_DATOS!C122)=0,LEN(INGRESO_DATOS!C123)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!C121<0,"DATOS INVÁLIDOS",IF(AND(INGRESO_DATOS!C121>=MU_CONEXION!B78,MU_CONEXION!B76<=CONEXION_COLUMNA_ZAPATA!B77,INGRESO_DATOS!C122="SI"),"CUMPLE","NO CUMPLE")))))))
```

**MU_CONEXION!B98**

```excel
=IF(COMBOS_ULTIMOS!CU8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",COMBOS_ULTIMOS!CU8,IF(COUNTIF(MU_CONEXION!B86:B96,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(MU_CONEXION!B86:B96,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(MU_CONEXION!B86:B96,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(MU_CONEXION!B86:B96,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(MU_CONEXION!B86:B96,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE"))))))
```

**MU_CORT!C8**

```excel
=IF(MU_PRESION!D20="OK",MAX(0,MU_CORT!B8-MU_CORT!J8/100),"")
```

**MU_CORT!D8**

```excel
=IF(MU_PRESION!D20="OK",MU_PRESION!D23+MU_PRESION!D24*(-INGRESO_DATOS!C30/2+MU_CORT!C8/2)+MU_PRESION!D26,"")
```

**MU_CORT!E8**

```excel
=IF(MU_PRESION!D20="OK",MU_PRESION!D23+MU_PRESION!D24*(-INGRESO_DATOS!C30/2+MU_CORT!C8/2),"")
```

**MU_CORT!F8**

```excel
=IF(MU_PRESION!D20="OK",ABS(MU_CORT!E8*MU_CORT!C8),"")
```

**MU_CORT!G8**

```excel
=IF(MU_PRESION!D20="OK",INGRESO_DATOS!C23*0.17*PUNZONAMIENTO!B22*SQRT(INGRESO_DATOS!C14)*100*MU_CORT!J8/1000,"")
```

**MU_CORT!H8**

```excel
=IF(MU_PRESION!D20="OK",MU_CORT!F8/MU_CORT!G8,"")
```

**MU_CORT!C9**

```excel
=IF(MU_PRESION!D20="OK",MAX(0,MU_CORT!B9-MU_CORT!J9/100),"")
```

**MU_CORT!D9**

```excel
=IF(MU_PRESION!D20="OK",MU_PRESION!D23+MU_PRESION!D24*(INGRESO_DATOS!C30/2-MU_CORT!C9/2)+MU_PRESION!D26,"")
```

**MU_CORT!E9**

```excel
=IF(MU_PRESION!D20="OK",MU_PRESION!D23+MU_PRESION!D24*(INGRESO_DATOS!C30/2-MU_CORT!C9/2),"")
```

**MU_CORT!F9**

```excel
=IF(MU_PRESION!D20="OK",ABS(MU_CORT!E9*MU_CORT!C9),"")
```

**MU_CORT!G9**

```excel
=IF(MU_PRESION!D20="OK",INGRESO_DATOS!C23*0.17*PUNZONAMIENTO!B22*SQRT(INGRESO_DATOS!C14)*100*MU_CORT!J9/1000,"")
```

**MU_CORT!H9**

```excel
=IF(MU_PRESION!D20="OK",MU_CORT!F9/MU_CORT!G9,"")
```

**MU_CORT!C10**

```excel
=IF(MU_PRESION!D20="OK",MAX(0,MU_CORT!B10-MU_CORT!J10/100),"")
```

**MU_CORT!D10**

```excel
=IF(MU_PRESION!D20="OK",MU_PRESION!D23+MU_PRESION!D25*(-INGRESO_DATOS!C31/2+MU_CORT!C10/2)+MU_PRESION!D26,"")
```

**MU_CORT!E10**

```excel
=IF(MU_PRESION!D20="OK",MU_PRESION!D23+MU_PRESION!D25*(-INGRESO_DATOS!C31/2+MU_CORT!C10/2),"")
```

**MU_CORT!F10**

```excel
=IF(MU_PRESION!D20="OK",ABS(MU_CORT!E10*MU_CORT!C10),"")
```

**MU_CORT!G10**

```excel
=IF(MU_PRESION!D20="OK",INGRESO_DATOS!C23*0.17*PUNZONAMIENTO!B22*SQRT(INGRESO_DATOS!C14)*100*MU_CORT!J10/1000,"")
```

**MU_CORT!H10**

```excel
=IF(MU_PRESION!D20="OK",MU_CORT!F10/MU_CORT!G10,"")
```

**MU_CORT!C11**

```excel
=IF(MU_PRESION!D20="OK",MAX(0,MU_CORT!B11-MU_CORT!J11/100),"")
```

**MU_CORT!D11**

```excel
=IF(MU_PRESION!D20="OK",MU_PRESION!D23+MU_PRESION!D25*(INGRESO_DATOS!C31/2-MU_CORT!C11/2)+MU_PRESION!D26,"")
```

**MU_CORT!E11**

```excel
=IF(MU_PRESION!D20="OK",MU_PRESION!D23+MU_PRESION!D25*(INGRESO_DATOS!C31/2-MU_CORT!C11/2),"")
```

**MU_CORT!F11**

```excel
=IF(MU_PRESION!D20="OK",ABS(MU_CORT!E11*MU_CORT!C11),"")
```

**MU_CORT!G11**

```excel
=IF(MU_PRESION!D20="OK",INGRESO_DATOS!C23*0.17*PUNZONAMIENTO!B22*SQRT(INGRESO_DATOS!C14)*100*MU_CORT!J11/1000,"")
```

**MU_CORT!H11**

```excel
=IF(MU_PRESION!D20="OK",MU_CORT!F11/MU_CORT!G11,"")
```

**MU_FLEX!D8**

```excel
=IF(MU_PRESION!D20="OK",MAX(0,MU_DIAG_X!B10,MU_DIAG_X!B11)/INGRESO_DATOS!C31,"")
```

**MU_FLEX!E8**

```excel
=IF(MU_PRESION!D20="OK",PUNZONAMIENTO!B8,"")
```

**MU_FLEX!F8**

```excel
=IF(MU_PRESION!D20="OK",IF(MU_FLEX!D8<=0,0,IF((INGRESO_DATOS!C15*MU_FLEX!E8)^2-4*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))*(MU_FLEX!D8*100000/INGRESO_DATOS!C22)<0,"",(INGRESO_DATOS!C15*MU_FLEX!E8-SQRT((INGRESO_DATOS!C15*MU_FLEX!E8)^2-4*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))*(MU_FLEX!D8*100000/INGRESO_DATOS!C22)))/(2*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))))),"")
```

**MU_FLEX!G8**

```excel
=IF(AND(MU_PRESION!D20="OK",FLEXION_ACERO!B34="OK",ISNUMBER(FLEXION_ACERO!B23)),MAX(FLEXION_ACERO!B35,IF(AND(INGRESO_DATOS!C165="DOS CARAS",MU_FLEX!D8>0.000001),0.0012,0))*100*INGRESO_DATOS!C32*100,"")
```

**MU_FLEX!H8**

```excel
=IF(MU_PRESION!D20="OK",IF(COUNT(MU_FLEX!F8,MU_FLEX!G8)=2,MAX(MU_FLEX!F8,MU_FLEX!G8),""),"")
```

**MU_FLEX!D9**

```excel
=IF(MU_PRESION!D20="OK",MAX(0,MU_DIAG_Y!B10,MU_DIAG_Y!B11)/INGRESO_DATOS!C30,"")
```

**MU_FLEX!E9**

```excel
=IF(MU_PRESION!D20="OK",PUNZONAMIENTO!B9,"")
```

**MU_FLEX!F9**

```excel
=IF(MU_PRESION!D20="OK",IF(MU_FLEX!D9<=0,0,IF((INGRESO_DATOS!C15*MU_FLEX!E9)^2-4*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))*(MU_FLEX!D9*100000/INGRESO_DATOS!C22)<0,"",(INGRESO_DATOS!C15*MU_FLEX!E9-SQRT((INGRESO_DATOS!C15*MU_FLEX!E9)^2-4*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))*(MU_FLEX!D9*100000/INGRESO_DATOS!C22)))/(2*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))))),"")
```

**MU_FLEX!G9**

```excel
=IF(AND(MU_PRESION!D20="OK",FLEXION_ACERO!B34="OK",ISNUMBER(FLEXION_ACERO!B23)),MAX(FLEXION_ACERO!B35,IF(AND(INGRESO_DATOS!C165="DOS CARAS",MU_FLEX!D9>0.000001),0.0012,0))*100*INGRESO_DATOS!C32*100,"")
```

**MU_FLEX!H9**

```excel
=IF(MU_PRESION!D20="OK",IF(COUNT(MU_FLEX!F9,MU_FLEX!G9)=2,MAX(MU_FLEX!F9,MU_FLEX!G9),""),"")
```

**MU_FLEX!D10**

```excel
=IF(MU_PRESION!D20="OK",MAX(0,-MU_DIAG_X!B10,-MU_DIAG_X!B11)/INGRESO_DATOS!C31,"")
```

**MU_FLEX!E10**

```excel
=IF(MU_PRESION!D20="OK",INGRESO_DATOS!C32*100-INGRESO_DATOS!C21-IF(INGRESO_DATOS!C68="X exterior / Y interior",INDEX(BARRAS_PERU!$E$5:$E$13,MATCH(INGRESO_DATOS!C56,BARRAS_PERU!$A$5:$A$13,0))/2,INDEX(BARRAS_PERU!$E$5:$E$13,MATCH(INGRESO_DATOS!C57,BARRAS_PERU!$A$5:$A$13,0))+INDEX(BARRAS_PERU!$E$5:$E$13,MATCH(INGRESO_DATOS!C56,BARRAS_PERU!$A$5:$A$13,0))/2),"")
```

**MU_FLEX!F10**

```excel
=IF(MU_PRESION!D20="OK",IF(MU_FLEX!D10<=0,0,IF((INGRESO_DATOS!C15*MU_FLEX!E10)^2-4*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))*(MU_FLEX!D10*100000/INGRESO_DATOS!C22)<0,"",(INGRESO_DATOS!C15*MU_FLEX!E10-SQRT((INGRESO_DATOS!C15*MU_FLEX!E10)^2-4*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))*(MU_FLEX!D10*100000/INGRESO_DATOS!C22)))/(2*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))))),"")
```

**MU_FLEX!G10**

```excel
=IF(AND(MU_PRESION!D20="OK",FLEXION_ACERO!B34="OK",ISNUMBER(FLEXION_ACERO!B23)),MAX(FLEXION_ACERO!B36,IF(AND(INGRESO_DATOS!C165="DOS CARAS",MU_FLEX!D10>0.000001),0.0012,0))*100*INGRESO_DATOS!C32*100,"")
```

**MU_FLEX!H10**

```excel
=IF(MU_PRESION!D20="OK",IF(COUNT(MU_FLEX!F10,MU_FLEX!G10)=2,MAX(MU_FLEX!F10,MU_FLEX!G10),""),"")
```

**MU_FLEX!D11**

```excel
=IF(MU_PRESION!D20="OK",MAX(0,-MU_DIAG_Y!B10,-MU_DIAG_Y!B11)/INGRESO_DATOS!C30,"")
```

**MU_FLEX!E11**

```excel
=IF(MU_PRESION!D20="OK",INGRESO_DATOS!C32*100-INGRESO_DATOS!C21-IF(INGRESO_DATOS!C68="Y exterior / X interior",INDEX(BARRAS_PERU!$E$5:$E$13,MATCH(INGRESO_DATOS!C57,BARRAS_PERU!$A$5:$A$13,0))/2,INDEX(BARRAS_PERU!$E$5:$E$13,MATCH(INGRESO_DATOS!C56,BARRAS_PERU!$A$5:$A$13,0))+INDEX(BARRAS_PERU!$E$5:$E$13,MATCH(INGRESO_DATOS!C57,BARRAS_PERU!$A$5:$A$13,0))/2),"")
```

**MU_FLEX!F11**

```excel
=IF(MU_PRESION!D20="OK",IF(MU_FLEX!D11<=0,0,IF((INGRESO_DATOS!C15*MU_FLEX!E11)^2-4*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))*(MU_FLEX!D11*100000/INGRESO_DATOS!C22)<0,"",(INGRESO_DATOS!C15*MU_FLEX!E11-SQRT((INGRESO_DATOS!C15*MU_FLEX!E11)^2-4*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))*(MU_FLEX!D11*100000/INGRESO_DATOS!C22)))/(2*(INGRESO_DATOS!C15^2/(2*0.85*INGRESO_DATOS!C14*100))))),"")
```

**MU_FLEX!G11**

```excel
=IF(AND(MU_PRESION!D20="OK",FLEXION_ACERO!B34="OK",ISNUMBER(FLEXION_ACERO!B23)),MAX(FLEXION_ACERO!B36,IF(AND(INGRESO_DATOS!C165="DOS CARAS",MU_FLEX!D11>0.000001),0.0012,0))*100*INGRESO_DATOS!C32*100,"")
```

**MU_FLEX!H11**

```excel
=IF(MU_PRESION!D20="OK",IF(COUNT(MU_FLEX!F11,MU_FLEX!G11)=2,MAX(MU_FLEX!F11,MU_FLEX!G11),""),"")
```

**MU_FLEX!H15**

```excel
=IF(MU_PRESION!D20="OK",MU_ACERO!B14,"")
```

**MU_PRESION!D20**

```excel
=IF(CONTROL_FASE7!$B$41<>"OK",CONTROL_FASE7!$B$41,IF(GEOMETRIA!B14<>"OK","DATOS INVÁLIDOS",IF(NOT(AND(COUNT(INGRESO_DATOS!C14,INGRESO_DATOS!C15,INGRESO_DATOS!C22,INGRESO_DATOS!C23,INGRESO_DATOS!C24,INGRESO_DATOS!C25,INGRESO_DATOS!C26,INGRESO_DATOS!C58,INGRESO_DATOS!C59,INGRESO_DATOS!C60,INGRESO_DATOS!C61,COMBOS_ULTIMOS!R8,COMBOS_ULTIMOS!S8)=13,MIN(INGRESO_DATOS!C14,INGRESO_DATOS!C15,INGRESO_DATOS!C26,INGRESO_DATOS!C58,INGRESO_DATOS!C59,INGRESO_DATOS!C60,INGRESO_DATOS!C61)>0,INGRESO_DATOS!C25>=0,MIN(COMBOS_ULTIMOS!R8,COMBOS_ULTIMOS!S8)>=0,INGRESO_DATOS!C22=0.9,INGRESO_DATOS!C23=0.85,INGRESO_DATOS!C24=0.85)),"DATOS INVÁLIDOS",IF(MU_PRESION!B28<>"OK",MU_PRESION!B28,IF(OR(INGRESO_DATOS!C85<>"NORMAL",INGRESO_DATOS!C84<>"CORRUGADAS"),"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNT(PUNZONAMIENTO!B8,PUNZONAMIENTO!B9)<2,"DATOS INVÁLIDOS",IF(MIN(PUNZONAMIENTO!B8,PUNZONAMIENTO!B9)<=0,"DATOS INVÁLIDOS",IF(MU_CARGAS!E27<=0,"REQUIERE ANÁLISIS ESPECIAL",IF(MU_PRESION!D16<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS DE CONTACTO PARCIAL","OK")))))))))
```

**MU_PRESION!D23**

```excel
=IF(MU_PRESION!D20="OK",(MU_CARGAS!E27-COMBOS_ULTIMOS!CW8)/GEOMETRIA!B4,"")
```

**MU_PRESION!D24**

```excel
=IF(MU_PRESION!D20="OK",MU_RESULTANTE!G9/GEOMETRIA!B10,"")
```

**MU_PRESION!D25**

```excel
=IF(MU_PRESION!D20="OK",MU_RESULTANTE!F9/GEOMETRIA!B9,"")
```

**MU_PRESION!D26**

```excel
=IF(MU_PRESION!D20="OK",(COMBOS_ULTIMOS!BL8+COMBOS_ULTIMOS!CX8)/GEOMETRIA!B4,"")
```

**MU_PUNZ!B16**

```excel
=IF(AND(MU_PRESION!D20="OK",ISNUMBER(PUNZONAMIENTO!B11)),MU_PRESION!D23+MU_PRESION!D24*INGRESO_DATOS!C44+MU_PRESION!D25*INGRESO_DATOS!C45,"")
```

**MU_PUNZ!B17**

```excel
=IF(MU_PUNZ!B31="OK",MU_CARGAS!E27-MU_PUNZ!B16*PUNZONAMIENTO!B12-COMBOS_ULTIMOS!CW8,"")
```

**MU_PUNZ!B20**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B41/PUNZONAMIENTO!B40,"")
```

**MU_PUNZ!B21**

```excel
=IF(MU_PUNZ!B31<>"OK",MU_PUNZ!B31,IF(MU_PUNZ!B20<=1,"CUMPLE","NO CUMPLE"))
```

**MU_PUNZ!B31**

```excel
=IF(MU_PRESION!D20<>"OK",MU_PRESION!D20,IF(INGRESO_DATOS!C66<>"INTERIOR","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(PUNZONAMIENTO!B64<>"OK",PUNZONAMIENTO!B65<>"OK"),"FUERA DEL ALCANCE IMPLEMENTADO","OK")))
```

**MU_PUNZ!B32**

```excel
=MU_CARGAS!E27
```

**MU_PUNZ!B33**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B16*PUNZONAMIENTO!B12+COMBOS_ULTIMOS!CW8,"")
```

**MU_PUNZ!B41**

```excel
=IF(MU_PUNZ!B31="OK",MAX(MAX(MU_PUNZ!B52:B55),-MIN(MU_PUNZ!B52:B55)),"")
```

**MU_PUNZ!B42**

```excel
=IF(MU_PUNZ!B31="OK",MIN(MU_PUNZ!B52:B55),"")
```

**MU_PUNZ!B46**

```excel
=MU_CARGAS!E28
```

**MU_PUNZ!B47**

```excel
=MU_CARGAS!E29
```

**MU_PUNZ!B48**

```excel
=IF(MU_PUNZ!B31="OK",MU_CARGAS!E28+MU_PRESION!D25*PUNZONAMIENTO!B12*(PUNZONAMIENTO!B32/100)^2/12,"")
```

**MU_PUNZ!B49**

```excel
=IF(MU_PUNZ!B31="OK",MU_CARGAS!E29-MU_PRESION!D24*PUNZONAMIENTO!B12*(PUNZONAMIENTO!B31/100)^2/12,"")
```

**MU_PUNZ!B50**

```excel
=IF(MU_PUNZ!B31="OK",PUNZONAMIENTO!B36*MU_PUNZ!B48,"")
```

**MU_PUNZ!B51**

```excel
=IF(MU_PUNZ!B31="OK",PUNZONAMIENTO!B37*MU_PUNZ!B49,"")
```

**MU_PUNZ!B52**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B17*1000/PUNZONAMIENTO!B33-PUNZONAMIENTO!B41*MU_PUNZ!B48*100000*(PUNZONAMIENTO!B32/2)/PUNZONAMIENTO!B34+PUNZONAMIENTO!B42*MU_PUNZ!B49*100000*(PUNZONAMIENTO!B31/2)/PUNZONAMIENTO!B35,"")
```

**MU_PUNZ!B53**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B17*1000/PUNZONAMIENTO!B33+PUNZONAMIENTO!B41*MU_PUNZ!B48*100000*(PUNZONAMIENTO!B32/2)/PUNZONAMIENTO!B34+PUNZONAMIENTO!B42*MU_PUNZ!B49*100000*(PUNZONAMIENTO!B31/2)/PUNZONAMIENTO!B35,"")
```

**MU_PUNZ!B54**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B17*1000/PUNZONAMIENTO!B33-PUNZONAMIENTO!B41*MU_PUNZ!B48*100000*(PUNZONAMIENTO!B32/2)/PUNZONAMIENTO!B34-PUNZONAMIENTO!B42*MU_PUNZ!B49*100000*(PUNZONAMIENTO!B31/2)/PUNZONAMIENTO!B35,"")
```

**MU_PUNZ!B55**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B17*1000/PUNZONAMIENTO!B33+PUNZONAMIENTO!B41*MU_PUNZ!B48*100000*(PUNZONAMIENTO!B32/2)/PUNZONAMIENTO!B34-PUNZONAMIENTO!B42*MU_PUNZ!B49*100000*(PUNZONAMIENTO!B31/2)/PUNZONAMIENTO!B35,"")
```

**MU_PUNZ!B73**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B17*1000/PUNZONAMIENTO!B33-1*MU_PUNZ!B48*100000*(PUNZONAMIENTO!B32/2)/PUNZONAMIENTO!B34+1*MU_PUNZ!B49*100000*(PUNZONAMIENTO!B31/2)/PUNZONAMIENTO!B35,"")
```

**MU_PUNZ!B74**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B17*1000/PUNZONAMIENTO!B33--1*MU_PUNZ!B48*100000*(PUNZONAMIENTO!B32/2)/PUNZONAMIENTO!B34+1*MU_PUNZ!B49*100000*(PUNZONAMIENTO!B31/2)/PUNZONAMIENTO!B35,"")
```

**MU_PUNZ!B75**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B17*1000/PUNZONAMIENTO!B33-1*MU_PUNZ!B48*100000*(PUNZONAMIENTO!B32/2)/PUNZONAMIENTO!B34+-1*MU_PUNZ!B49*100000*(PUNZONAMIENTO!B31/2)/PUNZONAMIENTO!B35,"")
```

**MU_PUNZ!B76**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B17*1000/PUNZONAMIENTO!B33--1*MU_PUNZ!B48*100000*(PUNZONAMIENTO!B32/2)/PUNZONAMIENTO!B34+-1*MU_PUNZ!B49*100000*(PUNZONAMIENTO!B31/2)/PUNZONAMIENTO!B35,"")
```

**MU_PUNZ!B77**

```excel
=IF(MU_PUNZ!B31="OK",MAX(MU_PUNZ!B41,MAX(MU_PUNZ!B73:B76),-MIN(MU_PUNZ!B73:B76)),"")
```

**MU_PUNZ!B78**

```excel
=IF(MU_PUNZ!B31="OK",MU_PUNZ!B77/PUNZONAMIENTO!B40,"")
```

**MU_PUNZ!B79**

```excel
=IF(MU_PUNZ!B31<>"OK",MU_PUNZ!B31,IF(MU_PUNZ!B78<=1,"CUMPLE","REQUIERE ANÁLISIS ESPECIAL"))
```

**MU_RESULTANTE!F9**

```excel
=IF(MU_PRESION!B28="OK",-MU_CARGAS!E28+MU_CARGAS!E27*INGRESO_DATOS!C45-COMBOS_ULTIMOS!CW8*inp_yc,"")
```

**MU_RESULTANTE!G9**

```excel
=IF(MU_PRESION!B28="OK",MU_CARGAS!E29+MU_CARGAS!E27*INGRESO_DATOS!C44-COMBOS_ULTIMOS!CW8*inp_xc,"")
```

**ESPECTROS_U!A8**

```excel
=IF(AND(COMBOS_ULTIMOS!A8="SI",DEMANDAS_E030!AC8="SI"),"SI",IF(COMBOS_ULTIMOS!BS8="D. RESULTADO EXTERNO YA COMBINADO","NO",IF(AND(COMBOS_ULTIMOS!A8="SI",OR(COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA")),"SI","NO")))
```

**ESPECTROS_U!AI8**

```excel
=IF(AND(DEMANDAS_E030!AC8="SI",NOT(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"))),IF(COMBOS_ULTIMOS!K8="OK",IF(AND(DEMANDAS_E030!AC8="SI",NOT(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"))),IF(A8<>"SI","NO APLICA",IF(DEMANDAS_E030!Y8<>"OK",DEMANDAS_E030!Y8,IF(COMBOS_ULTIMOS!CS8<>"OK",COMBOS_ULTIMOS!CS8,"OK"))),IF(AND(A8="SI",DEMANDAS_E030!Y8<>"OK"),DEMANDAS_E030!Y8,IF(OR(AND(A8="SI",C8=D8),AND(A8="SI",COMBOS_ULTIMOS!BI8<>"OK"),COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"U",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$I$8:$I$1447,"<>OK")>0),"REQUIERE DATOS — FUENTE ESPECTRAL",IF(A8<>"SI","NO APLICA",IF(COMBOS_ULTIMOS!CS8<>"OK",COMBOS_ULTIMOS!CS8,IF(CONTROL_FASE7!$B$10<>"OK",CONTROL_FASE7!$B$10,IF(OR(LEN(C8)=0,LEN(D8)=0,LEN(G8)=0,LEN(H8)=0,LEN(J8)=0,I8<>"SI",LEN(COMBOS_ULTIMOS!BQ8)=0,LEN(COMBOS_ULTIMOS!CK8)=0,LEN(COMBOS_ULTIMOS!CL8)=0),"REQUIERE DATOS",IF(OR(COMBOS_ULTIMOS!BV8<>"INTERFAZ COLUMNA-ZAPATA",NOT(ISNUMBER(COMBOS_ULTIMOS!CR8)),ABS(COMBOS_ULTIMOS!CR8)>0.00000001),"REQUIERE VECTOR HORIZONTAL FIRMADO EN INTERFAZ",IF(COUNT(K8:AB8)<>18,"REQUIERE DATOS",IF(MIN(Q8:AB8)<0,"DATOS INVÁLIDOS",IF(OR(NOT(OR(F8="SI",F8="NO")),CONTROL_FASE7!$B$14="REQUIERE DEFINIR",LEN(CONTROL_FASE7!$B$15)=0),"REQUIERE DEFINIR COMPONENTE VERTICAL",IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",F8<>"SI"),"REQUIERE COMPONENTE VERTICAL",IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",OR(LEN(E8)=0,COUNT(AC8:AH8)<>6,MIN(AC8:AH8)<0)),"REQUIERE DATOS",IF(AND(CONTROL_FASE7!$B$7="E.030 ANTERIOR A RM 183-2026",OR(CONTROL_FASE7!$B$12<>"REGULAR",LEN(CONTROL_FASE7!$B$13)=0)),"REQUIERE DIRECCIÓN MÁS DESFAVORABLE DOCUMENTADA","OK")))))))))))))),COMBOS_ULTIMOS!K8),IF(AND(DEMANDAS_E030!AC8="SI",NOT(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"))),IF(A8<>"SI","NO APLICA",IF(DEMANDAS_E030!Y8<>"OK",DEMANDAS_E030!Y8,IF(COMBOS_ULTIMOS!CS8<>"OK",COMBOS_ULTIMOS!CS8,"OK"))),IF(AND(A8="SI",DEMANDAS_E030!Y8<>"OK"),DEMANDAS_E030!Y8,IF(OR(AND(A8="SI",C8=D8),AND(A8="SI",COMBOS_ULTIMOS!BI8<>"OK"),COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"U",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$I$8:$I$1447,"<>OK")>0),"REQUIERE DATOS — FUENTE ESPECTRAL",IF(A8<>"SI","NO APLICA",IF(COMBOS_ULTIMOS!CS8<>"OK",COMBOS_ULTIMOS!CS8,IF(CONTROL_FASE7!$B$10<>"OK",CONTROL_FASE7!$B$10,IF(OR(LEN(C8)=0,LEN(D8)=0,LEN(G8)=0,LEN(H8)=0,LEN(J8)=0,I8<>"SI",LEN(COMBOS_ULTIMOS!BQ8)=0,LEN(COMBOS_ULTIMOS!CK8)=0,LEN(COMBOS_ULTIMOS!CL8)=0),"REQUIERE DATOS",IF(OR(COMBOS_ULTIMOS!BV8<>"INTERFAZ COLUMNA-ZAPATA",NOT(ISNUMBER(COMBOS_ULTIMOS!CR8)),ABS(COMBOS_ULTIMOS!CR8)>0.00000001),"REQUIERE RECOMBINACIÓN MODAL EN INTERFAZ",IF(COUNT(K8:AB8)<>18,"REQUIERE DATOS",IF(MIN(Q8:AB8)<0,"DATOS INVÁLIDOS",IF(OR(NOT(OR(F8="SI",F8="NO")),CONTROL_FASE7!$B$14="REQUIERE DEFINIR",LEN(CONTROL_FASE7!$B$15)=0),"REQUIERE DEFINIR COMPONENTE VERTICAL",IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",F8<>"SI"),"REQUIERE COMPONENTE VERTICAL",IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",OR(LEN(E8)=0,COUNT(AC8:AH8)<>6,MIN(AC8:AH8)<0)),"REQUIERE DATOS",IF(AND(CONTROL_FASE7!$B$7="E.030 ANTERIOR A RM 183-2026",OR(CONTROL_FASE7!$B$12<>"REGULAR",LEN(CONTROL_FASE7!$B$13)=0)),"REQUIERE DIRECCIÓN MÁS DESFAVORABLE DOCUMENTADA","OK")))))))))))))))
```

**ESPECTROS_U!AJ8**

```excel
=IF(zap7_norma_estado<>"OK",zap7_norma_estado,IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026","SRSS SX100 SY30 / ART.43","SX100 SY0 / ART.24.1"))
```

**ESPECTROS_U!AK8**

```excel
=IF(zap7_norma_estado<>"OK",zap7_norma_estado,IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026","SRSS SX30 SY100 / ART.43","SX0 SY100 / ART.24.1"))
```

**DERIVADOS_U!B8**

```excel
=ESPECTROS_U!B8&"-X01"&IF(DEMANDAS_E030!AC8="SI","+Ev","")
```

**DERIVADOS_U!D8**

```excel
=IF(AND(DEMANDAS_E030!AC8="SI",NOT(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"))),IF(LEN(COMBOS_ULTIMOS!AQ8)>0,COMBOS_ULTIMOS!AQ8,COMBOS_ULTIMOS!B8),ESPECTROS_U!C8)
```

**DERIVADOS_U!E8**

```excel
=IF(AND(DEMANDAS_E030!AC8="SI",NOT(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"))),"",ESPECTROS_U!D8)
```

**DERIVADOS_U!F8**

```excel
=IF(DEMANDAS_E030!AC8="SI",IF(VERTICAL_F9!C8="","",VERTICAL_F9!C8),ESPECTROS_U!E8)
```

**DERIVADOS_U!H8**

```excel
=IF(AND(DEMANDAS_E030!AC8="SI",NOT(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"))),"HORIZONTAL FIRMADA EN INTERFAZ; VERTICAL +Ev / -Ev",ESPECTROS_U!AJ8)
```

**DERIVADOS_U!I8**

```excel
=IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",1,1)
```

**DERIVADOS_U!J8**

```excel
=IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",0.3,0)
```

**DERIVADOS_U!K8**

```excel
=IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),1,0)
```

**DERIVADOS_U!R8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!K8+L8*(SQRT((I8*ESPECTROS_U!Q8)^2+(J8*ESPECTROS_U!W8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AC8),ESPECTROS_U!AC8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!S8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!L8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!S8*VERTICAL_F9!AD8,0),"")))
```

**DERIVADOS_U!S8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!L8+M8*(SQRT((I8*ESPECTROS_U!R8)^2+(J8*ESPECTROS_U!X8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AD8),ESPECTROS_U!AD8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!T8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!M8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!T8*VERTICAL_F9!AD8,0),"")))
```

**DERIVADOS_U!T8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!M8+N8*(SQRT((I8*ESPECTROS_U!S8)^2+(J8*ESPECTROS_U!Y8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AE8),ESPECTROS_U!AE8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!U8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!N8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!U8*VERTICAL_F9!AD8,0),"")))
```

**DERIVADOS_U!U8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!N8+O8*(SQRT((I8*ESPECTROS_U!T8)^2+(J8*ESPECTROS_U!Z8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AF8),ESPECTROS_U!AF8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!V8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!O8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!V8*VERTICAL_F9!AD8,0),"")))
```

**DERIVADOS_U!V8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!O8+P8*(SQRT((I8*ESPECTROS_U!U8)^2+(J8*ESPECTROS_U!AA8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AG8),ESPECTROS_U!AG8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!W8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!P8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!W8*VERTICAL_F9!AD8,0),"")))
```

**DERIVADOS_U!W8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!P8+Q8*(SQRT((I8*ESPECTROS_U!V8)^2+(J8*ESPECTROS_U!AB8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AH8),ESPECTROS_U!AH8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!X8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!Q8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!X8*VERTICAL_F9!AD8,0),"")))
```

**DERIVADOS_U!Z8**

```excel
=ESPECTROS_U!AI8
```

**DERIVADOS_U!AA8**

```excel
=MOTOR_ESPECTRAL_U!ASQ8
```

**DERIVADOS_U!AB8**

```excel
=MOTOR_ESPECTRAL_U!ASR8
```

**DERIVADOS_U!AD8**

```excel
=IF($A8<>"SI","",IF($Z8="OK",IF(ABS($W8)>zap7_mz_tol,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA","OK"),$Z8))
```

**DERIVADOS_U!AS8**

```excel
=IF(A8="SI",MOTOR_H_U!AYN8,"")
```

**DERIVADOS_U!AT8**

```excel
=IF(A8="SI",MOTOR_H_U!AYM8,"")
```

**DERIVADOS_U!AU8**

```excel
=IF(A8="SI",MOTOR_H_U!AXR8,"")
```

**DERIVADOS_U!AX8**

```excel
=IF(DEMANDAS_E030!AC8="SI",1,"ESTADÍSTICO / EXTERNO")
```

**DU_INPUT!A8**

```excel
=IF(AND(TRUE,ESPECTROS_U!A8="SI",OR(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),TRUE)),"SI","NO")
```

**DU_INPUT!B8**

```excel
=ESPECTROS_U!B8&"-"&IF(0=0,"X","Y")&TEXT((0*32+IF(ESPECTROS_U!L8<0,16,0)+IF(ESPECTROS_U!M8<0,8,0)+0*4+0*2+IF(ESPECTROS_U!P8<0,1,0))+1,"00")&IF(DEMANDAS_E030!AC8="SI","+Ev","")
```

**DU_INPUT!L8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!K8+1*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!Q8)^2+(0.3*ESPECTROS_U!W8)^2),ESPECTROS_U!Q8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AC8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!S8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!L8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!S8*VERTICAL_F9!AD8,0),""))
```

**DU_INPUT!M8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!L8+IF(ESPECTROS_U!L8<0,-1,1)*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!R8)^2+(0.3*ESPECTROS_U!X8)^2),ESPECTROS_U!R8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AD8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!T8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!M8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!T8*VERTICAL_F9!AD8,0),""))
```

**DU_INPUT!N8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!M8+IF(ESPECTROS_U!M8<0,-1,1)*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!S8)^2+(0.3*ESPECTROS_U!Y8)^2),ESPECTROS_U!S8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AE8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!U8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!N8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!U8*VERTICAL_F9!AD8,0),""))
```

**DU_INPUT!O8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!N8+1*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!T8)^2+(0.3*ESPECTROS_U!Z8)^2),ESPECTROS_U!T8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AF8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!V8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!O8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!V8*VERTICAL_F9!AD8,0),""))
```

**DU_INPUT!P8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!O8+1*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!U8)^2+(0.3*ESPECTROS_U!AA8)^2),ESPECTROS_U!U8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AG8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!W8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!P8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!W8*VERTICAL_F9!AD8,0),""))
```

**DU_INPUT!Q8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!P8+IF(ESPECTROS_U!P8<0,-1,1)*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!V8)^2+(0.3*ESPECTROS_U!AB8)^2),ESPECTROS_U!V8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AH8,0))+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!X8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!Q8+IF(DEMANDAS_E030!AC8="SI",1*VERTICAL_F9!X8*VERTICAL_F9!AD8,0),""))
```

**ESPECTROS_S!AI8**

```excel
=IF(AND(DEMANDAS_E030!AC68="SI",NOT(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"))),IF(COMBOS_SERVICIO!O8="OK",IF(AND(DEMANDAS_E030!AC68="SI",NOT(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"))),IF(A8<>"SI","NO APLICA",IF(DEMANDAS_E030!Y68<>"OK",DEMANDAS_E030!Y68,IF(COMBOS_SERVICIO!DL8<>"OK",COMBOS_SERVICIO!DL8,"OK"))),IF(AND(A8="SI",DEMANDAS_E030!Y68<>"OK"),DEMANDAS_E030!Y68,IF(OR(AND(A8="SI",C8=D8),AND(A8="SI",COMBOS_SERVICIO!BV8<>"OK"),COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"S",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$I$8:$I$1447,"<>OK")>0,AND(A8="SI",OR(COMBOS_SERVICIO!L8=0.8,COMBOS_SERVICIO!M8="SI"),LEN(COMBOS_SERVICIO!AC8)=0)),"REQUIERE DATOS — FUENTE ESPECTRAL",IF(OR(COMBOS_SERVICIO!C8<>"SISMO",NOT(OR(COMBOS_SERVICIO!L8=1,COMBOS_SERVICIO!L8=0.8)),AND(COMBOS_SERVICIO!AI8="SI",COMBOS_SERVICIO!L8<>1),NOT(ISNUMBER(COMBOS_SERVICIO!K8)),COMBOS_SERVICIO!K8<=0,AND(COMBOS_SERVICIO!AE8="SI",OR(LEN(COMBOS_SERVICIO!AG8)=0,LEN(COMBOS_SERVICIO!AH8)=0))),"DATOS INVÁLIDOS",IF(A8<>"SI","NO APLICA",IF(COMBOS_SERVICIO!DL8<>"OK",COMBOS_SERVICIO!DL8,IF(CONTROL_FASE7!$B$10<>"OK",CONTROL_FASE7!$B$10,IF(OR(LEN(C8)=0,LEN(D8)=0,LEN(G8)=0,LEN(H8)=0,LEN(J8)=0,I8<>"SI",LEN(COMBOS_SERVICIO!CJ8)=0,LEN(COMBOS_SERVICIO!DD8)=0,LEN(COMBOS_SERVICIO!DE8)=0),"REQUIERE DATOS",IF(OR(COMBOS_SERVICIO!CO8<>"INTERFAZ COLUMNA-ZAPATA",NOT(ISNUMBER(COMBOS_SERVICIO!DK8)),ABS(COMBOS_SERVICIO!DK8)>0.00000001),"REQUIERE VECTOR HORIZONTAL FIRMADO EN INTERFAZ",IF(COUNT(K8:AB8)<>18,"REQUIERE DATOS",IF(MIN(Q8:AB8)<0,"DATOS INVÁLIDOS",IF(OR(NOT(OR(F8="SI",F8="NO")),CONTROL_FASE7!$B$14="REQUIERE DEFINIR",LEN(CONTROL_FASE7!$B$15)=0),"REQUIERE DEFINIR COMPONENTE VERTICAL",IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",F8<>"SI"),"REQUIERE COMPONENTE VERTICAL",IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",OR(LEN(E8)=0,COUNT(AC8:AH8)<>6,MIN(AC8:AH8)<0)),"REQUIERE DATOS",IF(AND(CONTROL_FASE7!$B$7="E.030 ANTERIOR A RM 183-2026",OR(CONTROL_FASE7!$B$12<>"REGULAR",LEN(CONTROL_FASE7!$B$13)=0)),"REQUIERE DIRECCIÓN MÁS DESFAVORABLE DOCUMENTADA","OK"))))))))))))))),COMBOS_SERVICIO!O8),IF(AND(DEMANDAS_E030!AC68="SI",NOT(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"))),IF(A8<>"SI","NO APLICA",IF(DEMANDAS_E030!Y68<>"OK",DEMANDAS_E030!Y68,IF(COMBOS_SERVICIO!DL8<>"OK",COMBOS_SERVICIO!DL8,"OK"))),IF(AND(A8="SI",DEMANDAS_E030!Y68<>"OK"),DEMANDAS_E030!Y68,IF(OR(AND(A8="SI",C8=D8),AND(A8="SI",COMBOS_SERVICIO!BV8<>"OK"),COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"S",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$I$8:$I$1447,"<>OK")>0,AND(A8="SI",OR(COMBOS_SERVICIO!L8=0.8,COMBOS_SERVICIO!M8="SI"),LEN(COMBOS_SERVICIO!AC8)=0)),"REQUIERE DATOS — FUENTE ESPECTRAL",IF(OR(COMBOS_SERVICIO!C8<>"SISMO",NOT(OR(COMBOS_SERVICIO!L8=1,COMBOS_SERVICIO!L8=0.8)),AND(COMBOS_SERVICIO!AI8="SI",COMBOS_SERVICIO!L8<>1),NOT(ISNUMBER(COMBOS_SERVICIO!K8)),COMBOS_SERVICIO!K8<=0,AND(COMBOS_SERVICIO!AE8="SI",OR(LEN(COMBOS_SERVICIO!AG8)=0,LEN(COMBOS_SERVICIO!AH8)=0))),"DATOS INVÁLIDOS",IF(A8<>"SI","NO APLICA",IF(COMBOS_SERVICIO!DL8<>"OK",COMBOS_SERVICIO!DL8,IF(CONTROL_FASE7!$B$10<>"OK",CONTROL_FASE7!$B$10,IF(OR(LEN(C8)=0,LEN(D8)=0,LEN(G8)=0,LEN(H8)=0,LEN(J8)=0,I8<>"SI",LEN(COMBOS_SERVICIO!CJ8)=0,LEN(COMBOS_SERVICIO!DD8)=0,LEN(COMBOS_SERVICIO!DE8)=0),"REQUIERE DATOS",IF(OR(COMBOS_SERVICIO!CO8<>"INTERFAZ COLUMNA-ZAPATA",NOT(ISNUMBER(COMBOS_SERVICIO!DK8)),ABS(COMBOS_SERVICIO!DK8)>0.00000001),"REQUIERE RECOMBINACIÓN MODAL EN INTERFAZ",IF(COUNT(K8:AB8)<>18,"REQUIERE DATOS",IF(MIN(Q8:AB8)<0,"DATOS INVÁLIDOS",IF(OR(NOT(OR(F8="SI",F8="NO")),CONTROL_FASE7!$B$14="REQUIERE DEFINIR",LEN(CONTROL_FASE7!$B$15)=0),"REQUIERE DEFINIR COMPONENTE VERTICAL",IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",F8<>"SI"),"REQUIERE COMPONENTE VERTICAL",IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",OR(LEN(E8)=0,COUNT(AC8:AH8)<>6,MIN(AC8:AH8)<0)),"REQUIERE DATOS",IF(AND(CONTROL_FASE7!$B$7="E.030 ANTERIOR A RM 183-2026",OR(CONTROL_FASE7!$B$12<>"REGULAR",LEN(CONTROL_FASE7!$B$13)=0)),"REQUIERE DIRECCIÓN MÁS DESFAVORABLE DOCUMENTADA","OK"))))))))))))))))
```

**DERIVADOS_S!D8**

```excel
=IF(AND(DEMANDAS_E030!AC68="SI",NOT(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"))),IF(LEN(COMBOS_SERVICIO!BD8)>0,COMBOS_SERVICIO!BD8,COMBOS_SERVICIO!B8),ESPECTROS_S!C8)
```

**DERIVADOS_S!E8**

```excel
=IF(AND(DEMANDAS_E030!AC68="SI",NOT(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"))),"",ESPECTROS_S!D8)
```

**DERIVADOS_S!F8**

```excel
=IF(DEMANDAS_E030!AC68="SI",IF(VERTICAL_F9!C68="","",VERTICAL_F9!C68),ESPECTROS_S!E8)
```

**DERIVADOS_S!H8**

```excel
=IF(AND(DEMANDAS_E030!AC68="SI",NOT(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"))),"HORIZONTAL FIRMADA EN INTERFAZ; VERTICAL +Ev / -Ev",ESPECTROS_S!AJ8)
```

**DERIVADOS_S!R8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!K8+L8*((SQRT((I8*ESPECTROS_S!Q8)^2+(J8*ESPECTROS_S!W8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AC8),ESPECTROS_S!AC8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!S68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AG68+(COMBOS_SERVICIO!Q8-VERTICAL_F9!AG68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!Q8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!S68*VERTICAL_F9!AD68,0),"")))
```

**DERIVADOS_S!S8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!L8+M8*((SQRT((I8*ESPECTROS_S!R8)^2+(J8*ESPECTROS_S!X8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AD8),ESPECTROS_S!AD8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!T68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AH68+(COMBOS_SERVICIO!R8-VERTICAL_F9!AH68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!R8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!T68*VERTICAL_F9!AD68,0),"")))
```

**DERIVADOS_S!T8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!M8+N8*((SQRT((I8*ESPECTROS_S!S8)^2+(J8*ESPECTROS_S!Y8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AE8),ESPECTROS_S!AE8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!U68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AI68+(COMBOS_SERVICIO!S8-VERTICAL_F9!AI68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!S8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!U68*VERTICAL_F9!AD68,0),"")))
```

**DERIVADOS_S!U8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!N8+O8*((SQRT((I8*ESPECTROS_S!T8)^2+(J8*ESPECTROS_S!Z8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AF8),ESPECTROS_S!AF8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!V68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AJ68+(COMBOS_SERVICIO!T8-VERTICAL_F9!AJ68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!T8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!V68*VERTICAL_F9!AD68,0),"")))
```

**DERIVADOS_S!V8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!O8+P8*((SQRT((I8*ESPECTROS_S!U8)^2+(J8*ESPECTROS_S!AA8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AG8),ESPECTROS_S!AG8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!W68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AK68+(COMBOS_SERVICIO!U8-VERTICAL_F9!AK68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!U8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!W68*VERTICAL_F9!AD68,0),"")))
```

**DERIVADOS_S!W8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!P8+Q8*((SQRT((I8*ESPECTROS_S!V8)^2+(J8*ESPECTROS_S!AB8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AH8),ESPECTROS_S!AH8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!X68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AL68+(COMBOS_SERVICIO!V8-VERTICAL_F9!AL68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!V8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!X68*VERTICAL_F9!AD68,0),"")))
```

**DERIVADOS_S!AD8**

```excel
=IF($A8<>"SI","",IF($Z8="OK",IF(ABS($W8)>zap7_mz_tol,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA","OK"),$Z8))
```

**DERIVADOS_S!AE8**

```excel
=MOTOR_ESPECTRAL_S!DC8
```

**DERIVADOS_S!AF8**

```excel
=MOTOR_ESPECTRAL_S!DD8
```

**DERIVADOS_S!AG8**

```excel
=MOTOR_ESPECTRAL_S!EA8
```

**DS_INPUT!A8**

```excel
=IF(AND(TRUE,ESPECTROS_S!A8="SI",OR(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),TRUE)),"SI","NO")
```

**DS_INPUT!B8**

```excel
=ESPECTROS_S!B8&"-"&IF(0=0,"X","Y")&TEXT((0*32+IF(ESPECTROS_S!L8<0,16,0)+IF(ESPECTROS_S!M8<0,8,0)+0*4+0*2+IF(ESPECTROS_S!P8<0,1,0))+1,"00")&IF(DEMANDAS_E030!AC68="SI","+Ev","")
```

**DS_INPUT!L8**

```excel
=1
```

**DS_INPUT!M8**

```excel
=IF(LEN(COMBOS_SERVICIO!M8)=0,"",COMBOS_SERVICIO!M8)
```

**DS_INPUT!N8**

```excel
=IF(LEN(COMBOS_SERVICIO!N8)=0,"",COMBOS_SERVICIO!N8)
```

**DS_INPUT!O8**

```excel
=ESPECTROS_S!AI8
```

**DS_INPUT!P8**

```excel
=IF(LEN(COMBOS_SERVICIO!P8)=0,"",COMBOS_SERVICIO!P8)
```

**DS_INPUT!Q8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!K8+1*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!Q8)^2+(0.3*ESPECTROS_S!W8)^2),ESPECTROS_S!Q8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AC8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!S68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AG68+(COMBOS_SERVICIO!Q8-VERTICAL_F9!AG68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!Q8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!S68*VERTICAL_F9!AD68,0),""))
```

**DS_INPUT!R8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!L8+IF(ESPECTROS_S!L8<0,-1,1)*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!R8)^2+(0.3*ESPECTROS_S!X8)^2),ESPECTROS_S!R8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AD8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!T68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AH68+(COMBOS_SERVICIO!R8-VERTICAL_F9!AH68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!R8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!T68*VERTICAL_F9!AD68,0),""))
```

**DS_INPUT!S8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!M8+IF(ESPECTROS_S!M8<0,-1,1)*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!S8)^2+(0.3*ESPECTROS_S!Y8)^2),ESPECTROS_S!S8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AE8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!U68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AI68+(COMBOS_SERVICIO!S8-VERTICAL_F9!AI68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!S8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!U68*VERTICAL_F9!AD68,0),""))
```

**DS_INPUT!T8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!N8+1*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!T8)^2+(0.3*ESPECTROS_S!Z8)^2),ESPECTROS_S!T8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AF8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!V68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AJ68+(COMBOS_SERVICIO!T8-VERTICAL_F9!AJ68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!T8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!V68*VERTICAL_F9!AD68,0),""))
```

**DS_INPUT!U8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!O8+1*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!U8)^2+(0.3*ESPECTROS_S!AA8)^2),ESPECTROS_S!U8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AG8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!W68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AK68+(COMBOS_SERVICIO!U8-VERTICAL_F9!AK68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!U8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!W68*VERTICAL_F9!AD68,0),""))
```

**DS_INPUT!V8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!P8+IF(ESPECTROS_S!P8<0,-1,1)*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!V8)^2+(0.3*ESPECTROS_S!AB8)^2),ESPECTROS_S!V8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AH8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!X68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AL68+(COMBOS_SERVICIO!V8-VERTICAL_F9!AL68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!V8)+IF(DEMANDAS_E030!AC68="SI",1*VERTICAL_F9!X68*VERTICAL_F9!AD68,0),""))
```

**MOTOR_ESPECTRAL_U!AY8**

```excel
=IF(DU_INPUT!A8="SI",BW8,"")
```

**TOTAL_F7_U!A8**

```excel
=IF(ESPECTROS_U!A8="SI","NO",RESULTADOS_ULTIMOS!A8)
```

**TOTAL_F7_U!AQ8**

```excel
=IF(DEMANDAS_E030!AC8="SI",IF(OR(ISNUMBER(IF(ISBLANK(RESULTADOS_ULTIMOS!AQ8),"",RESULTADOS_ULTIMOS!AQ8)),IF(ISBLANK(RESULTADOS_ULTIMOS!AQ8),"",RESULTADOS_ULTIMOS!AQ8)=""),"","NO APLICA"),IF(ISBLANK(RESULTADOS_ULTIMOS!AQ8),"",RESULTADOS_ULTIMOS!AQ8))
```

**TOTAL_F7_U!HW8**

```excel
=IF(ISNUMBER($GN8),COUNTIF($GN$8:$GN$1987,">"&$GN8)+COUNTIF($GN$8:$GN8,$GN8),"")
```

**TOTAL_F7_U!GN68**

```excel
=IF(DU_INPUT!A8="SI",MOTOR_ESPECTRAL_U!AZL8,"")
```

**TOTAL_F7_U!HW68**

```excel
=IF(ISNUMBER($GN68),COUNTIF($GN$8:$GN$1987,">"&$GN68)+COUNTIF($GN$8:$GN68,$GN68),"")
```

**TOTAL_F7_U!JD68**

```excel
=COUNTIF(AP68:AR68,"NO CUMPLE")+COUNTIF(AT68:BQ68,"NO CUMPLE")+COUNTIF(EQ68:ES68,"NO CUMPLE")+COUNTIF(FQ68:GK68,"NO CUMPLE")+COUNTIF(IV68:JC68,"NO CUMPLE")+COUNTIF(EU68:FP68,"NO CUMPLE")+COUNTIF(CA68:EO68,"NO FACTIBLE")>0
```

**TOTAL_F7_U!JE68**

```excel
=DEMANDAS_E030!AA8
```

**TOTAL_F7_U!GN1028**

```excel
=IF(DU_EV_MENOS!A8="SI",MOTOR_EV_U!AZL8,"")
```

**TOTAL_F7_U!HW1028**

```excel
=IF(ISNUMBER($GN1028),COUNTIF($GN$8:$GN$1987,">"&$GN1028)+COUNTIF($GN$8:$GN1028,$GN1028),"")
```

**TOTAL_F7_S!BT68**

```excel
=COUNTIF(AF68:BA68,"NO CUMPLE")>0
```

**TOTAL_F7_S!BU68**

```excel
=DEMANDAS_E030!AA68
```

**VISTA_DERIVADO!B11**

```excel
=IF(IF(B7="U",INDEX(DERIVADOS_U!$A$8:$A$15367,B8),INDEX(DERIVADOS_S!$A$8:$A$15367,B8))="SI",IFERROR(IF(B7="U",INDEX(DERIVADOS_U!B8:B15367,B8),INDEX(DERIVADOS_S!B8:B15367,B8)),""),"NO APLICA")
```

**VISTA_DERIVADO!B14**

```excel
=IF(IF(B7="U",INDEX(DERIVADOS_U!$A$8:$A$15367,B8),INDEX(DERIVADOS_S!$A$8:$A$15367,B8))="SI",IFERROR(IF(B7="U",INDEX(DERIVADOS_U!H8:H15367,B8),INDEX(DERIVADOS_S!H8:H15367,B8)),""),"NO APLICA")
```

**VISTA_DERIVADO!B15**

```excel
=IF(IF(B7="U",INDEX(DERIVADOS_U!$A$8:$A$15367,B8),INDEX(DERIVADOS_S!$A$8:$A$15367,B8))="SI",IFERROR(IF(B7="U",INDEX(DERIVADOS_U!X8:X15367,B8),INDEX(DERIVADOS_S!X8:X15367,B8)),""),"NO APLICA")
```

**VISTA_DERIVADO!B22**

```excel
=IF(IF(B7="U",INDEX(DERIVADOS_U!$A$8:$A$15367,B8),INDEX(DERIVADOS_S!$A$8:$A$15367,B8))="SI",IFERROR(IF(B7="U",INDEX(DERIVADOS_U!Z8:Z15367,B8),INDEX(DERIVADOS_S!Z8:Z15367,B8)),""),"NO APLICA")
```

**VISTA_DERIVADO!B28**

```excel
=IF(IF(B7="U",INDEX(DERIVADOS_U!$A$8:$A$15367,B8),INDEX(DERIVADOS_S!$A$8:$A$15367,B8))="SI",IF(B7="U",INDEX(DERIVADOS_U!AW8:AW15367,B8),INDEX(DERIVADOS_S!AW8:AW15367,B8)),"NO APLICA")
```

**VISTA_DERIVADO!B29**

```excel
=IF(IF(B7="U",INDEX(DERIVADOS_U!$A$8:$A$15367,B8),INDEX(DERIVADOS_S!$A$8:$A$15367,B8))="SI",IF(B7="U",INDEX(DERIVADOS_U!AX8:AX15367,B8),INDEX(DERIVADOS_S!AX8:AX15367,B8)),"NO APLICA")
```

**MOTOR_H_U!ZU8**

```excel
=IF(DERIVADOS_U!Z8="OK",DERIVADOS_U!W8,"")
```

**MOTOR_H_U!AAE8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(DERIVADOS_U!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_U!AD8,IF(CONEXION_ESPECTRAL!M8<>"OK",CONEXION_ESPECTRAL!M8,IF(CONEXION_COLUMNA_ZAPATA!$B$30<>"OK",CONEXION_COLUMNA_ZAPATA!$B$30,IF(MOTOR_ESPECTRAL_U!$AQN$8<>"OK",MOTOR_ESPECTRAL_U!$AQN$8,IF(CONEXION_COLUMNA_ZAPATA!$B$7<>"EXTERNO","FUERA DEL ALCANCE IMPLEMENTADO",IF(ABS(MOTOR_H_U!ZU8)>0.000001,"REQUIERE ANÁLISIS ESPECIAL",IF(OR(NOT(ISTEXT(MOTOR_ESPECTRAL_U!$ZV$8)),LEN(MOTOR_ESPECTRAL_U!$ZV$8)=0,NOT(ISTEXT(MOTOR_ESPECTRAL_U!$ZW$8)),LEN(MOTOR_ESPECTRAL_U!$ZW$8)=0,NOT(ISTEXT(CONEXION_COLUMNA_ZAPATA!$B$18)),LEN(CONEXION_COLUMNA_ZAPATA!$B$18)=0,NOT(ISTEXT(CONEXION_COLUMNA_ZAPATA!$B$22)),LEN(CONEXION_COLUMNA_ZAPATA!$B$22)=0,LEN(CONEXION_COLUMNA_ZAPATA!$B$10)=0),"REQUIERE DATOS",IF(OR(MOTOR_ESPECTRAL_U!$ZW$8<>MOTOR_ESPECTRAL_U!$ACR$8,CONEXION_COLUMNA_ZAPATA!$B$10<>"ACCIONES AMPLIFICADAS"),"DATOS INVÁLIDOS",IF(COUNT(MOTOR_ESPECTRAL_U!$ZX$8,MOTOR_ESPECTRAL_U!$ZY$8,MOTOR_ESPECTRAL_U!$ZZ$8,MOTOR_ESPECTRAL_U!$AAA$8,MOTOR_ESPECTRAL_U!$AAB$8,MOTOR_ESPECTRAL_U!$AAC$8,MOTOR_ESPECTRAL_U!$AAD$8)<>7,"REQUIERE DATOS",IF(OR(MOTOR_ESPECTRAL_U!$ZX$8<0,MOTOR_ESPECTRAL_U!$ZZ$8<0,MOTOR_ESPECTRAL_U!$AAC$8<0,MOTOR_ESPECTRAL_U!$AAC$8>CONEXION_COLUMNA_ZAPATA!$B$29,MOTOR_ESPECTRAL_U!$AAD$8<0,ABS(MOTOR_ESPECTRAL_U!$AAA$8)>INGRESO_DATOS!$C$42*50,ABS(MOTOR_ESPECTRAL_U!$AAB$8)>INGRESO_DATOS!$C$43*50,MOTOR_ESPECTRAL_U!$ZY$8<=0,MOTOR_ESPECTRAL_U!$ZY$8>1),"DATOS INVÁLIDOS",IF(CONEXION_ESPECTRAL!M8<>"OK",CONEXION_ESPECTRAL!M8,IF(MOTOR_ESPECTRAL_U!$ZZ$8=0,IF(AND(MOTOR_ESPECTRAL_U!$AAC$8=0,MOTOR_ESPECTRAL_U!$AAD$8=0,MOTOR_ESPECTRAL_U!$AAA$8=0,MOTOR_ESPECTRAL_U!$AAB$8=0),"OK","DATOS INVÁLIDOS"),IF(MOTOR_ESPECTRAL_U!$AAC$8<=0,"DATOS INVÁLIDOS",IF(MOTOR_ESPECTRAL_U!$AAD$8+0.00000001>=MOTOR_ESPECTRAL_U!$ZZ$8*1000/MOTOR_ESPECTRAL_U!$AAC$8,"OK","DATOS INVÁLIDOS")))))))))))))),"")
```

**MOTOR_H_U!AAG8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(AND(MOTOR_H_U!AAE8="OK",MOTOR_ESPECTRAL_U!$AAF$8="CUMPLE"),SUM(MOTOR_ESPECTRAL_U!$EP$8:$GW$8)+MOTOR_ESPECTRAL_U!$ZZ$8,""),"")
```

**MOTOR_H_U!AAH8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(AND(MOTOR_H_U!AAE8="OK",MOTOR_ESPECTRAL_U!$AAF$8="CUMPLE"),-SUMPRODUCT(MOTOR_ESPECTRAL_U!$EP$8:$GW$8,BARRAS_CONEXION!$C$12:$C$71)/100-MOTOR_ESPECTRAL_U!$ZZ$8*MOTOR_ESPECTRAL_U!$AAB$8/100,""),"")
```

**MOTOR_H_U!AAI8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(AND(MOTOR_H_U!AAE8="OK",MOTOR_ESPECTRAL_U!$AAF$8="CUMPLE"),SUMPRODUCT(MOTOR_ESPECTRAL_U!$EP$8:$GW$8,BARRAS_CONEXION!$B$12:$B$71)/100+MOTOR_ESPECTRAL_U!$ZZ$8*MOTOR_ESPECTRAL_U!$AAA$8/100,""),"")
```

**MOTOR_H_U!AAJ8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(ISNUMBER(MOTOR_H_U!AAG8),MOTOR_H_U!AAG8-MOTOR_ESPECTRAL_U!$ZR$8,""),"")
```

**MOTOR_H_U!AAK8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(ISNUMBER(MOTOR_H_U!AAH8),MOTOR_H_U!AAH8-MOTOR_ESPECTRAL_U!$ZS$8,""),"")
```

**MOTOR_H_U!AAL8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(ISNUMBER(MOTOR_H_U!AAI8),MOTOR_H_U!AAI8-MOTOR_ESPECTRAL_U!$ZT$8,""),"")
```

**MOTOR_H_U!AAM8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAE8<>"OK",MOTOR_H_U!AAE8,IF(MOTOR_ESPECTRAL_U!$AAF$8<>"CUMPLE",MOTOR_ESPECTRAL_U!$AAF$8,IF(AND(ABS(MOTOR_H_U!AAJ8)<=MAX(0.00000001,ABS(MOTOR_ESPECTRAL_U!$ZR$8)*0.00000001),ABS(MOTOR_H_U!AAK8)<=MAX(0.00000001,ABS(MOTOR_ESPECTRAL_U!$ZS$8)*0.00000001),ABS(MOTOR_H_U!AAL8)<=MAX(0.00000001,ABS(MOTOR_ESPECTRAL_U!$ZT$8)*0.00000001)),"CUMPLE","DATOS INVÁLIDOS"))),"")
```

**MOTOR_H_U!AAN8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAE8<>"OK",MOTOR_H_U!AAE8,IF(MOTOR_ESPECTRAL_U!$ZX$8<=1,"CUMPLE","NO CUMPLE")),"")
```

**MOTOR_H_U!AAP8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAE8="OK",0.7*0.85*INGRESO_DATOS!$C$14*MOTOR_ESPECTRAL_U!$AAC$8/1000,""),"")
```

**MOTOR_H_U!AAQ8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAE8="OK",0.7*0.85*INGRESO_DATOS!$C$108*MOTOR_ESPECTRAL_U!$AAC$8/1000,""),"")
```

**MOTOR_H_U!AAR8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAE8="OK",IF(MOTOR_ESPECTRAL_U!$ZZ$8=0,0,MAX(MOTOR_ESPECTRAL_U!$ZZ$8/MIN(MOTOR_H_U!AAP8:AAQ8),MOTOR_ESPECTRAL_U!$AAD$8/(0.7*0.85*MIN(INGRESO_DATOS!$C$14,INGRESO_DATOS!$C$108)))),""),"")
```

**MOTOR_H_U!AAS8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAE8<>"OK",MOTOR_H_U!AAE8,IF(MOTOR_H_U!AAR8<=1,"CUMPLE","NO CUMPLE")),"")
```

**MOTOR_H_U!AAU8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_ESPECTRAL_U!$AQN$8="OK",SQRT(DERIVADOS_U!S8^2+DERIVADOS_U!T8^2),""),"")
```

**MOTOR_H_U!AAV8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(AND(CONEXION_COLUMNA_ZAPATA!$B$30="OK",ISNUMBER(CONEXION_COLUMNA_ZAPATA!$B$74),ISNUMBER(MOTOR_H_U!AAU8)),MOTOR_H_U!AAU8*1000/(0.85*CONEXION_COLUMNA_ZAPATA!$B$74*MIN(INGRESO_DATOS!$C$109,420/0.0980665)),""),"")
```

**MOTOR_H_U!AAW8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(DERIVADOS_U!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_U!AD8,IF(MOTOR_ESPECTRAL_U!$AQN$8<>"OK",MOTOR_ESPECTRAL_U!$AQN$8,IF(MOTOR_H_U!AAU8<=0.000000001,"NO APLICA",IF(CONEXION_COLUMNA_ZAPATA!$B$30<>"OK",CONEXION_COLUMNA_ZAPATA!$B$30,IF(OR(NOT(ISNUMBER(CONEXION_COLUMNA_ZAPATA!$B$74)),COUNT(INGRESO_DATOS!$C$121)<>1,LEN(INGRESO_DATOS!$C$122)=0,LEN(INGRESO_DATOS!$C$123)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!$C$121<0,"DATOS INVÁLIDOS",IF(AND(INGRESO_DATOS!$C$121>=MOTOR_H_U!AAV8,MOTOR_H_U!AAU8<=CONEXION_COLUMNA_ZAPATA!$B$77,INGRESO_DATOS!$C$122="SI"),"CUMPLE","NO CUMPLE"))))))),"")
```

**MOTOR_H_U!AAX8**

```excel
=MOTOR_ESPECTRAL_U!$AAX$8
```

**MOTOR_H_U!AAY8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAE8="OK","CUMPLE",MOTOR_H_U!AAE8),"")
```

**MOTOR_H_U!AAZ8**

```excel
=MOTOR_ESPECTRAL_U!$AAZ$8
```

**MOTOR_H_U!ABA8**

```excel
=MOTOR_ESPECTRAL_U!$ABA$8
```

**MOTOR_H_U!ABB8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAM8="OK","CUMPLE",MOTOR_H_U!AAM8),"")
```

**MOTOR_H_U!ABC8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAN8="OK","CUMPLE",MOTOR_H_U!AAN8),"")
```

**MOTOR_H_U!ABD8**

```excel
=MOTOR_ESPECTRAL_U!$ABD$8
```

**MOTOR_H_U!ABE8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAS8="OK","CUMPLE",MOTOR_H_U!AAS8),"")
```

**MOTOR_H_U!ABF8**

```excel
=MOTOR_ESPECTRAL_U!$ABF$8
```

**MOTOR_H_U!ABG8**

```excel
=MOTOR_ESPECTRAL_U!$ABG$8
```

**MOTOR_H_U!ABH8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(MOTOR_H_U!AAW8="OK","CUMPLE",MOTOR_H_U!AAW8),"")
```

**MOTOR_H_U!ABI8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(DERIVADOS_U!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_U!AD8,IF(COUNTIF(MOTOR_H_U!AAX8:ABH8,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(MOTOR_H_U!AAX8:ABH8,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(MOTOR_H_U!AAX8:ABH8,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(MOTOR_H_U!AAX8:ABH8,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(MOTOR_H_U!AAX8:ABH8,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))),"")
```

**MOTOR_H_U!AXR8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(DU_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_U!ABI8)=0,"",MOTOR_H_U!ABI8)),"")
```

**MOTOR_H_U!AYE8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(DU_INPUT!A8="NO","",IF(LEN(MOTOR_H_U!AAR8)=0,"",MOTOR_H_U!AAR8)),"")
```

**MOTOR_H_U!AYI8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(DU_INPUT!A8="NO","",IF(LEN(MOTOR_H_U!AAU8)=0,"",MOTOR_H_U!AAU8)),"")
```

**MOTOR_H_U!AYJ8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(DU_INPUT!A8="NO","",IF(LEN(MOTOR_H_U!AAV8)=0,"",MOTOR_H_U!AAV8)),"")
```

**MOTOR_H_U!AYK8**

```excel
=MOTOR_ESPECTRAL_U!$AYK$8
```

**MOTOR_H_U!AYL8**

```excel
=MOTOR_ESPECTRAL_U!$AYL$8
```

**MOTOR_H_U!AYM8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(DU_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_U!AAW8)=0,"",MOTOR_H_U!AAW8)),"")
```

**MOTOR_H_U!AYN8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(DU_INPUT!A8="NO","",IF(MOTOR_H_U!AYI8=0,IF(ISNUMBER(MOTOR_H_U!AYI8),0,""),IF(AND(COUNT(MOTOR_H_U!AYJ8:AYL8)=3,MOTOR_ESPECTRAL_U!$AYK$8>0,MOTOR_ESPECTRAL_U!$AYL$8>0),MAX(MOTOR_H_U!AYJ8/MOTOR_ESPECTRAL_U!$AYK$8,MOTOR_H_U!AYI8/MOTOR_ESPECTRAL_U!$AYL$8),""))),"")
```

**MOTOR_H_U!AZK8**

```excel
=IF(AND(DU_INPUT!A8="SI",DERIVADOS_U!A8="SI"),IF(DU_INPUT!A8="NO","NO APLICA",IF(MOTOR_ESPECTRAL_U!$ARY$8="NO","NO APLICA",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"DATOS INVÁLIDOS")+COUNTIF(MOTOR_H_U!AXR8,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(MOTOR_H_U!AXR8,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(MOTOR_H_U!AXR8,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")>0,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(MOTOR_H_U!AXR8,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(MOTOR_H_U!AXR8,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"REQUIERE DATOS")+COUNTIF(MOTOR_H_U!AXR8,"REQUIERE DATOS")>0,"REQUIERE DATOS",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"NO CUMPLE")+COUNTIF(MOTOR_H_U!AXR8,"NO CUMPLE")>0,"NO CUMPLE","CUMPLE")))))))),"")
```

**MOTOR_H_S!W8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),MOTOR_H_S!AW8,"")
```

**MOTOR_H_S!X8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),MOTOR_H_S!AZ8,"")
```

**MOTOR_H_S!Y8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),MOTOR_H_S!BE8,"")
```

**MOTOR_H_S!AV8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(MOTOR_ESPECTRAL_S!$AF$8="OK",SQRT(DERIVADOS_S!S8^2+DERIVADOS_S!T8^2),""),"")
```

**MOTOR_H_S!AW8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_H_S!AV8<=0.000000001,"NO APLICA",IF(AND(INGRESO_DATOS!$C$79="SI",LEN(INGRESO_DATOS!$C$80)>0),"CUMPLE","REQUIERE DATOS"))),"")
```

**MOTOR_H_S!AY8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(AND(MOTOR_ESPECTRAL_S!$AF$8="OK",MOTOR_ESPECTRAL_S!$AG$8>0,MOTOR_H_S!AV8>0.000000001,ISNUMBER(PRESIONES_SERVICIO!$B$44)),(MOTOR_ESPECTRAL_S!$AX$8+PRESIONES_SERVICIO!$B$44)/MOTOR_H_S!AV8,""),"")
```

**MOTOR_H_S!AZ8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DERIVADOS_S!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_S!AD8,IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_H_S!AV8<=0.000000001,"NO APLICA",IF(MOTOR_ESPECTRAL_S!$BM$8<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(NOT(OR(INGRESO_DATOS!$C$128="NO",INGRESO_DATOS!$C$128="SI")),"DATOS INVÁLIDOS",IF(OR(COUNT(INGRESO_DATOS!$C$126)<>1,LEN(INGRESO_DATOS!$C$127)=0,AND(INGRESO_DATOS!$C$128="SI",OR(COUNT(INGRESO_DATOS!$C$129)<>1,LEN(INGRESO_DATOS!$C$130)=0))),"REQUIERE DATOS",IF(OR(INGRESO_DATOS!$C$126<=0,PRESIONES_SERVICIO!$B$44<0),"DATOS INVÁLIDOS",IF(MOTOR_H_S!AY8>=INGRESO_DATOS!$C$126,"CUMPLE","NO CUMPLE")))))))),"")
```

**MOTOR_H_S!BE8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(COUNTIF(MOTOR_H_S!BV8:BY8,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(MOTOR_H_S!BV8:BY8,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(MOTOR_H_S!BV8:BY8,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(MOTOR_H_S!BV8:BY8,"REQUIERE DATOS")>0,"REQUIERE DATOS",IF(COUNTIF(MOTOR_H_S!BV8:BY8,"NO APLICA")=4,"NO APLICA","CUMPLE")))))),"")
```

**MOTOR_H_S!BV8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DERIVADOS_S!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_S!AD8,IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_ESPECTRAL_S!$BN$8=0,"NO APLICA",IF(MOTOR_ESPECTRAL_S!$BM$8<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(INGRESO_DATOS!$C$131)<>1,LEN(INGRESO_DATOS!$C$132)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!$C$131<=0,"DATOS INVÁLIDOS",IF(MOTOR_ESPECTRAL_S!$BR$8>=INGRESO_DATOS!$C$131,"CUMPLE","NO CUMPLE"))))))),"")
```

**MOTOR_H_S!BW8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DERIVADOS_S!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_S!AD8,IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_ESPECTRAL_S!$BO$8=0,"NO APLICA",IF(MOTOR_ESPECTRAL_S!$BM$8<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(INGRESO_DATOS!$C$131)<>1,LEN(INGRESO_DATOS!$C$132)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!$C$131<=0,"DATOS INVÁLIDOS",IF(MOTOR_ESPECTRAL_S!$BS$8>=INGRESO_DATOS!$C$131,"CUMPLE","NO CUMPLE"))))))),"")
```

**MOTOR_H_S!BX8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DERIVADOS_S!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_S!AD8,IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_ESPECTRAL_S!$BP$8=0,"NO APLICA",IF(MOTOR_ESPECTRAL_S!$BM$8<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(INGRESO_DATOS!$C$131)<>1,LEN(INGRESO_DATOS!$C$132)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!$C$131<=0,"DATOS INVÁLIDOS",IF(MOTOR_ESPECTRAL_S!$BT$8>=INGRESO_DATOS!$C$131,"CUMPLE","NO CUMPLE"))))))),"")
```

**MOTOR_H_S!BY8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DERIVADOS_S!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_S!AD8,IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_ESPECTRAL_S!$BQ$8=0,"NO APLICA",IF(MOTOR_ESPECTRAL_S!$BM$8<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(INGRESO_DATOS!$C$131)<>1,LEN(INGRESO_DATOS!$C$132)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!$C$131<=0,"DATOS INVÁLIDOS",IF(MOTOR_ESPECTRAL_S!$BU$8>=INGRESO_DATOS!$C$131,"CUMPLE","NO CUMPLE"))))))),"")
```

**MOTOR_H_S!DH8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DS_INPUT!A8="NO","",IF(LEN(MOTOR_H_S!AY8)=0,"",MOTOR_H_S!AY8)),"")
```

**MOTOR_H_S!DI8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DS_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_S!AZ8)=0,"",MOTOR_H_S!AZ8)),"")
```

**MOTOR_H_S!DS8**

```excel
=MOTOR_ESPECTRAL_S!$DS$8
```

**MOTOR_H_S!DT8**

```excel
=MOTOR_ESPECTRAL_S!$DT$8
```

**MOTOR_H_S!DU8**

```excel
=MOTOR_ESPECTRAL_S!$DU$8
```

**MOTOR_H_S!DV8**

```excel
=MOTOR_ESPECTRAL_S!$DV$8
```

**MOTOR_H_S!DW8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DS_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_S!W8)=0,"",MOTOR_H_S!W8)),"")
```

**MOTOR_H_S!DX8**

```excel
=MOTOR_ESPECTRAL_S!$DX$8
```

**MOTOR_H_S!DY8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DS_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_S!X8)=0,"",MOTOR_H_S!X8)),"")
```

**MOTOR_H_S!DZ8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DS_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_S!Y8)=0,"",MOTOR_H_S!Y8)),"")
```

**MOTOR_H_S!EB8**

```excel
=IF(AND(DS_INPUT!A8="SI",DERIVADOS_S!A8="SI"),IF(DS_INPUT!A8="NO","NO APLICA",IF(MOTOR_ESPECTRAL_S!$BZ$8="NO","NO APLICA",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"DATOS INVÁLIDOS")+COUNTIF(MOTOR_H_S!DS8:DZ8,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(MOTOR_H_S!DS8:DZ8,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(MOTOR_H_S!DS8:DZ8,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")>0,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(MOTOR_H_S!DS8:DZ8,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(MOTOR_H_S!DS8:DZ8,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"REQUIERE DATOS")+COUNTIF(MOTOR_H_S!DS8:DZ8,"REQUIERE DATOS")>0,"REQUIERE DATOS",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"NO CUMPLE")+COUNTIF(MOTOR_H_S!DS8:DZ8,"NO CUMPLE")>0,"NO CUMPLE","CUMPLE")))))))),"")
```

**CONTROL_E030_F8!B12**

```excel
=IF(OR(NOT(OR(B7="REGULAR",B7="IRREGULAR")),LEN(B8)=0),"REQUIERE DEFINIR REGULARIDAD",IF(OR(NOT(OR(B9="SI",B9="NO")),LEN(B10)=0),"REQUIERE DEFINIR SISTEMAS NO PARALELOS","OK"))
```

**CONTROL_E030_F8!B17**

```excel
=IF(OR(AND(ISNUMBER(INGRESO_DATOS!C42),INGRESO_DATOS!C42>0,ISNUMBER(INGRESO_DATOS!C43),INGRESO_DATOS!C43>0),B14="ELEMENTO VERTICAL",B14="GRAN LUZ",B14="PRE/POSTENSADO",B14="VOLADIZO/SALIENTE"),IF(B15="SI","OK","REQUIERE COMPONENTE VERTICAL OBLIGATORIA"),IF(AND(B14="OTRO DOCUMENTADO",OR(B15="SI",B15="NO"),LEN(B16)>0),"OK","REQUIERE DEFINIR COMPONENTE VERTICAL"))
```

**CONTROL_E030_F8!B19**

```excel
=IF(CONTROL_FASE7!B10<>"OK",CONTROL_FASE7!B10,IF(CONTROL_FASE7!B7="E.030 MODIFICADA RM 183-2026","SRSS 100/30 E.030 — SOLO MODAL ESPECTRAL","DIRECCIONES SEGÚN E.030 ANTERIOR"))
```

**CONTROL_E030_F8!B26**

```excel
=CONTROL_FASE7!B10
```

**FUENTES_E030!D8**

```excel
=IF(AND(COUNT(B8,C8)=2,B8>0),C8/B8,"")
```

**FUENTES_E030!H8**

```excel
=IF(AND(COUNT(F8,G8)=2,F8>0),G8/F8,"")
```

**FUENTES_E030!Q8**

```excel
=IF(AND(ISNUMBER(O8),ISNUMBER(P8)),O8*P8,"")
```

**FUENTES_E030!R8**

```excel
=IF(AND(COUNT(O8,N8)=2,O8>0,N8>0,OR(CONTROL_E030_F8!$B$7="REGULAR",CONTROL_E030_F8!$B$7="IRREGULAR")),MAX(1,IF(CONTROL_E030_F8!$B$7="REGULAR",0.8,0.9)*N8/O8),"")
```

**FUENTES_E030!V8**

```excel
=IF(AND(ISNUMBER(T8),ISNUMBER(U8)),T8*U8,"")
```

**FUENTES_E030!W8**

```excel
=IF(AND(COUNT(T8,S8)=2,T8>0,S8>0,OR(CONTROL_E030_F8!$B$7="REGULAR",CONTROL_E030_F8!$B$7="IRREGULAR")),MAX(1,IF(CONTROL_E030_F8!$B$7="REGULAR",0.8,0.9)*S8/T8),"")
```

**FUENTES_E030!Z8**

```excel
=IF(A8="","REQUIERE FUENTE MODAL",IF(OR(COUNT(B8,C8,E8,F8,G8,I8)<>6,B8<=0,F8<=0,LEN(J8)=0),"REQUIERE DATOS MASA MODAL",IF(OR(C8<0,G8<0,C8>B8,G8>F8,MOD(E8,1)<>0,MOD(I8,1)<>0),"DATOS INVÁLIDOS MASA MODAL",IF(OR(D8<0.9,H8<0.9,E8<3,I8<3),"NO CUMPLE FUENTE E.030","OK"))))
```

**FUENTES_E030!AA8**

```excel
=IF(AND(OR(K8="CQC",K8="ALTERNATIVO ART.42.3"),L8="SI",LEN(M8)>0),"OK","REQUIERE COMBINACIÓN MODAL DOCUMENTADA")
```

**FUENTES_E030!AB8**

```excel
=IF(NOT(AND(COUNT(N8,O8,P8,S8,T8,U8,R8,W8)=8,MIN(N8,O8,P8,S8,T8,U8)>0,OR(CONTROL_E030_F8!$B$7="REGULAR",CONTROL_E030_F8!$B$7="IRREGULAR"),LEN(CONTROL_E030_F8!$B$8)>0,LEN(AF8)>0)),"REQUIERE TRAZABILIDAD VEST / VDIN",IF(OR(P8<R8-0.0000000001,U8<W8-0.0000000001,Q8<IF(CONTROL_E030_F8!$B$7="REGULAR",0.8,0.9)*N8-0.0000000001,V8<IF(CONTROL_E030_F8!$B$7="REGULAR",0.8,0.9)*S8-0.0000000001),"REQUIERE ESCALAMIENTO E.030",IF(NOT(IF(OR(MAX(R8,W8)>1+0.0000000001,OR(P8>1+0.0000000001,U8>1+0.0000000001)),AND(X8="APLICADO",LEN(Y8)>0),OR(AND(X8="NO REQUERIDO",ABS(P8-1)<0.0000000001,ABS(U8-1)<0.0000000001),AND(X8="APLICADO",LEN(Y8)>0)))),"REQUIERE DEFINIR ESTADO ART.44",IF(AND(AD8="ESCALAMIENTO CONSERVADOR ADICIONAL",LEN(AE8)=0),"REQUIERE JUSTIFICACIÓN SOBRESCALA","OK"))))
```

**FUENTES_E030!AC8**

```excel
=IF(A8="","NO APLICA",IF(COUNTIF($A$8:$A$67,A8)<>1,"DATOS INVÁLIDOS — FUENTE DUPLICADA",IF(Z8<>"OK",Z8,IF(AA8<>"OK",AA8,AB8))))
```

**FUENTES_E030!AD8**

```excel
=IF(COUNT(P8,U8,R8,W8)<>4,"REQUIERE DATOS",IF(OR(P8>R8*(1+CONTROL_E030_F8!$B$32),U8>W8*(1+CONTROL_E030_F8!$B$32)),"ESCALAMIENTO CONSERVADOR ADICIONAL","SIN SOBRESCALA SIGNIFICATIVA"))
```

**DEMANDAS_E030!A8**

```excel
=COMBOS_ULTIMOS!A8
```

**DEMANDAS_E030!C8**

```excel
=COMBOS_ULTIMOS!B8
```

**DEMANDAS_E030!S8**

```excel
=IF(CONTROL_FASE7!B10<>"OK",CONTROL_FASE7!B10,IF(CONTROL_E030_F8!B12<>"OK",CONTROL_E030_F8!B12,IF(CONTROL_FASE7!B7="E.030 MODIFICADA RM 183-2026",IF(CONTROL_E030_F8!B9="SI",IF(AND(COMBOS_ULTIMOS!BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(COMBOS_ULTIMOS!BU8)>0,LEN(CONTROL_E030_F8!B11)>0),"OK","REQUIERE EJES NO PARALELOS — PROCEDIMIENTO EXTERNO"),"OK"),IF(CONTROL_E030_F8!B7="IRREGULAR",IF(AND(COMBOS_ULTIMOS!BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(COMBOS_ULTIMOS!BU8)>0),"OK","REQUIERE DIRECCIÓN DESFAVORABLE EXTERNA"),"OK"))))
```

**DEMANDAS_E030!T8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",NOT(OR(COMBOS_ULTIMOS!BP8="LINEAR STATIC",COMBOS_ULTIMOS!BP8="NONLINEAR STATIC")),CONTROL_FASE7!B7<>"E.030 MODIFICADA RM 183-2026"),"NO APLICA",IF(OR(E8<>"SI",LEN(F8)=0),"REQUIERE MÉTODO ESTÁTICO ADMISIBLE ART.33.2",IF(OR(G8<>"SI",LEN(H8)=0),"REQUIERE COMBINACIÓN DIRECCIONAL ESTÁTICA","OK")))
```

**DEMANDAS_E030!U8**

```excel
=IF(AND(I8="SI",J8="SI",LEN(K8)>0,L8="SI",M8="SI",LEN(N8)>0),"OK","REQUIERE PROCEDIMIENTO EXTERNO DOCUMENTADO — EXCENTRICIDAD X100/Y100")
```

**DEMANDAS_E030!V8**

```excel
=IF(NOT(COMBOS_ULTIMOS!BR8="SI"),"NO APLICA",IF(OR(LEN(D8)=0,COUNTIF(FUENTES_E030!$A$8:$A$67,D8)<>1),"REQUIERE FUENTE MODAL ÚNICA",INDEX(FUENTES_E030!$AC$8:$AC$67,MATCH(D8,FUENTES_E030!$A$8:$A$67,0))))
```

**DEMANDAS_E030!W8**

```excel
=VERTICAL_F9!AA8
```

**DEMANDAS_E030!Y8**

```excel
=IF(A8<>"SI","NO APLICA",IF(NOT(OR(COMBOS_ULTIMOS!BT8="SI",COMBOS_ULTIMOS!BR8="SI")),"OK",IF(S8<>"OK",S8,IF(AND(T8<>"OK",T8<>"NO APLICA"),T8,IF(U8<>"OK",U8,IF(AND(V8<>"OK",V8<>"NO APLICA"),V8,IF(W8<>"OK",W8,IF(AND(X8<>"OK",X8<>"NO APLICA"),X8,"OK"))))))))
```

**DEMANDAS_E030!Z8**

```excel
=IF(COMBOS_ULTIMOS!BS8="D. RESULTADO EXTERNO YA COMBINADO",COMBOS_ULTIMOS!BU8,"")
```

**DEMANDAS_E030!AA8**

```excel
=IF(COMBOS_ULTIMOS!BR8="SI",IF(COMBOS_ULTIMOS!BS8="D. RESULTADO EXTERNO YA COMBINADO","RESULTADO EXTERNO DOCUMENTADO","ENVOLVENTE CONSERVADORA DE SIGNOS"),"VECTOR CONCURRENTE / ESTÁTICO FIRMADO")
```

**DEMANDAS_E030!AB8**

```excel
=IF(CONTROL_FASE7!B10<>"OK",CONTROL_FASE7!B10,IF(CONTROL_FASE7!B7="E.030 MODIFICADA RM 183-2026",IF(COMBOS_ULTIMOS!BR8="SI","SRSS 100/30 E.030","SUMA ABS 100/30 E.030 ART.33.3"),"E.030 ANTERIOR — DIRECCIONES DOCUMENTADAS"))
```

**DEMANDAS_E030!AC8**

```excel
=IF(AND(OR(COMBOS_ULTIMOS!C8="SISMO",COMBOS_ULTIMOS!BT8="SI",OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA")),VERTICAL_F9!B8="A. ESTÁTICA ART.38.1",VERTICAL_F9!Y8="NO"),"SI","NO")
```

**DEMANDAS_E030!AD8**

```excel
=IF(AND(A8="SI",COMBOS_ULTIMOS!BR8="SI",COUNTIF(FUENTES_E030!$A$8:$A$67,D8)=1),INDEX(FUENTES_E030!$AD$8:$AD$67,MATCH(D8,FUENTES_E030!$A$8:$A$67,0)),"NO APLICA")
```

**DEMANDAS_E030!Q68**

```excel
=COMBOS_SERVICIO!AI8
```

**DEMANDAS_E030!R68**

```excel
=IF(LEN(COMBOS_SERVICIO!AC8)>0,COMBOS_SERVICIO!AC8,"")
```

**DEMANDAS_E030!X68**

```excel
=IF(NOT(ISNUMBER(COMBOS_SERVICIO!L8)),"DATOS INVÁLIDOS — FACTOR SUELO NO NUMÉRICO",IF(CONTROL_FASE7!B7<>"E.030 MODIFICADA RM 183-2026","NO APLICA",IF(Q68="NO",IF(ABS(COMBOS_SERVICIO!L8-0.8)<0.0000000001,"OK","DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO"),IF(Q68="SI",IF(AND(ABS(COMBOS_SERVICIO!L8-1)<0.0000000001,LEN(R68)>0),"OK","DATOS INVÁLIDOS — DOBLE REDUCCIÓN O REFERENCIA 0.80 FALTANTE"),"REQUIERE DEFINIR REDUCCIÓN 0.80"))))
```

**DEMANDAS_E030!Y68**

```excel
=IF(A68<>"SI","NO APLICA",IF(NOT(OR(COMBOS_SERVICIO!CM8="SI",COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!C8="SISMO")),"OK",IF(S68<>"OK",S68,IF(AND(T68<>"OK",T68<>"NO APLICA"),T68,IF(U68<>"OK",U68,IF(AND(V68<>"OK",V68<>"NO APLICA"),V68,IF(W68<>"OK",W68,IF(AND(X68<>"OK",X68<>"NO APLICA"),X68,"OK"))))))))
```

**DEMANDAS_E030!AC68**

```excel
=IF(AND(OR(COMBOS_SERVICIO!C8="SISMO",COMBOS_SERVICIO!CM8="SI",OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA")),VERTICAL_F9!B68="A. ESTÁTICA ART.38.1",VERTICAL_F9!Y68="NO"),"SI","NO")
```

**DEMANDAS_E030!AD68**

```excel
=IF(AND(A68="SI",COMBOS_SERVICIO!CK8="SI",COUNTIF(FUENTES_E030!$A$8:$A$67,D68)=1),INDEX(FUENTES_E030!$AD$8:$AD$67,MATCH(D68,FUENTES_E030!$A$8:$A$67,0)),"NO APLICA")
```

**VERTICAL_F9!AA8**

```excel
=IF(CONTROL_E030_F8!B17<>"OK",CONTROL_E030_F8!B17,IF(B8="D. NO APLICA",IF(AC8="NO","OK","REQUIERE COMPONENTE VERTICAL OBLIGATORIA"),IF(NOT(OR(B8="A. ESTÁTICA ART.38.1",B8="B. ESPECTRO VERTICAL ART.41.2",B8="C. RESULTADO EXTERNO DOCUMENTADO")),"REQUIERE DEFINIR MÉTODO VERTICAL",IF(NOT(AND(LEN(C8)>0,LEN(D8)>0,LEN(I8)>0,J8=COMBOS_ULTIMOS!BV8,ISNUMBER(K8),ISNUMBER(COMBOS_ULTIMOS!BX8),ABS(K8-COMBOS_ULTIMOS!BX8)<0.00000001,L8="SI",LEN(M8)>0)),"REQUIERE TRAZABILIDAD VERTICAL / INTERFAZ",IF(NOT(TRUE),"DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80",IF(B8="A. ESTÁTICA ART.38.1",IF(OR(CONTROL_E030_F8!B14="GRAN LUZ",CONTROL_E030_F8!B14="VOLADIZO/SALIENTE"),IF(CONTROL_FASE7!B7="E.030 MODIFICADA RM 183-2026","REQUIERE VERTICAL DINÁMICA ART.38.2","REQUIERE VERTICAL DINÁMICA ART.28.6.2 ANTERIOR"),IF(AND(COUNT(E8:H8,S8:X8)=10,MIN(E8:G8)>0,E8<=1,ABS(H8-2/3)<0.0000000001,OR(Y8="NO",AND(Y8="SI",LEN(Z8)>0,IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),COMBOS_ULTIMOS!BS8="D. RESULTADO EXTERNO YA COMBINADO",TRUE))),TRUE),IF(AND(Y8="NO",COMBOS_ULTIMOS!BS8="D. RESULTADO EXTERNO YA COMBINADO"),"DATOS INVÁLIDOS — VECTOR EXTERNO YA COMBINADO","OK"),IF(CONTROL_FASE7!B7="E.030 MODIFICADA RM 183-2026","REQUIERE VECTOR ESTÁTICO ART.38.1","REQUIERE VECTOR ESTÁTICO ART.28.6.1 ANTERIOR"))),IF(B8="B. ESPECTRO VERTICAL ART.41.2",IF(AND(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),ESPECTROS_U!F8="SI",ESPECTROS_U!E8=C8,COUNT(ESPECTROS_U!AC8:AH8)=6,MIN(ESPECTROS_U!AC8:AH8)>=0,LEN(N8)>0,ISNUMBER(O8),O8>0),"OK","REQUIERE ESPECTRO VERTICAL DOCUMENTADO"),IF(AND(Y8="SI",LEN(Z8)>0,COUNT(S8:X8)=6,COMBOS_ULTIMOS!BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(COMBOS_ULTIMOS!BU8)>0,IF(OR(CONTROL_E030_F8!B14="GRAN LUZ",CONTROL_E030_F8!B14="VOLADIZO/SALIENTE"),AND(P8="SI",LEN(N8)>0,ISNUMBER(O8),O8>0),TRUE)),"OK","REQUIERE COMBINACIÓN VERTICAL EXTERNA DOCUMENTADA"))))))))
```

**VERTICAL_F9!AB8**

```excel
=IF(COUNT(E8:H8)=4,E8*F8*G8*H8,"")
```

**VERTICAL_F9!AC8**

```excel
=CONTROL_E030_F8!B15
```

**VERTICAL_F9!AE8**

```excel
=IF(CONTROL_FASE7!B7="E.030 MODIFICADA RM 183-2026","E.030-2026: 28.4/28.5, 38.1/38.2, 41.2","E.030 anterior: 28.6.1/28.6.2, 29.2")
```

**VERTICAL_F9!AF8**

```excel
=IF(B8="A. ESTÁTICA ART.38.1",IF(Y8="NO","VECTOR FIRMADO: +Ev / -Ev","SENTIDOS ADVERSOS EN FUENTE EXTERNA"),IF(B8="B. ESPECTRO VERTICAL ART.41.2","MÁXIMOS ESTADÍSTICOS — CAJA DE SIGNOS",IF(B8="C. RESULTADO EXTERNO DOCUMENTADO","SIMULTANEIDAD EXTERNA DOCUMENTADA","REQUIERE DEFINIR")))
```

**VERTICAL_F9!AA68**

```excel
=IF(CONTROL_E030_F8!B17<>"OK",CONTROL_E030_F8!B17,IF(B68="D. NO APLICA",IF(AC68="NO","OK","REQUIERE COMPONENTE VERTICAL OBLIGATORIA"),IF(NOT(OR(B68="A. ESTÁTICA ART.38.1",B68="B. ESPECTRO VERTICAL ART.41.2",B68="C. RESULTADO EXTERNO DOCUMENTADO")),"REQUIERE DEFINIR MÉTODO VERTICAL",IF(NOT(AND(LEN(C68)>0,LEN(D68)>0,LEN(I68)>0,J68=COMBOS_SERVICIO!CO8,ISNUMBER(K68),ISNUMBER(COMBOS_SERVICIO!CQ8),ABS(K68-COMBOS_SERVICIO!CQ8)<0.00000001,L68="SI",LEN(M68)>0)),"REQUIERE TRAZABILIDAD VERTICAL / INTERFAZ",IF(NOT(IF(ISNUMBER(AD68),AND(Q68=COMBOS_SERVICIO!AI8,IF(CONTROL_FASE7!B7="E.030 MODIFICADA RM 183-2026",OR(AND(Q68="NO",ABS(AD68-0.8)<0.0000000001),AND(Q68="SI",ABS(AD68-1)<0.0000000001,LEN(R68)>0)),OR(AND(Q68="NO",OR(AD68=0.8,AD68=1)),AND(Q68="SI",AD68=1,LEN(R68)>0)))),FALSE)),"DATOS INVÁLIDOS — REDUCCIÓN VERTICAL 0.80",IF(B68="A. ESTÁTICA ART.38.1",IF(OR(CONTROL_E030_F8!B14="GRAN LUZ",CONTROL_E030_F8!B14="VOLADIZO/SALIENTE"),IF(CONTROL_FASE7!B7="E.030 MODIFICADA RM 183-2026","REQUIERE VERTICAL DINÁMICA ART.38.2","REQUIERE VERTICAL DINÁMICA ART.28.6.2 ANTERIOR"),IF(AND(COUNT(E68:H68,S68:X68)=10,MIN(E68:G68)>0,E68<=1,ABS(H68-2/3)<0.0000000001,OR(Y68="NO",AND(Y68="SI",LEN(Z68)>0,IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),COMBOS_SERVICIO!CL8="D. RESULTADO EXTERNO YA COMBINADO",TRUE))),IF(AND(Y68="NO",NOT(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA")),Q68="NO"),AND(COUNT(AG68:AL68)=6,LEN(AM68)>0),TRUE)),IF(AND(Y68="NO",COMBOS_SERVICIO!CL8="D. RESULTADO EXTERNO YA COMBINADO"),"DATOS INVÁLIDOS — VECTOR EXTERNO YA COMBINADO","OK"),IF(CONTROL_FASE7!B7="E.030 MODIFICADA RM 183-2026","REQUIERE VECTOR ESTÁTICO ART.38.1","REQUIERE VECTOR ESTÁTICO ART.28.6.1 ANTERIOR"))),IF(B68="B. ESPECTRO VERTICAL ART.41.2",IF(AND(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),ESPECTROS_S!F8="SI",ESPECTROS_S!E8=C68,COUNT(ESPECTROS_S!AC8:AH8)=6,MIN(ESPECTROS_S!AC8:AH8)>=0,LEN(N68)>0,ISNUMBER(O68),O68>0),"OK","REQUIERE ESPECTRO VERTICAL DOCUMENTADO"),IF(AND(Y68="SI",LEN(Z68)>0,COUNT(S68:X68)=6,COMBOS_SERVICIO!CL8="D. RESULTADO EXTERNO YA COMBINADO",LEN(COMBOS_SERVICIO!CN8)>0,IF(OR(CONTROL_E030_F8!B14="GRAN LUZ",CONTROL_E030_F8!B14="VOLADIZO/SALIENTE"),AND(P68="SI",LEN(N68)>0,ISNUMBER(O68),O68>0),TRUE)),"OK","REQUIERE COMBINACIÓN VERTICAL EXTERNA DOCUMENTADA"))))))))
```

**VERTICAL_F9!AD68**

```excel
=IF(AND(ISNUMBER(COMBOS_SERVICIO!L8),OR(COMBOS_SERVICIO!L8=0.8,COMBOS_SERVICIO!L8=1)),COMBOS_SERVICIO!L8,"")
```

**VERTICAL_F9!AG68**

```excel
=IF(COMBOS_SERVICIO!W8="","",COMBOS_SERVICIO!W8)
```

**VERTICAL_F9!AH68**

```excel
=IF(COMBOS_SERVICIO!X8="","",COMBOS_SERVICIO!X8)
```

**VERTICAL_F9!AI68**

```excel
=IF(COMBOS_SERVICIO!Y8="","",COMBOS_SERVICIO!Y8)
```

**VERTICAL_F9!AJ68**

```excel
=IF(COMBOS_SERVICIO!Z8="","",COMBOS_SERVICIO!Z8)
```

**VERTICAL_F9!AK68**

```excel
=IF(COMBOS_SERVICIO!AA8="","",COMBOS_SERVICIO!AA8)
```

**VERTICAL_F9!AL68**

```excel
=IF(COMBOS_SERVICIO!AB8="","",COMBOS_SERVICIO!AB8)
```

**VERTICAL_F9!AM68**

```excel
=IF(COMBOS_SERVICIO!AC8="","",COMBOS_SERVICIO!AC8)
```

**DER_EV_U!A8**

```excel
=IF(AND(DEMANDAS_E030!AC8="SI",ESPECTROS_U!A8="SI",OR(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),TRUE)),"SI","NO")
```

**DER_EV_U!B8**

```excel
=ESPECTROS_U!B8&"-X01"&"-Ev"
```

**DER_EV_U!D8**

```excel
=IF(AND(DEMANDAS_E030!AC8="SI",NOT(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"))),IF(LEN(COMBOS_ULTIMOS!AQ8)>0,COMBOS_ULTIMOS!AQ8,COMBOS_ULTIMOS!B8),ESPECTROS_U!C8)
```

**DER_EV_U!E8**

```excel
=IF(AND(DEMANDAS_E030!AC8="SI",NOT(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"))),"",ESPECTROS_U!D8)
```

**DER_EV_U!F8**

```excel
=IF(DEMANDAS_E030!AC8="SI",IF(VERTICAL_F9!C8="","",VERTICAL_F9!C8),ESPECTROS_U!E8)
```

**DER_EV_U!H8**

```excel
=IF(AND(DEMANDAS_E030!AC8="SI",NOT(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"))),"HORIZONTAL FIRMADA EN INTERFAZ; VERTICAL +Ev / -Ev",ESPECTROS_U!AJ8)
```

**DER_EV_U!R8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!K8+L8*(SQRT((I8*ESPECTROS_U!Q8)^2+(J8*ESPECTROS_U!W8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AC8),ESPECTROS_U!AC8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!S8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!L8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!S8*VERTICAL_F9!AD8,0),"")))
```

**DER_EV_U!S8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!L8+M8*(SQRT((I8*ESPECTROS_U!R8)^2+(J8*ESPECTROS_U!X8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AD8),ESPECTROS_U!AD8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!T8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!M8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!T8*VERTICAL_F9!AD8,0),"")))
```

**DER_EV_U!T8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!M8+N8*(SQRT((I8*ESPECTROS_U!S8)^2+(J8*ESPECTROS_U!Y8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AE8),ESPECTROS_U!AE8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!U8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!N8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!U8*VERTICAL_F9!AD8,0),"")))
```

**DER_EV_U!U8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!N8+O8*(SQRT((I8*ESPECTROS_U!T8)^2+(J8*ESPECTROS_U!Z8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AF8),ESPECTROS_U!AF8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!V8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!O8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!V8*VERTICAL_F9!AD8,0),"")))
```

**DER_EV_U!V8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!O8+P8*(SQRT((I8*ESPECTROS_U!U8)^2+(J8*ESPECTROS_U!AA8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AG8),ESPECTROS_U!AG8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!W8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!P8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!W8*VERTICAL_F9!AD8,0),"")))
```

**DER_EV_U!W8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_U!P8+Q8*(SQRT((I8*ESPECTROS_U!V8)^2+(J8*ESPECTROS_U!AB8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AH8),ESPECTROS_U!AH8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!X8*VERTICAL_F9!AD8,0),""),IF(Z8="OK",COMBOS_ULTIMOS!Q8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!X8*VERTICAL_F9!AD8,0),"")))
```

**DER_EV_U!AD8**

```excel
=IF($A8<>"SI","",IF($Z8="OK",IF(ABS($W8)>zap7_mz_tol,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA","OK"),$Z8))
```

**DU_EV_MENOS!A8**

```excel
=IF(AND(DEMANDAS_E030!AC8="SI",ESPECTROS_U!A8="SI",OR(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),TRUE)),"SI","NO")
```

**DU_EV_MENOS!B8**

```excel
=ESPECTROS_U!B8&"-"&IF(0=0,"X","Y")&TEXT((0*32+IF(ESPECTROS_U!L8<0,16,0)+IF(ESPECTROS_U!M8<0,8,0)+0*4+0*2+IF(ESPECTROS_U!P8<0,1,0))+1,"00")&"-Ev"
```

**DU_EV_MENOS!L8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!K8+1*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!Q8)^2+(0.3*ESPECTROS_U!W8)^2),ESPECTROS_U!Q8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AC8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!S8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!L8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!S8*VERTICAL_F9!AD8,0),""))
```

**DU_EV_MENOS!M8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!L8+IF(ESPECTROS_U!L8<0,-1,1)*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!R8)^2+(0.3*ESPECTROS_U!X8)^2),ESPECTROS_U!R8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AD8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!T8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!M8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!T8*VERTICAL_F9!AD8,0),""))
```

**DU_EV_MENOS!N8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!M8+IF(ESPECTROS_U!M8<0,-1,1)*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!S8)^2+(0.3*ESPECTROS_U!Y8)^2),ESPECTROS_U!S8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AE8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!U8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!N8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!U8*VERTICAL_F9!AD8,0),""))
```

**DU_EV_MENOS!O8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!N8+1*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!T8)^2+(0.3*ESPECTROS_U!Z8)^2),ESPECTROS_U!T8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AF8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!V8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!O8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!V8*VERTICAL_F9!AD8,0),""))
```

**DU_EV_MENOS!P8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!O8+1*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!U8)^2+(0.3*ESPECTROS_U!AA8)^2),ESPECTROS_U!U8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AG8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!W8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!P8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!W8*VERTICAL_F9!AD8,0),""))
```

**DU_EV_MENOS!Q8**

```excel
=IF(OR(COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_U!AI8="OK",ESPECTROS_U!P8+IF(ESPECTROS_U!P8<0,-1,1)*(IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_U!V8)^2+(0.3*ESPECTROS_U!AB8)^2),ESPECTROS_U!V8)+IF(AND(VERTICAL_F9!B8="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_U!F8="SI"),ESPECTROS_U!AH8,0))+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!X8*VERTICAL_F9!AD8,0),""),IF(ESPECTROS_U!AI8="OK",COMBOS_ULTIMOS!Q8+IF(DEMANDAS_E030!AC8="SI",-1*VERTICAL_F9!X8*VERTICAL_F9!AD8,0),""))
```

**DER_EV_S!D8**

```excel
=IF(AND(DEMANDAS_E030!AC68="SI",NOT(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"))),IF(LEN(COMBOS_SERVICIO!BD8)>0,COMBOS_SERVICIO!BD8,COMBOS_SERVICIO!B8),ESPECTROS_S!C8)
```

**DER_EV_S!E8**

```excel
=IF(AND(DEMANDAS_E030!AC68="SI",NOT(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"))),"",ESPECTROS_S!D8)
```

**DER_EV_S!F8**

```excel
=IF(DEMANDAS_E030!AC68="SI",IF(VERTICAL_F9!C68="","",VERTICAL_F9!C68),ESPECTROS_S!E8)
```

**DER_EV_S!H8**

```excel
=IF(AND(DEMANDAS_E030!AC68="SI",NOT(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"))),"HORIZONTAL FIRMADA EN INTERFAZ; VERTICAL +Ev / -Ev",ESPECTROS_S!AJ8)
```

**DER_EV_S!R8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!K8+L8*((SQRT((I8*ESPECTROS_S!Q8)^2+(J8*ESPECTROS_S!W8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AC8),ESPECTROS_S!AC8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!S68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AG68+(COMBOS_SERVICIO!Q8-VERTICAL_F9!AG68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!Q8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!S68*VERTICAL_F9!AD68,0),"")))
```

**DER_EV_S!S8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!L8+M8*((SQRT((I8*ESPECTROS_S!R8)^2+(J8*ESPECTROS_S!X8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AD8),ESPECTROS_S!AD8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!T68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AH68+(COMBOS_SERVICIO!R8-VERTICAL_F9!AH68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!R8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!T68*VERTICAL_F9!AD68,0),"")))
```

**DER_EV_S!T8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!M8+N8*((SQRT((I8*ESPECTROS_S!S8)^2+(J8*ESPECTROS_S!Y8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AE8),ESPECTROS_S!AE8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!U68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AI68+(COMBOS_SERVICIO!S8-VERTICAL_F9!AI68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!S8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!U68*VERTICAL_F9!AD68,0),"")))
```

**DER_EV_S!U8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!N8+O8*((SQRT((I8*ESPECTROS_S!T8)^2+(J8*ESPECTROS_S!Z8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AF8),ESPECTROS_S!AF8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!V68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AJ68+(COMBOS_SERVICIO!T8-VERTICAL_F9!AJ68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!T8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!V68*VERTICAL_F9!AD68,0),"")))
```

**DER_EV_S!V8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!O8+P8*((SQRT((I8*ESPECTROS_S!U8)^2+(J8*ESPECTROS_S!AA8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AG8),ESPECTROS_S!AG8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!W68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AK68+(COMBOS_SERVICIO!U8-VERTICAL_F9!AK68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!U8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!W68*VERTICAL_F9!AD68,0),"")))
```

**DER_EV_S!W8**

```excel
=IF(A8<>"SI","",IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(Z8="OK",ESPECTROS_S!P8+Q8*((SQRT((I8*ESPECTROS_S!V8)^2+(J8*ESPECTROS_S!AB8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AH8),ESPECTROS_S!AH8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!X68*VERTICAL_F9!AD68,0),""),IF(Z8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AL68+(COMBOS_SERVICIO!V8-VERTICAL_F9!AL68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!V8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!X68*VERTICAL_F9!AD68,0),"")))
```

**DER_EV_S!AD8**

```excel
=IF($A8<>"SI","",IF($Z8="OK",IF(ABS($W8)>zap7_mz_tol,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA","OK"),$Z8))
```

**DS_EV_MENOS!A8**

```excel
=IF(AND(DEMANDAS_E030!AC68="SI",ESPECTROS_S!A8="SI",OR(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),TRUE)),"SI","NO")
```

**DS_EV_MENOS!B8**

```excel
=ESPECTROS_S!B8&"-"&IF(0=0,"X","Y")&TEXT((0*32+IF(ESPECTROS_S!L8<0,16,0)+IF(ESPECTROS_S!M8<0,8,0)+0*4+0*2+IF(ESPECTROS_S!P8<0,1,0))+1,"00")&"-Ev"
```

**DS_EV_MENOS!L8**

```excel
=1
```

**DS_EV_MENOS!M8**

```excel
=IF(LEN(COMBOS_SERVICIO!M8)=0,"",COMBOS_SERVICIO!M8)
```

**DS_EV_MENOS!N8**

```excel
=IF(LEN(COMBOS_SERVICIO!N8)=0,"",COMBOS_SERVICIO!N8)
```

**DS_EV_MENOS!O8**

```excel
=ESPECTROS_S!AI8
```

**DS_EV_MENOS!P8**

```excel
=IF(LEN(COMBOS_SERVICIO!P8)=0,"",COMBOS_SERVICIO!P8)
```

**DS_EV_MENOS!Q8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!K8+1*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!Q8)^2+(0.3*ESPECTROS_S!W8)^2),ESPECTROS_S!Q8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AC8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!S68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AG68+(COMBOS_SERVICIO!Q8-VERTICAL_F9!AG68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!Q8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!S68*VERTICAL_F9!AD68,0),""))
```

**DS_EV_MENOS!R8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!L8+IF(ESPECTROS_S!L8<0,-1,1)*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!R8)^2+(0.3*ESPECTROS_S!X8)^2),ESPECTROS_S!R8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AD8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!T68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AH68+(COMBOS_SERVICIO!R8-VERTICAL_F9!AH68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!R8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!T68*VERTICAL_F9!AD68,0),""))
```

**DS_EV_MENOS!S8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!M8+IF(ESPECTROS_S!M8<0,-1,1)*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!S8)^2+(0.3*ESPECTROS_S!Y8)^2),ESPECTROS_S!S8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AE8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!U68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AI68+(COMBOS_SERVICIO!S8-VERTICAL_F9!AI68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!S8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!U68*VERTICAL_F9!AD68,0),""))
```

**DS_EV_MENOS!T8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!N8+1*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!T8)^2+(0.3*ESPECTROS_S!Z8)^2),ESPECTROS_S!T8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AF8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!V68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AJ68+(COMBOS_SERVICIO!T8-VERTICAL_F9!AJ68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!T8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!V68*VERTICAL_F9!AD68,0),""))
```

**DS_EV_MENOS!U8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!O8+1*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!U8)^2+(0.3*ESPECTROS_S!AA8)^2),ESPECTROS_S!U8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AG8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!W68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AK68+(COMBOS_SERVICIO!U8-VERTICAL_F9!AK68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!U8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!W68*VERTICAL_F9!AD68,0),""))
```

**DS_EV_MENOS!V8**

```excel
=IF(OR(COMBOS_SERVICIO!CK8="SI",COMBOS_SERVICIO!CI8="RESPONSE SPECTRUM",COMBOS_SERVICIO!CL8="B. ESPECTRO DE RESPUESTA"),IF(ESPECTROS_S!AI8="OK",ESPECTROS_S!P8+IF(ESPECTROS_S!P8<0,-1,1)*((IF(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",SQRT((1*ESPECTROS_S!V8)^2+(0.3*ESPECTROS_S!AB8)^2),ESPECTROS_S!V8)+IF(AND(VERTICAL_F9!B68="B. ESPECTRO VERTICAL ART.41.2",ESPECTROS_S!F8="SI"),ESPECTROS_S!AH8,0))*COMBOS_SERVICIO!L8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!X68*VERTICAL_F9!AD68,0),""),IF(ESPECTROS_S!AI8="OK",IF(VERTICAL_F9!Q68="NO",VERTICAL_F9!AL68+(COMBOS_SERVICIO!V8-VERTICAL_F9!AL68)*VERTICAL_F9!AD68,COMBOS_SERVICIO!V8)+IF(DEMANDAS_E030!AC68="SI",-1*VERTICAL_F9!X68*VERTICAL_F9!AD68,0),""))
```

**MOTOR_EV_U!A8**

```excel
=IF(DU_EV_MENOS!A8="SI",IF(AND(AQV8="OK",COUNT(CZ8:DC8,DZ8:EC8)=8),MAX(IF(DZ8>0,CZ8/DZ8,0),IF(EA8>0,DA8/EA8,0),IF(EB8>0,DB8/EB8,0),IF(EC8>0,DC8/EC8,0)),""),"")
```

**MOTOR_EV_U!A9**

```excel
=IF(DU_EV_MENOS!A9="SI",IF(AND(AQV9="OK",COUNT(CZ9:DC9,DZ9:EC9)=8),MAX(IF(DZ9>0,CZ9/DZ9,0),IF(EA9>0,DA9/EA9,0),IF(EB9>0,DB9/EB9,0),IF(EC9>0,DC9/EC9,0)),""),"")
```

**MOTOR_HEV_S!DH8**

```excel
=IF(AND(DS_EV_MENOS!A8="SI",DER_EV_S!A8="SI"),IF(DS_EV_MENOS!A8="NO","",IF(LEN(MOTOR_HEV_S!AY8)=0,"",MOTOR_HEV_S!AY8)),"")
```
