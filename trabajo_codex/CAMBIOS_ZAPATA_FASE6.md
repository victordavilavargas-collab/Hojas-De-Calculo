# Fase 6 — integridad del motor multicombo de zapata aislada

Fecha: 2026-10-01. Repositorio: `victordavilavargas-collab/Hojas-De-Calculo`, rama `main`. Base F5: `db60c898b429339dab81f5e02223ecf3494e8e73`.

**Resultado técnico actual: NO CUMPLE. Completitud / validez: REQUIERE DATOS. Cobertura: REQUIERE CONFIRMAR ENVOLVENTE COMPLETA.** Son resultados simultáneos; un dato pendiente no sustituye un incumplimiento conocido.

Se creó `Diseño de zapata aislada_CORREGIDA_FASE6.xlsx` desde la copia F5. No se cambiaron dimensiones, materiales, acciones originales ni acero para lograr CUMPLE. Los datos de prueba se ejecutaron en sesiones de Excel que cerraron sin guardarlos. El libro conserva un último y un servicio activos del caso original; las otras filas siguen inactivas. Las confirmaciones de factores, envolventes y plano de armado permanecen pendientes.

## Cambios y ubicación

| Hoja / rango | Cambio |
|---|---|
| CONTROL_MULTICOMBO B7:B12 | Pesos incluidos en modelo, suma manual vinculada a INGRESO C34:C35 y referencias; detecta doble conteo |
| CONTROL_MULTICOMBO B14:B16 | qadm global, referencia EMS y base NETA/BRUTA vinculadas a los datos originales |
| CONTROL_MULTICOMBO B18:B20 / B33 | Envolventes U/S completas, fuente de modelo/archivo/fecha/referencia y estado de cobertura |
| CONTROL_MULTICOMBO B22:B23 / B35 | Armado confirmado en plano y referencia |
| COMBOS_ULTIMOS R:V | gamma_Wz, gamma_Ws, referencia, confirmación y estado por fila |
| COMBOS_ULTIMOS W:BA | Tipo de resultado, extremo/estación, ejes, convención, tipo CSI, estado/step y seis procedencias |
| COMBOS_ULTIMOS BB:BO | T aplicada, determinante, error ortogonal, concurrencia, pesos y validez |
| COMBOS_SERVICIO K | Fórmula qadm base EMS u override documentado; ya no son 60 números independientes |
| COMBOS_SERVICIO AE:AI | Override, valor, EMS, justificación y reducción CS ya incluida |
| COMBOS_SERVICIO AJ:BN / BO:CH | Metadatos, matriz, validación y seis contribuciones CS normalizadas |
| RESULTADOS_ULTIMOS IV:JC | Ocho estados de ARMADO separados de los estados de CÁLCULO As |
| ENVOLVENTES B5 / B6 / B54 | Técnico / validez / cobertura separados |
| ENVOLVENTES F / K | Estado de control o armado / cálculo As; gobernantes de As independientes |
| ENVOLVENTES L37:L39 | Resultado técnico de conexión antes del condicionamiento por cobertura |
| ENV_BARRAS M:O / Y:AB | Estados condicionados por cobertura y estados técnicos independientes de anclaje/empalme/barras |
| CONEXION_COMBOS, FUERZAS_BARRAS B5 | Confirmación de cobertura visible |
| RESUMEN B23 / B164:B166 | Resultado técnico, validez, cobertura y armado; incluidos en impresión |

Las columnas de metadatos están agrupadas para facilitar la lectura. Expandir los grupos al importar datos. Los factores U R:V y las opciones de servicio AE:AI quedan visibles. Amarillo identifica entradas; azul identifica fórmulas. Los factores antiguos `inp_fwz_u` e `inp_fws_u` se conservaron como registro histórico, con comentarios que indican que el motor utiliza R:S por combinación. MAPEO_IMPORTACION conserva el registro F5; sus permutaciones no gobiernan la conversión F6.

## Pesos, contacto y presión neta

El peso físico de zapata se obtiene de volumen por densidad; el de relleno, de área por altura y densidad. No dependen del selector de suma manual. Por último se aplican factores independientes y documentados:

