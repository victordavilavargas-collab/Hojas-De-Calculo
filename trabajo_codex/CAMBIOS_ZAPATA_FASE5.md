# Fase 5 — motor multicombo y envolventes de zapata aislada

Fecha: 2026-10-01. Base: `main`, commit `79aa54f37c4b435c2141f1e484897523c51d57fe`, Fase 4. Repositorio: victordavilavargas-collab/Hojas-De-Calculo.

La plantilla ahora recibe hasta **60 vectores últimos completos y 60 vectores de servicio completos**, calcula cada fila independientemente y obtiene gobernantes de los resultados. La conexión conserva el Modo B externo de F4 y se extiende a 60 análisis y una matriz de **60 barras × 60 combinaciones**. El selector de diagramas no interviene en las envolventes.

No se cambiaron dimensiones, materiales, cargas originales ni detalle para obtener CUMPLE. El libro entregado contiene únicamente los dos registros completos migrados de F4; las demás combinaciones están inactivas. Los datos sintéticos de verificación no se guardaron en el entregable. Estado actual: **REQUIERE DATOS**, conexión **REQUIERE DATOS**, cuerpo de zapata **NO CUMPLE**.

## 1. Arquitectura y conservación

F4 tenía 17 hojas, 24 gráficos y 456 nombres: un vector último, otro de servicio, un análisis externo y una fuerza por barra. F5 tiene **57 hojas, 24 gráficos y 510 nombres**. Mantiene las 17 hojas originales y todos sus objetos gráficos. Los datos de `INGRESO_DATOS!C14:C188` y `CARGAS!C7:C38` se compararon exactamente; el original y las cuatro fases previas permanecen intactos por SHA-256.

Flujo de cálculo:

`COMBOS completos → MAPEO/normalización → MU_*/MS_* independientes → RESULTADOS_* → ENVOLVENTES`

`Geometría real de barras + CONEXION_COMBOS + FUERZAS_BARRAS → conexión por combo → CALC_ENV_BARRAS → ENV_BARRAS`

`ENVOLVENTES → VISTA_COMBO → módulos/diagramas originales seleccionados`

El grafo de dependencias de F4 identificó 1251 celdas variables necesarias por combinación última y 85 por combinación de servicio. Sus fórmulas se traducen a 60 bloques independientes. Materiales, dimensiones y detalle que no dependen de las acciones se comparten. No hay macros, tablas de datos iterativas ni resultados pegados como sustituto de fórmulas. Hay 164381 fórmulas; longitud máxima 6739 caracteres, inferior al límite 8192.

| Hoja nueva visible | Función |
|---|---|
| MAPEO_IMPORTACION | Correspondencias, signos y fuentes separados ETABS/SAP |
| COMBOS_ULTIMOS | 60 vectores, activación, ID, origen, observación, estado y vista global |
| COMBOS_SERVICIO | 60 vectores, tipo, qadm, factor CS, incremento y seis componentes CS |
| CONEXION_COMBOS | Análisis externo completo asociado al ID real de cada último |
| FUERZAS_BARRAS | 3600 fuerzas firmadas; filas por ID real de barra |
| RESULTADOS_ULTIMOS | 255 columnas por combo, estados y auxiliares de admisión en envolventes |
| RESULTADOS_SERVICIO | 71 columnas por combo, estados y auxiliares |
| ENVOLVENTES | 46 controles, gobernantes, demandas, capacidades, D/C, pendientes, barras y adopción |
| ENV_BARRAS | Tracción, compresión, esfuerzo, inversión, empalme y anclaje por barra |
| VISTA_COMBO | Selectores AUTO/MANUAL independientes para último y servicio |
| ANALISIS_COMPLEMENTARIO | Análisis eta del ID citado y adopción separada |
| GUIA_MULTICOMBO | Procedimiento, convenciones, estados y alcance |

Los auxiliares ordinarios ocultos se pueden mostrar desde Excel: `CALC_ENV_BARRAS`, 13 `MU_*`, 5 `MS_*` y 9 `MC_*`. Los resultados extensos agrupan columnas sin eliminar datos. Las tablas de entrada y conexión usan filas **8:67**. `FUERZAS_BARRAS!C8:BJ67` contiene las fuerzas; las columnas A/B muestran ID y estado de la geometría, y la fila 6 identifica el combo.

