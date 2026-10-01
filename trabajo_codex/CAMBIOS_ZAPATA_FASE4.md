# CAMBIOS ZAPATA FASE 4 — CONEXIÓN COLUMNA–ZAPATA Y ALCANCE E.060

Fecha: 30/09/2026, America/Lima. Base: `trabajo_codex/Diseño de zapata aislada_CORREGIDA_FASE3.xlsx`, documento `CAMBIOS_ZAPATA_FASE3.md`, commit `36917b0af619398865b2a1f2aedaf5da79fd39c2`. Se verificó origin `victordavilavargas-collab/Hojas-De-Calculo`, rama main y pull --ff-only antes de editar. El repositorio CSI padre no se modifica.

La Fase 4 incorpora el **Modo B de fuerzas externas por barra** para la conexión de una columna rectangular interior construida in situ. Exige análisis de sección identificado, combinación, fuerzas firmadas de cada barra, resultante y pico de contacto del concreto y D/C externo de sección. Comprueba equilibrio, material, aplastamiento, acero que cruza la junta, desarrollo y empalmes. No calcula una superficie de interacción interna mediante distribución elástica ni presenta 12.17 como ecuación P–Mx–My.

Se depuró el módulo eta: el acero básico de 15.4, el análisis horizontal complementario y su adopción tienen resultados y estados separados. El caso actual conserva todas las entradas; no se ajustó qadm, geometría, cargas, barras o separaciones para conseguir CUMPLE.

## 1. Entregables, estructura y conservación

- `trabajo_codex/Diseño de zapata aislada_CORREGIDA_FASE4.xlsx`.
- `trabajo_codex/CAMBIOS_ZAPATA_FASE4.md`, este registro.

Estos son los únicos dos archivos del commit solicitado: `Fase 4 - conexión columna zapata P-Mx-My E060`. Los ensayos, scripts, manifiestos, capturas/PDF y JSON quedan como evidencia local fuera del commit.

Se conservan las 15 hojas previas en orden y sus 24 gráficos, referencias de series, comentarios, combinaciones originales, validaciones y paneles. Se añaden `CONEXION_COLUMNA_ZAPATA` y `BARRAS_CONEXION`: **17 hojas, 24 gráficos y 456 nombres definidos**, frente a 368 nombres en Fase 3. Los nombres heredados mantienen sus destinos. Hay 5947 celdas de contenido nuevas/modificadas, incluidas las 3600 distancias auxiliares de barras, todas incluidas en el manifiesto; ninguna modificación de contenido fuera de éste.

Todas las entradas de `INGRESO_DATOS!C14:C188` y `CARGAS!C7:C38` se compararon exactamente contra Fase 3. Permanecen Bx=By=3.75 m, h=.50 m, qadm=8.5 tf/m² y fy de resistencia de la zapata=4200 kgf/cm². El libro entregado no contiene los datos sintéticos de las pruebas. Los nuevos datos de análisis/barras quedan vacíos; modo EXTERNO y adopción local NO son selectores de método, no un resultado de cálculo ni una certificación.

Los archivos originales y las tres fases anteriores permanecen íntegros por SHA256:

| Archivo en trabajo_codex | SHA256 conservado |
|---|---|
| `CAMBIOS_ZAPATA_FASE1.md` | `24e6f0077e2f8ba51c8d80b51056834aa8400998d2532d9b83693d426eddbf3d` |
| `CAMBIOS_ZAPATA_FASE2.md` | `18aad8f776b00fde74027dca632bb60b503cbd6e4c24a366803ecaa87a5612a1` |
| `CAMBIOS_ZAPATA_FASE3.md` | `21cbc8089acc65b6aa2292954fcda880c3e652a4d24611c968fa0230af6ef1b2` |
| `Diseño de zapata aislada.xlsx` | `24f60a8b5a8b170de9ef528cc7f96120f0b5c651ccdad33acf8a6562965a7060` |
| `Diseño de zapata aislada_CORREGIDA_FASE1.xlsx` | `8d66b5590812704f8bdd1173b5583a4bcaaf00d500c1d854d00c42051192ded5` |
| `Diseño de zapata aislada_CORREGIDA_FASE2.xlsx` | `8d92bc7d557dcbb691b1d538e2dd3f96d830e54f69bb1f407a402637b3e2bd01` |
| `Diseño de zapata aislada_CORREGIDA_FASE3.xlsx` | `7074baa04d42f3637931dc92594fb0c314405ad015c4d37c8dcf21e81eaab433` |
| `README.md` | `aa90b4263adbbcba2b328767807e2ef41778e702a1dcbd49daeb2e057cb89057` |

