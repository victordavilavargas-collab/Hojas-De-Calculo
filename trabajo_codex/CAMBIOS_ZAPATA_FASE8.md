# Fase 8: auditoría E.030 y depuración del motor de zapata

Base: Fase 7, commit `a48a97e939f0026884715cb2f5b1e259eea90057`. El trabajo incorpora controles documentales de la fuente sísmica y elimina fórmulas repetidas o auxiliares sin consumidores. Conserva 60 combinaciones últimas, 60 de servicio, 128 estados de signos por padre, 16 evaluaciones del cuerpo por padre, las verificaciones con H/Mz propios, conexión, barras 60×60, gobernantes y vistas.

La geometría, materiales, acero, cargas y qadm del proyecto no se ajustaron para obtener CUMPLE. Los ejemplos de verificación son sintéticos y se cerraron sin guardar sus datos. Las declaraciones SI y referencias de esos ejemplos no se trasladaron al proyecto.

## Cambios normativos y uso

`CONTROL_E030_F8` contiene regularidad y sistemas no paralelos como entradas distintas, ambas con referencia. IRREGULAR + sistemas paralelos NO ya no activa por sí solo el art.28.2. SI exige un procedimiento externo con direcciones adicionales; el generador X/Y no acredita esa comprobación. La selección de versión y su justificación siguen en `CONTROL_FASE7!B7:B10`.

`FUENTES_E030` admite 60 identificadores únicos de modelo/fuente. Las masas se registran en kg, las fuerzas en tf; se calculan participación, cortantes finales y factores mínimos. Cada demanda remite a un ID exacto, sin sumar masas ni cortantes de modelos diferentes. X e Y deben alcanzar 90% de masa efectiva y considerar al menos los tres primeros modos predominantes, con referencia. Se rechazan masas negativas, efectivas mayores que la total, modos fraccionarios e IDs duplicados. CQC o la alternativa del art.42.3 requieren confirmación de aplicación y referencia; no equivalen a combinación direccional.

El art.44 se audita con Vest, Vdin antes de escala, factor aplicado en fuente y Vdin final por dirección. Se exige 0.80Vest para regular y 0.90Vest para irregular. El factor requerido es MAX(1, límite×Vest/Vdin). La declaración de escalamiento proporcional de fuerzas y su referencia son obligatorias. Esos factores **no vuelven a multiplicar las acciones importadas a la zapata**.

`DEMANDAS_E030` contiene 120 registros vinculados a las filas 8:67 de U/S. Para sismo estático del texto 2026, exige verificación externa documentada de admisibilidad 33.2 y de combinación 33.3. No presume SI. La referencia 33.2 debe acreditar zona, altura, regularidad y sistema; el art.33.2 permite el método para todas las estructuras de zona 1 y, en otras zonas, para estructuras regulares hasta 30 m y los supuestos de muros portantes hasta 15 m que allí se especifican. La fuente debe documentar la suma absoluta 100/30; un EX o EY simple se rechaza.

Se registran por separado X100 +e, X100 −e, su referencia de rama, y Y100 +e, Y100 −e, su referencia. Una declaración genérica de excentricidad no sustituye esa correspondencia. La historia de tiempo conserva sus componentes simultáneas y controles de Time/Step de F7; no se rotula como SRSS modal.

El requerimiento vertical se separa de disponibilidad y procedimiento. Las dimensiones positivas de la columna permiten reconocer un elemento vertical y hacen obligatorio SI, incluso si se intenta seleccionar OTRO DOCUMENTADO o NO. En una demanda espectral interna se exige además `ESPECTROS_U/S!F="SI"`; disponer de una referencia sin el componente no basta. El procedimiento fuente debe acreditar el espectro vertical y la condición adversa de signos de los arts.28.4/28.5 y 41.2. No se inventa un SZ del proyecto.

Para servicio sísmico 2026, la reducción 0.80 de los arts.29/62.2 es obligatoria. La declaración previa se conserva en `COMBOS_SERVICIO!AI`; su referencia en AC, y el factor adicional en L. NO + 0.80 es válido; SI + 1.00 exige referencia. NO + 1.00, SI + 0.80 y factor no numérico se rechazan. La base gravitatoria firmada no se reduce. El aumento opcional de qadm de E.060 15.2.4 se conserva como autorización independiente del proyecto/EMS y no sustituye la reducción de fuerzas.

La combinación direccional modal SRSS 100/30 E.030 y la **ENVOLVENTE CONSERVADORA DE SIGNOS** aparecen como conceptos separados. La segunda cubre interacciones no reconstruidas físicamente y puede ser más exigente que un resultado externo con interacción documentada. Cuando el único fallo técnico procede de esa caja, se muestra **NO CUMPLE ENVOLVENTE CONSERVADORA — VERIFICAR INTERACCIÓN EXTERNA**. El D/C y los IDs permanecen visibles. No se transforma ese fallo en CUMPLE ni en un incumplimiento normativo atribuido automáticamente a E.030. Los fallos directos independientes mantienen NO CUMPLE.

Los controles de demanda alimentan los estados de entradas U/S, espectros y validez global. `ENVOLVENTES` y `RESUMEN` muestran versión/dirección, interacción y estado de fuente. `CONTROL_FASE7!B12:B15` son ahora enlaces al control F8; no son entradas duplicadas.

En DEMANDAS, las columnas S:X presentan requisitos parciales de preparación. La columna Y determina su aplicabilidad: un padre inactivo devuelve NO APLICA y uno únicamente gravitatorio devuelve OK sin exigir documentos sísmicos. Ese OK no certifica una fuente modal ni significa que los campos parciales sísmicos se hayan completado. En FUENTES, un ID vacío devuelve NO APLICA en AC; los requisitos de Z:AB permanecen visibles para preparar la fuente.

## Fuentes y régimen aplicable