En MU/MS, una celda original de fila r queda en `r+3+(i−1)·(alto_F4+5)`. El encabezado de cada bloque identifica su posición; el ID verdadero procede de COMBOS fila i+7. Las fórmulas INDEX usan rangos acotados al motor, evitando columnas completas. Se comprobó la apertura normal desde una instancia nueva de Excel.

Hojas originales modificadas: `ACERO_DETALLADO`, `BARRAS_CONEXION`, `CARGAS`, `CONEXION_COLUMNA_ZAPATA`, `CORTANTE_UNIDIRECCIONAL`, `DIAGRAMAS_X`, `DIAGRAMAS_Y`, `FLEXION_ACERO`, `GRAFICOS`, `PRESIONES_SERVICIO`, `PRESIONES_ULTIMAS`, `PUNZONAMIENTO`, `RESULTANTE`, `RESUMEN`. Se convirtieron las salidas variables en vistas del combo seleccionado y se añadieron enlaces/resúmenes visibles. `BARRAS_CONEXION!M12:M71` pasa a ser una vista azul: las fuerzas se ingresan en la matriz nueva. `CONEXION_COLUMNA_ZAPATA` conserva los datos comunes del plano, materiales y detalle; las resultantes y el análisis seleccionado se muestran en azul. `RESUMEN` distingue cuerpo/conexión del combo mostrado y el estado global multicombo.

## 2. Ingreso, unidades y mapeo

Fuerzas en tf; momentos en tf·m; geometría en m o cm según rótulo; áreas de acero en cm² o cm²/m; esfuerzos en kgf/cm². Los usuarios no ingresan N, kN ni MPa. Las constantes de conversión necesarias para las expresiones de E.060 son internas y los resultados vuelven a las unidades rotuladas.

Cada fila activa requiere `SI`, ID textual único y **seis números**: P, Fx/Fy o V2/V3, y tres momentos. Un cero numérico es válido; una celda vacía no equivale a cero. Duplicados, texto en componentes y correspondencias repetidas producen DATOS INVÁLIDOS. Campos ausentes producen REQUIERE DATOS. `NO` ignora residuos de la fila, incluidos errores de datos que no participan. No se calcula un vector artificial con máximos de P, Mx y My de filas diferentes.

MANUAL/OTRO reciben `P,Fx,Fy,Mx,My,Mz` ya globales. ETABS/SAP reciben crudos en el orden **P,V2,V3,T,M2,M3**. Es necesario declarar la correspondencia y su fuente, porque dependen de la orientación de ejes del modelo y de la tabla exportada.

| Componente cruda | Destino inicial | Ubicación ETABS | Ubicación SAP |
|---|---|---|---|
| P | P | fila 8 | fila 15 |
| V2 | Fx | fila 9 | fila 16 |
| V3 | Fy | fila 10 | fila 17 |
| T | Mz | fila 11 | fila 18 |
| M2 | Mx | fila 12 | fila 19 |
| M3 | My | fila 13 | fila 20 |

En MAPEO_IMPORTACION, C es destino, D signo ±1 y E referencia. Se admite intercambiar V2/V3 y M2/M3, conservando una correspondencia biyectiva. Los valores crudos permanecen visibles e intactos; la normalización aparece en columnas separadas. Los datos migrados de F4 se marcan MANUAL porque ya incorporan la interpretación global original; no se vuelven a mapear ni a cambiar de signo.

P positivo actúa hacia abajo. Con traslado habilitado desde altura zh:

```text
Mx_plano = Mx − Fy·zh
My_plano = My + Fx·zh
Mx_origen = Mx_plano − P·yc
My_origen = My_plano + P·xc
q(x,y) = Q/A + My_origen·x/Iy − Mx_origen·y/Ix
```

Se usan acciones firmadas hasta calcular máximos/mínimos pertinentes. F4 denomina `res_u_mx_tot` al primer momento `P·yc−Mx`; la columna pública Mx_origen muestra su opuesto físico. Esto corrige la etiqueta/signo de exposición, manteniendo intacto el equilibrio de F4. Mz no se convierte en Mx/My; los controles no implementados conservan su bloqueo.

En servicio, factor 0,80 solo se admite en SISMO con **seis componentes CS numéricos y referencia**: `vector_resultante = vector_total + (factor−1)·CS`. Se normalizan también esos componentes con el mismo mapa. No se reduce indiscriminadamente todo el vector. El selector toma valores numéricos 1 y 0,8 desde una lista de celdas, compatible con el separador decimal de Excel español. Incremento de qadm requiere SI, tipo SISMO/VIENTO y fuente explícita: `qadm_aplicada=1,30·qadm`. No se fabrica automáticamente una combinación 9.2 sin sus componentes reales.