`Wz,u = Wz · gamma_Wz`, `Ws,u = Ws · gamma_Ws`.

La incorporación en el modelo y la suma manual son opciones excluyentes para cada peso. SI de inclusión requiere referencia. SI incluido + SI suma manual da DATOS INVÁLIDOS. No se infieren factores por el nombre de la combinación. Los valores iniciales 1.00 son editables y **pendientes de confirmación**, aunque permiten diagnósticos numéricos provisionales; no habilitan CUMPLE definitivo.

Si los pesos no están importados: `Qbruto = P + Wzu + Wsu`. Si ya están importados, el motor deduce la parte uniforme para obtener las acciones de superestructura y conserva el bruto sin volver a sumar. Con excentricidad geométrica, también retira el momento del peso uniforme referido al punto de aplicación: `Psuper=Pimport−Winc`, `Mxsuper=Mximport−Winc·yc`, `Mysuper=Myimport+Winc·xc`. Esto preserva el equilibrio al pasar al centro de la base.

Con contacto completo, el cuerpo usa la presión estructural neta. La prueba específica cambió ambos factores de 0.9 a 1.4: cambió q bruta, pero se mantuvieron punzonamiento, cuatro cortantes y ocho As. Otra prueba pasó de contacto parcial a completo al cambiar los pesos brutos. En contacto parcial el cálculo estructural sigue bloqueado; no se desarrolló un solver de contacto.

Para pesos declarados incluidos, la deducción supone acciones uniformes centradas en la base de esta zapata y factores coherentes con el modelo. Una distribución diferente requiere análisis externo documentado; no puede representarse con estos selectores.

## Importación CSI y transformación

Cada fila exige tipo de resultado, identificación de elemento/apoyo, tabla exportada, modo de ejes y referencia. Las acciones finales son de la superestructura sobre la cimentación: P positivo hacia abajo y fuerzas/momentos horizontales globales. Los tipos previstos son FRAME FORCE, JOINT REACTION, BASE REACTION, GLOBAL MANUAL y OTRO. Una reacción de base agregada de todo un edificio no se admite como acción de esta zapata; esa correspondencia debe estar sustentada por la referencia del modelo.

El orden crudo depende de la convención declarada:

| Convención | Orden de seis entradas |
|---|---|
| ACCIONES DEL LIBRO, GLOBAL | P, Fx, Fy, Mx, My, Mz |
| ACCIONES DEL LIBRO, local horizontal | P, V2, V3, M2 de acción, M3 de acción, Mz |
| CSI ORIGINAL, FRAME | P, V2, V3, T, M2, M3 |
| CSI ORIGINAL, reacción GLOBAL | F1, F2, F3, M1, M2, M3 |

En reacciones se invierten las componentes de acción/reacción: P=R3, Fx=−R1, Fy=−R2 y momentos de acción opuestos. Para frame se exige Station en metros desde I, extremo de cimentación I/J, verticalidad y orientación +Z/−Z. Local 1 no vertical requiere datos globales o transformación 3D externa; queda FUERA DEL ALCANCE IMPLEMENTADO.

La matriz horizontal admite GLOBAL, presets 0/90/180/270, ángulo general o cuatro coeficientes trazables. θ se mide antihorario visto desde +Z, local 2=(cosθ,sinθ); se conserva la orientación física de local 3 según el signo vertical de local 1. Se verifica `T·Tᵀ=I` y `det(T)=s`, con tolerancia 1E−8, donde s es +1/−1 para local 1 hacia +Z/−Z. GLOBAL usa identidad.

La conversión de fuerzas internas a acciones se hace antes de la rotación. Con e=+1 para I y −1 para J: `P=−e·s·P_CSI`, `[Fx,Fy]=e·T[V2,V3]`, `[Mx,My]=e·T[−M2,M3]`, `Mz=e·s·T_CSI`. El signo de M2 resulta de la convención de compresión de caras CSI y su conversión a vector momento por mano derecha; **no se aplica ese cambio al modo ACCIONES DEL LIBRO**, que ya contiene momentos de acción. En ambos casos la misma matriz T transforma el vector horizontal de fuerza y el de momento. Esta conversión se probó en I, J y local 1 hacia −Z.

