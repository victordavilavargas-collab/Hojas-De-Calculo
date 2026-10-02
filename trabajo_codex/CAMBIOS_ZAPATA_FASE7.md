# Fase 7 — acciones espectrales CSI, plano de corte y pesos reales de zapata

Fecha de cierre: 2026-10-02. Repositorio: `victordavilavargas-collab/Hojas-De-Calculo`. Rama: `main`. Base: `a1cf62521afca5a43aca09f777371c44c88ea159`, archivo F6.

Se creó `Diseño de zapata aislada_CORREGIDA_FASE7.xlsx`. El resultado técnico actual sigue siendo **NO CUMPLE**, la validez es **REQUIERE DATOS** y la cobertura es **REQUIERE CONFIRMAR ENVOLVENTE COMPLETA**. La selección E.030 permanece **REQUIERE DEFINIR**: no se escogió una versión para el proyecto por su fecha. Los cálculos gravitacionales continúan disponibles.

Los datos originales de geometría, materiales, acciones, qadm, acero y recubrimientos permanecen intactos. Se compararon todas las celdas originales de datos y acciones conservadas; cero diferencias. Los hashes de archivos y documentos F1–F6 siguen coincidiendo. Los escenarios sintéticos se cerraron sin guardar sus datos en el entregable.

## Fuentes primarias y criterio normativo