## 2. Fuentes, unidades y alcance normativo

- [E.060, DS 010-2009-VIVIENDA, fuente oficial](https://cdn.www.gob.pe/uploads/document/file/2686419/E.060%20Concreto%20Armado%20DS%20N%C2%B0%20010-2009.pdf): 15.8.1/.1.1/.1.2/.1.3/.1.4/.2/.2.1; 10.17; 12.1, 12.2, 12.3, 12.14, 12.15, 12.16, 12.17; 7.6/7.7; 11.7; 9.3/9.4/9.5; 15.4/15.5, 11.12 y alcance de Capítulo 13.
- [E.050, RM 406-2018-VIVIENDA, fuente oficial](https://cdn.www.gob.pe/uploads/document/file/2366655/54%20E.050%20SUELOS%20Y%20CIMENTACIONES%20RM%20N%C2%B0%20406-2018-VIVIENDA.pdf): se mantienen presión/área efectiva, EMS y estabilidad de Fase 3.
- [Reglamento Nacional de Edificaciones, catálogo oficial](https://www.gob.pe/institucion/vivienda/informes-publicaciones/2309793-reglamento-nacional-de-edificaciones-rne).

Las entradas son kgf, tf, m y cm; esfuerzos kgf/cm², áreas cm² y momentos tf·m. Las conversiones normativas a MPa son internas: `k=.0980665 MPa/(kgf/cm²)`. No se reemplaza E.060 por un ACI posterior. El material de columna/dowels usa el fy de resistencia declarado en la entrada existente C109, común a las barras de este módulo; el grado nominal de la zapata conserva la separación de Fase 3.

| Regla | Tratamiento en Fase 4 |
|---|---|
| 15.8 | Transferencia concreta y de barras verticales; horizontal adicional no la sustituye |
| 10.17 / 9.3 | Aplastamiento en ambas superficies; phi=.70 y aumento opcional A2/A1=1 conservador |
| 12.17 | Empalmes según esfuerzo, porcentaje y escalonamiento; no fórmula de capacidad de sección |
| 12.1/2/3 | Desarrollo completo a fy en tracción/compresión, a ambos lados; conservador sin crédito por exceso |
| 11.7 | Cortante por fricción con Avf dedicado, anclado y con fuente de detalle |
| 15.4 / 10.5.4 / 9.7 | Acero básico a partir de momentos de caras y mínimo, independiente de eta |
| 15.5 / 11.12.1/2 | Cortante de losas y zapatas; se mantienen fuerzas y momentos biaxiales |
| 11.12.6 / Cap13 | Referencias que hablan de losa–columna / sistemas de losas; interpretación complementaria para este detalle de zapata |
| eta=.50 | Hipótesis del diseñador conservada como entrada; no valor prescrito por E.060 |

## 3. Separación del cuerpo, conexión y análisis adicional

`RESUMEN!B114:B120` muestra:

| Celda | Resultado |
|---|---|
| B114/B115 | Controles básicos del cuerpo / texto de estado normativo |
| B116 | Conexión columna–zapata 15.8 |
| B117 | Análisis complementario horizontal |
| B118 | Adopción explícita del refuerzo adicional |
| B120 | Cuerpo y conexión |
| B23 | Estado conjunto: cuerpo y conexión; complementario solo si se decide adoptarlo |

La tabla básica B130:B158 reproduce los controles previos excluyendo `B86` (eta), `B88` (conexión, separada) y `B107` (equilibrio del análisis local). Incluye los mínimos y distribución superior de Fase 3 y el nuevo contraste de alcance del punzonamiento. Se conservan controles EMS y criterios declarados de diseño. `NO CUMPLE NORMA` se usa para el fallo de controles del cuerpo; los pendientes/fallos complementarios se rotulan `REQUIERE ANÁLISIS COMPLEMENTARIO` / `NO CUMPLE ANÁLISIS COMPLEMENTARIO`, sin convertirlos en fallo normativo del cuerpo.

La prioridad de estados básicos se conserva: DATOS INVÁLIDOS > FUERA DEL ALCANCE IMPLEMENTADO > REQUIERE ANÁLISIS ESPECIAL > NO CUMPLE > REQUIERE DATOS > CUMPLE. `NO APLICA` es neutral solo en el componente que no corresponde. Los contadores B95:B98 excluyen eta y no se cuentan a sí mismos.

`ACERO_DETALLADO!B313` exige `inp_repartition_ok=SI`, referencia textual no vacía y combinación del análisis igual a `inp_case`. El selector SI solo no verifica compatibilidad o validez del análisis citado; CUMPLE queda condicionado a ese análisis y a los controles implementados. Datos/estado del caso se verifican aparte. Con momento gamma_f nulo, el componente es NO APLICA y no exige una referencia innecesaria.

## 4. Acero 15.4, local y adoptado

Antes, B251:B254 utilizaban `MAX(acero_global, MAX(As_franja_lados)+MAX(As_fuera_lados))` con la hipótesis eta, mezclando aplicación normativa y análisis adicional.

Ahora B251:B254 son exclusivamente:

```text
As_15_4_inf_x = FLEXION_ACERO!H5 * inp_by
As_15_4_inf_y = FLEXION_ACERO!H6 * inp_bx
As_15_4_sup_x = FLEXION_ACERO!H7 * inp_by
As_15_4_sup_y = FLEXION_ACERO!H8 * inp_bx
```

Las guardas requieren estado de resistencia y resultado numérico. H5:H8 conservan demanda por metro de la cara correspondiente y mínimo de Fase 3. La tabla nueva A306:F311 separa As_15_4 (B), As_local_complementario (C), As_adoptado (D), componente gobernante (E) y cantidad real usada por el análisis local (F).

`As_local` conserva el mayor requisito de cada región entre lados y suma franja+exterior. Si gamma_f Mu es cero devuelve cero. `As_adoptado=As_15_4` con adopción NO. Con SI y referencia/combinación válidas es MAX(básico, local); sin respaldo queda pendiente/vacío. Los controles regionales y el estado de adopción deben cumplir además de la cantidad adoptada; no basta sumar áreas.

Las verificaciones de desarrollo/recubrimiento complementarias B316:B320 tienen aplicabilidad propia: una capa superior exigida solo por análisis local no se da por desarrollada usando el NO APLICA de la capa básica. Se conservan el reparto firmado y su cierre de momentos de Fase 3; sus conteos reales usan nombres `n_comp_total_*` separados. La validación de eta y de su selector no gobierna la geometría normativa del cuerpo.

Se conservaron el mínimo **total** 10.5.4/9.7, UNA CARA/DOS CARAS y fracción explícita, piso .0012 cuando hay tracción en la cara aplicable, distribución inferior/superior 15.4.4, grado nominal separado de fy, qmax opcional, área efectiva E.050, pasivo solo en deslizamiento, signos y equilibrio de diagramas. Se verificaron numéricamente esos resultados para los 101 casos heredados.

## 5. Modo B: contrato y equilibrio de la conexión

Entradas nuevas `CONEXION_COLUMNA_ZAPATA!B7:B22`: método, fuente, combinación, base de fuerzas, D/C externo, phi, Fc, centroide x/y, Ac comprimida, pico de contacto, plano de barras, estribo real, exposición, epoxi y referencia de continuidad/confinamiento.

Se exige una referencia que identifique el documento/archivo, página y caso del análisis de sección que sustenta compatibilidad, equilibrio y resistencia reducida. La plantilla comprueba los valores proporcionados y su consistencia; no abre ni reproduce ese solver externo ni certifica el contenido de una referencia escrita. El D/C de sección externo es **dato**, no capacidad calculada internamente. Debe evaluarse el conjunto de combinaciones del proyecto; el libro evalúa el caso seleccionado y exige coincidencia de combinación.

Las fuerzas de barras y Fc deben corresponder a **acciones amplificadas actuales**: no ingresar fuerzas nominales de un análisis con Pu/phi como si equilibraran Pu. El D/C externo ya incluye phi. El control de esfuerzo de barras no vuelve a aplicar phi a sus fuerzas; no se duplica la reducción.

```text
F_i [tf]: compresión positiva, tracción negativa
x_i, y_i [cm]: respecto al centro de columna
ΣP  = Fc + ΣF_i
ΣMx = -Fc*y_c/100 - Σ(F_i*y_i)/100
ΣMy =  Fc*x_c/100 + Σ(F_i*x_i)/100
```

Se comparan con ult_p, ult_mx y ult_my trasladados al plano de junta según CARGAS. Las acciones corresponden a la superestructura: no se agregan pesos de zapata/relleno al análisis de sección. Cierre aceptado por eje: `abs(error)<=MAX(1e-8,abs(acción)*1e-8)`. El cierre prueba equilibrio; la compatibilidad constitutiva y la capacidad P–Mx–My provienen del análisis citado.

Fc no negativo; centroide dentro de sección; Ac no mayor que Ag, positiva si Fc>0; sigma_max no inferior a Fc/Ac. Si Fc=0, Ac, centroide y sigma_max deben ser cero explícitos. La sección externa cumple si D/C<=1 con fuente y datos consistentes. Se admite automáticamente phi=.70 en compresión de columna rectangular con estribos y .90 en tracción/flexión sin axial. El incremento permitido por 9.3 según carga/eje neutro requiere análisis especial: no se calcula Pb dentro de este Modo B. Torsión Mz, modo INTERNO y sistemas no implementados quedan bloqueados.

## 6. Barras reales, mínimo y aplastamiento

`BARRAS_CONEXION!A12:W71`: hasta 60 IDs únicos, coordenadas reales, barra comercial y área calculada, continuidad SI/NO, ID y barra asociada, L disponible en zapata y sobre junta, terminación, fuerza firmada, tipo y longitud de empalme, grupo de sección, escalonamiento, resistencia certificada de unión, referencia/AWS, alineación de dowel, separación libre del traslape y observación.

No se crea una distribución por conteo. Los IDs asociados deben ser únicos y distintos de los IDs que ya cruzan la junta: no se implementan asociaciones muchos-a-uno. Se bloquea reutilizar un dowel en varias filas para no duplicar su área ni su capacidad. Coordenadas/barras/fuerzas faltantes quedan pendientes; IDs duplicados, coordenadas fuera de columna y fuerzas no numéricas son inválidos. Las filas sin ID deben estar vacías. Una fuerza cero es válida si se ingresa numéricamente; vacío no significa cero.

Para continua SI, As real que cruza junta es el área de la columna. Para NO, usa el dowel real asociado sin sumar columna+dowel dos veces. El dowel requiere ID/barra/alineación/unión explícitos; solo se admite alineado con unión mecánica/soldada. Un dowel con traslape/offset requiere otro detalle/análisis y queda fuera del alcance implementado.

Se comprueba `As_real>=.005Ag` conforme a 15.8.2.1. El mínimo no demuestra transferencia P–Mx–My. El esfuerzo firmado individual es `F_i*1000/As_junta` y su valor absoluto se compara con fy de columna/dowels como control de material, separado del D/C externo. Se comprueban fc>=17 MPa (9.4) y fy de diseño<=550 MPa (9.5) en el dominio implementado.

Aplastamiento B54:B59: capacidades reducidas `.70*.85*fc_zapata*Ac/1000` y `.70*.85*fc_columna*Ac/1000`, demanda Fc y D/C con menor capacidad. Se añade comprobación conservadora del pico de presión de contacto frente a `.70*.85*MIN(fc)`; no se supone presión uniforme favorable ni aumento por A2/A1. El diagnóstico de exceso axial sobre capacidad de Ag no sustituye las fuerzas externas y su equilibrio. Compresión y tracción total en barras se muestran por separado.

## 7. Desarrollo completo a fy, independiente de capacidad P–Mx–My

Cada barra se verifica en tracción y compresión dentro de zapata; sobre junta se usa la mayor longitud de ambas para la barra de columna. Son barras verticales, psi_t=1 por orientación. Para 12.2.3 se usa Ktr=0 y límite de `(cb+Ktr)/db<=2.5`; no se toman reducciones por exceso de acero. psi_s=.8 hasta db=1.905 cm, luego1. psi_e corresponde al epoxi/recubrimiento/espacio declarado. Las raíces se limitan a8.3 en unidades MPa.

```text
ld_tr [cm] = MAX(30, fy_MPa*psi_s*psi_e /
                    (1.1*MIN(SQRT(fc_MPa),8.3)*MIN(2.5,cb/db))*db_cm)
ld_c [cm]  = MAX(20, .24*fy_MPa/MIN(SQRT(fc_MPa),8.3)*db_cm,
                    .043*fy_MPa*db_cm)
```

Se comprueban longitudes numéricas no negativas, Lzapata>=MAX(ld_tr,ld_c), Lsobre_junta>=MAX(ld_tr_col,ld_c_col), terminación RECTA, Lzapata<=h_cm−rec_inf, recubrimiento contra terreno al menos7cm, y espacio libre conforme a 7.6.3: MAX(1.5db,4cm,4/3 agregado). Ganchos no se usan para justificar compresión ni se implementa su desarrollo.

El recubrimiento de columna considera el estribo real: la distancia desde cara hasta acero longitudinal menos db del estribo debe alcanzar el mínimo a acero exterior según exposición. Los espacios entre barras se obtienen de las coordenadas reales. En traslapes se utiliza una envolvente conservadora del conjunto principal/compañera con su diámetro y separación declarados, independientemente de orientación, para cover/espacio de 7.6.4. Puede ser más restrictiva que un plano favorable resuelto geométricamente; un detalle que no pasa requiere revisión específica, no un ajuste oculto.

cb toma menor distancia a cara y una cota conservadora de media distancia entre barras. Se usa el menor diámetro real para mantener esa cota segura con diámetros mixtos. La matriz A80:BI139 contiene 60×60 distancias; diagonal/filas inactivas usan1e6 como auxiliar de MIN, no distancia física. AD en fila inactiva también usa1e6 auxiliar para mínimo de diámetros; se oculta visualmente por formato numérico y no representa una barra. Las barras activas muestran su diámetro real.

`BARRAS DESARROLLADAS A FY` es un control conservador de anclaje. No prueba por sí mismo interacción de sección, compatibilidad de deformaciones ni transmisión de una combinación P–Mx–My.

## 8. Empalmes de columnas, 12.17

- Continua sin empalme: seleccionar SIN EMPALME; muestra NO APLICA al traslape, conservando el anclaje a fy. No se presume empalme.
- Tracción: esfuerzo de la menor área de las barras asociadas frente a fy. Si <=.5fy, no más de la mitad del **número de barras** se empalma en la sección/grupo y escalonamiento>=ld, Clase A; en los demás casos Clase B. Porcentaje se calcula de los IDs/grupos declarados, no se ingresa una casilla favorable.
- Clase A requiere ld; Clase B1.3ld; mínimo de tracción30cm. Se calcula ld a tracción para el mayor db con cb reducido por espacio de la compañera del traslape. No se aplica reducción por exceso.
- Compresión: 12.16, `MAX(30, .071fy_MPa*db)` si fy<=420 MPa, o `MAX(30,(.13fy_MPa−24)*db)` si mayor. Se aumenta1.3 si fc<21 MPa. Con diámetros distintos se exige el mayor entre ld de compresión de barra mayor y longitud de empalme de barra menor. Sin reducciones por estribos/espirales de 12.17.2.4/.5.
- Longitud real debe alcanzar la requerida y caber en L disponible sobre junta. Separación de centros del traslape no mayor que MIN(longitud requerida/5,15cm). Se declaran pareja, grupo, separación y fuente de plano. Diámetros mayores que3.4925cm no se empalman por este módulo de traslape.
- Mecánico/soldado: resistencia certificada>=1.25fy del área mayor de las dos barras; referencia obligatoria y AWS conforme SI para soldado. No se deduce capacidad de un nombre comercial. Tope queda fuera de alcance.

Los grupos/escalonamientos son datos del plano citado. El análisis externo debe cubrir todas las combinaciones relevantes para seleccionar el estado de empalme; evaluar una combinación sola no comprueba una envolvente del proyecto. Los campos externos se conservan explícitos y vacíos cuando faltan. En uniones mecánicas/soldadas se exige también ID y diámetro de la pareja, sin presuponer su área; la referencia del certificado debe ser texto.

## 9. Cortante por fricción y alcance pendiente

H=raíz(Fx²+Fy²), en tf amplificadas. Mu=1.4 monolítica,1 rugosa limpia con amplitud6mm, .6 lisa. Se necesita fuente de detalle y Avf dedicado declarado en entradas existentes; no se acredita automáticamente el acero .005Ag ni el acero horizontal. `Avf_req=H*1000/(.85*mu*MIN(fy,420/k))`, y límite concreto `.85*MIN(.2*fc_min,5.5/k)*Ag/1000`. Anclaje SI y área suficiente obligatorios. H=0 hace NO APLICA al componente lateral.

Quedan fuera: solver interno P–Mx–My, torsión Mz de esta conexión, incremento de phi por Pb, dowel con offset/traslape, ganchos/paquetes, tope y detalles especiales de Cap21. El CUMPLE mostrado corresponde a los controles implementados de la combinación citada; no genera un certificado externo ni sustituye esos detalles específicos. No se implementó contacto parcial, columna de borde/esquina ni perímetro abierto. Conservan los bloqueos de Fase 3.

## 10. Punzonamiento con momento: requisito e interpretación

15.5 remite a11.12 para zapatas. 11.12.1/2 incluyen losas y zapatas en secciones críticas y resistencia a cortante. El procedimiento específico de11.12.6 habla de conexión losa–columna y enlaza13.5.3; Cap13 tiene alcance de sistemas de losas en dos direcciones. No se atribuye eta=.50 a esas disposiciones.

Se conservan Vu, Mx/My críticos firmados, gamma_v, las cuatro esquinas, pico y D/C de Fase 3. El modelo de excentricidad en un perímetro cerrado interior se mantiene como interpretación documentada de transferencia, debido a que el equilibrio de la reacción exterior deja momento resultante en ese perímetro; no se suprime Mu al separar el refuerzo horizontal.

Como contraste conservador para evitar un crédito flexional horizontal sin sustento, B70:B73 calculan una **hipótesis alternativa** con todo el momento crítico en la distribución excéntrica de cortante:

```text
vu = Vu*1000/Ac − Mx_crit*100000*y/Jx + My_crit*100000*x/Jy
```

B74 toma envolvente de picos del modelo gamma_v y de esta hipótesis; B75 su D/C. No se suman las tensiones de dos modelos ni se duplican las acciones. No se presenta coeficiente1 como fórmula literal obligatoria de E.060 para toda zapata. Si falla solo el contraste adicional, B76 exige REQUIERE ANÁLISIS ESPECIAL, en vez de un falso incumplimiento de una disposición directa. Se aplica únicamente al dominio interior/cerrado ya implementado; no se extiende a bordes/esquinas.

## 11. Validación independiente y nativa

**163 casos**: 101 heredados para regresión de mínimos/caras, distribución, grado/fy, área efectiva, pico opcional, pasivo, signos, equilibrio, cortantes y desarrollo; **62 nuevos** de conexión y separación de alcance. **80178 comprobaciones independientes, cero fallos.**

Se reconstruyeron presiones/integrales y diagramas, acero mediante inversión independiente de resistencia a flexión, punzonamiento, longitudes y distribución. En conexión se reconstruyeron ΣP/ΣMx/ΣMy desde coordenadas/fuerzas, As real y .005Ag, esfuerzos firmados, capacidades/D/C de ambas superficies, radios/distancias, desarrollo tracción/compresión, clase/porcentaje/longitud de empalme, capacidad1.25fy y Avf/límite concreto. Comparación numérica abs1e−8 + rel1e−8.

Los fixtures de Modo B son **datos sintéticos para verificar el motor**: sus fuerzas/resultantes satisfacen equilibrio por construcción independiente y su D/C externo es un dato de prueba etiquetado, no un análisis constitutivo certificado de una columna real. No se usó un reparto elástico ficticio como resistencia última. Los datos se aplicaron en una copia descartable, sin guardarlos en el entregable.

| Ensayo Fase 4 | Estado conexión | Estado conjunto |
|---|---|---|
| P-puro | CUMPLE | CUMPLE |
| P-Mx | CUMPLE | CUMPLE |
| P-My | CUMPLE | CUMPLE |
| P-Mx-My | CUMPLE | CUMPLE |
| signos-inversos | CUMPLE | CUMPLE |
| una-barra-traccion | CUMPLE | CUMPLE |
| varias-traccion | CUMPLE | CUMPLE |
| todas-compresion | CUMPLE | CUMPLE |
| barra-a-fy | CUMPLE | CUMPLE |
| barra-supera-fy | NO CUMPLE | NO CUMPLE |
| ld-zapata-insuficiente | NO CUMPLE | NO CUMPLE |
| ld-sobre-junta-insuficiente | NO CUMPLE | NO CUMPLE |
| As-menor-005Ag | NO CUMPLE | NO CUMPLE |
| As-mayor-005Ag | CUMPLE | CUMPLE |
| aplastamiento-gobierna | NO CUMPLE | NO CUMPLE |
| friccion-gobierna | NO CUMPLE | NO CUMPLE |
| friccion-cumple | CUMPLE | CUMPLE |
| continua-sin-empalme | CUMPLE | CUMPLE |
| traslape-compresion | CUMPLE | CUMPLE |
| traslape-traccion-clase-A | CUMPLE | CUMPLE |
| traslape-traccion-clase-B-esfuerzo | CUMPLE | CUMPLE |
| traslape-clase-B-porcentaje | CUMPLE | CUMPLE |
| traslape-insuficiente | NO CUMPLE | NO CUMPLE |
| empalme-mecanico | CUMPLE | CUMPLE |
| mecanico-insuficiente | NO CUMPLE | NO CUMPLE |
| empalme-soldado | CUMPLE | CUMPLE |
| soldado-sin-AWS | NO CUMPLE | NO CUMPLE |
| dowel-alineado | CUMPLE | CUMPLE |
| dowel-offset-bloqueado | FUERA DEL ALCANCE IMPLEMENTADO | FUERA DEL ALCANCE IMPLEMENTADO |
| referencia-externa-faltante | REQUIERE DATOS | REQUIERE DATOS |
| fuerza-faltante | REQUIERE DATOS | REQUIERE DATOS |
| fuerza-texto | DATOS INVÁLIDOS | DATOS INVÁLIDOS |
| cierre-P-invalido | DATOS INVÁLIDOS | DATOS INVÁLIDOS |
| cierre-Mx-invalido | DATOS INVÁLIDOS | DATOS INVÁLIDOS |
| capacidad-externa-no-cumple | NO CUMPLE | NO CUMPLE |
| modo-interno-bloqueado | FUERA DEL ALCANCE IMPLEMENTADO | FUERA DEL ALCANCE IMPLEMENTADO |
| phi-incrementado | REQUIERE ANÁLISIS ESPECIAL | REQUIERE ANÁLISIS ESPECIAL |
| torsion-no-implementada | REQUIERE ANÁLISIS ESPECIAL | REQUIERE ANÁLISIS ESPECIAL |
| barra-duplicada | DATOS INVÁLIDOS | DATOS INVÁLIDOS |
| coordenada-faltante | REQUIERE DATOS | REQUIERE DATOS |
| recubrimiento-columna-falla | NO CUMPLE | NO CUMPLE |
| gancho-bloqueado | FUERA DEL ALCANCE IMPLEMENTADO | FUERA DEL ALCANCE IMPLEMENTADO |
| 60-barras | CUMPLE | CUMPLE |
| eta-sin-fuente-no-contamina | CUMPLE | CUMPLE |
| eta-invalido-no-contamina | CUMPLE | CUMPLE |
| eta-adopcion-sin-fuente | CUMPLE | REQUIERE ANÁLISIS COMPLEMENTARIO |
| traslape-barra-asociada-mayor | CUMPLE | CUMPLE |
| traslape-barra-asociada-menor | CUMPLE | CUMPLE |
| traslape-excede-longitud-disponible | NO CUMPLE | NO CUMPLE |
| escalonamiento-clase-B | CUMPLE | CUMPLE |
| exposicion-invalida | DATOS INVÁLIDOS | DATOS INVÁLIDOS |
| referencia-no-texto | REQUIERE DATOS | REQUIERE DATOS |
| fy-supera-550MPa | NO CUMPLE | NO CUMPLE |
| fy5000-traslape-compresion | CUMPLE | CUMPLE |
| fc-menor-21-traslape-compresion | CUMPLE | CUMPLE |
| eta-validado-adoptado | CUMPLE | CUMPLE |
| eta-validado-armado-local-falla | CUMPLE | NO CUMPLE ANÁLISIS COMPLEMENTARIO |
| mecanico-asociada-faltante | REQUIERE DATOS | REQUIERE DATOS |
| mecanico-certificado-no-texto | REQUIERE DATOS | REQUIERE DATOS |
| dowel-ID-duplicado | DATOS INVÁLIDOS | DATOS INVÁLIDOS |
| dowel-reutiliza-barra-junta | DATOS INVÁLIDOS | DATOS INVÁLIDOS |
| pareja-empalme-duplicada | DATOS INVÁLIDOS | DATOS INVÁLIDOS |

Pruebas de aislamiento con Mu no nulo: falta de fuente/eta inválido no cambian B251:B254 ni B114 frente al mismo caso de referencia. La adopción SI sin fuente queda pendiente. Se probaron60 barras reales declaradas y diámetros asociados mayor/menor, escalonamiento, longitud de traslape que no cabe, fy>550 y las ramas de compresión fy>420 / fc<21 MPa. Los ensayos negativos de datos no generaron errores de fórmula.

Microsoft Excel COM **16.0**, interfaz española comprobada (LanguageID 3082 y FormulaLocal con SI, CONTAR.SI, SUMAPRODUCTO, ESNUMERO y RAIZ), apertura normal, `CalculateFullRebuild`, guardado, cierre, reapertura y nuevo recálculo. Se compararon tres snapshots nativos de persistencia sin variación de valores/estados. El recorrido de las 17 hojas detectó cero errores y cero circularidad; el XLSX guardado no tiene cachés de error, macros, links externos, _xlfn/_xludf ni funciones posteriores a Excel2016. Las fórmulas OOXML/COM estándar se localizan en Excel español. Se revisaron 18 vistas nativas de los módulos modificados/nuevos y se exportaron los 24 gráficos, manteniendo referencias y tipos.

## 12. Resultado del caso original

| Componente | Estado conservado / nuevo |
|---|---|
| Estado conjunto B23 | NO CUMPLE |
| Cuerpo B115 | NO CUMPLE NORMA |
| Conexión B116 | REQUIERE DATOS |
| Análisis horizontal B117 | REQUIERE ANÁLISIS COMPLEMENTARIO |
| Adopción adicional | NO / NO APLICA |

La presión/área efectiva y acero básico existentes siguen sin cumplir; además faltan EMS/detalles declarados en los controles previos. No se inventan fc/fy de columna, fuerzas, plano, anclajes o certificados de uniones. Para cerrar la conexión real se necesita el análisis externo de sección para la combinación, resultante/pico de concreto, tabla de barras real y longitudes/empalmes. Eso es información del proyecto, no optimización para forzar CUMPLE.