## Concurrencia y completitud

LINEAR ADD solo se acepta como vector cuando sus resultados son single-valued y están confirmados. SINGLE CASE / SINGLE STEP debe identificar el estado. ENVELOPE, ABSOLUTE ADD, SRSS, RANGE ADD, MULTISTEP y OTRO no constituyen automáticamente un vector simultáneo.

Para un extremo correspondiente se exige CORRESPONDENCE SI, componente, Max/Min, Case/Combo, StepType, StepNum si existe y exportación. Las seis claves de origen deben coincidir **exactamente** con `Case/Combo|StepType|StepNum`. Time/Step/Mode/Frequency exigen StepNum. Faltantes producen REQUIERE DATOS; procedencias mezcladas producen **DATOS NO CONCURRENTES — NO USAR COMO COMBO** y bloquean los resultados numéricos. Se rechazó el vector Pmax(A), Mxmax(B), Mymax(C) aunque perteneciera a un mismo ENVELOPE nominal.

Las referencias y claves son declaraciones auditables del usuario: la plantilla no lee la base CSI ni demuestra por sí misma que una exportación sea auténtica o que estén todas las combinaciones. Las confirmaciones U y S están por defecto en NO, y requieren fuente de modelo/archivo/fecha/referencia. La cobertura se aplica también a conexión y a las envolventes de anclaje/empalme de las 60 barras: un resultado técnico favorable no publica CUMPLE de la envolvente mientras la cobertura esté pendiente. Un NO CUMPLE conocido se conserva.

## qadm y CS

La base EMS está en INGRESO C18, su referencia en C80 y la convención NETA/BRUTA en C77; CONTROL_MULTICOMBO los vincula. Sin override, todas las filas S toman esa misma base. Override SI requiere valor positivo, referencia EMS y justificación. El incremento temporal de 1.30 sigue requiriendo sismo/viento y habilitación documentada. Se conserva la comparación NETA/BRUTA de F5.

La reducción sísmica opera como `vector + (factor−1)·CS`, con CS firmado presente en esa combinación, referido al mismo estado y ejes, y normalizado con la misma conversión. Para factor 0.80 se exigen los seis componentes y fuente. Si el vector ya contiene 0.80CS, el factor adicional debe ser 1.00; otra reducción da DATOS INVÁLIDOS. Se comprobaron ambos caminos sin reducir la parte gravitacional. El incremento qadm corresponde a E.060 15.2.4; el 80% de CS, a **15.2.5**.

## Flexión y armado

CALCULADO indica que se obtuvo As requerido, no que el acero real cumple. Se separan cálculo (CALCULADO, REQUIERE DATOS, NO FACTIBLE, FUERA DE ALCANCE) y armado (CUMPLE, NO CUMPLE, REQUIERE DATOS). Las ocho caras/capas conservan sus demandas, As y gobernantes. El armado exige plano confirmado y los controles F5 de conteos, áreas, separaciones y ubicación de franjas; el desarrollo y los restantes detalles normativos conservan sus verificaciones independientes en el cuerpo/RESUMEN.

Se corrigió además un enlace de exposición F5: en dirección larga de zapata rectangular, el resumen de As de franja multiplicaba por lado corto/largo, creando un exterior artificial. Ahora esa dirección usa As total uniforme; en la corta se mantiene la franja central `2/(beta+1)` y el resto exterior. El detalle original F5 ya seguía esa distribución; la corrección hace coherente el resumen con el motor y E.060 15.4.4. Se probaron rectángulos con lado largo X y lado largo Y. Los datos geométricos del caso real permanecen intactos.

## Validación