## 3. Verificaciones independientes y envolventes

Por cada último se conservan acciones trasladadas, resultante, cuatro presiones físicas y extremas, dominio y contacto, momentos de caras, cuatro cortantes, punzonamiento, ocho requisitos de acero y distribución regional, estados del cuerpo y conexión.

El punzonamiento registra Vu, Mx/My críticos, cuatro esfuerzos gamma_v, capacidad y D/C de F4. También registra el contraste conservador de transferencia completa de momento de F4; el control principal envuelve ese D/C completo, sin crédito eta. Si falla solo el contraste adicional exige REQUIERE ANÁLISIS ESPECIAL. El coeficiente de transferencia completa no se presenta como una disposición literal universal de E.060. Se muestran tres posiciones gobernantes distintas; los empates se ordenan por aparición, sin repetir la misma fila.

Los cortantes X−/X+/Y−/Y+ tienen sección crítica y profundidad de su capa, Vu, φVc y D/C propios. Se envuelve D/C, sin escoger primero la mayor fuerza axial o el mayor momento. Cada cara X−/X+/Y−/Y+ calcula INF y SUP usando su momento firmado, profundidad, mínimo correspondiente y límite de cuantía. Los requisitos se calculan antes de tomar la envolvente.

La distribución 15.4.4 se calcula por combo/cara/capa. En dirección larga es uniforme; en dirección corta la fracción central es `2/(β+1)`, β=dimensión larga/corta. Los requisitos de franja y exterior se envuelven separadamente, con sus propios IDs. Un mínimo incompleto exige datos, una resistencia insuficiente informa NO CUMPLE; no se reemplazan por cero.

En servicio se conservan qmax/qmin físicos, ex/ey, B′/L′, área efectiva, qef comparable y D/C con la qadm particular, FS de deslizamiento y cuatro FS de volteo. qmax físico y qef E.050 son conceptos distintos. El pasivo permanece limitado al tratamiento de deslizamiento heredado. Los límites de FS requieren criterio y referencia del proyecto; no se atribuye un valor universal no sustentado a E.050.

Cada control tiene una columna `ENV válido`: solo deja pasar un número de una fila activa con entrada completa y resultado calculable. Para MAX:

```text
valor = MAX(RESULTADOS_*![columna ENV válido]8:67)
fila = MATCH(valor, RESULTADOS_*![columna ENV válido]8:67, 0)+7
ID = INDEX(RESULTADOS_*![ID]1:67, fila)
```

Para MIN se sustituye MAX por MIN. Antes se verifica que exista un número; una envolvente sin valores devuelve vacío y conserva su estado pendiente, nunca un gobernador ficticio o cero favorable. Demanda, capacidad y D/C se extraen de **esa misma fila**. La etiqueta de estado de una cantidad informativa no reemplaza el D/C de capacidad admisible o del detalle instalado.

Jerarquía global: DATOS INVÁLIDOS → FUERA DEL ALCANCE IMPLEMENTADO → REQUIERE ANÁLISIS DE CONTACTO PARCIAL → REQUIERE ANÁLISIS ESPECIAL → REQUIERE DATOS → NO CUMPLE → CUMPLE. NO APLICA es neutral. Sin últimos o sin servicio activos exige datos. Las listas visibles identifican IDs pendientes y con contacto parcial. Los incumplimientos individuales permanecen visibles aunque un pendiente tenga prioridad global.

qmin<0 no se recorta: bloquea el diseño último por contacto completo, conserva diagnóstico de servicio y exige análisis de contacto parcial. Los demás combos continúan. P≤0 y área efectiva fuera del dominio requieren análisis especial; nunca habilitan CUMPLE global.

## 4. Conexión, barras y empalmes

CONEXION_COMBOS vincula activación e ID de la tabla última. Exige referencia, ID externo coincidente, D/C que ya incluya φ, φ y fundamento de transición cuando φ>0,70, Fc, centroide Cx/Cy, área de contacto y pico de esfuerzo del concreto. El intervalo permitido es 0,70–0,90 conforme al análisis documentado de 9.3.2.2; no se calcula internamente Pb ni se aplica φ dos veces. Fuera de intervalo es DATOS INVÁLIDOS; transición sin fundamento exige datos.

FUERZAS_BARRAS admite compresión positiva y tracción negativa. Cada ID de barra se asocia a la geometría real, continuidad/dowel y área que efectivamente cruza la junta; no se suman columna+dowel dos veces. Fuerza vacía activa exige datos; cero explícito se acepta. Se comprueba por combo:

```text
ΣP  = Fc + ΣFi
ΣMx = −Fc·Cy − ΣFi·yi
ΣMy =  Fc·Cx + ΣFi·xi
```

Coordenadas se convierten de cm a m para el cierre en tf·m. Se conservan los límites/tolerancias de F4, aplastamiento, .005Ag, materiales, detalle, anclaje y fricción. Un análisis externo válido no suple fuerzas ausentes o un cierre incompatible.

ENV_BARRAS toma de todas las filas válidas máximas tracción, compresión y |fs| con IDs independientes; informa inversión de signo. Los esfuerzos de traslape consideran la menor área asociada también en compresión. Se evalúan clase y longitud en cada combinación, luego se conserva la clase y longitud más desfavorables con sus IDs.

Para tracción, Clase A exige esfuerzo≤0,5fy, no más de la mitad del número de barras empalmadas en el grupo/sección y escalonamiento≥ld; en los demás casos Clase B. Las barras/grupos reales determinan el porcentaje. Se usan longitudes a fy, sin reducciones por exceso de acero. Compresión conserva 12.16/12.17 y sus mínimos/aumentos. Mecánico y soldado requieren resistencia certificada≥1,25fy del área mayor y referencias; soldado además AWS. La clase se rotula MECANICO/SOLDADO cuando corresponde.

Se verifican anclajes rectos en columna y zapata para ambos signos a fy completo, aun cuando una combinación tenga demanda baja. La inversión no permite elegir una longitud favorable de otra fila. ENVOLVENTES muestra las peores barras y combos de esfuerzo, empalme y anclaje; pendientes/invalidaciones de fuente o geometría no entran como capacidades favorables.

## 5. Selector y complemento eta

VISTA_COMBO permite AUTO según el control escogido o MANUAL por ID, por separado para último y servicio. Los 24 gráficos originales conservan tipos, series y posiciones; se alimentan del combo seleccionado. Los IDs son visibles en VISTA_COMBO y en las notas de GRAFICOS/RESUMEN. No se duplican 60 diagramas ni se enlazan las envolventes al selector.

ANALISIS_COMPLEMENTARIO usa exclusivamente el ID citado para la adopción eta. Sus 383 celdas dependientes se calculan en MC_* a partir del resultado de ese combo, independientemente de VISTA_COMBO. Adopción NO conserva acero básico. Adopción SI exige referencia, validación y combo citado real: `As_adoptado=MAX(As_básico_envolvente, As_local_citado)` solo cuando corresponde. Una adopción pendiente bloquea CUMPLE global; no cambia el punzonamiento, el acero básico ni sus gobernantes.

## 6. Pruebas y ejemplos auditables

**64 escenarios, 204454 comprobaciones independientes, 0 fallos.** Cada caso se calculó con CalculateFullRebuild en Excel real, sin guardar fixtures. La verificación independiente integró presiones por cuadratura para equilibrio y acciones críticas, invirtió resistencia a flexión por bisección y reconstruyó cierre de conexión, fuerzas, áreas, recubrimientos, distancias, anclajes a fy, clases y longitudes de empalme. Tolerancia numérica abs/rel 2·10⁻⁸.

Se verificaron 1/3/10/60 últimos y servicios; vector inseparable; cuatro gobernantes de cortante; gobernantes diferentes por cara/capa; casos donde la mayor P/M no gobierna; mapeos de ambos programas, permutas/signos/referencias; factores CS e incremento; duplicados, vacíos/texto/ceros; inactivos con residuos; contacto parcial y levantamiento; φ/IDs externos; matriz completa 3600 fuerzas; equilibrio biaxial; inversión, Clase A/B y dowels certificados; selector y eta independientes; traslado/offsets y dominio de área efectiva.

### Ejemplo obligatorio: tres gobernantes distintos

Fixture de contacto completo con acciones no listadas iguales a cero:

| ID | P tf | Mx tf·m | My tf·m |
|---|---:|---:|---:|
| U1 | 300 | 180 | 0 |
| U2 | 350 | 0 | 0 |
| U3 | 250 | 0 | 100 |