- [Texto oficial de la E.030 modificada por RM 183-2026-VIVIENDA, El Peruano](https://epdoc2.elperuano.pe/EpPo/DescargaIN.asp?Referencias=MjUxMTI1OF8xMjAyNjA1MDM=), consultado y extraído antes de implementar las ecuaciones.
- [E.030 anterior, publicación oficial RNE/MVCS](https://cdn.www.gob.pe/uploads/document/file/2366641/51%20E.030%20DISE%C3%91O%20SISMORRESISTENTE%20RM-043-2019-VIVIENDA.pdf?v=1677250657).
- [Disposiciones transitorias RM 217-2026-VIVIENDA, El Peruano](https://busquedas.elperuano.pe/dispositivo/NL/2521423-1).
- [CSI Analysis Reference, sección Response Spectrum Analysis](https://docs.csiamerica.com/manuals/etabs/Analysis%20Reference.pdf), especialmente respuestas estadísticas y reacciones de base, páginas impresas 383–395.
- [Definición oficial de Response Spectrum en ETABS](https://docs.csiamerica.com/help-files/etabs/Menus/Define/Load_Cases/Response_Spectrum.htm).

El régimen transitorio admite continuidad con el texto anterior en determinados proyectos en curso. Se exige fundamento y referencia en CONTROL_FASE7 B8:B9; la plantilla no decide si un proyecto satisface ese régimen.

| Versión / artículo | Regla verificada | Aplicación y límite |
|---|---|---|
| E.030 anterior, 24.1 | Direcciones independientes para estructuras regulares; dirección más desfavorable para irregulares | Dos ramas SX y SY independientes para REGULAR. Para irregularidad se exige procedimiento externo documentado; no se supone automáticamente 100/30 |
| E.030 2026, 28.1 y 43 | Para análisis espectral: raíz cuadrada de suma de cuadrados de los esfuerzos al 100% y 30% ortogonal | `rX,j=SQRT(SXj^2+(0.3*SYj)^2)` y `rY,j=SQRT((0.3*SXj)^2+SYj^2)`; DERIVADOS_U/S R:W |
| E.030 2026, 33.3 | Para análisis estático: suma de valores absolutos de los esfuerzos al 100% y 30% ortogonal | Es una regla distinta de art.43. La plantilla recibe acciones estáticas firmadas ya analizadas/combinadas; no genera espectro, modelo ni combinaciones estáticas del edificio |
| E.030 2026, 28.2 | Evaluar direcciones adicionales cuando los ejes no son paralelos | El generador interno se restringe a ejes X/Y ortogonales y configuración REGULAR; otros casos requieren método externo |
| E.030 2026, 28.3 | Excentricidad accidental asociada a la dirección al 100% | Debe estar incorporada correctamente en las fuentes analizadas; no se calcula aquí torsión accidental del edificio |
| E.030 2026, 28.4–28.5 y 41.2 | Evaluar vertical cuando corresponde, simultáneamente y con signo adverso; espectro vertical según norma | Se exige decidir SI/NO y fundamentarlo. SZ es respuesta ya analizada. Se añade su magnitud adversa al límite horizontal como hipótesis conservadora documentada; no se atribuye a la norma una ley modal conjunta horizontal–vertical |
| E.030 2026, 44 | Escalamiento mínimo de resultados dinámicos | El escalamiento/modalidad debe estar aplicado en origen y documentado en ESPECTROS H; no se vuelve a aplicar automáticamente |

Las verificaciones de concreto E.060 y suelo E.050 de F6 se conservan. No se añadió Capítulo 21, solver de contacto parcial, borde/esquina, perímetro abierto ni solver interno general P-Mx-My.

## Dónde ingresar y revisar

| Hoja / rango | Función |
|---|---|
| CONTROL_FASE7 B7:B16 | Versión E.030, régimen, referencia, configuración, ejes y componente vertical |
| CONTROL_FASE7 B20:B41 | Geometría vertical, volumen ocupado, pedestal, relleno real y dominio de cargas localizadas |
| COMBOS_ULTIMOS BP:CZ / COMBOS_SERVICIO CI:DS | Tipo de análisis, demanda, naturaleza, plano, end offsets, inclusión de pesos, factores y fuentes |
| CASOS_CONSTITUYENTES A:I | Inventario de hasta 12 casos por padre U/S: tipo, coeficiente firmado y fuente. Detección real de RESPONSE SPECTRUM dentro de LINEAR ADD |
| ESPECTROS_U/S C:J | SX/SY/SZ, referencias globales/modalidad/escalamiento y aceptación del procedimiento de signos |
| ESPECTROS_U/S K:P / Q:V / W:AB / AC:AH | Base firmada de seis componentes; magnitudes SX, SY y SZ separadas. Unidades tf y tf·m |
| DERIVADOS_U/S A:AD | 128 estados por padre: ID, padre, casos, norma/artículo, coeficientes, seis signos, seis acciones, naturaleza y contacto/torsión |
| DERIVADOS_U/S AE en adelante | Resultados propios del cuerpo, fricción, conexión y servicio |
| CONEXION_ESPECTRAL / BARRAS_ESPECTRALES | Datos externos por evaluación P-Mx-My derivada, sin heredar capacidad ni fuerzas del padre |
| ENVOLVENTES B5 / B6 / B54 | Técnico, validez y cobertura independientes |
| ENVOLVENTES B8:B53 / 145:148 | Identificador gobernante efectivo de cada control y panel sísmico |
| RESUMEN A168:B174 | Norma, demanda, tratamiento, estado sísmico, IDs gobernantes y naturaleza |
| VISTA_DERIVADO B7:B8 | Consulta U/S y estado 1–7680; no interviene en el motor |

Se conservan 60 últimos, 60 servicio, ocho As independientes, sus ocho estados de armado, 60 barras × 60 combinaciones originales, conexión multicombo, qadm global EMS/override documentado, normalización local–global, cobertura y VISTA_COMBO. Las nuevas columnas de metadatos están agrupadas. Expandirlas para revisar la fuente. Las entradas se distinguen por color de las fórmulas y estados.

`COMBOS_ULTIMOS!BR8:BR67` y `COMBOS_SERVICIO!CK8:CK67` contienen fórmulas de detección espectral desde el tipo principal y CASOS_CONSTITUYENTES; conservar esas fórmulas. Registrar todos los casos reales del padre en el inventario y confirmar su fuente antes de declarar completo el conjunto. Los coeficientes son trazabilidad de las acciones ya preparadas, no un segundo factor automático.

## Naturaleza espectral y estados de diseño

CSI obtiene una magnitud máxima estadística por cantidad de respuesta; no proporciona un instante en el que los seis máximos sean simultáneos. SINGLE CASE, LINEAR ADD y correspondence no cambian esa naturaleza cuando existe un RESPONSE SPECTRUM. Los padres espectrales se excluyen del camino directo firmado y se rotulan **ESTADÍSTICO ESPECTRAL**.

Modo B separa la base gravitacional firmada de SX/SY/SZ. **Los seis valores de la base y las magnitudes SX/SY/SZ deben estar ya ponderados por los coeficientes constituyentes del combo**, además del escalamiento del análisis. El inventario registra esos coeficientes para trazabilidad y detección de tipo; no los aplica otra vez. Los únicos factores adicionales del generador son los direccionales normativos, el tratamiento adverso SZ y la reducción de servicio explícita. Confirmar esta preparación en la referencia del procedimiento ESPECTROS J y aceptación I. Para cada rama direccional se generan los 64 signos de las seis componentes:

`v_j = base_j + signo_j * (rH,j + |SZ_j|)`.

SZ se suma solo cuando aplica. En servicio, el factor 0.8 se aplica una sola vez al incremento sísmico, manteniendo la base firmada: `base_j + 0.8*signo_j*(rH,j+|SZ_j|)`. Si el resultado ya está reducido, el factor debe ser 1. La fuente de la reducción es obligatoria.

Este procedimiento es una **caja conservadora de hipótesis de diseño**, con confirmación y referencia obligatorias. No reconstruye un instante físico ni adopta todos los máximos como un único vector. Puede producir hipótesis que no ocurrieron juntas, deliberadamente para cubrir correlaciones no disponibles. Cada estado mantiene su propio vector y naturaleza estadística. No basta ingresar seis máximos sin las fuentes, ejes, régimen y procedimiento de signos.

Cada padre produce IDs `U1-X01`…`U1-X64`, `U1-Y01`…`U1-Y64`, análogamente S. El generador cubre hasta 7680 estados por grupo. Los estados del cuerpo comparten una evaluación solo cuando P, Mx y My son idénticos y Δz=0: 16 evaluaciones por padre, 960 por grupo. Se compiló el mismo grafo de fórmulas del motor F6, conservando sus controles; no se reemplazaron por otra implementación numérica. Los signos propios de Fx, Fy y Mz vuelven a calcular fricción, deslizamiento y estados afectados en MOTOR_H_U/S. Las envolventes del cuerpo usan candidatos reales de esas evaluaciones y muestran un ID existente en DERIVADOS.

La conexión externa implementada está basada en P-Mx-My y fuerzas axiales de barras. No se heredan datos externos del padre. La evaluación representativa usa un miembro real de los 64 signos que maximiza H y |Mz|; las verificaciones que dependen de H/Mz se recalculan por signo propio. Un procedimiento externo con interacción adicional de corte/torsión requiere análisis explícito y no puede certificarse como PMM simple. Mz significativo bloquea las verificaciones afectadas.

Modo D admite un resultado externo ya combinado con referencia del procedimiento y norma válida; conserva la naturaleza estadística si contiene RS. Modo C requiere las seis claves exactas del mismo Time/Step y número. El envelope de historia no se acepta como simultáneo. Un caso MODAL aislado tampoco es demanda de diseño.

Las magnitudes de modo B deben proceder de resultados globales **recombinados modalmente en la interfaz**. Rotar o trasladar seis máximos espectrales como un vector físico es incorrecto: la mezcla puede requerir respuestas modales con signos/correlación que no están en esos máximos. Por ello, para RS con Δz distinto de cero se exige recombinación modal en origen, en lugar de aplicar el traslado estático a magnitudes. BASE REACTION espectral exige ejes y transformación documentados.

## Plano físico y normalización

Para acciones firmadas: `Δz=Zi−Zr`, `Mx_i=Mx_r−Fy*Δz`, `My_i=My_r+Fx*Δz`; P y Mz no se trasladan. La operación se aplica una sola vez, sustituyendo el traslado global histórico del motor para los combos. FRAME registra extremo I/J, Station, plano, cotas, end offset y referencia; Station=0 no acredita interfaz.

La transformación F6 conserva T, determinante y error ortogonal. Para CSI ORIGINAL / FRAME: `P=−e*s*Praw`, `Fx=e*(a*V2+b*V3)`, `Fy=e*(c*V2+d*V3)`, `Mx=e*(−a*M2+b*M3)`, `My=e*(−c*M2+d*M3)`, `Mz=e*s*Traw`, con e=+1 en I/−1 en J y s=+1 para local1 hacia +Z/−1 hacia −Z. Para reacción global firmada: `P=F3`, `Fx=−F1`, `Fy=−F2`, `Mx=−M1`, `My=−M2`, `Mz=−M3`. Esta conversión de signos no autoriza tratar resultados RS como concurrentes.

FRAME normal no puede incluir Wz/Ws ni un pedestal situado fuera del corte. Solo se admite modo especial con modelo y justificación. JOINT y BASE con pesos incluidos exigen cimentación modelada, apoyo bajo la interfaz/pesos, nivel, elementos incluidos y referencia. BASE REACTION del edificio completo se rechaza; únicamente se admite apoyo único o grupo exclusivo de esa zapata y suma trazable.

## Metrado, contacto bruto y cuerpo neto

`Vprisma=Bx*By*hs`. Para columna directa, `Vocupado=cx*cy*hs`. Para pedestal rectangular/circular: `Vocupado=Aped*MIN(hped,hs)+cx*cy*MAX(hs−hped,0)`. Geometría manual exige metrado y referencia. `Vrelleno=Vprisma−Vocupado`; no se reemplazan volúmenes negativos por cero para ocultar geometría inválida.

`Wz=Bx*By*h*γconcreto`, `Wped=Vped*γconcreto`, `Ws=Vrelleno*γsuelo`. Cada peso tiene factor explícito por combo. Los factores pueden coincidir; si difieren, se exige justificación. El pedestal SI incluido no se vuelve a sumar; NO incluido se suma como carga localizada. Columna directa no añade otro peso de columna, porque debe formar parte de P importado.

Definiendo `Winc` como los pesos uniformes ya importados y `Wp_add` como el pedestal no importado: `Pcuerpo=Pimport−Winc+Wp_add`, `Mxcuerpo=Mxi−Winc*yc`, `Mycuerpo=Myi+Winc*xc`. En la conexión de columna se excluye el pedestal de P cuando ese peso se incluyó aguas abajo del corte. El equilibrio externo debe corresponder a esa sección, no a la fuerza del cuerpo que incorpora pedestal.

`Qbruto=Pcuerpo+Wz_considerado+Ws_considerado`. El relleno real tiene un hueco localizado en el elemento vertical; para el equilibrio y gradientes se consideran sus primeros momentos. Con `Wvoid=Vocupado*γsuelo*gamma_Ws`: `F=−Mxcuerpo+(Pcuerpo−Wvoid)*yc`, `G=Mycuerpo+(Pcuerpo−Wvoid)*xc`, `qbruta=Qbruto/A+G*x/Iy+F*y/Ix`. Mz no interviene en esta distribución normal.

Fuera de la huella vertical, `qneta=(Pcuerpo−Wvoid)/A+G*x/Iy+F*y/Ix`. Se sustraen el peso uniforme de zapata y el prisma completo de suelo; el hueco se repone como carga localizada. Dentro de un perímetro de punzonamiento que contiene esa huella, la reacción integra además Wvoid. Esto evita sumar relleno inexistente o cancelar como uniforme el peso localizado del pedestal.

**Límite geométrico explícito:** el cálculo interno del cuerpo conserva las caras de la columna F6. La corrección de hueco localizado solo es válida cuando el pedestal rectangular/circular queda completamente dentro de esa huella. Un pedestal que la rebasa, o GEOMETRÍA MANUAL, permite metrado/pesos y presiones brutas, pero bloquea el cuerpo con **REQUIERE ANÁLISIS GEOMETRÍA LOCALIZADA**. No se afirma que la integración uniforme F6 resuelva esos casos; requieren desarrollar la distribución localizada y secciones/perímetros que correspondan. El límite aparece en CONTROL_FASE7 B41 y en el dominio del motor. El contacto parcial sigue bloqueado.

Mz mayor que `1E−6 tf·m` exige **REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA** en conexión, fricción y estabilidad. La tolerancia se fijó para ruido numérico. La presión normal continúa disponible; una q favorable no habilita certificación de la conexión torsional.

## Validación ejecutada

- 48 escenarios de Excel, 22667 comprobaciones independientes y cero fallos finales. Incluyen los 30 casos solicitados y pruebas adicionales de reducción única, vertical, geometría circular/manual, excentricidad, norma indefinida en gravedad, fuente constituyente real, procedimiento externo, Frame CSI I/J, rotación 37°, cancelación de Mz y vistas.
- Cálculo independiente de las seis acciones de los 128 estados de cada caso espectral válido, pesos/volúmenes, presión bruta/neto, integrales de cuatro cortantes y momentos, ocho As mediante bisección, punzonamiento con hueco localizado, selección numérica e ID gobernante, fricción/deslizamiento propios. Tolerancia de comparación numérica: relativa y absoluta 2E−8.
- Corrección de los fixtures I/J para registrar el modo local CSI, conforme al contrato F6; las pruebas repetidas pasan. No se modificó el libro para aceptar una orientación no acreditada.
- CalculateFullRebuild, guardar/cerrar, normalizar nombres reservados de impresión y conservar cálculo automático en los metadatos, reapertura en una nueva instancia, CalculateFullRebuild y comparación de valores persistidos: **True**.
- Excel nativo 16.0, idioma 3082 (español). Se verificaron fórmulas locales, funciones compatibles con la generación Excel 2016, ausencia de `_xlfn`/`_xludf`, macros y vínculos externos. Version 16.0 por sí sola no identifica la edición comercial instalada.
- 75 hojas, 24 gráficos, 3,467,540 fórmulas; longitud máxima 6739 caracteres, menor que 8192. Cero errores almacenados, circularidad y dependencias de selectores de vista en el motor. 888 entradas originales comparadas; 92,160 fórmulas de componentes revisadas para comprobar el padre correcto en los 60 padres de ambos grupos.
- Segundo/tercer gobernante de punzonamiento preservados con sus IDs y ratios en B56/E56 y B57/E57; verificados nuevamente en un caso espectral y después de guardar/reabrir. El visor oculta datos de registros inactivos con NO APLICA y no muestra un artículo anterior como criterio cuando la norma sigue indefinida.
- Vista impresa nativa del control normativo, pesos, envolventes, panel sísmico, visor e inventario revisada visualmente. Los gráficos originales se conservaron.

| Escenario | Entrada / naturaleza | Técnico | Validez |
|---|---|---|---|
| F7 01 Linear Static | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 02 Response Spectrum puro | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS |
| F7 03 D + Response Spectrum | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS |
| F7 04 Linear Add estático | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 05 Linear Add contiene RS declarado | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS |
| F7 06 Envelope estático correspondence | OK / CORRESPONDENCE DE COMBO | NO CUMPLE | REQUIERE DATOS |
| F7 07 RS con correspondence | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS |
| F7 08 Time History mismo step | OK / STEP DE HISTORIA | NO CUMPLE | REQUIERE DATOS |
| F7 09 Time History Envelope rechazado | DATOS NO CONCURRENTES — NO USAR COMO COMBO / STEP DE HISTORIA | NO CUMPLE | REQUIERE DATOS / REVISAR ENTRADAS FASE 7 |
| F7 10 E030 anterior | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS |
| F7 11 E030 2026 | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS |
| F7 12 E030 sin definir | REQUIERE DEFINIR NORMA E.030 APLICABLE / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DEFINIR NORMA E.030 APLICABLE |
| F7 13 FRAME interfaz | OK / CONCURRENTE | NO CUMPLE | REQUIERE DATOS |
| F7 14 FRAME 0.30m encima | OK / CONCURRENTE | NO CUMPLE | REQUIERE DATOS |
| F7 15 End offset activo | OK / CONCURRENTE | NO CUMPLE | REQUIERE DATOS |
| F7 16 FRAME normal pesos incluidos rechazado | DATOS INVÁLIDOS — PESOS FUERA DEL CORTE FRAME / CONCURRENTE | NO CUMPLE | REQUIERE DATOS / REVISAR ENTRADAS FASE 7 |
| F7 17 FRAME especial documentado | OK / CONCURRENTE | NO CUMPLE | REQUIERE DATOS |
| F7 18 JOINT cimentación modelada | OK / CONCURRENTE | NO CUMPLE | REQUIERE DATOS |
| F7 19 BASE edificio completo | FUERA DEL ALCANCE / RESULTADO NO LOCALIZABLE / CONCURRENTE | NO CUMPLE | REQUIERE DATOS / REVISAR ENTRADAS FASE 7 |
| F7 20 BASE única válida | OK / CONCURRENTE | NO CUMPLE | REQUIERE DATOS |
| F7 21 Relleno sin pedestal | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 22 Relleno columna rectangular | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 23 Relleno con pedestal | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 24 Pedestal incluido en P | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 25 Pedestal sumado manual | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 26 Gamma tres pesos iguales | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 27 Gamma diferentes sin justificar | REQUIERE JUSTIFICACIÓN FACTORES DE PESOS / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS / REVISAR ENTRADAS FASE 7 |
| F7 28 Gamma diferentes documentados | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 29 Mz cero | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 30 Mz significativo | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA |
| F7 31 Servicio espectral reducción única 0.8 | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 32 Espectral SZ adverso | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE ANÁLISIS ESPECIAL |
| F7 33 RS en plano distinto bloqueado | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS — ESTADOS ESPECTRALES |
| F7 34 RS base sin ejes documentados | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS — ESTADOS ESPECTRALES |
| F7 35 Pedestal circular en dominio | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 36 Geometría manual bruto y bloqueo cuerpo | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE ANÁLISIS GEOMETRÍA LOCALIZADA |
| F7 37 Pedestal rebasa cara columna | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE ANÁLISIS GEOMETRÍA LOCALIZADA |
| F7 38 Relleno y pedestal excéntricos | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 39 Invariancia VISTA eta | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS |
| F7 40 Mz ruido | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 41 Cancelación Mz por signo propio | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA |
| F7 42 Constituyente RS detectado automáticamente | ESPECTRAL — USAR ESTADOS DERIVADOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS |
| F7 43 Externo combinado documentado | OK / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS |
| F7 44 Externo combinado sin procedimiento | REQUIERE DATOS / ESTADÍSTICO ESPECTRAL | NO CUMPLE | REQUIERE DATOS / REVISAR ENTRADAS FASE 7 |
| F7 45 CSI Frame I original | OK / CONCURRENTE | NO CUMPLE | REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA |
| F7 46 CSI Frame J original | OK / CONCURRENTE | NO CUMPLE | REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA |
| F7 47 Rotación local 37 grados | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |
| F7 48 Norma indefinida gravedad intacta | OK / MANUAL DOCUMENTADO | NO CUMPLE | REQUIERE DATOS |

## FORMULAS_CRITICAS_AUDITABLES

Las siguientes fórmulas son texto literal del XLSX final, en la sintaxis interna OOXML (funciones inglesas y separador coma). Excel español las presenta traducidas; no son instrucciones para pegarlas como fórmulas locales. Las filas 8 y primer bloque MU corresponden al primer último; las otras 59 filas conservan el mismo patrón desplazado. TOTAL_F7 integra 60 filas directas y 960 evaluaciones derivadas; las filas derivadas contienen IDs reales del registro. Las fórmulas de salida se incluyen junto con las de cálculo para poder seguir sus referencias.

### Nombres definidos → hoja/celda

Los aliases `zap7_*_u` de auditoría apuntan a la primera fila U8 / primer bloque MU, con referencias absolutas. No son selectores ni entradas nuevas. Los nombres globales de pesos y norma sí gobiernan los cálculos de todo el libro.

| Nombre | Referencia literal |
|---|---|
| `inp_cx` | `INGRESO_DATOS!$C$42` |
| `inp_cy` | `INGRESO_DATOS!$C$43` |
| `inp_fc` | `INGRESO_DATOS!$C$14` |
| `inp_fy` | `INGRESO_DATOS!$C$15` |
| `inp_gamma_c` | `INGRESO_DATOS!$C$16` |
| `inp_gamma_s` | `INGRESO_DATOS!$C$17` |
| `inp_h` | `INGRESO_DATOS!$C$32` |
| `inp_qadm` | `INGRESO_DATOS!$C$18` |
| `inp_xc` | `INGRESO_DATOS!$C$44` |
| `inp_yc` | `INGRESO_DATOS!$C$45` |
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

### Fórmulas literales por celda

**ENVOLVENTES!B5**

```excel
=IF(COUNTIF(TOTAL_F7_U!AP8:AR1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!AT8:BQ1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!EQ8:ES1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!FQ8:GK1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!IV8:JC1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!EU8:FP1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_S!AF8:BA1027,"NO CUMPLE")+COUNTIF(ENV_BARRAS!Y8:AA67,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!CA8:EO1027,"NO FACTIBLE")+COUNTIF(CALC_ENV_BARRAS!C8:BJ522,"NO CUMPLE")>0,"NO CUMPLE",IF(B6="COMPLETO","CUMPLE","SIN RESULTADO COMPLETO"))
```

**ENVOLVENTES!B6**

```excel
=IF(SUM(COUNTIF(COMBOS_ULTIMOS!CT8:CT67,"REQUIERE DEFINIR NORMA E.030 APLICABLE"),COUNTIF(COMBOS_SERVICIO!DM8:DM67,"REQUIERE DEFINIR NORMA E.030 APLICABLE"))>0,"REQUIERE DEFINIR NORMA E.030 APLICABLE",IF(COUNTIF(TOTAL_F7_U!ET8:ET1027,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA")+COUNTIF(TOTAL_F7_S!AJ8:AJ1027,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA")>0,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",IF(COUNTIFS(ESPECTROS_U!A8:A67,"SI",ESPECTROS_U!AI8:AI67,"<>OK")+COUNTIFS(ESPECTROS_S!A8:A67,"SI",ESPECTROS_S!AI8:AI67,"<>OK")>0,"REQUIERE DATOS — ESTADOS ESPECTRALES",IF(CONTROL_FASE7!B41<>"OK",CONTROL_FASE7!B41,IF(COUNTIFS(COMBOS_ULTIMOS!A8:A67,"SI",COMBOS_ULTIMOS!K8:K67,"<>OK",COMBOS_ULTIMOS!K8:K67,"<>ESPECTRAL — USAR ESTADOS DERIVADOS")+COUNTIFS(COMBOS_SERVICIO!A8:A67,"SI",COMBOS_SERVICIO!O8:O67,"<>OK",COMBOS_SERVICIO!O8:O67,"<>ESPECTRAL — USAR ESTADOS DERIVADOS")>0,"REQUIERE DATOS / REVISAR ENTRADAS FASE 7",IF(COUNTIF(TOTAL_F7_U!GM8:GM1027,"DATOS INVÁLIDOS")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"DATOS INVÁLIDOS")+COUNTIF(ENV_BARRAS!Y8:AA67,"DATOS INVÁLIDOS")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"DATOS INVÁLIDOS")+COUNTIF(COMBOS_ULTIMOS!K8:K67,"DATOS NO CONCURRENTES — NO USAR COMO COMBO")+COUNTIF(COMBOS_SERVICIO!O8:O67,"DATOS NO CONCURRENTES — NO USAR COMO COMBO")>0,"DATOS INVÁLIDOS",IF(COUNTIF(TOTAL_F7_U!GM8:GM1027,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(ENV_BARRAS!Y8:AA67,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE",IF(COUNTIF(TOTAL_F7_U!GM8:GM1027,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(ENV_BARRAS!Y8:AA67,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")>0,"REQUIERE CONTACTO PARCIAL",IF(COUNTIF(TOTAL_F7_U!GM8:GM1027,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(ENV_BARRAS!Y8:AA67,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(TOTAL_F7_U!GM8:GM1027,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(ENV_BARRAS!Y8:AA67,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(OR(CONTROL_MULTICOMBO!$B$33<>"COMPLETO",CONTROL_MULTICOMBO!$B$35<>"OK",COUNTIF(COMBOS_ULTIMOS!V8:V67,"REQUIERE DATOS")>0,COUNTIF(COMBOS_ULTIMOS!A8:A67,"SI")=0,COUNTIF(COMBOS_SERVICIO!A8:A67,"SI")=0,COUNTIF(TOTAL_F7_U!GM8:GM1027,"REQUIERE DATOS")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"REQUIERE DATOS")+COUNTIF(ENV_BARRAS!Y8:AA67,"REQUIERE DATOS")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"REQUIERE DATOS")>0),"REQUIERE DATOS","COMPLETO"))))))))))
```

**ENVOLVENTES!B8**

```excel
=IF(ISNUMBER(H8),INDEX(TOTAL_F7_U!B1:B1027,H8),"")
```

**ENVOLVENTES!G8**

```excel
=IF(J8>0,MAX(TOTAL_F7_U!$GN$8:$GN$1027),"")
```

**ENVOLVENTES!H8**

```excel
=IF(J8>0,MATCH(G8,TOTAL_F7_U!$GN$8:$GN$1027,0)+7,"")
```

**ENVOLVENTES!B48**

```excel
=IF(ISNUMBER(H48),INDEX(TOTAL_F7_S!B1:B1027,H48),"")
```

**ENVOLVENTES!G48**

```excel
=IF(J48>0,MAX(TOTAL_F7_S!$BN$8:$BN$1027),"")
```

**ENVOLVENTES!H48**

```excel
=IF(J48>0,MATCH(G48,TOTAL_F7_S!$BN$8:$BN$1027,0)+7,"")
```

**ENVOLVENTES!B54**

```excel
=CONTROL_MULTICOMBO!$B$33
```

**ENVOLVENTES!B56**

```excel
=IF(COUNT(TOTAL_F7_U!HW8:HW1027)>=2,INDEX(TOTAL_F7_U!B8:B1027,MATCH(2,TOTAL_F7_U!HW8:HW1027,0)),"")
```

**ENVOLVENTES!E56**

```excel
=IF(COUNT(TOTAL_F7_U!HW8:HW1027)>=2,INDEX(TOTAL_F7_U!AQ8:AQ1027,MATCH(2,TOTAL_F7_U!HW8:HW1027,0)),"")
```

**ENVOLVENTES!B57**

```excel
=IF(COUNT(TOTAL_F7_U!HW8:HW1027)>=3,INDEX(TOTAL_F7_U!B8:B1027,MATCH(3,TOTAL_F7_U!HW8:HW1027,0)),"")
```

**ENVOLVENTES!E57**

```excel
=IF(COUNT(TOTAL_F7_U!HW8:HW1027)>=3,INDEX(TOTAL_F7_U!AQ8:AQ1027,MATCH(3,TOTAL_F7_U!HW8:HW1027,0)),"")
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

**CONTROL_FASE7!B10**

```excel
=IF(OR(B7="REQUIERE DEFINIR",LEN(B8)=0,LEN(B9)=0),"REQUIERE DEFINIR NORMA E.030 APLICABLE",IF(OR(B7="E.030 ANTERIOR A RM 183-2026",B7="E.030 MODIFICADA RM 183-2026"),"OK","DATOS INVÁLIDOS"))
```

**CONTROL_FASE7!B16**

```excel
=IF(B10<>"OK",B10,IF(B7="E.030 MODIFICADA RM 183-2026","ART. 28.1 / 43: SRSS 100-30; vertical adversa ART. 28.5",IF(B12="REGULAR","ART. 24.1: SX y SY independientes","REQUIERE DIRECCIÓN MÁS DESFAVORABLE DOCUMENTADA")))
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

**COMBOS_ULTIMOS!K8**

```excel
=IF(AND(BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(BU8)=0),"REQUIERE DATOS",IF(OR(BP8="MODAL",COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"U",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$F$8:$F$1447,"MODAL")>0),"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"U",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$I$8:$I$1447,"<>OK")>0,"REQUIERE DATOS — INVENTARIO CSI",IF(AND(AND(BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(BU8)>0,zap7_norma_estado="OK"),CS8="OK"),CZ8,IF(A8="NO","NO APLICA",IF(CS8<>"OK",CS8,IF(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA"),CT8,IF(CT8<>"NO APLICA",IF(CT8="OK",CZ8,CT8),CZ8))))))))
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
=IF(AND(BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(BU8)>0,zap7_norma_estado="OK"),"OK",IF(AND(NOT(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA")),BT8="NO"),"NO APLICA",IF(CONTROL_FASE7!$B$10<>"OK",CONTROL_FASE7!$B$10,IF(OR(LEN(BP8)=0,LEN(BQ8)=0,NOT(OR(BR8="SI",BR8="NO"))),"REQUIERE DATOS",IF(AND(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA"),BS8<>"B. ESPECTRO DE RESPUESTA"),"REQUIERE TRATAMIENTO ESPECTRAL",IF(AND(BS8="D. RESULTADO EXTERNO YA COMBINADO",LEN(BU8)=0),"REQUIERE DATOS",IF(AND(NOT(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA")),CY8<>"OK"),CY8,IF(OR(BP8="RESPONSE SPECTRUM",BR8="SI",BS8="B. ESPECTRO DE RESPUESTA"),"ESPECTRAL — USAR ESTADOS DERIVADOS","OK"))))))))
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
=IF(AND(CL8="D. RESULTADO EXTERNO YA COMBINADO",LEN(CN8)=0),"REQUIERE DATOS",IF(OR(CI8="MODAL",COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"S",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$F$8:$F$1447,"MODAL")>0),"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"S",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$I$8:$I$1447,"<>OK")>0,"REQUIERE DATOS — INVENTARIO CSI",IF(AND(AND(CL8="D. RESULTADO EXTERNO YA COMBINADO",LEN(CN8)>0,zap7_norma_estado="OK"),DL8="OK"),DS8,IF(A8="NO","NO APLICA",IF(DL8<>"OK",DL8,IF(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA"),DM8,IF(DM8<>"NO APLICA",IF(DM8="OK",DS8,DM8),DS8))))))))
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
=IF(AND(CL8="D. RESULTADO EXTERNO YA COMBINADO",LEN(CN8)>0,zap7_norma_estado="OK"),"OK",IF(AND(NOT(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA")),CM8="NO"),"NO APLICA",IF(CONTROL_FASE7!$B$10<>"OK",CONTROL_FASE7!$B$10,IF(OR(LEN(CI8)=0,LEN(CJ8)=0,NOT(OR(CK8="SI",CK8="NO"))),"REQUIERE DATOS",IF(AND(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA"),CL8<>"B. ESPECTRO DE RESPUESTA"),"REQUIERE TRATAMIENTO ESPECTRAL",IF(AND(CL8="D. RESULTADO EXTERNO YA COMBINADO",LEN(CN8)=0),"REQUIERE DATOS",IF(AND(NOT(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA")),DR8<>"OK"),DR8,IF(OR(CI8="RESPONSE SPECTRUM",CK8="SI",CL8="B. ESPECTRO DE RESPUESTA"),"ESPECTRAL — USAR ESTADOS DERIVADOS","OK"))))))))
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
=IF(COMBOS_ULTIMOS!BS8="D. RESULTADO EXTERNO YA COMBINADO","NO",IF(AND(COMBOS_ULTIMOS!A8="SI",OR(COMBOS_ULTIMOS!BP8="RESPONSE SPECTRUM",COMBOS_ULTIMOS!BR8="SI",COMBOS_ULTIMOS!BS8="B. ESPECTRO DE RESPUESTA")),"SI","NO"))
```

**ESPECTROS_U!AI8**

```excel
=IF(OR(AND(A8="SI",C8=D8),AND(A8="SI",COMBOS_ULTIMOS!BI8<>"OK"),COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"U",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$I$8:$I$1447,"<>OK")>0),"REQUIERE DATOS — FUENTE ESPECTRAL",IF(A8<>"SI","NO APLICA",IF(COMBOS_ULTIMOS!CS8<>"OK",COMBOS_ULTIMOS!CS8,IF(CONTROL_FASE7!$B$10<>"OK",CONTROL_FASE7!$B$10,IF(OR(LEN(C8)=0,LEN(D8)=0,LEN(G8)=0,LEN(H8)=0,LEN(J8)=0,I8<>"SI",LEN(COMBOS_ULTIMOS!BQ8)=0,LEN(COMBOS_ULTIMOS!CK8)=0,LEN(COMBOS_ULTIMOS!CL8)=0),"REQUIERE DATOS",IF(OR(COMBOS_ULTIMOS!BV8<>"INTERFAZ COLUMNA-ZAPATA",NOT(ISNUMBER(COMBOS_ULTIMOS!CR8)),ABS(COMBOS_ULTIMOS!CR8)>0.00000001),"REQUIERE RECOMBINACIÓN MODAL EN INTERFAZ",IF(COUNT(K8:AB8)<>18,"REQUIERE DATOS",IF(MIN(Q8:AB8)<0,"DATOS INVÁLIDOS",IF(OR(NOT(OR(F8="SI",F8="NO")),CONTROL_FASE7!$B$14="REQUIERE DEFINIR",LEN(CONTROL_FASE7!$B$15)=0),"REQUIERE DEFINIR COMPONENTE VERTICAL",IF(AND(CONTROL_FASE7!$B$14="SI",F8<>"SI"),"REQUIERE COMPONENTE VERTICAL",IF(AND(F8="SI",OR(LEN(E8)=0,COUNT(AC8:AH8)<>6,MIN(AC8:AH8)<0)),"REQUIERE DATOS",IF(AND(CONTROL_FASE7!$B$7="E.030 ANTERIOR A RM 183-2026",OR(CONTROL_FASE7!$B$12<>"REGULAR",LEN(CONTROL_FASE7!$B$13)=0)),"REQUIERE DIRECCIÓN MÁS DESFAVORABLE DOCUMENTADA",IF(AND(CONTROL_FASE7!$B$7="E.030 MODIFICADA RM 183-2026",OR(CONTROL_FASE7!$B$12<>"REGULAR",LEN(CONTROL_FASE7!$B$13)=0)),"REQUIERE EJES NO PARALELOS / PROCEDIMIENTO EXTERNO","OK")))))))))))))
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
=ESPECTROS_U!B8&"-X01"
```

**DERIVADOS_U!H8**

```excel
=ESPECTROS_U!AJ8
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
=IF(ESPECTROS_U!F8="SI",1,0)
```

**DERIVADOS_U!R8**

```excel
=IF(Z8="OK",ESPECTROS_U!K8+L8*(SQRT((I8*ESPECTROS_U!Q8)^2+(J8*ESPECTROS_U!W8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AC8),ESPECTROS_U!AC8,0)),"")
```

**DERIVADOS_U!S8**

```excel
=IF(Z8="OK",ESPECTROS_U!L8+M8*(SQRT((I8*ESPECTROS_U!R8)^2+(J8*ESPECTROS_U!X8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AD8),ESPECTROS_U!AD8,0)),"")
```

**DERIVADOS_U!T8**

```excel
=IF(Z8="OK",ESPECTROS_U!M8+N8*(SQRT((I8*ESPECTROS_U!S8)^2+(J8*ESPECTROS_U!Y8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AE8),ESPECTROS_U!AE8,0)),"")
```

**DERIVADOS_U!U8**

```excel
=IF(Z8="OK",ESPECTROS_U!N8+O8*(SQRT((I8*ESPECTROS_U!T8)^2+(J8*ESPECTROS_U!Z8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AF8),ESPECTROS_U!AF8,0)),"")
```

**DERIVADOS_U!V8**

```excel
=IF(Z8="OK",ESPECTROS_U!O8+P8*(SQRT((I8*ESPECTROS_U!U8)^2+(J8*ESPECTROS_U!AA8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AG8),ESPECTROS_U!AG8,0)),"")
```

**DERIVADOS_U!W8**

```excel
=IF(Z8="OK",ESPECTROS_U!P8+Q8*(SQRT((I8*ESPECTROS_U!V8)^2+(J8*ESPECTROS_U!AB8)^2)+K8*IF(ISNUMBER(ESPECTROS_U!AH8),ESPECTROS_U!AH8,0)),"")
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
=IF(Z8="OK",IF(ABS(W8)>zap7_mz_tol,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA","OK"),Z8)
```

**DERIVADOS_U!AS8**

```excel
=MOTOR_H_U!AYN8
```

**DERIVADOS_U!AT8**

```excel
=MOTOR_H_U!AYM8
```

**DERIVADOS_U!AU8**

```excel
=MOTOR_H_U!AXR8
```

**TOTAL_F7_U!A8**

```excel
=IF(ESPECTROS_U!A8="SI","NO",RESULTADOS_ULTIMOS!A8)
```

**TOTAL_F7_U!AQ8**

```excel
=IF(ISBLANK(RESULTADOS_ULTIMOS!AQ8),"",RESULTADOS_ULTIMOS!AQ8)
```

**TOTAL_F7_U!GN68**

```excel
=IF(DU_INPUT!A8="SI",MOTOR_ESPECTRAL_U!AZL8,"")
```

**TOTAL_F7_U!HW68**

```excel
=IF(ISNUMBER(GN68),COUNTIF($GN$8:$GN$1027,">"&GN68)+COUNTIF($GN$8:GN68,GN68),"")
```

**VISTA_DERIVADO!B11**

```excel
=IF(IF(B7="U",INDEX(DERIVADOS_U!$A$8:$A$7687,B8),INDEX(DERIVADOS_S!$A$8:$A$7687,B8))="SI",IFERROR(IF(B7="U",INDEX(DERIVADOS_U!B8:B7687,B8),INDEX(DERIVADOS_S!B8:B7687,B8)),""),"NO APLICA")
```

**VISTA_DERIVADO!B14**

```excel
=IF(IF(B7="U",INDEX(DERIVADOS_U!$A$8:$A$7687,B8),INDEX(DERIVADOS_S!$A$8:$A$7687,B8))="SI",IFERROR(IF(B7="U",INDEX(DERIVADOS_U!H8:H7687,B8),INDEX(DERIVADOS_S!H8:H7687,B8)),""),"NO APLICA")
```

**VISTA_DERIVADO!B15**

```excel
=IF(IF(B7="U",INDEX(DERIVADOS_U!$A$8:$A$7687,B8),INDEX(DERIVADOS_S!$A$8:$A$7687,B8))="SI",IFERROR(IF(B7="U",INDEX(DERIVADOS_U!X8:X7687,B8),INDEX(DERIVADOS_S!X8:X7687,B8)),""),"NO APLICA")
```

**VISTA_DERIVADO!B22**

```excel
=IF(IF(B7="U",INDEX(DERIVADOS_U!$A$8:$A$7687,B8),INDEX(DERIVADOS_S!$A$8:$A$7687,B8))="SI",IFERROR(IF(B7="U",INDEX(DERIVADOS_U!Z8:Z7687,B8),INDEX(DERIVADOS_S!Z8:Z7687,B8)),""),"NO APLICA")
```

## Integridad de la entrega

Solo se incorporan al commit el XLSX F7 y este documento. Los informes, scripts, PDF oficiales, vistas y fixtures de auditoría se mantienen como soporte local sin formar parte de los dos entregables. El tamaño y tiempo de apertura aumentaron por los estados espectrales y la trazabilidad explícita; los motores auxiliares permanecen ocultos, y el visor facilita la consulta. La validación corresponde a los escenarios declarados y al alcance descrito; la aplicabilidad E.030 y las fuentes reales del proyecto siguen pendientes de acreditación.

SHA-256 del XLSX final: `abf3154b4e3276578ba2e3330b48cd72a0346a264f9cd080b51d7e3a7330f593`. Tamaño: 76,684,061 bytes.