- **108 casos distintos aprobados**: 64 de regresión F5 y 44 F6, incluidas las 30 pruebas obligatorias y controles adicionales de StepNum, procedencia exacta, local 1 −Z, pesos incluidos con offset y cambio de contacto bruto.
- Verificador independiente: **337838 comprobaciones, cero fallos**, con cuadratura de presiones, equilibrio, flexión por bisección y geometría/desarrollo de barras.
- Comparación directa contra los 64 resultados F5: **47392 comprobaciones numéricas y de gobernantes, cero diferencias**. Los antiguos casos de mapeo se conservaron como acciones previamente interpretadas; su rechazo se ejercitó con las validaciones equivalentes. Las nuevas pruebas cubren CSI ORIGINAL.
- Pruebas semánticas F6: **234 comprobaciones, cero fallos**. Los casos suficientes/insuficientes de armado usan conteos, separación y recubrimiento explícitos; únicamente en pruebas.
- Se conservan 60 U, 60 S, cuatro cortantes, ocho estados de flexión, conexión, 60×60 fuerzas de barras, gobernantes independientes y análisis eta del ID citado. El selector visual sigue sin alterar resultados ni envolventes.
- **58 hojas, 24 gráficos, 510 nombres globales, 167320 fórmulas**. Series, posiciones y tipos de los 24 gráficos conservados. Longitud máxima de fórmula: 6739 caracteres.
- Entradas originales INGRESO C14:C188 y CARGAS C7:C38 comparadas exactamente. Original y Fases 1–5 conservados por SHA-256.
- Excel nativo **16.0**, idioma español **3082**; funciones compatibles con Excel 2016. La versión 16.0 identifica la familia de Excel, no certifica una edición comercial concreta.
- CalculateFullRebuild, guardar, cerrar, nueva aplicación Excel, reabrir, recalcular y comparar persistencia: **True**. Reapertura final ordinaria, sin reparación: **True**. Cero errores, circularidad, VBA, enlaces externos, `_xlfn` o `_xludf`.
- Revisión visual de resumen, cálculo As, control de proyecto, convenciones, entradas, selector y análisis complementario. Se normalizaron solo nombres reservados de impresión tras los guardados para evitar el conflicto de `Print_Area` en esta instalación; ninguna fórmula ni dato se editó en XML.

La aprobación de una prueba significa que se obtuvo el comportamiento esperado, incluso cuando es rechazo, REQUIERE DATOS o NO CUMPLE. No son alternativas de diseño del proyecto.

### Casos F6

| Caso | Comprobaciones semánticas | Entrada U observada | Cobertura observada |
|---|---:|---|---|
| F6 01 gamma 1.4D | 4 | OK | COMPLETO |
| F6 02 gamma 0.9D | 4 | OK | COMPLETO |
| F6 03 gamma diferentes | 5 | OK | COMPLETO |
| F6 04 pesos incluidos | 6 | OK | COMPLETO |
| F6 05 doble conteo | 3 | DATOS INVÁLIDOS | COMPLETO |
| F6 06 bruto factor bajo | 3 | OK | COMPLETO |
| F6 07 neto factor alto | 3 | OK | COMPLETO |
| F6 08 theta 0 | 8 | OK | COMPLETO |
| F6 09 theta 90 | 8 | OK | COMPLETO |
| F6 10 theta 37 | 8 | OK | COMPLETO |
| F6 11 matriz ortogonal | 5 | OK | COMPLETO |
| F6 12 matriz no ortogonal | 3 | DATOS INVÁLIDOS | COMPLETO |
| F6 13 FRAME I | 9 | OK | COMPLETO |
| F6 14 FRAME J | 9 | OK | COMPLETO |
| F6 15 JOINT REACTION | 9 | OK | COMPLETO |
| F6 16 BASE REACTION | 9 | OK | COMPLETO |
| F6 17 Linear Add | 4 | OK | COMPLETO |
| F6 18 Envelope sin correspondence | 4 | DATOS NO CONCURRENTES — NO USAR COMO COMBO | COMPLETO |
| F6 19 Envelope M3 Max | 4 | OK | COMPLETO |
| F6 20 SRSS sin correspondence | 4 | DATOS NO CONCURRENTES — NO USAR COMO COMBO | COMPLETO |
| F6 21 Range Add sin correspondence | 4 | DATOS NO CONCURRENTES — NO USAR COMO COMBO | COMPLETO |
| F6 22 Step concurrente | 5 | OK | COMPLETO |
| F6 23 Envolvente NO | 5 | OK | REQUIERE CONFIRMAR ENVOLVENTE COMPLETA |
| F6 24 Envolvente SI | 4 | OK | COMPLETO |
| F6 25 NO CUMPLE y pendientes | 4 | OK | COMPLETO |
| F6 26 As calculado armado pendiente | 5 | OK | COMPLETO |
| F6 27 As y armado cumple | 4 | OK | COMPLETO |
| F6 28 As y armado falla | 4 | OK | COMPLETO |
| F6 29 CS ya reducido | 4 | OK | COMPLETO |
| F6 30 CS aplicar una vez | 8 | OK | COMPLETO |
| F6 31 Envelope artificial | 4 | DATOS NO CONCURRENTES — NO USAR COMO COMBO | COMPLETO |
| F6 32 reducción duplicada | 3 | OK | COMPLETO |
| F6 33 local1 inclinado | 3 | FUERA DEL ALCANCE IMPLEMENTADO | COMPLETO |
| F6 34 override incompleto | 3 | OK | COMPLETO |
| F6 35 override completo | 4 | OK | COMPLETO |
| F6 36 rectangular largo X | 5 | OK | COMPLETO |
| F6 37 rectangular largo Y | 5 | OK | COMPLETO |
| F6 38 factores pendientes | 4 | OK | COMPLETO |
| F6 39 StepNum omitido | 3 | REQUIERE DATOS | COMPLETO |
| F6 40 clave con diferencia exacta | 3 | DATOS NO CONCURRENTES — NO USAR COMO COMBO | COMPLETO |
| F6 41 frame local1 -Z | 10 | OK | COMPLETO |
| F6 42 pesos incluidos offset | 5 | OK | COMPLETO |
| F6 43 cambio contacto gamma 0.1 | 3 | OK | COMPLETO |
| F6 44 cambio contacto gamma 1.4 | 3 | OK | COMPLETO |