| Control | Gobernante | Demanda | Capacidad/requisito | D/C | Estado |
|---|---|---:|---:|---:|---|
| Punzonamiento | U1 | 67.86139735 | 12.98022364 | 5.22806072 | REQUIERE ANÁLISIS ESPECIAL |
| Cortante X+ | U3 | 31.84055321 | 27.99421232 | 1.13739772 | NO CUMPLE |
| Acero Y+ INF | U2 | 34.91444444 | 24.49146453 | — | CUMPLE |

Punzonamiento: esfuerzo pico kgf/cm² y φvn; cortante: tf/m y φVc; flexión: Mu tf·m/m y As requerido cm²/m. El estado de acero indica que el requisito se pudo calcular, y no certifica el acero instalado. El ejemplo demuestra gobernantes U1/U3/U2; no se usa para hacer cumplir la base ni se guarda en ella.

### Servicio: gobernantes independientes

| Control | Gobernante | Demanda | Capacidad | D/C o FS | Estado |
|---|---|---:|---:|---:|---|
| qef comparable tf/m² | S2 | 14.60469159 | — | — | CUMPLE |
| Deslizamiento | S3 | 2.13398437 | — | 2.13398437 | CUMPLE |
| Volteo X+ | S1 | 9.82910156 | — | 9.82910156 | CUMPLE |

qef gobierna S2, deslizamiento S3 y volteo X+ S1. La capacidad admisible se compara en su control separado y en este fixture no cumple; un extremo informativo no sustituye esa verificación.

### Regresión de un solo combo contra F4

Los registros migrados reproducen Q, presiones físicas, excentricidades/área efectiva/qef, cuatro D/C de cortante, D/C gamma_v y contraste completo de punzonamiento, y acero básico de ambas direcciones/capas. Las diferencias deliberadas son la identificación multicombo, la exposición física firmada de Mx_origen, la separación de estados por cara y la admisión documentada del φ externo de transición. El caso conserva Bx=By=3,75m, h=0,50m, qadm=8,5tf/m², fc=210kgf/cm² y fy=4200kgf/cm².

| Magnitud | Resultado migrado |
|---|---:|
| Q último tf | 203.98375000 |
| qmax último físico tf/m² | 14.61906133 |
| qmin último físico tf/m² | 14.39196089 |
| D/C gamma_v | 0.82537869 |
| D/C contraste completo | 0.83730070 |
| qef servicio comparable tf/m² | 11.09971192 |

### Registro de escenarios

| Nº | Escenario | Errores de fórmula |
|---:|---|---:|
| 1 | Regresión F4 — datos migrados | 0 |
| 2 | 1 combos últimos y 1 servicio | 0 |
| 3 | 3 combos últimos y 3 servicio | 0 |
| 4 | 10 combos últimos y 10 servicio | 0 |
| 5 | 60 combos últimos y 60 servicio | 0 |
| 6 | Vector inseparable obligatorio | 0 |
| 7 | Cuatro gobernantes de cortante | 0 |
| 8 | Mayor P no gobierna punzonamiento | 0 |
| 9 | Mayor Mx no gobierna cortante X | 0 |
| 10 | Mayor My no gobierna flexión Y | 0 |
| 11 | Inferior y superior de distintos combos | 0 |
| 12 | Tres gobernantes punzonamiento cortante flexión | 0 |
| 13 | Gobernantes de servicio independientes | 0 |
| 14 | Contacto parcial último intermedio | 0 |
| 15 | Contacto parcial servicio intermedio | 0 |
| 16 | Levantamiento último P cero | 0 |
| 17 | Levantamiento último P negativo | 0 |
| 18 | Levantamiento servicio | 0 |
| 19 | Fila inactiva con residuos | 0 |
| 20 | ID último duplicado | 0 |
| 21 | ID servicio duplicado | 0 |
| 22 | Componente última activa vacía | 0 |
| 23 | Componente servicio activa vacía | 0 |
| 24 | Componente última texto inválido | 0 |
| 25 | Cero numérico válido | 0 |
| 26 | Signo inverso Mx | 0 |
| 27 | Signo inverso My | 0 |
| 28 | Ningún combo activo | 0 |
| 29 | Datos ETABS | 0 |
| 30 | ETABS V2/V3 invertidos | 0 |
| 31 | ETABS M2/M3 invertidos | 0 |
| 32 | ETABS Signo -1 | 0 |
| 33 | Datos SAP2000 | 0 |
| 34 | SAP2000 V2/V3 invertidos | 0 |
| 35 | SAP2000 M2/M3 invertidos | 0 |
| 36 | SAP2000 Signo -1 | 0 |
| 37 | Mapa inválido destinos repetidos | 0 |
| 38 | Mapa sin referencia | 0 |
| 39 | Factor CS 0,80 por combo | 0 |
| 40 | Factor CS 0,80 sin componente | 0 |
| 41 | Factor CS prohibido gravedad | 0 |
| 42 | Incremento qadm por combo | 0 |
| 43 | Incremento qadm sin fuente | 0 |
| 44 | Conexión multicomponente y barra cambia signo | 0 |
| 45 | Empalme Clase B por otra combinación | 0 |
| 46 | Empalme Clase A en tracción baja | 0 |
| 47 | Phi externo 0,80 con fundamento | 0 |
| 48 | Phi externo 0,90 con fundamento | 0 |
| 49 | Phi externo sin fundamento | 0 |
| 50 | Phi externo fuera intervalo | 0 |
| 51 | ID externo diferente | 0 |
| 52 | Fuerza de barra activa vacía | 0 |
| 53 | Cero de barra válido | 0 |
| 54 | Cierre de equilibrio erróneo | 0 |
| 55 | Punzonamiento y conexión distintos | 0 |
| 56 | Dowel unión mecánica con inversión | 0 |
| 57 | Dowel soldado con inversión | 0 |
| 58 | 60 barras × 60 combos — matriz completa | 0 |
| 59 | Selector manual U2 | 0 |
| 60 | Eta adopción pendiente conserva gobernantes | 0 |
| 61 | Eta combo citado U2 vista AUTO | 0 |
| 62 | Eta combo citado U2 vista U3 | 0 |
| 63 | Traslado y offsets con signos | 0 |
| 64 | Área efectiva fuera de dominio | 0 |