La [RM 183-2026-VIVIENDA](https://www.gob.pe/institucion/vivienda/normas-legales/8081915-183-2026-vivienda) modifica E.030; se revisó el [texto oficial 2026](https://epdoc2.elperuano.pe/EpPo/DescargaIN.asp?Referencias=MjUxMTI1OF8xMjAyNjA1MDM=), en particular arts.28–29, 33, 37, 40–45 y 62. La [RM 217-2026-VIVIENDA](https://busquedas.elperuano.pe/dispositivo/NL/2521423-1) amplía el régimen transitorio a los supuestos documentados de expedientes, licencias, anteproyectos, APP y saldos de obra que describe. La fecha de archivo o de esta revisión no decide por sí sola la versión aplicable. Si corresponde transición, se conserva la opción de [E.030 anterior](https://cdn.www.gob.pe/uploads/document/file/2366641/51%20E.030%20DISE%C3%91O%20SISMORRESISTENTE%20RM-043-2019-VIVIENDA.pdf?v=1677250657), sin presumir elegibilidad.

Se mantienen [E.060 DS 010-2009](https://cdn.www.gob.pe/uploads/document/file/2686419/E.060%20Concreto%20Armado%20DS%20N%C2%B0%20010-2009.pdf) y [E.050 RM 406-2018](https://cdn.www.gob.pe/uploads/document/file/2366655/54%20E.050%20SUELOS%20Y%20CIMENTACIONES%20RM%20N%C2%B0%20406-2018-VIVIENDA.pdf), contrastadas con el [catálogo oficial RNE](https://www.gob.pe/institucion/vivienda/informes-publicaciones/2309793-reglamento-nacional-de-edificaciones-rne). La [referencia de análisis CSI](https://docs.csiamerica.com/manuals/etabs/Analysis%20Reference.pdf) y la [documentación de Response Spectrum](https://docs.csiamerica.com/help-files/etabs/Menus/Define/Load_Cases/Response_Spectrum.htm) sustentan la separación de máximos estadísticos y acciones concurrentes. La auditoría registra evidencia del modelo; no reproduce ni certifica el análisis global externo.

## Refactorización aplicada y límites

Se eliminan 264895 fórmulas con expresiones completas repetidas: DU_INPUT 92038, DS_INPUT 109557, MOTOR_ESPECTRAL_U 41940 y MOTOR_ESPECTRAL_S 21360. Los consumidores apuntan a la celda propietaria existente mediante referencias absolutas. Se conservaron columnas que participan en rangos para evitar cambiar el tratamiento de celdas vacías, texto o agregaciones. No se pegaron resultados como valores.

Un análisis adicional de consumidores externos y dependencias internas eliminó 192060 fórmulas auxiliares sin uso: 60 en MOTOR_ESPECTRAL_U, 115200 en MOTOR_H_U y 76800 en MOTOR_H_S. Las celdas de presentación y los registros de DERIVADOS permanecen. La cadena de cálculo se ajustó con los sheetId reales, incluyendo sus discontinuidades; no se reasignaron IDs por posición de hoja.

Columnas internas retiradas: MOTOR_ESPECTRAL_U BAU/BAY/BBA/BBE/BBG/BBK/BBM/BBQ/BBS; MOTOR_H_U AXS/AXW/AXX/AXY/AXZ/AYA/AYB/AYC/AYF/BAO/BAP/BAQ/BAR/BAS/BAT; MOTOR_H_S DG/DK/DM/DO/DQ/EN/EO/EP/EQ/ER. La mayoría de las nueve primeras ya había sido eliminada por reutilización exacta, de ahí que ese paso retire solo 60 fórmulas adicionales en U.

La meta del 40% **no se alcanzó**. Los bloques que se conservan están cuantificados por hoja en el perfil siguiente. El cuerpo U conserva 960 evaluaciones con geometría, presión, integración, punzonamiento, cuatro cortantes y ocho As; H conserva 7680 vectores propios por grupo; DERIVADOS conserva las 128 hipótesis por padre y sus referencias auditables; TOTAL conserva candidatos elegibles y gobernantes; las barras conservan fuerzas externas por estado. La reutilización adicional de expresiones parecidas, pero con validaciones o dependencias distintas, requeriría otra reestructuración y regresión completa. No se declaró equivalencia algebraica sin evidencia ni se redujo capacidad para forzar el porcentaje.

Se ensayaron shared formulas OOXML en los grandes motores. Excel local (Office 2021, motor 16.0) no conservó correctamente ese ensayo y pidió reparación; la variante se descartó. El entregable usa expresiones completas en esos motores y conserva solo fórmulas compartidas aceptadas nativamente. Las celdas con fórmula se cuentan incluyendo seguidores compartidos: no se confunde número de definiciones XML con número de celdas calculadas. La compresión ZIP final modifica almacenamiento, no el contenido de las fórmulas.

## Alcance que permanece pendiente

No se incorporan Capítulo 21, contacto parcial, borde/esquina, solver Mz, pedestal localizado mayor que la columna ni solver general interno P-Mx-My. Persisten los bloqueos F7 y la tolerancia Mz 1E−6 tf·m. Continúan plano de corte, end offsets, transformación CSI, concurrencia, pesos reales Wz/Wped/Ws y hueco del relleno, presión bruta/neto, integración localizada dentro del dominio F7, conexión, armado y cobertura. Que una fuente E.030 quede válida no significa que la zapata, conexión o cobertura cumplan.

Huellas SHA-256 de las copias primarias consultadas:

| Fuente | SHA-256 |
|---|---|
| E030-2026.pdf | `d119f9bd35a30dd0ea3a90296d7811c5811a0af7d93fc13c5a9a9d3963fefba6` |
| E060-fuente.pdf | `6b4676e849fd65243e3c4428c22156eba6e52829366f49a0a2d1cad550e1c709` |
| E050-fuente.pdf | `1877822c786a8747b9520934b97bdab5b3e505ab37ec9cbb28625442756160a3` |
| CSI.pdf | `7f6f6890afee2e1890d33f5d34d53d8e23f60850890bd230848642b50a6291ac` |

## Métricas finales y perfil

| Métrica | F7 | F8 | Cambio |
|---|---:|---:|---:|
| Hojas | 75 | 78 | +3 controles |
| Celdas con fórmula | 3467540 | 3012765 | −454775 (13.12%) |
| XLSX bytes | 76684061 | 68554205 | −8129856 (10.60%) |

CalculateFullRebuild del primer escenario común: F7 **132.369 s**; reutilización exacta previa a controles **123.072 s**; F8 final con controles **186.202 s**. El cierre del proyecto sin fixtures midió **341.668 s**, y la reapertura fría **172.190 s** de recálculo, con **242.357 s** de apertura. Son mediciones de esta máquina y ejecuciones sucesivas, sin aislamiento de otros procesos ni control de caché. No se acredita una mejora de rendimiento total si el tiempo final observado es mayor; tamaño y número de fórmulas son métricas separadas.

El perfil cuenta celdas con fórmula, bytes XML sin comprimir y tokens de referencia A1. Estos tokens y el volumen de expresión son una aproximación al costo de dependencias, no tiempos independientes de recálculo por hoja ni un conteo de aristas únicas. Parseo XML es costo de inspección, no cálculo de Excel. Se excluye del tamaño XML de cada hoja la cadena global de cálculo, estilos y dibujos.

| Hoja | Fórmulas F7 | Fórmulas F8 | XML F7 bytes | XML F8 bytes | Tokens refs F7/F8 | Parseo F8 s | Dependencias F8 | Tratamiento |
|---|---:|---:|---:|---:|---:|---:|---|---|
| ENVOLVENTES | 821 | 827 | 178822 | 181255 | 5035/5102 | 0.034 | ANALISIS_COMPLEMENTARIO, BARRAS_CONEXION, CALC_ENV_BARRAS, COMBOS_SERVICIO, COMBOS_ULTIMOS, CONTROL_E030_F8, CONTROL_FASE7, CONTROL_MULTICOMBO, DEMANDAS_E030, DERIVADOS_S, DERIVADOS_U, ENV_BARRAS, ESPECTROS_S, ESPECTROS_U, RESULTADOS_SERVICIO, RESULTADOS_ULTIMOS, TOTAL_F7_S, TOTAL_F7_U | Conservado: dependencias o salida trazable |
| VISTA_COMBO | 7 | 7 | 6839 | 6843 | 33/33 | 0.001 | ANALISIS_COMPLEMENTARIO, COMBOS_SERVICIO, COMBOS_ULTIMOS, ENVOLVENTES | Conservado: dependencias o salida trazable |
| CONTROL_MULTICOMBO | 13 | 13 | 9222 | 9222 | 38/38 | 0.001 | CONTROL_FASE7 | Conservado: dependencias o salida trazable |
| CONTROL_FASE7 | 13 | 17 | 12024 | 11951 | 74/95 | 0.002 | CONTROL_E030_F8 | Conservado: dependencias o salida trazable |
| INGRESO_DATOS | 9 | 9 | 59272 | 59272 | 0/0 | 0.006 | — | Conservado: dependencias o salida trazable |
| BARRAS_PERU | 0 | 0 | 5161 | 5161 | 0/0 | 0.001 | — | Conservado: dependencias o salida trazable |
| CARGAS | 14 | 14 | 12427 | 12427 | 50/50 | 0.002 | MS_CARGAS, MU_CARGAS | Conservado: dependencias o salida trazable |
| GEOMETRIA | 23424 | 23424 | 1938784 | 1938784 | 947/947 | 0.336 | — | Conservado: dependencias o salida trazable |
| RESULTANTE | 29 | 29 | 8602 | 8602 | 86/86 | 0.004 | MS_RESULTANTE, MU_RESULTANTE | Conservado: dependencias o salida trazable |
| PRESIONES_SERVICIO | 55 | 55 | 30846 | 30846 | 200/200 | 0.004 | MS_SERVICIO | Conservado: dependencias o salida trazable |
| PRESIONES_ULTIMAS | 15 | 15 | 11516 | 11516 | 53/53 | 0.001 | MU_PRESION | Conservado: dependencias o salida trazable |
| DIAGRAMAS_X | 599 | 599 | 72823 | 72823 | 813/813 | 0.011 | MU_DIAG_X | Conservado: dependencias o salida trazable |
| DIAGRAMAS_Y | 599 | 599 | 72626 | 72626 | 813/813 | 0.011 | MU_DIAG_Y | Conservado: dependencias o salida trazable |
| PUNZONAMIENTO | 65 | 65 | 32050 | 32050 | 204/204 | 0.004 | MU_PUNZ | Conservado: dependencias o salida trazable |
| CORTANTE_UNIDIRECCIONAL | 47 | 47 | 15417 | 15417 | 166/166 | 0.003 | MU_CORT | Conservado: dependencias o salida trazable |
| FLEXION_ACERO | 94 | 94 | 31608 | 31608 | 194/194 | 0.004 | DIAGRAMAS_X, DIAGRAMAS_Y, MU_FLEX, PUNZONAMIENTO | Conservado: dependencias o salida trazable |
| ACERO_DETALLADO | 551 | 551 | 186032 | 186032 | 1519/1519 | 0.024 | ACERO_DETALLADO, CONEXION_COLUMNA_ZAPATA, FLEXION_ACERO, MU_ACERO, PUNZONAMIENTO | Conservado: dependencias o salida trazable |
| GRAFICOS | 346 | 346 | 32539 | 32539 | 4/4 | 0.006 | — | Conservado: dependencias o salida trazable |
| RESUMEN | 189 | 195 | 82581 | 83870 | 172/178 | 0.009 | ACERO_DETALLADO, CONEXION_COLUMNA_ZAPATA, CONTROL_FASE7, CONTROL_MULTICOMBO, CORTANTE_UNIDIRECCIONAL, DIAGRAMAS_X, DIAGRAMAS_Y, ENVOLVENTES, ESPECTROS_S, ESPECTROS_U, FLEXION_ACERO, MS_ESTADOS, MU_ESTADOS, PRESIONES_SERVICIO, PRESIONES_ULTIMAS, PUNZONAMIENTO | Conservado: dependencias o salida trazable |
| CONEXION_COLUMNA_ZAPATA | 62 | 62 | 53278 | 53278 | 214/214 | 0.006 | BARRAS_CONEXION, CONEXION_COMBOS, MU_CONEXION | Conservado: dependencias o salida trazable |
| BARRAS_CONEXION | 5400 | 5400 | 777925 | 777925 | 38804/38804 | 0.225 | MU_BARRAS | Conservado: dependencias o salida trazable |
| MAPEO_IMPORTACION | 2 | 2 | 9387 | 9403 | 36/36 | 0.003 | — | Conservado: dependencias o salida trazable |
| COMBOS_ULTIMOS | 2160 | 2160 | 544326 | 552209 | 13630/14233 | 0.280 | CASOS_CONSTITUYENTES, CONTROL_FASE7, CONTROL_MULTICOMBO, DEMANDAS_E030 | Conservado: dependencias o salida trazable |
| COMBOS_SERVICIO | 2700 | 2700 | 593108 | 601147 | 14104/14706 | 0.326 | CASOS_CONSTITUYENTES, CONTROL_FASE7, CONTROL_MULTICOMBO, DEMANDAS_E030 | Conservado: dependencias o salida trazable |
| CONEXION_COMBOS | 181 | 181 | 58620 | 58636 | 1621/1621 | 0.026 | COMBOS_ULTIMOS, CONTROL_MULTICOMBO | Conservado: dependencias o salida trazable |
| FUERZAS_BARRAS | 181 | 181 | 102521 | 102537 | 301/301 | 0.037 | BARRAS_CONEXION, COMBOS_ULTIMOS, CONTROL_MULTICOMBO | Conservado: dependencias o salida trazable |
| RESULTADOS_ULTIMOS | 15840 | 15840 | 3246181 | 3246197 | 81632/81632 | 1.861 | COMBOS_ULTIMOS, CONEXION_COLUMNA_ZAPATA, CONTROL_MULTICOMBO, MU_ACERO, MU_CARGAS, MU_CONEXION, MU_CORT, MU_DIAG_X, MU_DIAG_Y, MU_ESTADOS, MU_FLEX, MU_PRESION, MU_PUNZ, MU_RESULTANTE, PUNZONAMIENTO, RESUMEN | Conservado: dependencias o salida trazable |
| RESULTADOS_SERVICIO | 4320 | 4320 | 667990 | 668006 | 18240/18240 | 0.330 | COMBOS_SERVICIO, MS_CARGAS, MS_ESTADOS, MS_SERVICIO, RESUMEN | Conservado: dependencias o salida trazable |
| ENV_BARRAS | 1920 | 1920 | 439909 | 439925 | 12134/12134 | 0.181 | BARRAS_CONEXION, CALC_ENV_BARRAS, COMBOS_ULTIMOS, CONTROL_MULTICOMBO, MOTOR_ESPECTRAL_U | Conservado: dependencias o salida trazable |
| CALC_ENV_BARRAS | 29280 | 29280 | 7957542 | 7957542 | 223680/223680 | 3.986 | BARRAS_CONEXION, COMBOS_ULTIMOS, CONEXION_COMBOS, ENV_BARRAS, FUERZAS_BARRAS, MU_BARRAS | Conservado: dependencias o salida trazable |
| ANALISIS_COMPLEMENTARIO | 25 | 25 | 7481 | 7493 | 64/64 | 0.007 | COMBOS_ULTIMOS, ENVOLVENTES, MC_ACERO | Conservado: dependencias o salida trazable |
| GUIA_MULTICOMBO | 0 | 0 | 7887 | 7903 | 0/0 | 0.002 | — | Conservado: dependencias o salida trazable |
| MC_ACERO | 281 | 281 | 64277 | 64277 | 2125/2125 | 0.041 | ACERO_DETALLADO, BARRAS_PERU, CONEXION_COLUMNA_ZAPATA, FLEXION_ACERO, GEOMETRIA, INGRESO_DATOS, MC_ACERO, MC_DATOS, MC_FLEX, MC_PRESION, MC_PUNZ, MU_ACERO | Conservado: dependencias o salida trazable |
| MC_CARGAS | 11 | 11 | 3631 | 3631 | 44/44 | 0.003 | MU_CARGAS | Conservado: dependencias o salida trazable |
| MC_DATOS | 1 | 1 | 1308 | 1308 | 4/4 | 0.001 | MU_DATOS | Conservado: dependencias o salida trazable |
| MC_DIAG_X | 4 | 4 | 1965 | 1965 | 16/16 | 0.001 | MU_DIAG_X | Conservado: dependencias o salida trazable |
| MC_DIAG_Y | 4 | 4 | 1965 | 1965 | 16/16 | 0.001 | MU_DIAG_Y | Conservado: dependencias o salida trazable |
| MC_FLEX | 58 | 58 | 9638 | 9638 | 216/216 | 0.005 | INGRESO_DATOS, MC_DIAG_X, MC_DIAG_Y, MC_FLEX, MC_PRESION, MC_PUNZ, MU_FLEX, PUNZONAMIENTO | Conservado: dependencias o salida trazable |
| MC_PRESION | 11 | 11 | 4058 | 4058 | 44/44 | 0.003 | MU_PRESION | Conservado: dependencias o salida trazable |
| MC_PUNZ | 7 | 7 | 3004 | 3004 | 38/38 | 0.001 | INGRESO_DATOS, MC_PUNZ, MU_PUNZ | Conservado: dependencias o salida trazable |
| MC_RESULTANTE | 6 | 6 | 2288 | 2288 | 24/24 | 0.002 | MU_RESULTANTE | Conservado: dependencias o salida trazable |
| MS_CARGAS | 1080 | 1080 | 177880 | 177880 | 3300/3300 | 0.089 | COMBOS_SERVICIO, MS_CARGAS, MS_DATOS, MS_SERVICIO | Conservado: dependencias o salida trazable |
| MS_DATOS | 240 | 240 | 47948 | 47948 | 480/480 | 0.022 | COMBOS_SERVICIO | Conservado: dependencias o salida trazable |
| MS_ESTADOS | 420 | 420 | 85325 | 85325 | 660/660 | 0.040 | MS_SERVICIO | Conservado: dependencias o salida trazable |
| MS_RESULTANTE | 360 | 360 | 51854 | 51854 | 1260/1260 | 0.029 | COMBOS_SERVICIO, GEOMETRIA, INGRESO_DATOS, MS_CARGAS, MS_RESULTANTE, MS_SERVICIO | Conservado: dependencias o salida trazable |
| MS_SERVICIO | 3000 | 3000 | 873259 | 873259 | 18420/18420 | 0.421 | COMBOS_SERVICIO, GEOMETRIA, INGRESO_DATOS, MS_CARGAS, MS_DATOS, MS_RESULTANTE, MS_SERVICIO, PRESIONES_SERVICIO | Conservado: dependencias o salida trazable |
| MU_ACERO | 8760 | 8760 | 2924620 | 2924620 | 87000/87000 | 1.446 | ACERO_DETALLADO, BARRAS_PERU, FLEXION_ACERO, GEOMETRIA, INGRESO_DATOS, MU_ACERO, MU_FLEX, MU_PRESION | Conservado: dependencias o salida trazable |
| MU_BARRAS | 36000 | 36000 | 21691955 | 21691955 | 604800/604800 | 12.070 | BARRAS_CONEXION, BARRAS_PERU, COMBOS_ULTIMOS, CONEXION_COLUMNA_ZAPATA, FUERZAS_BARRAS, INGRESO_DATOS, MU_BARRAS | Conservado: dependencias o salida trazable |
| MU_CARGAS | 720 | 720 | 107946 | 107946 | 2100/2100 | 0.067 | COMBOS_ULTIMOS, MU_CARGAS | Conservado: dependencias o salida trazable |
| MU_CONEXION | 2820 | 2820 | 823302 | 823302 | 14640/14640 | 0.381 | BARRAS_CONEXION, COMBOS_ULTIMOS, CONEXION_COLUMNA_ZAPATA, CONEXION_COMBOS, CONTROL_FASE7, INGRESO_DATOS, MU_BARRAS, MU_CARGAS, MU_CONEXION, MU_DATOS, MU_PRESION | Conservado: dependencias o salida trazable |
| MU_CORT | 2280 | 2280 | 302741 | 302741 | 9000/9000 | 0.207 | INGRESO_DATOS, MU_CORT, MU_DIAG_X, MU_DIAG_Y, MU_FLEX, MU_PRESION, PUNZONAMIENTO | Conservado: dependencias o salida trazable |
| MU_DATOS | 60 | 60 | 16586 | 16586 | 120/120 | 0.006 | COMBOS_ULTIMOS | Conservado: dependencias o salida trazable |
| MU_DIAG_X | 9720 | 9720 | 3464259 | 3464259 | 146940/146940 | 1.833 | DIAGRAMAS_X, INGRESO_DATOS, MU_CARGAS, MU_DIAG_X, MU_PRESION | Conservado: dependencias o salida trazable |
| MU_DIAG_Y | 9720 | 9720 | 3464407 | 3464407 | 146940/146940 | 2.216 | DIAGRAMAS_Y, INGRESO_DATOS, MU_CARGAS, MU_DIAG_Y, MU_PRESION | Conservado: dependencias o salida trazable |
| MU_ESTADOS | 900 | 900 | 151734 | 151734 | 1200/1200 | 0.084 | MU_ACERO, MU_CORT, MU_DIAG_X, MU_DIAG_Y, MU_PRESION, MU_PUNZ | Conservado: dependencias o salida trazable |
| MU_FLEX | 1320 | 1320 | 336662 | 336662 | 11040/11040 | 0.239 | BARRAS_PERU, FLEXION_ACERO, INGRESO_DATOS, MU_ACERO, MU_DIAG_X, MU_DIAG_Y, MU_FLEX, MU_PRESION, PUNZONAMIENTO | Conservado: dependencias o salida trazable |
| MU_PRESION | 780 | 780 | 283252 | 283252 | 7320/7320 | 0.177 | COMBOS_ULTIMOS, CONTROL_FASE7, GEOMETRIA, INGRESO_DATOS, MU_CARGAS, MU_PRESION, MU_RESULTANTE, PRESIONES_ULTIMAS, PUNZONAMIENTO | Conservado: dependencias o salida trazable |
| MU_PUNZ | 1560 | 1560 | 383757 | 383757 | 8760/8760 | 0.219 | COMBOS_ULTIMOS, INGRESO_DATOS, MU_CARGAS, MU_PRESION, MU_PUNZ, PUNZONAMIENTO | Conservado: dependencias o salida trazable |
| MU_RESULTANTE | 360 | 360 | 54269 | 54269 | 1380/1380 | 0.031 | COMBOS_ULTIMOS, GEOMETRIA, INGRESO_DATOS, MU_CARGAS, MU_PRESION, MU_RESULTANTE | Conservado: dependencias o salida trazable |
| ESPECTROS_U | 300 | 300 | 197005 | 190159 | 4860/4800 | 0.116 | CASOS_CONSTITUYENTES, COMBOS_ULTIMOS, CONTROL_FASE7, DEMANDAS_E030 | Conservado: dependencias o salida trazable |
| DERIVADOS_U | 307200 | 307200 | 29465023 | 29465023 | 745320/745320 | 17.593 | CONTROL_FASE7, ESPECTROS_U, MOTOR_ESPECTRAL_U, MOTOR_H_U | 128 estados/padre y resultados auditables conservados |
| DU_INPUT | 99840 | 7802 | 10263149 | 3091249 | 247710/25980 | 1.265 | COMBOS_ULTIMOS, CONTROL_FASE7, CONTROL_MULTICOMBO, DU_INPUT, ESPECTROS_U | Expresiones completas compartidas mediante referencias |
| CONEXION_ESPECTRAL | 3840 | 3840 | 1814062 | 1821190 | 24030/24030 | 0.752 | DU_INPUT | Conservado: dependencias o salida trazable |
| BARRAS_ESPECTRALES | 1920 | 1920 | 1381339 | 1383121 | 1920/1920 | 0.590 | DU_INPUT | Conservado: dependencias o salida trazable |
| ESPECTROS_S | 300 | 300 | 223720 | 216934 | 5700/5640 | 0.123 | CASOS_CONSTITUYENTES, COMBOS_SERVICIO, CONTROL_FASE7, DEMANDAS_E030 | Conservado: dependencias o salida trazable |
| DERIVADOS_S | 245760 | 245760 | 27768379 | 27782635 | 729960/729960 | 15.233 | COMBOS_SERVICIO, CONTROL_FASE7, ESPECTROS_S, MOTOR_ESPECTRAL_S, MOTOR_H_S | 128 estados/padre y resultados auditables conservados |
| DS_INPUT | 118080 | 8523 | 11848866 | 3555640 | 276510/28500 | 1.700 | COMBOS_SERVICIO, CONTROL_FASE7, CONTROL_MULTICOMBO, DS_INPUT, ESPECTROS_S | Expresiones completas compartidas mediante referencias |
| MOTOR_ESPECTRAL_U | 1374720 | 1332720 | 533060457 | 546287395 | 19032960/18745200 | 291.836 | ACERO_DETALLADO, BARRAS_CONEXION, BARRAS_ESPECTRALES, BARRAS_PERU, CONEXION_COLUMNA_ZAPATA, CONEXION_ESPECTRAL, CONTROL_FASE7, CONTROL_MULTICOMBO, DIAGRAMAS_X, DIAGRAMAS_Y, DU_INPUT, FLEXION_ACERO, GEOMETRIA, INGRESO_DATOS, MOTOR_ESPECTRAL_U, PRESIONES_ULTIMAS, PUNZONAMIENTO, RESUMEN | Reutilización exacta; cuerpo y rangos preservados |
| MOTOR_ESPECTRAL_S | 142080 | 120720 | 22259275 | 23333463 | 789120/725100 | 13.584 | CONTROL_MULTICOMBO, DS_INPUT, GEOMETRIA, INGRESO_DATOS, MOTOR_ESPECTRAL_S, PRESIONES_SERVICIO, RESUMEN | Reutilización exacta; cuerpo y rangos preservados |
| TOTAL_F7_U | 268260 | 268260 | 17594461 | 17703439 | 320820/320820 | 11.774 | DU_INPUT, ESPECTROS_U, MOTOR_ESPECTRAL_U, RESULTADOS_ULTIMOS | 60+960 candidatos y gobernantes conservados |
| TOTAL_F7_S | 72420 | 72420 | 4819096 | 4858702 | 90120/90120 | 3.190 | DS_INPUT, ESPECTROS_S, MOTOR_ESPECTRAL_S, RESULTADOS_SERVICIO | 60+960 candidatos y gobernantes conservados |
| CASOS_CONSTITUYENTES | 2880 | 2880 | 547770 | 547770 | 1739/1739 | 0.250 | COMBOS_SERVICIO, COMBOS_ULTIMOS | Conservado: dependencias o salida trazable |
| VISTA_DERIVADO | 16 | 16 | 8986 | 8946 | 224/224 | 0.007 | DERIVADOS_S, DERIVADOS_U | Conservado: dependencias o salida trazable |
| MOTOR_H_U | 407040 | 291840 | 95500398 | 76155428 | 2449920/1850880 | 40.892 | BARRAS_CONEXION, CONEXION_COLUMNA_ZAPATA, CONEXION_ESPECTRAL, DERIVADOS_U, DU_INPUT, INGRESO_DATOS, MOTOR_ESPECTRAL_U, MOTOR_H_U | Auxiliares sin consumidor retirados; estados H/Mz preservados |
| MOTOR_H_S | 253440 | 176640 | 66749448 | 52337752 | 1628160/1167360 | 31.086 | DERIVADOS_S, DS_INPUT, INGRESO_DATOS, MOTOR_ESPECTRAL_S, MOTOR_H_S, PRESIONES_SERVICIO | Auxiliares sin consumidor retirados; estados H/Mz preservados |
| CONTROL_E030_F8 | 0 | 4 | 0 | 13676 | 0/27 | 0.026 | CONTROL_FASE7, INGRESO_DATOS | Nuevo control de entradas/fuente normativa |
| FUENTES_E030 | 0 | 600 | 0 | 120876 | 0/3646 | 0.069 | CONTROL_E030_F8 | Nuevo control de entradas/fuente normativa |
| DEMANDAS_E030 | 0 | 1560 | 0 | 469945 | 0/11792 | 0.295 | COMBOS_SERVICIO, COMBOS_ULTIMOS, CONTROL_E030_F8, CONTROL_FASE7, ESPECTROS_S, ESPECTROS_U, FUENTES_E030 | Nuevo control de entradas/fuente normativa |

## Regresión y pruebas de aceptación

La regresión pura de reutilización exacta se comparó con F7 en 48 escenarios y 983712 comparaciones, sin diferencias. La regresión final, incluida la depuración, mantiene los mismos 48 escenarios y **983712 comparaciones**, tolerancia numérica absoluta/relativa **2E−8**, con **cero diferencias no justificadas**. Se compararon acciones, pesos, contacto, presiones, punzonamiento, cortantes, ocho As, conexión, estados técnicos/validez/cobertura, gobernantes, segundo/tercer punzonamiento, barras, VISTA_COMBO y VISTA_DERIVADO. Los 128 estados y las 16 evaluaciones del primer padre U/S se capturaron íntegros en cada escenario; todos los escenarios F7 modifican ese primer padre. Se capturaron las 60 filas de envolventes de barras.

Única diferencia de regresión admitida: **3840 celdas de metadatos** de DERIVADOS cambian de SZ ausente/coefficient 0 a SZ sintético RSZ/coefficient 1 con sus seis contribuciones exactamente cero. Esta adaptación de fixture permite comparar el algoritmo horizontal F7 bajo la obligación vertical nueva. No es una demanda real ni una relajación de la norma. Las acciones y resultados numéricos deben seguir iguales. Las declaraciones documentales de pruebas se completaron en F8 porque sus nuevos bloqueos son intencionales. No se admitieron diferencias numéricas de ingeniería, IDs, estados o vistas mediante esa excepción.

| Escenario F7 | Estado técnico F8 | Validez F8 | Errores/circularidad |
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

Las **40 pruebas E.030** adicionales superaron **2570 comprobaciones** de estados y resultados, sin fallos. Se verificaron además: art.44 sin doble escalamiento de acciones; igualdad de los seis componentes en 128 estados de servicio para reducción importada frente a reducción adicional; qadm×1.30 con acciones idénticas; conservación de D/C mayor que 1 en la caja; resultado externo P=100 tf frente a P>400 tf de la caja.

| Prueba E.030 | Resultado esperado y observado |
|---|---|
| F8 01 Regular y ejes paralelos | DEMANDAS_E030!Y8: OK; ESPECTROS_U!AI8: OK — verificado |
| F8 02 Irregular y ejes paralelos | DEMANDAS_E030!Y8: OK; ESPECTROS_U!AI8: OK — verificado |
| F8 03 Sistemas no paralelos | DEMANDAS_E030!Y8: REQUIERE EJES NO PARALELOS — PROCEDIMIENTO EXTERNO — verificado |
| F8 04 Estático admisible art.33.2 | DEMANDAS_E030!T8: OK; COMBOS_ULTIMOS!K8: OK — verificado |
| F8 05 Estático no admisible | DEMANDAS_E030!T8: REQUIERE MÉTODO ESTÁTICO ADMISIBLE ART.33.2 — verificado |
| F8 06 EX simple sin 30% | COMBOS_ULTIMOS!K8: REQUIERE COMBINACIÓN DIRECCIONAL ESTÁTICA — verificado |
| F8 07 100/30 estático documentado | DEMANDAS_E030!T8: OK; COMBOS_ULTIMOS!K8: OK — verificado |
| F8 08 Excentricidad X100 documentada | DEMANDAS_E030!U8: OK — verificado |
| F8 09 Excentricidad X100 faltante | DEMANDAS_E030!U8: REQUIERE PROCEDIMIENTO EXTERNO DOCUMENTADO — EXCENTRICIDAD X100/Y100 — verificado |
| F8 10 Excentricidad Y100 documentada | DEMANDAS_E030!U8: OK — verificado |
| F8 11 Masa X 89% | FUENTES_E030!Z8: NO CUMPLE FUENTE E.030; ESPECTROS_U!AI8: NO CUMPLE FUENTE E.030 — verificado |
| F8 12 Masa X 90% | FUENTES_E030!Z8: OK; DEMANDAS_E030!Y8: OK — verificado |
| F8 13 Masa Y 89% | FUENTES_E030!Z8: NO CUMPLE FUENTE E.030 — verificado |
| F8 14 Dos modos predominantes | FUENTES_E030!Z8: NO CUMPLE FUENTE E.030 — verificado |
| F8 15 Tres modos predominantes | FUENTES_E030!Z8: OK — verificado |
| F8 16 CQC documentado | FUENTES_E030!AA8: OK — verificado |
| F8 17 Alternativo art.42.3 documentado | FUENTES_E030!AA8: OK — verificado |
| F8 18 Vdin regular 0.79Vest | FUENTES_E030!AB8: REQUIERE ESCALAMIENTO E.030 — verificado |
| F8 19 Escala regular a 0.80Vest | FUENTES_E030!AB8: OK; FUENTES_E030!Q8: 80; FUENTES_E030!R8: 1.0126582278481013 — verificado |
| F8 20 Vdin irregular 0.89Vest | FUENTES_E030!AB8: REQUIERE ESCALAMIENTO E.030 — verificado |
| F8 21 Escala irregular a 0.90Vest | FUENTES_E030!AB8: OK; FUENTES_E030!Q8: 90 — verificado |
| F8 22 Servicio no reducido factor 1 | DEMANDAS_E030!X68: DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO — verificado |
| F8 23 Servicio no reducido factor 0.80 | DEMANDAS_E030!X68: OK; ESPECTROS_S!AI8: OK — verificado |
| F8 24 Servicio ya reducido factor 1 | DEMANDAS_E030!X68: OK; ESPECTROS_S!AI8: OK — verificado |
| F8 25 Doble reducción | DEMANDAS_E030!X68: DATOS INVÁLIDOS — DOBLE REDUCCIÓN O REFERENCIA 0.80 FALTANTE — verificado |
| F8 26 qadm +30% desactivado | DEMANDAS_E030!X68: OK — verificado |
| F8 27 qadm +30% documentado | DEMANDAS_E030!X68: OK — verificado |
| F8 28 Caja gobierna | ENVOLVENTES!B5: NO CUMPLE ENVOLVENTE CONSERVADORA — VERIFICAR INTERACCIÓN EXTERNA — verificado |
| F8 29 Externo menos conservador documentado | DEMANDAS_E030!AA8: RESULTADO EXTERNO DOCUMENTADO; COMBOS_ULTIMOS!K8: OK; ESPECTROS_U!A8: NO — verificado |
| F8 30 Norma E030 indefinida | DEMANDAS_E030!Y8: REQUIERE DEFINIR NORMA E.030 APLICABLE — verificado |
| F8 31 Excentricidad -e Y faltante | DEMANDAS_E030!Y8: REQUIERE PROCEDIMIENTO EXTERNO DOCUMENTADO — EXCENTRICIDAD X100/Y100 — verificado |
| F8 32 CQC sin referencia | FUENTES_E030!AA8: REQUIERE COMBINACIÓN MODAL DOCUMENTADA — verificado |
| F8 33 Fuente repetida | DEMANDAS_E030!V8: REQUIERE FUENTE MODAL ÚNICA — verificado |
| F8 34 Elemento vertical NO prohibido | DEMANDAS_E030!W8: REQUIERE COMPONENTE VERTICAL OBLIGATORIA — verificado |
| F8 35 Vertical disponible sin espectro | DEMANDAS_E030!W8: REQUIERE COMPONENTE VERTICAL DOCUMENTADA — verificado |
| F8 36 Vertical requerido sin confirmar | DEMANDAS_E030!W8: REQUIERE COMPONENTE VERTICAL OBLIGATORIA — verificado |
| F8 37 No paralelo externo | DEMANDAS_E030!Y8: OK; COMBOS_ULTIMOS!K8: OK — verificado |
| F8 38 Fuente no escalada declarada | FUENTES_E030!AB8: REQUIERE ESCALAMIENTO E.030 — verificado |
| F8 39 Modos fraccionarios inválidos | FUENTES_E030!Z8: DATOS INVÁLIDOS MASA MODAL — verificado |
| F8 40 0.80 no sustituido por qadm+30% | DEMANDAS_E030!X68: DATOS INVÁLIDOS — FALTA REDUCCIÓN 0.80 PARA PRESIONES DE SUELO — verificado |

## Cierre nativo, integridad y estado del proyecto

Excel **16.0**, build **14332.0**, idioma UI **3082**. El registro de instalación identifica Office 2021, x64, es-es, 16.0.14332.20615. Se verificó sintaxis y funciones compatibles con Excel español 2016; **no se ejecutó sobre una instalación de Office 2016**, que no está disponible. La fórmula local registrada incluye `SI` y separador `;`. Se ejecutó CalculateFullRebuild, guardado, cierre, normalización exclusiva de nombres reservados de impresión, reapertura normal sin reparación y otro CalculateFullRebuild. Las capturas de cierre superaron **3188 comparaciones de persistencia**, con tolerancia 2E−8. Las vistas exportadas por Excel se revisaron visualmente. Se conservaron **24 gráficos** y 78 hojas.

Cero errores de fórmula en Excel y cero errores cacheados OOXML; cero circularidad, vínculos externos, VBA, `_xlfn`, `_xludf`, `#REF!` y grupos compartidos huérfanos. Se comprobaron **3688 celdas originales constantes** en las hojas de geometría/datos, acciones, combos, espectros, barras y acero sin cambios. Los hashes de todos los XLSX y documentos F1–F7 coinciden con los iniciales.

Funciones encontradas en las expresiones finales: `ABS`, `AND`, `CHOOSE`, `COS`, `COUNT`, `COUNTA`, `COUNTBLANK`, `COUNTIF`, `COUNTIFS`, `EXACT`, `IF`, `IFERROR`, `INDEX`, `INT`, `ISBLANK`, `ISNUMBER`, `ISTEXT`, `LEN`, `MATCH`, `MAX`, `MIN`, `MOD`, `NOT`, `OR`, `PI`, `RADIANS`, `ROUND`, `ROW`, `SIN`, `SQRT`, `SUM`, `SUMIF`, `SUMPRODUCT`, `TEXT`. Son funciones disponibles en Excel 2016; no se encontraron funciones de matrices dinámicas ni las funciones modernas excluidas en la revisión.

El proyecto actual conserva **NO CUMPLE**, validez **REQUIERE DATOS** y cobertura pendiente de confirmación. No se acredita una fuente sísmica sin documentos ni se optimizó la zapata. Para activar demandas sísmicas, completar la versión/régimen, regularidad, paralelismo, fuente modal cuando corresponda y las referencias por combinación; después revisar separadamente resistencia, conexión y cobertura.

SHA-256 del XLSX entregado: `daabf7c5840b5f2d04d7cc351e344b4000e82223e722a66c855d8846e3db87c5`.

## FORMULAS_CRITICAS_AUDITABLES

Texto literal del XLSX final en sintaxis OOXML: funciones inglesas y coma. Excel español 2016 muestra funciones traducidas y punto y coma. No pegar este texto como fórmula local. Las fórmulas compartidas de muestra se expanden desde su definición y desplazamiento nativos. No se transcriben fórmulas desde versiones descartadas. Las filas 8/68 son el primer padre U/S; el mismo patrón se conserva para los otros 59 padres.

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
=IF(B155,"NO CUMPLE ENVOLVENTE CONSERVADORA — VERIFICAR INTERACCIÓN EXTERNA",B153)
```

**ENVOLVENTES!B6**

```excel
=IF(COUNTIFS(DEMANDAS_E030!A8:A127,"SI",DEMANDAS_E030!Y8:Y127,"<>OK",DEMANDAS_E030!Y8:Y127,"<>NO APLICA")>0,INDEX(DEMANDAS_E030!Y8:Y127,MATCH(1,INDEX((DEMANDAS_E030!A8:A127="SI")*(DEMANDAS_E030!Y8:Y127<>"OK")*(DEMANDAS_E030!Y8:Y127<>"NO APLICA"),0),0)),IF(SUM(COUNTIF(COMBOS_ULTIMOS!CT8:CT67,"REQUIERE DEFINIR NORMA E.030 APLICABLE"),COUNTIF(COMBOS_SERVICIO!DM8:DM67,"REQUIERE DEFINIR NORMA E.030 APLICABLE"))>0,"REQUIERE DEFINIR NORMA E.030 APLICABLE",IF(COUNTIF(TOTAL_F7_U!ET8:ET1027,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA")+COUNTIF(TOTAL_F7_S!AJ8:AJ1027,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA")>0,"REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",IF(COUNTIFS(ESPECTROS_U!A8:A67,"SI",ESPECTROS_U!AI8:AI67,"<>OK")+COUNTIFS(ESPECTROS_S!A8:A67,"SI",ESPECTROS_S!AI8:AI67,"<>OK")>0,"REQUIERE DATOS — ESTADOS ESPECTRALES",IF(CONTROL_FASE7!B41<>"OK",CONTROL_FASE7!B41,IF(COUNTIFS(COMBOS_ULTIMOS!A8:A67,"SI",COMBOS_ULTIMOS!K8:K67,"<>OK",COMBOS_ULTIMOS!K8:K67,"<>ESPECTRAL — USAR ESTADOS DERIVADOS")+COUNTIFS(COMBOS_SERVICIO!A8:A67,"SI",COMBOS_SERVICIO!O8:O67,"<>OK",COMBOS_SERVICIO!O8:O67,"<>ESPECTRAL — USAR ESTADOS DERIVADOS")>0,"REQUIERE DATOS / REVISAR ENTRADAS FASE 7",IF(COUNTIF(TOTAL_F7_U!GM8:GM1027,"DATOS INVÁLIDOS")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"DATOS INVÁLIDOS")+COUNTIF(ENV_BARRAS!Y8:AA67,"DATOS INVÁLIDOS")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"DATOS INVÁLIDOS")+COUNTIF(COMBOS_ULTIMOS!K8:K67,"DATOS NO CONCURRENTES — NO USAR COMO COMBO")+COUNTIF(COMBOS_SERVICIO!O8:O67,"DATOS NO CONCURRENTES — NO USAR COMO COMBO")>0,"DATOS INVÁLIDOS",IF(COUNTIF(TOTAL_F7_U!GM8:GM1027,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(ENV_BARRAS!Y8:AA67,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE",IF(COUNTIF(TOTAL_F7_U!GM8:GM1027,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(ENV_BARRAS!Y8:AA67,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")>0,"REQUIERE CONTACTO PARCIAL",IF(COUNTIF(TOTAL_F7_U!GM8:GM1027,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(ENV_BARRAS!Y8:AA67,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(TOTAL_F7_U!GM8:GM1027,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(ENV_BARRAS!Y8:AA67,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(OR(CONTROL_MULTICOMBO!$B$33<>"COMPLETO",CONTROL_MULTICOMBO!$B$35<>"OK",COUNTIF(COMBOS_ULTIMOS!V8:V67,"REQUIERE DATOS")>0,COUNTIF(COMBOS_ULTIMOS!A8:A67,"SI")=0,COUNTIF(COMBOS_SERVICIO!A8:A67,"SI")=0,COUNTIF(TOTAL_F7_U!GM8:GM1027,"REQUIERE DATOS")+COUNTIF(TOTAL_F7_S!BC8:BC1027,"REQUIERE DATOS")+COUNTIF(ENV_BARRAS!Y8:AA67,"REQUIERE DATOS")+COUNTIF(ANALISIS_COMPLEMENTARIO!B9,"REQUIERE DATOS")>0),"REQUIERE DATOS","COMPLETO")))))))))))
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
=IF(COUNTIF(TOTAL_F7_U!AP8:AR1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!AT8:BQ1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!EQ8:ES1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!FQ8:GK1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!IV8:JC1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!EU8:FP1027,"NO CUMPLE")+COUNTIF(TOTAL_F7_S!AF8:BA1027,"NO CUMPLE")+COUNTIF(ENV_BARRAS!Y8:AA67,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!CA8:EO1027,"NO FACTIBLE")+COUNTIF(CALC_ENV_BARRAS!C8:BJ522,"NO CUMPLE")>0,"NO CUMPLE",IF(B6="COMPLETO","CUMPLE","SIN RESULTADO COMPLETO"))
```

**ENVOLVENTES!B154**

```excel
=IF(COUNTIF(TOTAL_F7_U!AP8:AR67,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!AT8:BQ67,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!EQ8:ES67,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!FQ8:GK67,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!IV8:JC67,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!EU8:FP67,"NO CUMPLE")+COUNTIF(TOTAL_F7_S!AF8:BA67,"NO CUMPLE")+COUNTIF(TOTAL_F7_U!CA8:EO67,"NO FACTIBLE")+COUNTIF(CALC_ENV_BARRAS!C8:BJ522,"NO CUMPLE")>0,"NO CUMPLE",IF(B6="COMPLETO","CUMPLE","SIN RESULTADO COMPLETO"))
```

**ENVOLVENTES!B155**

```excel
=AND(B153="NO CUMPLE",B154<>"NO CUMPLE",COUNTIFS(DERIVADOS_U!A8:A7687,"SI",DERIVADOS_U!Z8:Z7687,"OK")+COUNTIFS(DERIVADOS_S!A8:A7687,"SI",DERIVADOS_S!Z8:Z7687,"OK")>0)
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
=IF(AND(A8="SI",DEMANDAS_E030!Y8<>"OK"),DEMANDAS_E030!Y8,IF(OR(AND(A8="SI",C8=D8),AND(A8="SI",COMBOS_ULTIMOS!BI8<>"OK"),COUNTIFS(CASOS_CONSTITUYENTES!$A$8:$A$1447,"SI",CASOS_CONSTITUYENTES!$B$8:$B$1447,"U",CASOS_CONSTITUYENTES!$C$8:$C$1447,1,CASOS_CONSTITUYENTES!$I$8:$I$1447,"<>OK")>0),"REQUIERE DATOS — FUENTE ESPECTRAL",IF(A8<>"SI","NO APLICA",IF(COMBOS_ULTIMOS!CS8<>"OK",COMBOS_ULTIMOS!CS8,IF(CONTROL_FASE7!$B$10<>"OK",CONTROL_FASE7!$B$10,IF(OR(LEN(C8)=0,LEN(D8)=0,LEN(G8)=0,LEN(H8)=0,LEN(J8)=0,I8<>"SI",LEN(COMBOS_ULTIMOS!BQ8)=0,LEN(COMBOS_ULTIMOS!CK8)=0,LEN(COMBOS_ULTIMOS!CL8)=0),"REQUIERE DATOS",IF(OR(COMBOS_ULTIMOS!BV8<>"INTERFAZ COLUMNA-ZAPATA",NOT(ISNUMBER(COMBOS_ULTIMOS!CR8)),ABS(COMBOS_ULTIMOS!CR8)>0.00000001),"REQUIERE RECOMBINACIÓN MODAL EN INTERFAZ",IF(COUNT(K8:AB8)<>18,"REQUIERE DATOS",IF(MIN(Q8:AB8)<0,"DATOS INVÁLIDOS",IF(OR(NOT(OR(F8="SI",F8="NO")),CONTROL_FASE7!$B$14="REQUIERE DEFINIR",LEN(CONTROL_FASE7!$B$15)=0),"REQUIERE DEFINIR COMPONENTE VERTICAL",IF(AND(CONTROL_FASE7!$B$14="SI",F8<>"SI"),"REQUIERE COMPONENTE VERTICAL",IF(AND(F8="SI",OR(LEN(E8)=0,COUNT(AC8:AH8)<>6,MIN(AC8:AH8)<0)),"REQUIERE DATOS",IF(AND(CONTROL_FASE7!$B$7="E.030 ANTERIOR A RM 183-2026",OR(CONTROL_FASE7!$B$12<>"REGULAR",LEN(CONTROL_FASE7!$B$13)=0)),"REQUIERE DIRECCIÓN MÁS DESFAVORABLE DOCUMENTADA","OK")))))))))))))
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

**DERIVADOS_S!R8**

```excel
=IF(Z8="OK",ESPECTROS_S!K8+L8*((SQRT((I8*ESPECTROS_S!Q8)^2+(J8*ESPECTROS_S!W8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AC8),ESPECTROS_S!AC8,0))*COMBOS_SERVICIO!L8),"")
```

**DERIVADOS_S!W8**

```excel
=IF(Z8="OK",ESPECTROS_S!P8+Q8*((SQRT((I8*ESPECTROS_S!V8)^2+(J8*ESPECTROS_S!AB8)^2)+K8*IF(ISNUMBER(ESPECTROS_S!AH8),ESPECTROS_S!AH8,0))*COMBOS_SERVICIO!L8),"")
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

**MOTOR_H_S!DH8**

```excel
=IF(DS_INPUT!A8="SI",IF(DS_INPUT!A8="NO","",IF(LEN(MOTOR_H_S!AY8)=0,"",MOTOR_H_S!AY8)),"")
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
=IF(OR(CONTROL_E030_F8!$B$12<>"OK",COUNT(N8,O8,P8,S8,T8,U8)<>6,N8<=0,S8<=0,O8<=0,T8<=0,X8<>"SI",LEN(Y8)=0),"REQUIERE ESCALAMIENTO E.030",IF(OR(P8<R8-0.0000000001,U8<W8-0.0000000001,Q8<IF(CONTROL_E030_F8!$B$7="REGULAR",0.8,0.9)*N8-0.0000000001,V8<IF(CONTROL_E030_F8!$B$7="REGULAR",0.8,0.9)*S8-0.0000000001),"REQUIERE ESCALAMIENTO E.030","OK"))
```

**FUENTES_E030!AC8**

```excel
=IF(A8="","NO APLICA",IF(COUNTIF($A$8:$A$67,A8)<>1,"DATOS INVÁLIDOS — FUENTE DUPLICADA",IF(Z8<>"OK",Z8,IF(AA8<>"OK",AA8,AB8))))
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
=IF(CONTROL_E030_F8!B17<>"OK",CONTROL_E030_F8!B17,IF(CONTROL_E030_F8!B15="SI",IF(AND(O8="SI",LEN(P8)>0,IF(AND(COMBOS_ULTIMOS!BR8="SI",NOT(COMBOS_ULTIMOS!BS8="D. RESULTADO EXTERNO YA COMBINADO")),ESPECTROS_U!F8="SI",TRUE)),"OK","REQUIERE COMPONENTE VERTICAL DOCUMENTADA"),"OK"))
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

**MOTOR_H_U!ZU8**

```excel
=IF(DERIVADOS_U!Z8="OK",DERIVADOS_U!W8,"")
```

**MOTOR_H_U!AAE8**

```excel
=IF(DU_INPUT!A8="SI",IF(DERIVADOS_U!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_U!AD8,IF(CONEXION_ESPECTRAL!M8<>"OK",CONEXION_ESPECTRAL!M8,IF(CONEXION_COLUMNA_ZAPATA!$B$30<>"OK",CONEXION_COLUMNA_ZAPATA!$B$30,IF(MOTOR_ESPECTRAL_U!$AQN$8<>"OK",MOTOR_ESPECTRAL_U!$AQN$8,IF(CONEXION_COLUMNA_ZAPATA!$B$7<>"EXTERNO","FUERA DEL ALCANCE IMPLEMENTADO",IF(ABS(MOTOR_H_U!ZU8)>0.000001,"REQUIERE ANÁLISIS ESPECIAL",IF(OR(NOT(ISTEXT(MOTOR_ESPECTRAL_U!$ZV$8)),LEN(MOTOR_ESPECTRAL_U!$ZV$8)=0,NOT(ISTEXT(MOTOR_ESPECTRAL_U!$ZW$8)),LEN(MOTOR_ESPECTRAL_U!$ZW$8)=0,NOT(ISTEXT(CONEXION_COLUMNA_ZAPATA!$B$18)),LEN(CONEXION_COLUMNA_ZAPATA!$B$18)=0,NOT(ISTEXT(CONEXION_COLUMNA_ZAPATA!$B$22)),LEN(CONEXION_COLUMNA_ZAPATA!$B$22)=0,LEN(CONEXION_COLUMNA_ZAPATA!$B$10)=0),"REQUIERE DATOS",IF(OR(MOTOR_ESPECTRAL_U!$ZW$8<>MOTOR_ESPECTRAL_U!$ACR$8,CONEXION_COLUMNA_ZAPATA!$B$10<>"ACCIONES AMPLIFICADAS"),"DATOS INVÁLIDOS",IF(COUNT(MOTOR_ESPECTRAL_U!$ZX$8,MOTOR_ESPECTRAL_U!$ZY$8,MOTOR_ESPECTRAL_U!$ZZ$8,MOTOR_ESPECTRAL_U!$AAA$8,MOTOR_ESPECTRAL_U!$AAB$8,MOTOR_ESPECTRAL_U!$AAC$8,MOTOR_ESPECTRAL_U!$AAD$8)<>7,"REQUIERE DATOS",IF(OR(MOTOR_ESPECTRAL_U!$ZX$8<0,MOTOR_ESPECTRAL_U!$ZZ$8<0,MOTOR_ESPECTRAL_U!$AAC$8<0,MOTOR_ESPECTRAL_U!$AAC$8>CONEXION_COLUMNA_ZAPATA!$B$29,MOTOR_ESPECTRAL_U!$AAD$8<0,ABS(MOTOR_ESPECTRAL_U!$AAA$8)>INGRESO_DATOS!$C$42*50,ABS(MOTOR_ESPECTRAL_U!$AAB$8)>INGRESO_DATOS!$C$43*50,MOTOR_ESPECTRAL_U!$ZY$8<=0,MOTOR_ESPECTRAL_U!$ZY$8>1),"DATOS INVÁLIDOS",IF(CONEXION_ESPECTRAL!M8<>"OK",CONEXION_ESPECTRAL!M8,IF(MOTOR_ESPECTRAL_U!$ZZ$8=0,IF(AND(MOTOR_ESPECTRAL_U!$AAC$8=0,MOTOR_ESPECTRAL_U!$AAD$8=0,MOTOR_ESPECTRAL_U!$AAA$8=0,MOTOR_ESPECTRAL_U!$AAB$8=0),"OK","DATOS INVÁLIDOS"),IF(MOTOR_ESPECTRAL_U!$AAC$8<=0,"DATOS INVÁLIDOS",IF(MOTOR_ESPECTRAL_U!$AAD$8+0.00000001>=MOTOR_ESPECTRAL_U!$ZZ$8*1000/MOTOR_ESPECTRAL_U!$AAC$8,"OK","DATOS INVÁLIDOS")))))))))))))),"")
```

**MOTOR_H_U!AAG8**

```excel
=IF(DU_INPUT!A8="SI",IF(AND(MOTOR_H_U!AAE8="OK",MOTOR_ESPECTRAL_U!$AAF$8="CUMPLE"),SUM(MOTOR_ESPECTRAL_U!$EP$8:$GW$8)+MOTOR_ESPECTRAL_U!$ZZ$8,""),"")
```

**MOTOR_H_U!AAH8**

```excel
=IF(DU_INPUT!A8="SI",IF(AND(MOTOR_H_U!AAE8="OK",MOTOR_ESPECTRAL_U!$AAF$8="CUMPLE"),-SUMPRODUCT(MOTOR_ESPECTRAL_U!$EP$8:$GW$8,BARRAS_CONEXION!$C$12:$C$71)/100-MOTOR_ESPECTRAL_U!$ZZ$8*MOTOR_ESPECTRAL_U!$AAB$8/100,""),"")
```

**MOTOR_H_U!AAI8**

```excel
=IF(DU_INPUT!A8="SI",IF(AND(MOTOR_H_U!AAE8="OK",MOTOR_ESPECTRAL_U!$AAF$8="CUMPLE"),SUMPRODUCT(MOTOR_ESPECTRAL_U!$EP$8:$GW$8,BARRAS_CONEXION!$B$12:$B$71)/100+MOTOR_ESPECTRAL_U!$ZZ$8*MOTOR_ESPECTRAL_U!$AAA$8/100,""),"")
```

**MOTOR_H_U!AAJ8**

```excel
=IF(DU_INPUT!A8="SI",IF(ISNUMBER(MOTOR_H_U!AAG8),MOTOR_H_U!AAG8-MOTOR_ESPECTRAL_U!$ZR$8,""),"")
```

**MOTOR_H_U!AAK8**

```excel
=IF(DU_INPUT!A8="SI",IF(ISNUMBER(MOTOR_H_U!AAH8),MOTOR_H_U!AAH8-MOTOR_ESPECTRAL_U!$ZS$8,""),"")
```

**MOTOR_H_U!AAL8**

```excel
=IF(DU_INPUT!A8="SI",IF(ISNUMBER(MOTOR_H_U!AAI8),MOTOR_H_U!AAI8-MOTOR_ESPECTRAL_U!$ZT$8,""),"")
```

**MOTOR_H_U!AAM8**

```excel
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAE8<>"OK",MOTOR_H_U!AAE8,IF(MOTOR_ESPECTRAL_U!$AAF$8<>"CUMPLE",MOTOR_ESPECTRAL_U!$AAF$8,IF(AND(ABS(MOTOR_H_U!AAJ8)<=MAX(0.00000001,ABS(MOTOR_ESPECTRAL_U!$ZR$8)*0.00000001),ABS(MOTOR_H_U!AAK8)<=MAX(0.00000001,ABS(MOTOR_ESPECTRAL_U!$ZS$8)*0.00000001),ABS(MOTOR_H_U!AAL8)<=MAX(0.00000001,ABS(MOTOR_ESPECTRAL_U!$ZT$8)*0.00000001)),"CUMPLE","DATOS INVÁLIDOS"))),"")
```

**MOTOR_H_U!AAN8**

```excel
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAE8<>"OK",MOTOR_H_U!AAE8,IF(MOTOR_ESPECTRAL_U!$ZX$8<=1,"CUMPLE","NO CUMPLE")),"")
```

**MOTOR_H_U!AAP8**

```excel
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAE8="OK",0.7*0.85*INGRESO_DATOS!$C$14*MOTOR_ESPECTRAL_U!$AAC$8/1000,""),"")
```

**MOTOR_H_U!AAQ8**

```excel
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAE8="OK",0.7*0.85*INGRESO_DATOS!$C$108*MOTOR_ESPECTRAL_U!$AAC$8/1000,""),"")
```

**MOTOR_H_U!AAR8**

```excel
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAE8="OK",IF(MOTOR_ESPECTRAL_U!$ZZ$8=0,0,MAX(MOTOR_ESPECTRAL_U!$ZZ$8/MIN(MOTOR_H_U!AAP8:AAQ8),MOTOR_ESPECTRAL_U!$AAD$8/(0.7*0.85*MIN(INGRESO_DATOS!$C$14,INGRESO_DATOS!$C$108)))),""),"")
```

**MOTOR_H_U!AAS8**

```excel
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAE8<>"OK",MOTOR_H_U!AAE8,IF(MOTOR_H_U!AAR8<=1,"CUMPLE","NO CUMPLE")),"")
```

**MOTOR_H_U!AAU8**

```excel
=IF(DU_INPUT!A8="SI",IF(MOTOR_ESPECTRAL_U!$AQN$8="OK",SQRT(DERIVADOS_U!S8^2+DERIVADOS_U!T8^2),""),"")
```

**MOTOR_H_U!AAV8**

```excel
=IF(DU_INPUT!A8="SI",IF(AND(CONEXION_COLUMNA_ZAPATA!$B$30="OK",ISNUMBER(CONEXION_COLUMNA_ZAPATA!$B$74),ISNUMBER(MOTOR_H_U!AAU8)),MOTOR_H_U!AAU8*1000/(0.85*CONEXION_COLUMNA_ZAPATA!$B$74*MIN(INGRESO_DATOS!$C$109,420/0.0980665)),""),"")
```

**MOTOR_H_U!AAW8**

```excel
=IF(DU_INPUT!A8="SI",IF(DERIVADOS_U!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_U!AD8,IF(MOTOR_ESPECTRAL_U!$AQN$8<>"OK",MOTOR_ESPECTRAL_U!$AQN$8,IF(MOTOR_H_U!AAU8<=0.000000001,"NO APLICA",IF(CONEXION_COLUMNA_ZAPATA!$B$30<>"OK",CONEXION_COLUMNA_ZAPATA!$B$30,IF(OR(NOT(ISNUMBER(CONEXION_COLUMNA_ZAPATA!$B$74)),COUNT(INGRESO_DATOS!$C$121)<>1,LEN(INGRESO_DATOS!$C$122)=0,LEN(INGRESO_DATOS!$C$123)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!$C$121<0,"DATOS INVÁLIDOS",IF(AND(INGRESO_DATOS!$C$121>=MOTOR_H_U!AAV8,MOTOR_H_U!AAU8<=CONEXION_COLUMNA_ZAPATA!$B$77,INGRESO_DATOS!$C$122="SI"),"CUMPLE","NO CUMPLE"))))))),"")
```

**MOTOR_H_U!AAX8**

```excel
=MOTOR_ESPECTRAL_U!$AAX$8
```

**MOTOR_H_U!AAY8**

```excel
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAE8="OK","CUMPLE",MOTOR_H_U!AAE8),"")
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
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAM8="OK","CUMPLE",MOTOR_H_U!AAM8),"")
```

**MOTOR_H_U!ABC8**

```excel
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAN8="OK","CUMPLE",MOTOR_H_U!AAN8),"")
```

**MOTOR_H_U!ABD8**

```excel
=MOTOR_ESPECTRAL_U!$ABD$8
```

**MOTOR_H_U!ABE8**

```excel
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAS8="OK","CUMPLE",MOTOR_H_U!AAS8),"")
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
=IF(DU_INPUT!A8="SI",IF(MOTOR_H_U!AAW8="OK","CUMPLE",MOTOR_H_U!AAW8),"")
```

**MOTOR_H_U!ABI8**

```excel
=IF(DU_INPUT!A8="SI",IF(DERIVADOS_U!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_U!AD8,IF(COUNTIF(MOTOR_H_U!AAX8:ABH8,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(MOTOR_H_U!AAX8:ABH8,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(MOTOR_H_U!AAX8:ABH8,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(MOTOR_H_U!AAX8:ABH8,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(MOTOR_H_U!AAX8:ABH8,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))),"")
```

**MOTOR_H_U!AXR8**

```excel
=IF(DU_INPUT!A8="SI",IF(DU_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_U!ABI8)=0,"",MOTOR_H_U!ABI8)),"")
```

**MOTOR_H_U!AYE8**

```excel
=IF(DU_INPUT!A8="SI",IF(DU_INPUT!A8="NO","",IF(LEN(MOTOR_H_U!AAR8)=0,"",MOTOR_H_U!AAR8)),"")
```

**MOTOR_H_U!AYI8**

```excel
=IF(DU_INPUT!A8="SI",IF(DU_INPUT!A8="NO","",IF(LEN(MOTOR_H_U!AAU8)=0,"",MOTOR_H_U!AAU8)),"")
```

**MOTOR_H_U!AYJ8**

```excel
=IF(DU_INPUT!A8="SI",IF(DU_INPUT!A8="NO","",IF(LEN(MOTOR_H_U!AAV8)=0,"",MOTOR_H_U!AAV8)),"")
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
=IF(DU_INPUT!A8="SI",IF(DU_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_U!AAW8)=0,"",MOTOR_H_U!AAW8)),"")
```

**MOTOR_H_U!AYN8**

```excel
=IF(DU_INPUT!A8="SI",IF(DU_INPUT!A8="NO","",IF(MOTOR_H_U!AYI8=0,IF(ISNUMBER(MOTOR_H_U!AYI8),0,""),IF(AND(COUNT(MOTOR_H_U!AYJ8:AYL8)=3,MOTOR_ESPECTRAL_U!$AYK$8>0,MOTOR_ESPECTRAL_U!$AYL$8>0),MAX(MOTOR_H_U!AYJ8/MOTOR_ESPECTRAL_U!$AYK$8,MOTOR_H_U!AYI8/MOTOR_ESPECTRAL_U!$AYL$8),""))),"")
```

**MOTOR_H_U!AZK8**

```excel
=IF(DU_INPUT!A8="SI",IF(DU_INPUT!A8="NO","NO APLICA",IF(MOTOR_ESPECTRAL_U!$ARY$8="NO","NO APLICA",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"DATOS INVÁLIDOS")+COUNTIF(MOTOR_H_U!AXR8,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(MOTOR_H_U!AXR8,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(MOTOR_H_U!AXR8,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")>0,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(MOTOR_H_U!AXR8,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(MOTOR_H_U!AXR8,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"REQUIERE DATOS")+COUNTIF(MOTOR_H_U!AXR8,"REQUIERE DATOS")>0,"REQUIERE DATOS",IF(COUNTIF(MOTOR_ESPECTRAL_U!$AZJ$8,"NO CUMPLE")+COUNTIF(MOTOR_H_U!AXR8,"NO CUMPLE")>0,"NO CUMPLE","CUMPLE")))))))),"")
```

**MOTOR_H_S!W8**

```excel
=IF(DS_INPUT!A8="SI",MOTOR_H_S!AW8,"")
```

**MOTOR_H_S!X8**

```excel
=IF(DS_INPUT!A8="SI",MOTOR_H_S!AZ8,"")
```

**MOTOR_H_S!Y8**

```excel
=IF(DS_INPUT!A8="SI",MOTOR_H_S!BE8,"")
```

**MOTOR_H_S!AV8**

```excel
=IF(DS_INPUT!A8="SI",IF(MOTOR_ESPECTRAL_S!$AF$8="OK",SQRT(DERIVADOS_S!S8^2+DERIVADOS_S!T8^2),""),"")
```

**MOTOR_H_S!AW8**

```excel
=IF(DS_INPUT!A8="SI",IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_H_S!AV8<=0.000000001,"NO APLICA",IF(AND(INGRESO_DATOS!$C$79="SI",LEN(INGRESO_DATOS!$C$80)>0),"CUMPLE","REQUIERE DATOS"))),"")
```

**MOTOR_H_S!AY8**

```excel
=IF(DS_INPUT!A8="SI",IF(AND(MOTOR_ESPECTRAL_S!$AF$8="OK",MOTOR_ESPECTRAL_S!$AG$8>0,MOTOR_H_S!AV8>0.000000001,ISNUMBER(PRESIONES_SERVICIO!$B$44)),(MOTOR_ESPECTRAL_S!$AX$8+PRESIONES_SERVICIO!$B$44)/MOTOR_H_S!AV8,""),"")
```

**MOTOR_H_S!AZ8**

```excel
=IF(DS_INPUT!A8="SI",IF(DERIVADOS_S!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_S!AD8,IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_H_S!AV8<=0.000000001,"NO APLICA",IF(MOTOR_ESPECTRAL_S!$BM$8<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(NOT(OR(INGRESO_DATOS!$C$128="NO",INGRESO_DATOS!$C$128="SI")),"DATOS INVÁLIDOS",IF(OR(COUNT(INGRESO_DATOS!$C$126)<>1,LEN(INGRESO_DATOS!$C$127)=0,AND(INGRESO_DATOS!$C$128="SI",OR(COUNT(INGRESO_DATOS!$C$129)<>1,LEN(INGRESO_DATOS!$C$130)=0))),"REQUIERE DATOS",IF(OR(INGRESO_DATOS!$C$126<=0,PRESIONES_SERVICIO!$B$44<0),"DATOS INVÁLIDOS",IF(MOTOR_H_S!AY8>=INGRESO_DATOS!$C$126,"CUMPLE","NO CUMPLE")))))))),"")
```

**MOTOR_H_S!BE8**

```excel
=IF(DS_INPUT!A8="SI",IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(COUNTIF(MOTOR_H_S!BV8:BY8,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(MOTOR_H_S!BV8:BY8,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(MOTOR_H_S!BV8:BY8,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(MOTOR_H_S!BV8:BY8,"REQUIERE DATOS")>0,"REQUIERE DATOS",IF(COUNTIF(MOTOR_H_S!BV8:BY8,"NO APLICA")=4,"NO APLICA","CUMPLE")))))),"")
```

**MOTOR_H_S!BV8**

```excel
=IF(DS_INPUT!A8="SI",IF(DERIVADOS_S!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_S!AD8,IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_ESPECTRAL_S!$BN$8=0,"NO APLICA",IF(MOTOR_ESPECTRAL_S!$BM$8<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(INGRESO_DATOS!$C$131)<>1,LEN(INGRESO_DATOS!$C$132)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!$C$131<=0,"DATOS INVÁLIDOS",IF(MOTOR_ESPECTRAL_S!$BR$8>=INGRESO_DATOS!$C$131,"CUMPLE","NO CUMPLE"))))))),"")
```

**MOTOR_H_S!BW8**

```excel
=IF(DS_INPUT!A8="SI",IF(DERIVADOS_S!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_S!AD8,IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_ESPECTRAL_S!$BO$8=0,"NO APLICA",IF(MOTOR_ESPECTRAL_S!$BM$8<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(INGRESO_DATOS!$C$131)<>1,LEN(INGRESO_DATOS!$C$132)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!$C$131<=0,"DATOS INVÁLIDOS",IF(MOTOR_ESPECTRAL_S!$BS$8>=INGRESO_DATOS!$C$131,"CUMPLE","NO CUMPLE"))))))),"")
```

**MOTOR_H_S!BX8**

```excel
=IF(DS_INPUT!A8="SI",IF(DERIVADOS_S!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_S!AD8,IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_ESPECTRAL_S!$BP$8=0,"NO APLICA",IF(MOTOR_ESPECTRAL_S!$BM$8<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(INGRESO_DATOS!$C$131)<>1,LEN(INGRESO_DATOS!$C$132)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!$C$131<=0,"DATOS INVÁLIDOS",IF(MOTOR_ESPECTRAL_S!$BT$8>=INGRESO_DATOS!$C$131,"CUMPLE","NO CUMPLE"))))))),"")
```

**MOTOR_H_S!BY8**

```excel
=IF(DS_INPUT!A8="SI",IF(DERIVADOS_S!AD8="REQUIERE ANÁLISIS DE TORSIÓN EN PLANTA",DERIVADOS_S!AD8,IF(MOTOR_ESPECTRAL_S!$AF$8<>"OK",MOTOR_ESPECTRAL_S!$AF$8,IF(MOTOR_ESPECTRAL_S!$BQ$8=0,"NO APLICA",IF(MOTOR_ESPECTRAL_S!$BM$8<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(INGRESO_DATOS!$C$131)<>1,LEN(INGRESO_DATOS!$C$132)=0),"REQUIERE DATOS",IF(INGRESO_DATOS!$C$131<=0,"DATOS INVÁLIDOS",IF(MOTOR_ESPECTRAL_S!$BU$8>=INGRESO_DATOS!$C$131,"CUMPLE","NO CUMPLE"))))))),"")
```

**MOTOR_H_S!DI8**

```excel
=IF(DS_INPUT!A8="SI",IF(DS_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_S!AZ8)=0,"",MOTOR_H_S!AZ8)),"")
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
=IF(DS_INPUT!A8="SI",IF(DS_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_S!W8)=0,"",MOTOR_H_S!W8)),"")
```

**MOTOR_H_S!DX8**

```excel
=MOTOR_ESPECTRAL_S!$DX$8
```

**MOTOR_H_S!DY8**

```excel
=IF(DS_INPUT!A8="SI",IF(DS_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_S!X8)=0,"",MOTOR_H_S!X8)),"")
```

**MOTOR_H_S!DZ8**

```excel
=IF(DS_INPUT!A8="SI",IF(DS_INPUT!A8="NO","NO APLICA",IF(LEN(MOTOR_H_S!Y8)=0,"",MOTOR_H_S!Y8)),"")
```

**MOTOR_H_S!EB8**

```excel
=IF(DS_INPUT!A8="SI",IF(DS_INPUT!A8="NO","NO APLICA",IF(MOTOR_ESPECTRAL_S!$BZ$8="NO","NO APLICA",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"DATOS INVÁLIDOS")+COUNTIF(MOTOR_H_S!DS8:DZ8,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(MOTOR_H_S!DS8:DZ8,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")+COUNTIF(MOTOR_H_S!DS8:DZ8,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL")>0,"REQUIERE ANÁLISIS DE CONTACTO PARCIAL",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")+COUNTIF(MOTOR_H_S!DS8:DZ8,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(MOTOR_H_S!DS8:DZ8,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"REQUIERE DATOS")+COUNTIF(MOTOR_H_S!DS8:DZ8,"REQUIERE DATOS")>0,"REQUIERE DATOS",IF(COUNTIF(MOTOR_ESPECTRAL_S!$DR$8,"NO CUMPLE")+COUNTIF(MOTOR_H_S!DS8:DZ8,"NO CUMPLE")>0,"NO CUMPLE","CUMPLE")))))))),"")
```