## Pendientes del caso real y alcance

Confirmar por combinación los factores y su referencia, registrar el conjunto completo de U/S y fuente del modelo, completar datos de plano/conteos/recubrimientos, EMS y análisis externo de conexión requeridos por F4/F5. La plantilla muestra esos pendientes sin hacer ajustes para forzar CUMPLE. El incumplimiento técnico actual conserva los controles desfavorables del caso ingresado.

No se implementaron Capítulo 21, contacto parcial, bordes/esquinas, perímetros abiertos, transformación 3D ni solver interno P-Mx-My. Los controles de conexión continúan usando el análisis externo de Modo B.

## Fuentes

- [RNE oficial del Ministerio de Vivienda](https://www.gob.pe/institucion/vivienda/informes-publicaciones/2309793-reglamento-nacional-de-edificaciones-rne): E.060 DS 010-2009 y E.050 RM 406-2018. Textos oficiales preservados en la auditoría previa, con consulta del catálogo oficial para esta fase.
- [CSI: convenciones de fuerzas internas de frame](https://docs.csiamerica.com/help-files/sap/Output/Frame_Element_Internal_Forces_Output_Conventions.htm): estación desde I, caras, fuerzas y signos de flexión.
- [CSI: convenciones de reacciones de joint](https://docs.csiamerica.com/help-files/sap/Output/Joint_Element_Output_Conventions.htm): reacciones globales sobre elementos soportados.
- [CSI: tipos de combinación](https://docs.csiamerica.com/help-files/etabs/Menus/Define/Load_Combinations/Load_Combination_Data_Form.htm): Linear Add, Envelope, Absolute Add, SRSS y Range Add.
- [CSI: opciones de tablas](https://docs.csiamerica.com/help-files/etabs/Keyboard_Commands_and_Special_Features/Table_Options_form.htm): resultados por paso y envolventes.

La plantilla incluye la conversión y sus supuestos; la asociación al apoyo real, estación/cara del apoyo y referencias del modelo debe verificarse contra la exportación antes de usar resultados de proyecto.

SHA-256 del libro final: `6315d90f64da89867869e3a5580dfe8717f0bfeb73f0b885c04488ab565edae7`.