## 7. Control de calidad nativo

Microsoft Excel **16.0**, interfaz española LanguageID **3082**. Se comprobó FormulaLocal con SI, CONTAR.SI, INDICE, COINCIDIR y funciones estándar. No se emplearon funciones posteriores a 2016. La versión COM 16.0 se informa tal como fue observada; no se deduce una edición comercial a partir de ese número.

CalculateFullRebuild → guardar → cerrar → finalizar la instancia propia → abrir en instancia nueva → CalculateFullRebuild → guardar. Los snapshots de valores/estados coincidieron antes/después de reabrir. Se volvió a comprobar la apertura tras el guardado final. El recorrido de todas las hojas y las cachés OOXML detectó **0 #REF!, #DIV/0!, #VALUE!, #NAME?, #NUM!, #N/A**, cero circularidad, enlaces externos, macros, `_xlfn` y `_xludf`. ZIP/XML íntegros.

Se resolvió un conflicto de nombres de impresión detectado mediante el diálogo real de Excel: el guardado COM en este entorno serializa `Print_Area`/`Print_Titles` ordinarios junto a sus equivalentes reservados. Tras cada guardado cerrado se normalizó únicamente `xl/workbook.xml` a `_xlnm.Print_Area`/`_xlnm.Print_Titles`, eliminando duplicados del mismo ámbito. Esta corrección de metadatos no modifica hojas, fórmulas, valores, estilos, gráficos ni cachés de resultados; se comprobó por comparación de todos los componentes ZIP. La entrega final se abrió normalmente después de esa normalización, sin diálogo de conflicto ni modo de recuperación. No se utilizó la copia de diagnóstico reparada como entregable.

Se revisaron vistas exportadas desde Excel de las entradas, envolventes, selector y complemento. Se configuraron áreas de impresión/repetición para que la matriz y los campos extensos sean recorribles. Las 24 series/tipos/posiciones originales se compararon con F4. Las filas no activas y el selector no modifican las envolventes. Los archivos de soporte, PDFs, imágenes, fixtures y scripts permanecen fuera del commit; se publican únicamente el XLSX y este documento.

## 8. Nombres definidos

Se conservan los nombres F4 salvo `inp_case`, cuyo destino pasa de la entrada original al ID mostrado en VISTA_COMBO. El valor original de entrada no se modifica. Se añaden 54 nombres; la lista siguiente incluye esa redirección deliberada. Excel puede omitir comillas de un nombre de hoja simple al serializar, sin cambiar el destino.

| Nombre | Destino |
|---|---|
| `COMBO_MOSTRADO_U` | `'VISTA_COMBO'!$B$10` |
| `COMBO_MOSTRADO_S` | `'VISTA_COMBO'!$B$17` |
| `FILA_MOTOR_U` | `'VISTA_COMBO'!$B$11` |
| `FILA_MOTOR_S` | `'VISTA_COMBO'!$B$18` |
| `COMBO_PUNZ_GOB` | `'ENVOLVENTES'!$B$8` |
| `ESTADO_GLOBAL_MULTICOMBO` | `'ENVOLVENTES'!$B$5` |
| `inp_case` | `'VISTA_COMBO'!$B$10` |
| `FILA_COMPLEMENTARIO` | `'ANALISIS_COMPLEMENTARIO'!$B$8` |
| `GOB_U_PUNZONAMIENTO` | `'ENVOLVENTES'!$B$8` |
| `GOB_U_CORTANTE_XNEG` | `'ENVOLVENTES'!$B$9` |
| `GOB_U_CORTANTE_XPOS` | `'ENVOLVENTES'!$B$10` |
| `GOB_U_CORTANTE_YNEG` | `'ENVOLVENTES'!$B$11` |
| `GOB_U_CORTANTE_YPOS` | `'ENVOLVENTES'!$B$12` |
| `GOB_U_ACERO_XNEG_INF` | `'ENVOLVENTES'!$B$13` |
| `GOB_U_AS_XNEG_INF_FRANJA` | `'ENVOLVENTES'!$B$14` |
| `GOB_U_AS_XNEG_INF_EXTERIOR` | `'ENVOLVENTES'!$B$15` |
| `GOB_U_ACERO_XNEG_SUP` | `'ENVOLVENTES'!$B$16` |
| `GOB_U_AS_XNEG_SUP_FRANJA` | `'ENVOLVENTES'!$B$17` |
| `GOB_U_AS_XNEG_SUP_EXTERIOR` | `'ENVOLVENTES'!$B$18` |
| `GOB_U_ACERO_XPOS_INF` | `'ENVOLVENTES'!$B$19` |
| `GOB_U_AS_XPOS_INF_FRANJA` | `'ENVOLVENTES'!$B$20` |
| `GOB_U_AS_XPOS_INF_EXTERIOR` | `'ENVOLVENTES'!$B$21` |
| `GOB_U_ACERO_XPOS_SUP` | `'ENVOLVENTES'!$B$22` |
| `GOB_U_AS_XPOS_SUP_FRANJA` | `'ENVOLVENTES'!$B$23` |
| `GOB_U_AS_XPOS_SUP_EXTERIOR` | `'ENVOLVENTES'!$B$24` |
| `GOB_U_ACERO_YNEG_INF` | `'ENVOLVENTES'!$B$25` |
| `GOB_U_AS_YNEG_INF_FRANJA` | `'ENVOLVENTES'!$B$26` |
| `GOB_U_AS_YNEG_INF_EXTERIOR` | `'ENVOLVENTES'!$B$27` |
| `GOB_U_ACERO_YNEG_SUP` | `'ENVOLVENTES'!$B$28` |
| `GOB_U_AS_YNEG_SUP_FRANJA` | `'ENVOLVENTES'!$B$29` |
| `GOB_U_AS_YNEG_SUP_EXTERIOR` | `'ENVOLVENTES'!$B$30` |
| `GOB_U_ACERO_YPOS_INF` | `'ENVOLVENTES'!$B$31` |
| `GOB_U_AS_YPOS_INF_FRANJA` | `'ENVOLVENTES'!$B$32` |
| `GOB_U_AS_YPOS_INF_EXTERIOR` | `'ENVOLVENTES'!$B$33` |
| `GOB_U_ACERO_YPOS_SUP` | `'ENVOLVENTES'!$B$34` |
| `GOB_U_AS_YPOS_SUP_FRANJA` | `'ENVOLVENTES'!$B$35` |
| `GOB_U_AS_YPOS_SUP_EXTERIOR` | `'ENVOLVENTES'!$B$36` |
| `GOB_U_CONEXI_N_P_M_M` | `'ENVOLVENTES'!$B$37` |
| `GOB_U_APLASTAMIENTO` | `'ENVOLVENTES'!$B$38` |
| `GOB_U_CORTANTE_FRICCI_N` | `'ENVOLVENTES'!$B$39` |
| `GOB_S_QEF_COMPARABLE_TF_M_` | `'ENVOLVENTES'!$B$40` |
| `GOB_S_QMAX_F_SICO_TF_M_` | `'ENVOLVENTES'!$B$41` |
| `GOB_S_QMIN_F_SICO_TF_M_` | `'ENVOLVENTES'!$B$42` |
| `GOB_S_B__M` | `'ENVOLVENTES'!$B$43` |
| `GOB_S_L__M` | `'ENVOLVENTES'!$B$44` |
| `GOB_S_AEF_M_` | `'ENVOLVENTES'!$B$45` |
| `GOB_S_EX_M` | `'ENVOLVENTES'!$B$46` |
| `GOB_S_EY_M` | `'ENVOLVENTES'!$B$47` |
| `GOB_S_CAPACIDAD_ADMISIBLE` | `'ENVOLVENTES'!$B$48` |
| `GOB_S_DESLIZAMIENTO` | `'ENVOLVENTES'!$B$49` |
| `GOB_S_VOLTEO_XNEG` | `'ENVOLVENTES'!$B$50` |
| `GOB_S_VOLTEO_XPOS` | `'ENVOLVENTES'!$B$51` |
| `GOB_S_VOLTEO_YNEG` | `'ENVOLVENTES'!$B$52` |
| `GOB_S_VOLTEO_YPOS` | `'ENVOLVENTES'!$B$53` |
| `LISTA_FACTORES_CS` | `'GUIA_MULTICOMBO'!$L$7:$L$8` |

## 9. Alcance pendiente y fuentes

No se implementa solver de contacto parcial, columna de borde/esquina, perímetros abiertos ni solver interno general P–Mx–My. No se amplía Capítulo 21 sísmico. Se conservan bloqueos de ganchos, tope, agrupamientos/detalles no implementados y modos de análisis fuera de alcance. Las fuerzas/resultantes de la conexión proceden del análisis externo real; una celda vacía no se inventa. Anclajes a fy y contraste completo siguen siendo conservadores según los modelos declarados. eta permanece complementario y citado, sin reemplazar 15.4.

Fuentes normativas:

- [NTE E.060, DS 010-2009-VIVIENDA, PDF oficial](https://cdn.www.gob.pe/uploads/document/file/2686419/E.060%20Concreto%20Armado%20DS%20N%C2%B0%20010-2009.pdf): 9.3.2.2, 11.12, 12.2/12.3, 12.14–12.17, 15.2/15.4/15.8, además de los controles preservados de F4.
- [NTE E.050, RM 406-2018-VIVIENDA, PDF oficial](https://cdn.www.gob.pe/uploads/document/file/2366655/54%20E.050%20SUELOS%20Y%20CIMENTACIONES%20RM%20N%C2%B0%20406-2018-VIVIENDA.pdf): presión admisible, excentricidad/área efectiva y carga inclinada, con datos/referencias EMS por proyecto.
- [Catálogo oficial del RNE](https://www.gob.pe/institucion/vivienda/informes-publicaciones/2309793-reglamento-nacional-de-edificaciones-rne). Un proyecto de actualización no se adopta automáticamente como norma vigente.

### Preservación SHA-256

| Archivo previo | SHA-256 sin cambios |
|---|---|
| `CAMBIOS_ZAPATA_FASE1.md` | `24e6f0077e2f8ba51c8d80b51056834aa8400998d2532d9b83693d426eddbf3d` |
| `CAMBIOS_ZAPATA_FASE2.md` | `18aad8f776b00fde74027dca632bb60b503cbd6e4c24a366803ecaa87a5612a1` |
| `CAMBIOS_ZAPATA_FASE3.md` | `21cbc8089acc65b6aa2292954fcda880c3e652a4d24611c968fa0230af6ef1b2` |
| `CAMBIOS_ZAPATA_FASE4.md` | `cb657891aecb1a1242f597babf255079efc0304684e9bc68dee871832d0dc17e` |
| `Diseño de zapata aislada.xlsx` | `24f60a8b5a8b170de9ef528cc7f96120f0b5c651ccdad33acf8a6562965a7060` |
| `Diseño de zapata aislada_CORREGIDA_FASE1.xlsx` | `8d66b5590812704f8bdd1173b5583a4bcaaf00d500c1d854d00c42051192ded5` |
| `Diseño de zapata aislada_CORREGIDA_FASE2.xlsx` | `8d92bc7d557dcbb691b1d538e2dd3f96d830e54f69bb1f407a402637b3e2bd01` |
| `Diseño de zapata aislada_CORREGIDA_FASE3.xlsx` | `7074baa04d42f3637931dc92594fb0c314405ad015c4d37c8dcf21e81eaab433` |
| `Diseño de zapata aislada_CORREGIDA_FASE4.xlsx` | `aeb342a12be7b638489da67cd040dd024d88f79858dc88fa467a0151301f2db1` |
