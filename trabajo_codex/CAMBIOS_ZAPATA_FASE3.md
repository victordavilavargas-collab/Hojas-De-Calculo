# CAMBIOS ZAPATA FASE 3 — CORRECCIÓN DEL MOTOR E.060 / E.050

Fecha: 30/09/2026, America/Lima. Base: `trabajo_codex/Diseño de zapata aislada_CORREGIDA_FASE2.xlsx`, documento `CAMBIOS_ZAPATA_FASE2.md` y commit `9915e368dea08b32ec8a75cf7c80e8bd1cf67a64`. Repositorio independiente `victordavilavargas-collab/Hojas-De-Calculo`, rama `main`; origin verificado y pull --ff-only realizado antes de editar. El repositorio CSI padre permanece sin cambios.

Se corrigieron las seis observaciones específicas de Fase 3. Se revisaron fórmulas y consumidores del XLSX real; el informe previo no sustituyó esa revisión. La edición, recálculo, guardado y reapertura se hicieron con Microsoft Excel COM 16.0. Python/openpyxl se usó para lectura, manifiesto JSON y comparación independiente, sin regrabar el XLSX. Se conservó el caso actual: no se optimizaron dimensiones, qadm, barras, separaciones ni cargas para obtener CUMPLE.

## 1. Entregables y preservación

| Archivo | Función | SHA256 verificado |
|---|---|---|
| `trabajo_codex/CAMBIOS_ZAPATA_FASE1.md` | Original / Fase 1 / Fase 2 intacto | `24e6f0077e2f8ba51c8d80b51056834aa8400998d2532d9b83693d426eddbf3d` |
| `trabajo_codex/CAMBIOS_ZAPATA_FASE2.md` | Original / Fase 1 / Fase 2 intacto | `18aad8f776b00fde74027dca632bb60b503cbd6e4c24a366803ecaa87a5612a1` |
| `trabajo_codex/Diseño de zapata aislada.xlsx` | Original / Fase 1 / Fase 2 intacto | `24f60a8b5a8b170de9ef528cc7f96120f0b5c651ccdad33acf8a6562965a7060` |
| `trabajo_codex/Diseño de zapata aislada_CORREGIDA_FASE1.xlsx` | Original / Fase 1 / Fase 2 intacto | `8d66b5590812704f8bdd1173b5583a4bcaaf00d500c1d854d00c42051192ded5` |
| `trabajo_codex/Diseño de zapata aislada_CORREGIDA_FASE2.xlsx` | Original / Fase 1 / Fase 2 intacto | `8d92bc7d557dcbb691b1d538e2dd3f96d830e54f69bb1f407a402637b3e2bd01` |
| `trabajo_codex/Diseño de zapata aislada_CORREGIDA_FASE3.xlsx` | Nuevo entregable Fase 3 | `7074baa04d42f3637931dc92594fb0c314405ad015c4d37c8dcf21e81eaab433` |

Segundo entregable: `trabajo_codex/CAMBIOS_ZAPATA_FASE3.md`, este registro. Únicamente estos dos archivos se incluyen en el commit y push. Ensayos, scripts, PDFs/capturas y resultados JSON auxiliares quedan fuera del commit.

Se compararon exactamente `INGRESO_DATOS!C14:C152` y `CARGAS!C7:C38` contra Fase 2, incluyendo fórmulas de entradas y componentes sísmicas. Permanecen Bx=By=3.75 m, h=0.50 m, qadm=8.5 tf/m² y fy de resistencia=4200 kgf/cm². La selección inicial OTRO conserva la interpretación nominal anterior mientras no se declare el grado mediante certificado. El selector de pico inicia NO; el mínimo inicia UNA CARA/INFERIOR; eta X/Y=.50 es una hipótesis visible y su validación/referencia quedan vacías. Los conteos superiores adicionales quedan vacíos: no se inventó un plano ni EMS.

## 2. Normas y unidades

- [NTE E.060, texto oficial DS 010-2009-VIVIENDA](https://cdn.www.gob.pe/uploads/document/file/2686419/E.060%20Concreto%20Armado%20DS%20N%C2%B0%20010-2009.pdf): 9.7.2/3, 10.5.4, 11.12.6 y 13.5.3, 15.4.4, con los restantes controles E.060 de Fase 2 preservados.
- [NTE E.050, texto oficial RM 406-2018-VIVIENDA](https://cdn.www.gob.pe/uploads/document/file/2366655/54%20E.050%20SUELOS%20Y%20CIMENTACIONES%20RM%20N%C2%B0%20406-2018-VIVIENDA.pdf): artículo 28, área efectiva por excentricidad; se preserva el control de cargas inclinadas/EMS.
- [Catálogo oficial del Reglamento Nacional de Edificaciones](https://www.gob.pe/institucion/vivienda/informes-publicaciones/2309793-reglamento-nacional-de-edificaciones-rne). No se sustituyen los textos peruanos por un ACI posterior.
- [Ficha primaria del fabricante, barras ASTM A615 Grado 60 / NTP Grado 420](https://acerosarequipa.com/sites/default/files/fichas/2020-02/AA_FierroCorrugado_A615.pdf): ayuda a identificar grado nominal; no sustituye el certificado del material del proyecto ni la norma estructural.

Todas las entradas dimensionales siguen en kgf, tf, m y cm; esfuerzos ingresados en kgf/cm², presiones en tf/m² y As en cm². MPa/mm aparecen solo como conversiones internas o diagnósticos normativos. `1 kgf/cm²=0.0980665 MPa`: fy=4200 corresponde exactamente a 411.8793 MPa; 420 MPa nominales corresponden a 4282.809095 kgf/cm². Las fórmulas COM/OOXML usan nombres ingleses estándar y Excel español las localiza. Sin macros, vínculos externos, _xlfn/_xludf ni funciones posteriores a Excel 2016.

## 3. Acero mínimo total y caras — E.060 10.5.4 / 9.7

**Antes:** `FLEXION_ACERO!G5:G8` imponía rho_eff completo en inferior y también en superior si existía demanda; podía duplicar automáticamente el mínimo total de 9.7.

**Ahora:** rho_total=MAX(rho_nominal_norma,rho_usuario). Con b=100 cm para resultados por metro, As_min_total=rho_total*b*h_cm. UNA CARA asigna el mínimo total completo a la cara explícitamente elegida; la otra cara recibe la demanda de flexión correspondiente. DOS CARAS necesita fracción f explícita: rho_asignada_inf=f*rho_total y rho_asignada_sup=(1−f)*rho_total. Se exige 0<f<1; falta de f produce REQUIERE DATOS, sin operaciones sobre textos/vacíos.

Para DOS CARAS, si una cara está traccionada por el momento **global o regional firmado**, su rho mínima de cara se eleva a MAX(rho_asignada,0.0012). Si ambas caras tienen tracción en distintos lados, ambas reciben el piso .0012: la suma puede superar legítimamente el mínimo total, sin que se haya impuesto rho_total dos veces. `As_req_cara=MAX(As_flex_cara,As_min_cara)`; se mantiene el límite de flexión simple de Fase 2.

`ACERO_DETALLADO!B262:F263` comprueba además **As real inferior+As real superior≥As_min_total** en cada dirección, usando conteos declarados y áreas comerciales de barras. El cumplimiento del mínimo total no sustituye los mínimos/áreas exigidos en cada cara o región; los controles de distribución y acero local deben cumplir también. `B264` gobierna `RESUMEN!B104`; `FLEXION_ACERO!B34:B37`, G/H5:8 y nuevas tablas regionales muestran el reparto y los pisos. Las guardas no convierten un dato faltante en cero.

Prueba independiente: grado420, h=50 cm, rho_total=.0018, f=2/3, demanda pequeña: 6+3=9 cm²/m, frente al mínimo total9; **no9+9**. En el caso con tracción superior y DOS CARAS, esa cara exige6 cm²/m=.0012×100×50. Se verificaron solo positivo, cara negativa aislada, inversión por lados y acero repartido real.


## 4. Transferencia gamma_f Mu firmada y equilibrio — 11.12.6 / 13.5.3

**Antes:** las filas locales INF/SUP X e INF/SUP Y usaban ambas el mismo `ABS(gamma_f Mu)` completo y sumaban `ABS(gamma_f Mu)+Mu_global_por_m*ancho_franja`. Se elimina ese diseño duplicado de caras y ese incremento de momento sobre el campo global.

**Ahora:** cuatro lados X−, X+, Y−, Y+ en `FLEXION_ACERO!B52:L55`, resumen de lados en `ACERO_DETALLADO!A86:J89`, y 16 filas por lado/región/cara en `A232:Q247`. Se mantienen los momentos globales firmados integrados desde la presión física en `DIAGRAMAS_X/Y!B7:B8`, sin alterar cargas ni la solución de presión. La transferencia crítica se toma de `PUNZONAMIENTO!B47:B48`, incluidos sus momentos de reacción dentro del perímetro.

Convención de mano derecha: para barras X, Gamma=gamma_fy*My_crit; para barras Y, Gamma=−gamma_fx*Mx_crit. Se conserva el signo antes de decidir la cara traccionada. El signo positivo del momento escalar de voladizo produce tracción inferior y el negativo, superior. ABS se usa solo posteriormente para tolerancias/comprobaciones de magnitud, no para escoger una capa.

Se adopta un **modelo explícito de reasignación estática** con eta por dirección:

```text
T− = −eta*Gamma;      T+ = (1−eta)*Gamma
T+−T− = Gamma
W = ancho transversal total; b = franja c+3h intersectada con la zapata física
m_residual = (M_cara_global−T_lado)/W
M_franja = T_lado + m_residual*b
M_fuera  = m_residual*(W−b)
M_franja + M_fuera = M_cara_global
```

Se comprueba la última identidad en las cuatro caras, el par T+−T− por eje y `gamma_f*Mcrit+(1−gamma_f)*Mcrit=Mcrit`. `FLEXION_ACERO!J52:J55/B57:B60` muestra errores firmados y B61 su estado; `RESUMEN!B107` lo incorpora. Tolerancia absoluta1e−8 tf·m. La integración independiente de la presión verifica también ΣF/ΣMx/ΣMy y los momentos originales de cada voladizo; la reasignación regional conserva cada uno de ellos. No se añade una segunda acción gamma_fMu. El canal gamma_v del punzonamiento permanece íntegro y no se rediseña como otra carga global.

La cara de **T aislado** y la del **momento resultante en franja** se muestran separadamente: el momento global puede dominar y conservar tracción inferior aunque T aislado sea negativo. El dimensionamiento usa el signo del resultante regional. Se controlan también las regiones fuera de franja; no se oculta la eventual tracción exterior por cancelación o redistribución.

Para cada región/cara se calcula As de flexión, mínimo de cara, As requerido, N real, As real=N×área de barra, longitud disponible **por lado**, ld normativo de esa capa, geometría y estado. La franja usa los conteos/longitudes locales existentes; fuera usa N_total_capa−N_franja para barras rectas continuas. Se rechazan conteos fraccionarios, negativos o mayores que el total, acero insuficiente, barras que no caben, límites de flexión y desarrollo insuficiente. No se acredita una cara superior sin demanda ni mínimo asignado. Los controles posteriores no pueden dar CUMPLE si falta un dato aplicable.

**Alcance de la hipótesis:** E.060 prescribe la fracción gamma_f y la zona de transferencia; no prescribe eta=.50 como solución única de una placa. El reparto estático aquí no demuestra compatibilidad de deformaciones, rigidez fisurada ni solución elástica completa. Eta=.50 es un valor visible editable, no un resultado de análisis. Para obtener CUMPLE local se necesitan `inp_repartition_ok=SI`, referencia en `inp_repartition_ref` y detalle local confirmado. En el entregable esos datos permanecen vacíos. La referencia debe sustentar la compatibilidad, eta y el plano con barras continuas y localizadas en las zonas que se acreditan; una marca SI no genera ese análisis. No se certifica automáticamente la solución de placa.

**Conservadurismo residual sin duplicar Mu:** As_total por capa/dirección=MAX(As_global_por_m×W, MAX(As_req_franja−,As_req_franja+)+MAX(As_req_fuera−,As_req_fuera+)). Es una envolvente de acero para barras continuas, no una suma global+Gamma de momentos. El piso de mínimo del usuario y las demás restricciones conservadoras se mantienen visibles.


### Comprobación numérica del intercambio de lado/cara

| Caso | Gamma X tf·m | T X− tf·m | T X+ tf·m | Mu franja X− tf·m | Mu franja X+ tf·m | Cara X− / X+ | Local | Global |
|---|---:|---:|---:|---:|---:|---|---|---|
| F3-local-My-positivo | 11.97439713 | -5.987198567 | 5.987198567 | -7.023223599 | 7.40229471 | SUPERIOR / INFERIOR | CUMPLE | REQUIERE ANÁLISIS ESPECIAL |
| F3-local-My-negativo | -11.97439713 | 5.987198567 | -5.987198567 | 7.40229471 | -7.023223599 | INFERIOR / SUPERIOR | CUMPLE | REQUIERE ANÁLISIS ESPECIAL |
| F3-reparto-asimetrico | 11.97439713 | -3.59231914 | 8.382077994 | -5.841749749 | 8.583768561 | SUPERIOR / INFERIOR | CUMPLE | REQUIERE ANÁLISIS ESPECIAL |

Los valores se contrastaron con integración de Gauss de presión, momentos críticos y As resuelta por bisección independiente. Con My=+20tf·m, GammaX≈11.97439713tf·m y eta=.5: T−≈−5.987198567, T+≈+5.987198567. El cambio a My=−20 intercambia superior/inferior y lado−/+; no conserva el mismo ABS en dos parrillas. Mx solamente usa la convención Y firmada correspondiente; los casos biaxiales verifican ambos pares. CUMPLE del módulo local no convierte la conexión vertical P–Mx–My en un análisis implementado.

## 5. Distribución superior e inferior — E.060 15.4.4

Se aplica la misma función de distribución a las cuatro parrillas: inferior X/Y y superior X/Y. Beta=L/B≥1; gamma_s=2/(beta+1). En dirección larga/cuadrada el armado es uniforme en todo el ancho. En dirección corta, As_central=gamma_s×As_total en una franja de ancho B centrada en columna y As_exterior=(1−gamma_s)×As_total, uniformemente en el resto. Se usan las nuevas demandas totales de la capa, incluidas las regiones locales firmadas.

Bloques inferiores `ACERO_DETALLADO!B28:B44/B49:B65`; superiores `B181:B197/B203:B219`. Zonas físicas inferiores B148:B156/B160:B168 y superiores B282:B290/B294:B302. Se comprueban franja contenida, ambos anchos exteriores, Ncentral, Next_total=Next−+Next+, acero real por zona, As por metro, separaciones central/exterior, longitud que ocupa (N−1)s, recubrimiento y diámetro real. Los casos rectangulares biaxiales ejercitan **las dos parrillas superiores**, incluida la dirección corta, en ambas orientaciones: beta1.5 y gamma_s=.8; 80% central y20% exterior.

Las nuevas entradas superiores C177:C188 son aplicables solo cuando As_total_superior>0 por flexión local/global o por mínimo deliberadamente asignado. Si As_total=0, distribución, geometría y desarrollo de esa capa devuelven NO APLICA; no se requieren conteos ni terminación superior. El caso F3-sin-demanda-superior deja estos datos vacíos y cumple el dominio implementado. Se detectaron conteo superior90 que no cabe y separación50cm excesiva mediante NO CUMPLE del módulo. No se exige el armado superior solo por ABS del momento transferido.

La comprobación de ubicación por zonas es un control de factibilidad de franjas/zonas, conteos y separaciones; no genera coordenadas individuales de todas las barras, ganchos o cortes. La coincidencia exacta de los conteos locales con la franja c+3h y del resto con ambos sectores exteriores requiere el plano/referencia validado. No se acredita por duplicación de una misma barra como dos áreas independientes.


## 6. qadm, grado y pasivo

**E.050 artículo28:** qmax/qmin físicos, cuatro esquinas, campo lineal, contacto, equilibrio y gráficos permanecen. B′=Bx−2|ex|, L′=By−2|ey|, Aef=B′L′ y qef=Q/Aef se preservan como control de excentricidad; B35 gobierna según la base BRUTA/NETA declarada y datos EMS. `PRESIONES_SERVICIO!D13` pasa a control adicional **optativo**: inp_peak=NO→NO APLICA; SI sin referencia→REQUIERE DATOS; SI con fuente válida compara pico físico/qadm. B57 muestra diagnóstico incluso con NO, B58 selector/fuente; RESUMEN B73 no convierte el diagnóstico en exigencia universal. `D12=inp_qadm` se conserva como dato numérico.

Prueba independiente Q=80tf, ex=.25m, Bx=By=3.75m: Aef=12.1875m², qef=6.564102564tf/m²<qadm7<qmax7.964444444tf/m², contacto completo. Con NO el caso completo cumple; con SI y fuente EMS produce NO CUMPLE; sin fuente REQUIERE DATOS. Cambiar el selector no cambia el campo físico.

**Grado 420:** `INGRESO_DATOS!C160` declara NTP GRADO420/ASTM G60 u OTRO, independientemente de fy de resistencia C15. Para grado420 y barras corrugadas, el nominal normativo es420MPa y rho_norm=.0018; OTRO usa el nominal kgf/cm² explícito C161 convertido internamente. C161 inicia =inp_fy, sin inferir que4200kgf/cm² sea420MPa. `FLEXION_ACERO!B31:B33` muestra nominal, conversión y diferencia respecto de resistencia; no reemplaza fy ni modifica resistencia de flexión/desarrollo. Si fy calculado es menor que nominal aparece aviso; si es mayor pide verificar certificado. Ambos requieren respaldo de la selección de grado. El umbral420 se aplica al nominal exacto, evitando que redondeo binario cambie la clasificación. Los mínimos para otros tipos de refuerzo de9.7 se conservan; fuera del dominio de barras corrugadas/concreto normal permanece el estado correspondiente.

**Pasivo:** se adopta la solución A solicitada: “RESISTENCIA PASIVA CONSIDERADA SOLO EN DESLIZAMIENTO”. Nota visible en INGRESO_DATOS E128 y PRESIONES_SERVICIO B59/D59. Se mantienen fuente/dato del pasivo y el FS de deslizamiento existente. Las fórmulas de volteo respecto a los cuatro bordes no reciben pasivo. No se inventa altura/brazo ni se implementa solución B. Prueba: Rpasivo30tf con H10tf incrementa FSdeslizamiento de7.00722225 a10.00722225; los momentos y FS de volteo permanecen idénticos (bordeX−=29.196759375). El brazo pasivo y la prueba17 condicional no aplican porque B no se implementó.


## 7. Inventario y compatibilidad

| Hoja | Tamaño F2 → F3 | Fórmulas F2 → F3 | Gráficos |
|---|---|---:|---:|
| INGRESO_DATOS | 152×8 → 188×8 | 4 → 9 | 4 |
| BARRAS_PERU | 21×10 → 21×10 | 0 → 0 | 0 |
| CARGAS | 38×8 → 38×8 | 14 → 14 | 0 |
| GEOMETRIA | 2627×11 → 2627×11 | 23424 → 23424 | 0 |
| RESULTANTE | 12×14 → 12×14 | 29 → 29 | 0 |
| PRESIONES_SERVICIO | 55×8 → 59×8 | 53 → 55 | 0 |
| PRESIONES_ULTIMAS | 25×8 → 25×8 | 15 → 15 | 0 |
| DIAGRAMAS_X | 79×12 → 79×12 | 599 → 599 | 3 |
| DIAGRAMAS_Y | 79×12 → 79×12 | 599 → 599 | 3 |
| PUNZONAMIENTO | 66×6 → 66×6 | 58 → 58 | 0 |
| CORTANTE_UNIDIRECCIONAL | 23×10 → 23×10 | 47 → 47 | 0 |
| FLEXION_ACERO | 28×10 → 61×12 | 37 → 94 | 0 |
| ACERO_DETALLADO | 173×10 → 302×17 | 212 → 523 | 0 |
| GRAFICOS | 133×26 → 133×26 | 344 → 344 | 14 |
| RESUMEN | 99×8 → 109×8 | 136 → 142 | 0 |

Se preservaron las 15 hojas y su orden, los 24 gráficos con tipos/referencias/series, y los 324 nombres con destinos; total final368. Se comprobaron validaciones por cobertura celda a celda: Excel puede reunir listas iguales en un sqref mayor, sin retirar validación previa. Se conservaron reglas condicionales, comentarios, inmovilización, áreas/márgenes/configuración de impresión y anchos anteriores. Solo se amplían columnas vacías K:L de FLEXION y K:Q de ACERO para los bloques nuevos; se ajustan alturas/advertencias y se desplaza el gráfico bajo nuevas entradas sin cambiar sus series. Los estados adicionales usan coincidencia exacta y alimentan RESUMEN; los contadores no se incluyen en sí mismos.

En FLEXION_ACERO, el PageSetup no serializado en Fase2 fue explicitado por Excel como portrait/A4/DPI0 al guardar el ajuste de altura; se verificaron esos valores predeterminados y área/márgenes intactos. No se cambió una configuración explícita del usuario. La hoja conserva su área de impresión vacía; las áreas temporales PDF no se guardaron.

## 8. Pruebas independientes y Excel nativo

**101 escenarios**: 73 de regresión Fase2 más28 nuevos Fase3. **40626 comprobaciones**, **0 fallos**, **0 errores de fórmula**, **0 referencias circulares**. Las pruebas cambian datos exclusivamente en copia descartable y no se guardan en el entregable. El libro final se abrió normal en Excel16.0, CalculateFullRebuild, guardado, cierre y reapertura; se contrastó persistencia de entradas y resultados. Se repitió ese cierre después de ajustar solo alturas de advertencias. Se revisaron36 vistas nativas que cubren15 hojas y los24 gráficos comparados con Fase2; exportaciones auxiliares solo lectura, sin alterar áreas de impresión finales.

La comprobación numérica reconstruye desde entradas las acciones trasladadas, presiones/cargas propias, Aef/qef, cuatro esquinas y equilibrio vectorial por Gauss de orden4; momentos de cara por integración de voladizos; As por bisección de capacidad (independiente de la raíz de Excel); mínimos totales/repartidos/.0012; punzonamiento en SI y esfuerzos simultáneos, J/gamma/reacción y momentos críticos; pares firmados y franja/fuera; conteos/áreas y longitudes por lado; distribución en ambas caras/direcciones; desarrollo en MPa/mm; aplastamiento/interfase y momentos/FS respecto a bordes. Se seleccionaron estados esperados antes de comparar. Se verificaron hashes, cambios permitidos, compatibilidad y persistencia, además de los valores mecánicos.

Tolerancia numérica independiente: math.isclose(abs_tol=1e−8,rel_tol=1e−8), en unidades de cada resultado. Error local de equilibrio≤1e−8tf·m. Signo/tracción se decide después de una tolerancia de ruido1e−6tf·m; no se elimina un momento negativo de magnitud significativa. Las comprobaciones de geometría no permiten que pegar texto, barras inexistentes o números inválidos genere CUMPLE.

### Matriz de los28 casos nuevos

| Caso | M franja X− / X+ tf·m | M franja Y− / Y+ tf·m | As min infX / supX cm²/m | Local | SupX / SupY | Estado global | Errores |
|---|---|---|---|---|---|---|---:|
| F3-minimo-solo-inferior | 1.895355556 / 1.895355556 | 1.895355556 / 1.895355556 | 10 / 0 | NO APLICA | NO APLICA / NO APLICA | CUMPLE | 0 |
| F3-minimo-repartido | 1.895355556 / 1.895355556 | 1.895355556 / 1.895355556 | 6 / 3 | NO APLICA | CUMPLE / CUMPLE | CUMPLE | 0 |
| F3-local-My-positivo | -7.023223599 / 7.40229471 | 0.1895355556 / 0.1895355556 | 10 / 0 | CUMPLE | CUMPLE / NO APLICA | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-local-My-negativo | 7.40229471 / -7.023223599 | 0.1895355556 / 0.1895355556 | 10 / 0 | CUMPLE | CUMPLE / NO APLICA | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-local-Mx-positivo | 0.1895355556 / 0.1895355556 | 7.40229471 / -7.023223599 | 10 / 0 | CUMPLE | NO APLICA / CUMPLE | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-local-Mx-negativo | 0.1895355556 / 0.1895355556 | -7.023223599 / 7.40229471 | 10 / 0 | CUMPLE | NO APLICA / CUMPLE | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-local-biaxial | -7.023223599 / 7.40229471 | 5.599104922 / -5.220033811 | 10 / 0 | CUMPLE | CUMPLE / CUMPLE | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-superior-rho-0012 | -7.023223599 / 7.40229471 | 0.1895355556 / 0.1895355556 | 6 / 6 | CUMPLE | CUMPLE / CUMPLE | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-inversion-ambas-caras | 7.40229471 / -7.023223599 | 7.40229471 / -7.023223599 | 6 / 6 | CUMPLE | CUMPLE / CUMPLE | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-solo-negativo-cara | (vacía) / (vacía) | (vacía) / (vacía) | 0 / 10 | FUERA DEL ALCANCE IMPLEMENTADO | CUMPLE / CUMPLE | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| F3-rectangular-superior-X-larga | -7.391986017 / 7.98344898 | 5.246983557 / -5.009131706 | 10 / 0 | CUMPLE | CUMPLE / CUMPLE | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-rectangular-superior-Y-larga | -5.009131706 / 5.246983557 | 7.98344898 / -7.391986017 | 10 / 0 | CUMPLE | CUMPLE / CUMPLE | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-area-cumple-pico-no-selector-NO | 28.26733276 / 28.26733276 | 28.26733276 / 28.26733276 | 10 / 0 | NO APLICA | NO APLICA / NO APLICA | CUMPLE | 0 |
| F3-area-cumple-pico-no-selector-SI | 28.26733276 / 28.26733276 | 28.26733276 / 28.26733276 | 10 / 0 | NO APLICA | NO APLICA / NO APLICA | NO CUMPLE | 0 |
| F3-pico-SI-sin-fuente | 28.26733276 / 28.26733276 | 28.26733276 / 28.26733276 | 10 / 0 | NO APLICA | NO APLICA / NO APLICA | REQUIERE DATOS | 0 |
| F3-grado420-fy4200 | 1.895355556 / 1.895355556 | 1.895355556 / 1.895355556 | 9 / 0 | NO APLICA | NO APLICA / NO APLICA | CUMPLE | 0 |
| F3-otro-fy-menor420 | 1.895355556 / 1.895355556 | 1.895355556 / 1.895355556 | 10 / 0 | NO APLICA | NO APLICA / NO APLICA | CUMPLE | 0 |
| F3-otro-fy-nominal420 | 1.895355556 / 1.895355556 | 1.895355556 / 1.895355556 | 9 / 0 | NO APLICA | NO APLICA / NO APLICA | CUMPLE | 0 |
| F3-pasivo-NO | 28.26733276 / 28.26733276 | 28.26733276 / 28.26733276 | 10 / 0 | NO APLICA | NO APLICA / NO APLICA | CUMPLE | 0 |
| F3-pasivo-solo-deslizamiento | 28.26733276 / 28.26733276 | 28.26733276 / 28.26733276 | 10 / 0 | NO APLICA | NO APLICA / NO APLICA | CUMPLE | 0 |
| F3-sin-demanda-superior | 1.895355556 / 1.895355556 | 1.895355556 / 1.895355556 | 10 / 0 | NO APLICA | NO APLICA / NO APLICA | CUMPLE | 0 |
| F3-reparto-sin-validacion | -7.023223599 / 7.40229471 | 0.1895355556 / 0.1895355556 | 10 / 0 | REQUIERE DATOS | CUMPLE / NO APLICA | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-reparto-asimetrico | -5.841749749 / 8.583768561 | 0.1895355556 / 0.1895355556 | 10 / 0 | CUMPLE | CUMPLE / NO APLICA | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-eta-invalida | (vacía) / (vacía) | (vacía) / (vacía) | 10 / 0 | DATOS INVÁLIDOS | CUMPLE / NO APLICA | DATOS INVÁLIDOS | 0 |
| F3-minimo-repartido-sin-fraccion | 1.895355556 / 1.895355556 | 1.895355556 / 1.895355556 | (vacía) / (vacía) | NO APLICA | REQUIERE DATOS / REQUIERE DATOS | REQUIERE DATOS | 0 |
| F3-grado-nominal-texto | 1.895355556 / 1.895355556 | 1.895355556 / 1.895355556 | (vacía) / (vacía) | NO APLICA | REQUIERE DATOS / REQUIERE DATOS | DATOS INVÁLIDOS | 0 |
| F3-superior-conteo-imposible | -7.023223599 / 7.40229471 | 0.1895355556 / 0.1895355556 | 10 / 0 | NO CUMPLE | NO CUMPLE / NO APLICA | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-superior-separacion-excesiva | -7.023223599 / 7.40229471 | 0.1895355556 / 0.1895355556 | 10 / 0 | CUMPLE | NO CUMPLE / NO APLICA | REQUIERE ANÁLISIS ESPECIAL | 0 |

Los28 casos cubren todos los16 ensayos obligatorios aplicables, con pares de signo para Mx/My, intercambio de lados/capas, biaxial, eta asimétrica/inválida, superior corto en ambas orientaciones, grado nominal, qef/pico/selectores/fuente y pasivo. El caso negativo aislado global está próximo a borde: verifica la regla de cara/mínimo, y conserva FUERA DEL ALCANCE IMPLEMENTADO del perímetro interior. Los casos locales con momentos conservan REQUIERE ANÁLISIS ESPECIAL global por conexión P–M–M aunque sus módulos locales/distribución cumplan. No se modificó un estado de alcance para hacerlos CUMPLE.

### Regresión completa: entradas originales y estados físicos

| Caso | qmax servicio tf/m² | Aef m² | Vu punz tf | Estado global | Errores |
|---|---:|---:|---:|---|---:|
| base-preservada | 11.15269476 | 14.02883707 | 142.1421519 | NO CUMPLE | 0 |
| cuadrada-centrada-completa | 11.07314133 | 14.0625 | 142.251133 | CUMPLE | 0 |
| rectangular-X-larga | 11.37202222 | 13.5 | 141.9640968 | CUMPLE | 0 |
| rectangular-Y-larga | 11.37202222 | 13.5 | 141.9640968 | CUMPLE | 0 |
| columna-rectangular | 11.07314133 | 14.0625 | 140.859796 | NO CUMPLE | 0 |
| columna-excentrica-X | 14.36083111 | 12.31730446 | 141.581382 | CUMPLE | 0 |
| columna-excentrica-Y | 14.36083111 | 12.31730446 | 141.581382 | CUMPLE | 0 |
| excentricidad-biaxial | 13.59808708 | 13.01377863 | 142.1076976 | CUMPLE | 0 |
| momento-Mx | 11.07314133 | 14.0625 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| momento-My | 11.07314133 | 14.0625 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| momento-biaxial | 11.07314133 | 14.0625 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| signos-inversos | 11.07314133 | 14.0625 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| contacto-parcial-ultimo | 11.15269476 | 14.02883707 | (vacía) | REQUIERE ANÁLISIS ESPECIAL | 0 |
| contacto-parcial-servicio | 31.55314133 | 6.58062535 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| levantamiento | -10.2426688 | (vacía) | (vacía) | REQUIERE ANÁLISIS ESPECIAL | 0 |
| P-cero | 3.979553422 | 13.96699378 | (vacía) | REQUIERE ANÁLISIS ESPECIAL | 0 |
| h-insuficiente | 10.62469476 | 14.02715228 | 145.4987314 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| separacion-excesiva | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| minimo-gobernante | 11.07314133 | 14.0625 | 9.538093936 | CUMPLE | 0 |
| cara-X-izquierda | 11.07314133 | 14.0625 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| cara-X-derecha | 11.07314133 | 14.0625 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| transferencia-biaxial | 11.07314133 | 14.0625 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| area-efectiva-E050 | 13.91758578 | 12.88313003 | 142.251133 | CUMPLE | 0 |
| dimension-efectiva-X-negativa | 56.64645476 | (vacía) | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| dimension-efectiva-Y-negativa | 56.60160356 | (vacía) | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| sismo-opciones-apagadas | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| sismo-opciones-activadas | 10.7101174 | 14.03448848 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| sismo-sin-componentes | (vacía) | (vacía) | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| reduccion-no-sismica | (vacía) | (vacía) | 142.251133 | DATOS INVÁLIDOS | 0 |
| incremento-no-temporal | (vacía) | (vacía) | 142.251133 | DATOS INVÁLIDOS | 0 |
| barra-inexistente | (vacía) | (vacía) | (vacía) | DATOS INVÁLIDOS | 0 |
| dimension-cero | (vacía) | (vacía) | (vacía) | DATOS INVÁLIDOS | 0 |
| dimension-negativa | (vacía) | (vacía) | (vacía) | DATOS INVÁLIDOS | 0 |
| columna-parcialmente-fuera | (vacía) | (vacía) | (vacía) | DATOS INVÁLIDOS | 0 |
| columna-fuera | (vacía) | (vacía) | (vacía) | DATOS INVÁLIDOS | 0 |
| separacion-cero | 11.15269476 | 14.02883707 | (vacía) | DATOS INVÁLIDOS | 0 |
| fy-invalido | (vacía) | (vacía) | (vacía) | DATOS INVÁLIDOS | 0 |
| fc-invalido | (vacía) | (vacía) | (vacía) | DATOS INVÁLIDOS | 0 |
| phi-flexion-invalido | 11.15269476 | 14.02883707 | (vacía) | DATOS INVÁLIDOS | 0 |
| phi-cortante-invalido | 11.15269476 | 14.02883707 | (vacía) | DATOS INVÁLIDOS | 0 |
| phi-punzonamiento-invalido | 11.15269476 | 14.02883707 | (vacía) | DATOS INVÁLIDOS | 0 |
| recubrimiento-excesivo | 11.15269476 | 14.02883707 | (vacía) | DATOS INVÁLIDOS | 0 |
| dimensiones-texto | (vacía) | (vacía) | (vacía) | DATOS INVÁLIDOS | 0 |
| cargas-texto | 11.15269476 | 14.02883707 | (vacía) | DATOS INVÁLIDOS | 0 |
| fy-mayor-420MPa | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| rho-usuario-menor-norma | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| desarrollo-insuficiente | 56.89432216 | 1.941987159 | 99.71413636 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| gancho-inferior | 11.15269476 | 14.02883707 | 142.251133 | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| falta-recubrimiento-lateral | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| local-sin-acero | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| interfase-minimo-insuficiente | 11.07314133 | 14.0625 | 142.251133 | NO CUMPLE | 0 |
| interfase-anclaje-insuficiente | 11.07314133 | 14.0625 | 142.251133 | NO CUMPLE | 0 |
| pasivo-datos-faltantes | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| qadm-neta | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| qadm-neta-sin-sigma0 | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| borde-bloqueado | 11.15269476 | 14.02883707 | (vacía) | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| esquina-bloqueada | 11.15269476 | 14.02883707 | (vacía) | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| perimetro-cerrado-pero-filtro-conservador | 27.22053134 | 7.239710913 | (vacía) | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| concreto-liviano | 11.15269476 | 14.02883707 | (vacía) | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| inversion-neta-con-contacto-completo | 11.07314133 | 14.0625 | 28.61428181 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| conteo-central-no-cabe | 11.07314133 | 14.0625 | 142.251133 | NO CUMPLE | 0 |
| acero-exterior-todo-un-lado | 11.37202222 | 13.5 | 141.9640968 | NO CUMPLE | 0 |
| anclaje-negativo | 11.07314133 | 14.0625 | 142.251133 | DATOS INVÁLIDOS | 0 |
| fc-menor-17MPa | 11.07314133 | 14.0625 | 142.251133 | NO CUMPLE | 0 |
| fc-columna-menor-17MPa | 11.07314133 | 14.0625 | 142.251133 | NO CUMPLE | 0 |
| recubrimiento-superior-insuficiente | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| recubrimiento-superior-no-aplica | 11.07314133 | 14.0625 | 142.251133 | CUMPLE | 0 |
| exposicion-superior-faltante | 11.15269476 | 14.02883707 | 142.251133 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| malla-fy-menor-420MPa | 11.15269476 | 14.02883707 | (vacía) | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| malla-fy-mayor-420MPa | 11.15269476 | 14.02883707 | (vacía) | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| barra-lisa | 11.15269476 | 14.02883707 | (vacía) | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| columna-excentrica-sin-terminacion-superior | 12.45038447 | 13.47948322 | 142.1664826 | CUMPLE | 0 |
| columna-excentrica-gancho-superior | 12.45038447 | 13.47948322 | 142.1664826 | CUMPLE | 0 |
| F3-minimo-solo-inferior | 4.611111111 | 14.0625 | 9.538093936 | CUMPLE | 0 |
| F3-minimo-repartido | 4.611111111 | 14.0625 | 9.530786638 | CUMPLE | 0 |
| F3-local-My-positivo | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-local-My-negativo | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-local-Mx-positivo | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-local-Mx-negativo | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-local-biaxial | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-superior-rho-0012 | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-inversion-ambas-caras | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-solo-negativo-cara | 11.01688889 | 13.0820122 | (vacía) | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| F3-rectangular-superior-X-larga | 9.140740741 | 13.5 | 0.951884785 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-rectangular-superior-Y-larga | 9.140740741 | 13.5 | 0.951884785 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-area-cumple-pico-no-selector-NO | 7.964444444 | 12.1875 | 142.251133 | CUMPLE | 0 |
| F3-area-cumple-pico-no-selector-SI | 7.964444444 | 12.1875 | 142.251133 | NO CUMPLE | 0 |
| F3-pico-SI-sin-fuente | 7.964444444 | 12.1875 | 142.251133 | REQUIERE DATOS | 0 |
| F3-grado420-fy4200 | 4.611111111 | 14.0625 | 9.538093936 | CUMPLE | 0 |
| F3-otro-fy-menor420 | 4.611111111 | 14.0625 | 9.538093936 | CUMPLE | 0 |
| F3-otro-fy-nominal420 | 4.611111111 | 14.0625 | 9.538093936 | CUMPLE | 0 |
| F3-pasivo-NO | 12.21091911 | 13.58085408 | 142.251133 | CUMPLE | 0 |
| F3-pasivo-solo-deslizamiento | 12.21091911 | 13.58085408 | 142.251133 | CUMPLE | 0 |
| F3-sin-demanda-superior | 4.611111111 | 14.0625 | 9.538093936 | CUMPLE | 0 |
| F3-reparto-sin-validacion | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-reparto-asimetrico | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-eta-invalida | 9.111111111 | 14.0625 | 0.9538093936 | DATOS INVÁLIDOS | 0 |
| F3-minimo-repartido-sin-fraccion | 4.611111111 | 14.0625 | 9.538093936 | REQUIERE DATOS | 0 |
| F3-grado-nominal-texto | 4.611111111 | 14.0625 | 9.538093936 | DATOS INVÁLIDOS | 0 |
| F3-superior-conteo-imposible | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |
| F3-superior-separacion-excesiva | 9.111111111 | 14.0625 | 0.9538093936 | REQUIERE ANÁLISIS ESPECIAL | 0 |

Algunos estados F2 cambian deliberadamente: una excentricidad de columna cuyo resultante local mantiene únicamente tracción inferior ya no exige anclaje superior por ABS de gamma_f. Una ausencia de terminación superior no bloquea una capa NO APLICA. Por otra parte, el incumplimiento del área efectiva, de armado realmente requerido o de conexión pendiente permanece. Los ensayos de contacto parcial/levantamiento/borde y conexión con momentos no se reinterpretan como diseños certificados.

## 9. Caso entregado y límites aún abiertos

| Resultado actual | Valor | Celda |
|---|---:|---|
| qmax físico tf/m² | 11.15269476 | `PRESIONES_SERVICIO!D10` |
| qmin físico tf/m² | 10.99358791 | `PRESIONES_SERVICIO!D11` |
| Pico optativo | NO APLICA | `PRESIONES_SERVICIO!D13` |
| Aef m² | 14.02883707 | `PRESIONES_SERVICIO!B28` |
| qef bruta tf/m² | 11.09971192 | `PRESIONES_SERVICIO!B29` |
| Área efectiva | NO CUMPLE | `PRESIONES_SERVICIO!B35` |
| As req inferior X cm²/m | 10 | `FLEXION_ACERO!H5` |
| As req inferior Y cm²/m | 10.04403194 | `FLEXION_ACERO!H6` |
| Armado local real | REQUIERE DATOS | `ACERO_DETALLADO!B91` |
| Mínimo real total | REQUIERE DATOS | `ACERO_DETALLADO!B264` |
| Distribución superiorX | NO APLICA | `ACERO_DETALLADO!B197` |
| Distribución superiorY | NO APLICA | `ACERO_DETALLADO!B219` |
| Equilibrio local | CUMPLE | `FLEXION_ACERO!B61` |
| Estado global | NO CUMPLE | `RESUMEN!B23` |

El estado actual es **NO CUMPLE** y conserva controles REQUIERE DATOS visibles en RESUMEN. El área efectiva y acero global no cumplen; hay detalle/EMS/conexión no declarado. Equilibrio CUMPLE no demuestra armado suficiente ni análisis de compatibilidad. No se optimizaron datos ni se llenaron faltantes para modificar el resultado.

| Limitación / criterio residual | Tratamiento y alcance |
|---|---|
| Reparto local de placa | Hipótesis estática validable, eta explícita y referencia requerida; falta solución interna de compatibilidad/placa. No se atribuye eta=.5 a E.060. |
| Detalle local/zonas | Conteos/longitudes por lado y factibilidad; el plano externo debe confirmar posiciones individuales, continuidad y pertenencia a cada franja/sector. No genera un plano automático. |
| Contacto parcial / Q≤0 / levantamiento | REQUIERE ANÁLISIS ESPECIAL. No hay solver compresivo equilibrado; q negativa no se recorta a cero. |
| Perímetro BORDE/ESQUINA/proximidad | FUERA DEL ALCANCE IMPLEMENTADO. Falta perímetro abierto con orientación, centroide/J reales y secciones alternativas. Se conserva el filtro interior de Fase2. |
| Conexión columna-zapata P–Mx–My, tracción/torsión y empalmes | REQUIERE ANÁLISIS ESPECIAL según datos aplicables. El acero horizontal local no sustituye análisis de interacción, coordenadas verticales, compatibilidad, torsión ni empalmes. |
| Ganchos, paquetes, cortes, barras no continuas | Fuera del motor implementado: solo barras corrugadas rectas continuas, desarrolladas por ambos lados/capas requeridas. |
| Concreto liviano, lisas/mallas y columna prefabricada | No se certifica resistencia/anclaje de esos dominios; se conservan los estados de alcance existentes aunque9.7 muestre algún mínimo. |
| EMS/qadm BRUTA o NETA/carga inclinada | Requiere referencia y confirmaciones pertinentes; no se inventan parámetros geotécnicos ni qadm. Pico adicional requiere selectorSI y fuente. |
| Material/grado | Selección nominal debe respaldarse con certificado. Fy4200 se conserva; nominal420 y resistencia411.8793MPa se diferencian mediante advertencia. |
| Desarrollo / exposición / recubrimiento | Se conserva Ktr=0 y ld≥30cm sin reducir por exceso; se mantienen factores de desarrollo. Datos de exposición, recubrimiento lateral, epoxi, agregado y terminación deben declararse realmente. |
| Mínimo del usuario/envolvente | MAX(rho_norm,rho_usuario), límites de flexión simple y MAX(global,suma de envolventes regionales) conservadores explícitos. No son duplicación física de cargas. |
| Aplastamiento y junta | Se mantiene factor opcional sqrt(A2/A1)=1 conservador y acero dedicado Avf confirmado; no acredita P–M–M ni usa mu de suelo como mu de concreto. |
| Pasivo/FS/volteo | Pasivo solo en deslizamiento; no se implementa brazo/volteo pasivo. FS y fuente corresponden al criterio declarado del proyecto. |
| Acciones/envolventes externas | No se generan combinaciones E.020/E.030, importación ETABS/SAP, optimización ni solver no lineal. Las acciones son del proyectista. |

Esta fase cierra la corrección de las observaciones dentro del alcance declarado del motor. **La plantilla no se considera terminada ni se certifica un proyecto porque algunos ensayos den CUMPLE.** Los estados, hipótesis y límites anteriores deben acompañar su uso.


## 10. Registro completo de fórmulas/celdas anteriores y nuevas

Comparación directa F2→F3 guardada por Excel. Se agrupan filas consecutivas únicamente si ambos patrones anterior/nuevo se trasladan exactamente con referencias relativas y comparten motivo técnico. Se muestran las fórmulas exactas de la primera celda: cada fila del rango se reconstruye trasladando referencias relativas; nombres/absolutas permanecen. Una celda vacía se distingue de cero. Las unidades y artículos aplicables se identifican en la matriz normativa y en las notas de cada bloque.

928 celdas con cambio de contenido, consolidadas en 735 registros; cero cambios fuera del manifiesto. Los cambios corresponden a las seis observaciones Fase3 y sus consumidores; no a modificación de acciones.

| Hoja | Celda/rango | Anterior | Nueva | Motivo técnico |
|---|---|---|---|---|
| INGRESO_DATOS | `A155` | `(vacía)` | `FASE 3: EMS Y GRADO DECLARADO` | FASE 3: EMS Y GRADO DECLARADO |
| INGRESO_DATOS | `A156` | `(vacía)` | `Control adicional de pico lineal` | NO: diagnóstico; SI requiere fuente explícita. E.050 art.28 gobierna por Aef. |
| INGRESO_DATOS | `A157` | `(vacía)` | `Fuente de control del pico` | EMS/página o criterio del diseñador para comparar qmax con qadm. |
| INGRESO_DATOS | `A160` | `(vacía)` | `Clasificación normativa del acero` | No se infiere desde fy redondeado. No cambia fy de resistencia. |
| INGRESO_DATOS | `A161` | `(vacía)` | `fy nominal declarado si OTRO` | Solo OTRO: dato nominal para 9.7.2; editable. Grado420 usa 420MPa exactos convertidos. |
| INGRESO_DATOS | `A164` | `(vacía)` | `FASE 3: MÍNIMO TOTAL Y REPARTO LOCAL` | FASE 3: MÍNIMO TOTAL Y REPARTO LOCAL |
| INGRESO_DATOS | `A165` | `(vacía)` | `Distribución del mínimo total` | 10.5.4: total según9.7; DOS CARAS exige .0012 en cada cara traccionada. |
| INGRESO_DATOS | `A166` | `(vacía)` | `Cara que recibe mínimo íntegro` | Aplica solamente a UNA CARA. |
| INGRESO_DATOS | `A167` | `(vacía)` | `Fracción mínima asignada inferior` | Solo DOS CARAS: 0<fracción<1; superior=1-fracción. No es un factor de cargas. |
| INGRESO_DATOS | `A170` | `(vacía)` | `Fracción gamma_fMy al lado - X` | Reparto estático elegido: lado -=-eta*gamma_fMy; lado +=(1-eta)*gamma_fMy. Rango0..1. |
| INGRESO_DATOS | `A171` | `(vacía)` | `Fracción gamma_fMx al lado - Y` | La contribución escalar para barras Y es -gamma_fMx: signo global de mano derecha. |
| INGRESO_DATOS | `A172` | `(vacía)` | `Referencia del análisis de reparto` | Validación de redistribución y detalle; eta=.5 es hipótesis visible, no ecuación E.060. |
| INGRESO_DATOS | `A173` | `(vacía)` | `Reparto local validado en análisis` | Debe ser SI con referencia para acreditar la redistribución. No demuestra solución elástica de placa. |
| INGRESO_DATOS | `A176` | `(vacía)` | `FASE 3: DISTRIBUCIÓN SUPERIOR SOLO SI SE REQUIERE` | FASE 3: DISTRIBUCIÓN SUPERIOR SOLO SI SE REQUIERE |
| INGRESO_DATOS | `A177` | `(vacía)` | `Separación central superior X` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A178` | `(vacía)` | `Separación exterior superior X` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A179` | `(vacía)` | `N real superior X central` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A180` | `(vacía)` | `N real superior X exterior total` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A181` | `(vacía)` | `N superior X exterior lado -` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A182` | `(vacía)` | `N superior X exterior lado +` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A183` | `(vacía)` | `Separación central superior Y` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A184` | `(vacía)` | `Separación exterior superior Y` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A185` | `(vacía)` | `N real superior Y central` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A186` | `(vacía)` | `N real superior Y exterior total` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A187` | `(vacía)` | `N superior Y exterior lado -` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `A188` | `(vacía)` | `N superior Y exterior lado +` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B156` | `(vacía)` | `inp_peak` | NO: diagnóstico; SI requiere fuente explícita. E.050 art.28 gobierna por Aef. |
| INGRESO_DATOS | `B157` | `(vacía)` | `inp_peak_ref` | EMS/página o criterio del diseñador para comparar qmax con qadm. |
| INGRESO_DATOS | `B160` | `(vacía)` | `inp_grade` | No se infiere desde fy redondeado. No cambia fy de resistencia. |
| INGRESO_DATOS | `B161` | `(vacía)` | `inp_fy_nom` | Solo OTRO: dato nominal para 9.7.2; editable. Grado420 usa 420MPa exactos convertidos. |
| INGRESO_DATOS | `B165` | `(vacía)` | `inp_min_scheme` | 10.5.4: total según9.7; DOS CARAS exige .0012 en cada cara traccionada. |
| INGRESO_DATOS | `B166` | `(vacía)` | `inp_min_face` | Aplica solamente a UNA CARA. |
| INGRESO_DATOS | `B167` | `(vacía)` | `inp_min_frac` | Solo DOS CARAS: 0<fracción<1; superior=1-fracción. No es un factor de cargas. |
| INGRESO_DATOS | `B170` | `(vacía)` | `inp_eta_x` | Reparto estático elegido: lado -=-eta*gamma_fMy; lado +=(1-eta)*gamma_fMy. Rango0..1. |
| INGRESO_DATOS | `B171` | `(vacía)` | `inp_eta_y` | La contribución escalar para barras Y es -gamma_fMx: signo global de mano derecha. |
| INGRESO_DATOS | `B172` | `(vacía)` | `inp_repartition_ref` | Validación de redistribución y detalle; eta=.5 es hipótesis visible, no ecuación E.060. |
| INGRESO_DATOS | `B173` | `(vacía)` | `inp_repartition_ok` | Debe ser SI con referencia para acreditar la redistribución. No demuestra solución elástica de placa. |
| INGRESO_DATOS | `B177` | `(vacía)` | `inp_sc_sx` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B178` | `(vacía)` | `inp_so_sx` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B179` | `(vacía)` | `inp_nc_sx` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B180` | `(vacía)` | `inp_no_sx` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B181` | `(vacía)` | `inp_no_sx_minus` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B182` | `(vacía)` | `inp_no_sx_plus` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B183` | `(vacía)` | `inp_sc_sy` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B184` | `(vacía)` | `inp_so_sy` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B185` | `(vacía)` | `inp_nc_sy` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B186` | `(vacía)` | `inp_no_sy` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B187` | `(vacía)` | `inp_no_sy_minus` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `B188` | `(vacía)` | `inp_no_sy_plus` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `C156` | `(vacía)` | `NO` | NO: diagnóstico; SI requiere fuente explícita. E.050 art.28 gobierna por Aef. |
| INGRESO_DATOS | `C160` | `(vacía)` | `OTRO` | No se infiere desde fy redondeado. No cambia fy de resistencia. |
| INGRESO_DATOS | `C161` | `(vacía)` | `=inp_fy` | Solo OTRO: dato nominal para 9.7.2; editable. Grado420 usa 420MPa exactos convertidos. |
| INGRESO_DATOS | `C165` | `(vacía)` | `UNA CARA` | 10.5.4: total según9.7; DOS CARAS exige .0012 en cada cara traccionada. |
| INGRESO_DATOS | `C166` | `(vacía)` | `INFERIOR` | Aplica solamente a UNA CARA. |
| INGRESO_DATOS | `C170` | `(vacía)` | `0.5` | Reparto estático elegido: lado -=-eta*gamma_fMy; lado +=(1-eta)*gamma_fMy. Rango0..1. |
| INGRESO_DATOS | `C171` | `(vacía)` | `0.5` | La contribución escalar para barras Y es -gamma_fMx: signo global de mano derecha. |
| INGRESO_DATOS | `C177:C178` | `(vacía)` | `=inp_sep_sup_x` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `C183:C184` | `(vacía)` | `=inp_sep_sup_y` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `D156` | `(vacía)` | `-` | NO: diagnóstico; SI requiere fuente explícita. E.050 art.28 gobierna por Aef. |
| INGRESO_DATOS | `D157` | `(vacía)` | `-` | EMS/página o criterio del diseñador para comparar qmax con qadm. |
| INGRESO_DATOS | `D160` | `(vacía)` | `-` | No se infiere desde fy redondeado. No cambia fy de resistencia. |
| INGRESO_DATOS | `D161` | `(vacía)` | `kgf/cm2` | Solo OTRO: dato nominal para 9.7.2; editable. Grado420 usa 420MPa exactos convertidos. |
| INGRESO_DATOS | `D165` | `(vacía)` | `-` | 10.5.4: total según9.7; DOS CARAS exige .0012 en cada cara traccionada. |
| INGRESO_DATOS | `D166` | `(vacía)` | `-` | Aplica solamente a UNA CARA. |
| INGRESO_DATOS | `D167` | `(vacía)` | `-` | Solo DOS CARAS: 0<fracción<1; superior=1-fracción. No es un factor de cargas. |
| INGRESO_DATOS | `D170` | `(vacía)` | `-` | Reparto estático elegido: lado -=-eta*gamma_fMy; lado +=(1-eta)*gamma_fMy. Rango0..1. |
| INGRESO_DATOS | `D171` | `(vacía)` | `-` | La contribución escalar para barras Y es -gamma_fMx: signo global de mano derecha. |
| INGRESO_DATOS | `D172` | `(vacía)` | `-` | Validación de redistribución y detalle; eta=.5 es hipótesis visible, no ecuación E.060. |
| INGRESO_DATOS | `D173` | `(vacía)` | `-` | Debe ser SI con referencia para acreditar la redistribución. No demuestra solución elástica de placa. |
| INGRESO_DATOS | `D177:D178` | `(vacía)` | `cm` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `D179:D182` | `(vacía)` | `barras` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `D183:D184` | `(vacía)` | `cm` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `D185:D188` | `(vacía)` | `barras` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| INGRESO_DATOS | `E128` | `Por defecto NO; no calcula empuje a partir de parámetros inventados.` | `RESISTENCIA PASIVA CONSIDERADA SOLO EN DESLIZAMIENTO; no en volteo.` | Solución A solicitada: alcance explícito sin brazo supuesto. |
| INGRESO_DATOS | `E156` | `(vacía)` | `NO: diagnóstico; SI requiere fuente explícita. E.050 art.28 gobierna por Aef.` | NO: diagnóstico; SI requiere fuente explícita. E.050 art.28 gobierna por Aef. |
| INGRESO_DATOS | `E157` | `(vacía)` | `EMS/página o criterio del diseñador para comparar qmax con qadm.` | EMS/página o criterio del diseñador para comparar qmax con qadm. |
| INGRESO_DATOS | `E160` | `(vacía)` | `No se infiere desde fy redondeado. No cambia fy de resistencia.` | No se infiere desde fy redondeado. No cambia fy de resistencia. |
| INGRESO_DATOS | `E161` | `(vacía)` | `Solo OTRO: dato nominal para 9.7.2; editable. Grado420 usa 420MPa exactos convertidos.` | Solo OTRO: dato nominal para 9.7.2; editable. Grado420 usa 420MPa exactos convertidos. |
| INGRESO_DATOS | `E165` | `(vacía)` | `10.5.4: total según9.7; DOS CARAS exige .0012 en cada cara traccionada.` | 10.5.4: total según9.7; DOS CARAS exige .0012 en cada cara traccionada. |
| INGRESO_DATOS | `E166` | `(vacía)` | `Aplica solamente a UNA CARA.` | Aplica solamente a UNA CARA. |
| INGRESO_DATOS | `E167` | `(vacía)` | `Solo DOS CARAS: 0<fracción<1; superior=1-fracción. No es un factor de cargas.` | Solo DOS CARAS: 0<fracción<1; superior=1-fracción. No es un factor de cargas. |
| INGRESO_DATOS | `E170` | `(vacía)` | `Reparto estático elegido: lado -=-eta*gamma_fMy; lado +=(1-eta)*gamma_fMy. Rango0..1.` | Reparto estático elegido: lado -=-eta*gamma_fMy; lado +=(1-eta)*gamma_fMy. Rango0..1. |
| INGRESO_DATOS | `E171` | `(vacía)` | `La contribución escalar para barras Y es -gamma_fMx: signo global de mano derecha.` | La contribución escalar para barras Y es -gamma_fMx: signo global de mano derecha. |
| INGRESO_DATOS | `E172` | `(vacía)` | `Validación de redistribución y detalle; eta=.5 es hipótesis visible, no ecuación E.060.` | Validación de redistribución y detalle; eta=.5 es hipótesis visible, no ecuación E.060. |
| INGRESO_DATOS | `E173` | `(vacía)` | `Debe ser SI con referencia para acreditar la redistribución. No demuestra solución elástica de placa.` | Debe ser SI con referencia para acreditar la redistribución. No demuestra solución elástica de placa. |
| INGRESO_DATOS | `E177:E188` | `(vacía)` | `Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas.` | Dato requerido solamente si existe demanda superior o mínimo elegido en esa cara; barras rectas continuas. |
| GEOMETRIA | `B2627` | `=IF(AND(IF(LEN(inp_sigma0)=0,TRUE,IF(ISNUMBER(inp_sigma0),inp_sigma0>=0,FALSE)),IF(LEN(inp_rec_lat)=0,TRUE,IF(ISNUMBER(inp_rec_lat),inp_rec_lat>=0,FALSE)),IF(LEN(inp_nloc_ix)=0,TRUE,IF(ISNUMBER(inp_nloc_ix),AND(inp_nloc_ix>=0,MOD(inp_nloc_ix,1)=0),FALSE)),IF(LEN(inp_nloc_iy)=0,TRUE,IF(ISNUMBER(inp_nloc_iy),AND(inp_nloc_iy>=0,MOD(inp_nloc_iy,1)=0),FALSE)),IF(LEN(inp_nloc_sx)=0,TRUE,IF(ISNUMBER(inp_nloc_sx),AND(inp_nloc_sx>=0,MOD(inp_nloc_sx,1)=0),FALSE)),IF(LEN(inp_nloc_sy)=0,TRUE,IF(ISNUMBER(inp_nloc_sy),AND(inp_nloc_sy>=0,MOD(inp_nloc_sy,1)=0),FALSE)),IF(LEN(inp_ll_ix_m)=0,TRUE,IF(ISNUMBER(inp_ll_ix_m),inp_ll_ix_m>=0,FALSE)),IF(LEN(inp_ll_ix_p)=0,TRUE,IF(ISNUMBER(inp_ll_ix_p),inp_ll_ix_p>=0,FALSE)),IF(LEN(inp_ll_iy_m)=0,TRUE,IF(ISNUMBER(inp_ll_iy_m),inp_ll_iy_m>=0,FALSE)),IF(LEN(inp_ll_iy_p)=0,TRUE,IF(ISNUMBER(inp_ll_iy_p),inp_ll_iy_p>=0,FALSE)),IF(LEN(inp_ll_sx_m)=0,TRUE,IF(ISNUMBER(inp_ll_sx_m),inp_ll_sx_m>=0,FALSE)),IF(LEN(inp_ll_sx_p)=0,TRUE,IF(ISNUMBER(inp_ll_sx_p),inp_ll_sx_p>=0,FALSE)),IF(LEN(inp_ll_sy_m)=0,TRUE,IF(ISNUMBER(inp_ll_sy_m),inp_ll_sy_m>=0,FALSE)),IF(LEN(inp_ll_sy_p)=0,TRUE,IF(ISNUMBER(inp_ll_sy_p),inp_ll_sy_p>=0,FALSE)),IF(LEN(inp_n_col)=0,TRUE,IF(ISNUMBER(inp_n_col),AND(inp_n_col>=0,MOD(inp_n_col,1)=0),FALSE)),IF(LEN(inp_n_continue)=0,TRUE,IF(ISNUMBER(inp_n_continue),AND(inp_n_continue>=0,MOD(inp_n_continue,1)=0),FALSE)),IF(LEN(inp_n_dowel)=0,TRUE,IF(ISNUMBER(inp_n_dowel),AND(inp_n_dowel>=0,MOD(inp_n_dowel,1)=0),FALSE)),IF(LEN(inp_lcol_foot)=0,TRUE,IF(ISNUMBER(inp_lcol_foot),inp_lcol_foot>=0,FALSE)),IF(LEN(inp_lcol_above)=0,TRUE,IF(ISNUMBER(inp_lcol_above),inp_lcol_above>=0,FALSE)),IF(LEN(inp_ldow_foot)=0,TRUE,IF(ISNUMBER(inp_ldow_foot),inp_ldow_foot>=0,FALSE)),IF(LEN(inp_ldow_above)=0,TRUE,IF(ISNUMBER(inp_ldow_above),inp_ldow_above>=0,FALSE)),IF(LEN(inp_avf)=0,TRUE,IF(ISNUMBER(inp_avf),inp_avf>=0,FALSE)),IF(LEN(inp_rpassive)=0,TRUE,IF(ISNUMBER(inp_rpassive),inp_rpassive>=0,FALSE)),IF(LEN(inp_ncx)=0,TRUE,IF(ISNUMBER(inp_ncx),AND(inp_ncx>=0,MOD(inp_ncx,1)=0),FALSE)),IF(LEN(inp_nox)=0,TRUE,IF(ISNUMBER(inp_nox),AND(inp_nox>=0,MOD(inp_nox,1)=0),FALSE)),IF(LEN(inp_ncy)=0,TRUE,IF(ISNUMBER(inp_ncy),AND(inp_ncy>=0,MOD(inp_ncy,1)=0),FALSE)),IF(LEN(inp_noy)=0,TRUE,IF(ISNUMBER(inp_noy),AND(inp_noy>=0,MOD(inp_noy,1)=0),FALSE)),IF(LEN(inp_nox_minus)=0,TRUE,IF(ISNUMBER(inp_nox_minus),AND(inp_nox_minus>=0,MOD(inp_nox_minus,1)=0),FALSE)),IF(LEN(inp_nox_plus)=0,TRUE,IF(ISNUMBER(inp_nox_plus),AND(inp_nox_plus>=0,MOD(inp_nox_plus,1)=0),FALSE)),IF(LEN(inp_noy_minus)=0,TRUE,IF(ISNUMBER(inp_noy_minus),AND(inp_noy_minus>=0,MOD(inp_noy_minus,1)=0),FALSE)),IF(LEN(inp_noy_plus)=0,TRUE,IF(ISNUMBER(inp_noy_plus),AND(inp_noy_plus>=0,MOD(inp_noy_plus,1)=0),FALSE)),IF(LEN(inp_agg)=0,TRUE,IF(ISNUMBER(inp_agg),inp_agg>0,FALSE)),IF(LEN(inp_fc_col)=0,TRUE,IF(ISNUMBER(inp_fc_col),inp_fc_col>0,FALSE)),IF(LEN(inp_fy_col)=0,TRUE,IF(ISNUMBER(inp_fy_col),inp_fy_col>0,FALSE)),IF(LEN(inp_fs_slide)=0,TRUE,IF(ISNUMBER(inp_fs_slide),inp_fs_slide>0,FALSE)),IF(LEN(inp_fs_over)=0,TRUE,IF(ISNUMBER(inp_fs_over),inp_fs_over>0,FALSE)),IF(LEN(inp_scx)=0,TRUE,IF(ISNUMBER(inp_scx),inp_scx>0,FALSE)),IF(LEN(inp_sox)=0,TRUE,IF(ISNUMBER(inp_sox),inp_sox>0,FALSE)),IF(LEN(inp_scy)=0,TRUE,IF(ISNUMBER(inp_scy),inp_scy>0,FALSE)),IF(LEN(inp_soy)=0,TRUE,IF(ISNUMBER(inp_soy),inp_soy>0,FALSE)),IF(LEN(inp_srv_type)=0,TRUE,OR(inp_srv_type="GRAVEDAD",inp_srv_type="SISMO",inp_srv_type="VIENTO",inp_srv_type="OTRO")),IF(LEN(inp_qadm_inc)=0,TRUE,OR(inp_qadm_inc="NO",inp_qadm_inc="SI")),IF(LEN(inp_qadm_basis)=0,TRUE,OR(inp_qadm_basis="BRUTA",inp_qadm_basis="NETA")),IF(LEN(inp_ems_incl)=0,TRUE,OR(inp_ems_incl="SI",inp_ems_incl="NO",inp_ems_incl="NO CONFIRMADO")),IF(LEN(inp_edge_dir)=0,TRUE,OR(inp_edge_dir="NO APLICA",inp_edge_dir="+X",inp_edge_dir="-X",inp_edge_dir="+Y",inp_edge_dir="-Y",inp_edge_dir="+X/+Y",inp_edge_dir="+X/-Y",inp_edge_dir="-X/+Y",inp_edge_dir="-X/-Y")),IF(LEN(inp_rebar_type)=0,TRUE,OR(inp_rebar_type="CORRUGADAS",inp_rebar_type="LISAS",inp_rebar_type="MALLA SOLDADA")),IF(LEN(inp_concrete_type)=0,TRUE,OR(inp_concrete_type="NORMAL",inp_concrete_type="LIVIANO")),IF(LEN(inp_end_inf)=0,TRUE,OR(inp_end_inf="RECTA",inp_end_inf="GANCHO")),IF(LEN(inp_epoxy)=0,TRUE,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(LEN(inp_side_exposure)=0,TRUE,OR(inp_side_exposure="CONTRA SUELO",inp_side_exposure="CONTACTO SUELO",inp_side_exposure="INTERIOR")),IF(LEN(inp_end_sup)=0,TRUE,OR(inp_end_sup="RECTA",inp_end_sup="GANCHO")),IF(LEN(inp_local_detail)=0,TRUE,OR(inp_local_detail="SI",inp_local_detail="NO")),IF(LEN(inp_col_system)=0,TRUE,OR(inp_col_system="IN SITU",inp_col_system="PREFABRICADA")),IF(LEN(inp_end_col)=0,TRUE,OR(inp_end_col="RECTA",inp_end_col="GANCHO")),IF(LEN(inp_joint)=0,TRUE,OR(inp_joint="MONOLITICA",inp_joint="RUGOSA",inp_joint="LISA")),IF(LEN(inp_avf_anchor)=0,TRUE,OR(inp_avf_anchor="SI",inp_avf_anchor="NO")),IF(LEN(inp_passive)=0,TRUE,OR(inp_passive="NO",inp_passive="SI")),IF(LEN(inp_bottom_exposure)=0,TRUE,OR(inp_bottom_exposure="CONTRA SUELO",inp_bottom_exposure="CONTACTO SUELO",inp_bottom_exposure="INTERIOR")),IF(LEN(inp_top_exposure)=0,TRUE,OR(inp_top_exposure="CONTRA SUELO",inp_top_exposure="CONTACTO SUELO",inp_top_exposure="INTERIOR"))),"CUMPLE","DATOS INVÁLIDOS")` | `=IF(AND(OR(inp_peak="NO",inp_peak="SI"),OR(inp_grade="NTP GRADO 420 / ASTM G60",inp_grade="OTRO"),OR(inp_min_scheme="UNA CARA",inp_min_scheme="DOS CARAS"),OR(inp_min_face="INFERIOR",inp_min_face="SUPERIOR"),IF(ISNUMBER(inp_eta_x),AND(inp_eta_x>=0,inp_eta_x<=1),IF(LEN(inp_eta_x)=0,TRUE,FALSE)),IF(ISNUMBER(inp_eta_y),AND(inp_eta_y>=0,inp_eta_y<=1),IF(LEN(inp_eta_y)=0,TRUE,FALSE)),IF(LEN(inp_fy_nom)=0,TRUE,IF(ISNUMBER(inp_fy_nom),inp_fy_nom>0,FALSE)),IF(LEN(inp_sc_sx)=0,TRUE,IF(ISNUMBER(inp_sc_sx),inp_sc_sx>0,FALSE)),IF(LEN(inp_so_sx)=0,TRUE,IF(ISNUMBER(inp_so_sx),inp_so_sx>0,FALSE)),IF(LEN(inp_sc_sy)=0,TRUE,IF(ISNUMBER(inp_sc_sy),inp_sc_sy>0,FALSE)),IF(LEN(inp_so_sy)=0,TRUE,IF(ISNUMBER(inp_so_sy),inp_so_sy>0,FALSE)),IF(LEN(inp_nc_sx)=0,TRUE,IF(ISNUMBER(inp_nc_sx),AND(inp_nc_sx>=0,MOD(inp_nc_sx,1)=0),FALSE)),IF(LEN(inp_no_sx)=0,TRUE,IF(ISNUMBER(inp_no_sx),AND(inp_no_sx>=0,MOD(inp_no_sx,1)=0),FALSE)),IF(LEN(inp_no_sx_minus)=0,TRUE,IF(ISNUMBER(inp_no_sx_minus),AND(inp_no_sx_minus>=0,MOD(inp_no_sx_minus,1)=0),FALSE)),IF(LEN(inp_no_sx_plus)=0,TRUE,IF(ISNUMBER(inp_no_sx_plus),AND(inp_no_sx_plus>=0,MOD(inp_no_sx_plus,1)=0),FALSE)),IF(LEN(inp_nc_sy)=0,TRUE,IF(ISNUMBER(inp_nc_sy),AND(inp_nc_sy>=0,MOD(inp_nc_sy,1)=0),FALSE)),IF(LEN(inp_no_sy)=0,TRUE,IF(ISNUMBER(inp_no_sy),AND(inp_no_sy>=0,MOD(inp_no_sy,1)=0),FALSE)),IF(LEN(inp_no_sy_minus)=0,TRUE,IF(ISNUMBER(inp_no_sy_minus),AND(inp_no_sy_minus>=0,MOD(inp_no_sy_minus,1)=0),FALSE)),IF(LEN(inp_no_sy_plus)=0,TRUE,IF(ISNUMBER(inp_no_sy_plus),AND(inp_no_sy_plus>=0,MOD(inp_no_sy_plus,1)=0),FALSE)),IF(LEN(inp_min_frac)=0,TRUE,IF(ISNUMBER(inp_min_frac),AND(inp_min_frac>0,inp_min_frac<1),FALSE)),IF(LEN(inp_repartition_ok)=0,TRUE,OR(inp_repartition_ok="SI",inp_repartition_ok="NO"))),IF(AND(IF(LEN(inp_sigma0)=0,TRUE,IF(ISNUMBER(inp_sigma0),inp_sigma0>=0,FALSE)),IF(LEN(inp_rec_lat)=0,TRUE,IF(ISNUMBER(inp_rec_lat),inp_rec_lat>=0,FALSE)),IF(LEN(inp_nloc_ix)=0,TRUE,IF(ISNUMBER(inp_nloc_ix),AND(inp_nloc_ix>=0,MOD(inp_nloc_ix,1)=0),FALSE)),IF(LEN(inp_nloc_iy)=0,TRUE,IF(ISNUMBER(inp_nloc_iy),AND(inp_nloc_iy>=0,MOD(inp_nloc_iy,1)=0),FALSE)),IF(LEN(inp_nloc_sx)=0,TRUE,IF(ISNUMBER(inp_nloc_sx),AND(inp_nloc_sx>=0,MOD(inp_nloc_sx,1)=0),FALSE)),IF(LEN(inp_nloc_sy)=0,TRUE,IF(ISNUMBER(inp_nloc_sy),AND(inp_nloc_sy>=0,MOD(inp_nloc_sy,1)=0),FALSE)),IF(LEN(inp_ll_ix_m)=0,TRUE,IF(ISNUMBER(inp_ll_ix_m),inp_ll_ix_m>=0,FALSE)),IF(LEN(inp_ll_ix_p)=0,TRUE,IF(ISNUMBER(inp_ll_ix_p),inp_ll_ix_p>=0,FALSE)),IF(LEN(inp_ll_iy_m)=0,TRUE,IF(ISNUMBER(inp_ll_iy_m),inp_ll_iy_m>=0,FALSE)),IF(LEN(inp_ll_iy_p)=0,TRUE,IF(ISNUMBER(inp_ll_iy_p),inp_ll_iy_p>=0,FALSE)),IF(LEN(inp_ll_sx_m)=0,TRUE,IF(ISNUMBER(inp_ll_sx_m),inp_ll_sx_m>=0,FALSE)),IF(LEN(inp_ll_sx_p)=0,TRUE,IF(ISNUMBER(inp_ll_sx_p),inp_ll_sx_p>=0,FALSE)),IF(LEN(inp_ll_sy_m)=0,TRUE,IF(ISNUMBER(inp_ll_sy_m),inp_ll_sy_m>=0,FALSE)),IF(LEN(inp_ll_sy_p)=0,TRUE,IF(ISNUMBER(inp_ll_sy_p),inp_ll_sy_p>=0,FALSE)),IF(LEN(inp_n_col)=0,TRUE,IF(ISNUMBER(inp_n_col),AND(inp_n_col>=0,MOD(inp_n_col,1)=0),FALSE)),IF(LEN(inp_n_continue)=0,TRUE,IF(ISNUMBER(inp_n_continue),AND(inp_n_continue>=0,MOD(inp_n_continue,1)=0),FALSE)),IF(LEN(inp_n_dowel)=0,TRUE,IF(ISNUMBER(inp_n_dowel),AND(inp_n_dowel>=0,MOD(inp_n_dowel,1)=0),FALSE)),IF(LEN(inp_lcol_foot)=0,TRUE,IF(ISNUMBER(inp_lcol_foot),inp_lcol_foot>=0,FALSE)),IF(LEN(inp_lcol_above)=0,TRUE,IF(ISNUMBER(inp_lcol_above),inp_lcol_above>=0,FALSE)),IF(LEN(inp_ldow_foot)=0,TRUE,IF(ISNUMBER(inp_ldow_foot),inp_ldow_foot>=0,FALSE)),IF(LEN(inp_ldow_above)=0,TRUE,IF(ISNUMBER(inp_ldow_above),inp_ldow_above>=0,FALSE)),IF(LEN(inp_avf)=0,TRUE,IF(ISNUMBER(inp_avf),inp_avf>=0,FALSE)),IF(LEN(inp_rpassive)=0,TRUE,IF(ISNUMBER(inp_rpassive),inp_rpassive>=0,FALSE)),IF(LEN(inp_ncx)=0,TRUE,IF(ISNUMBER(inp_ncx),AND(inp_ncx>=0,MOD(inp_ncx,1)=0),FALSE)),IF(LEN(inp_nox)=0,TRUE,IF(ISNUMBER(inp_nox),AND(inp_nox>=0,MOD(inp_nox,1)=0),FALSE)),IF(LEN(inp_ncy)=0,TRUE,IF(ISNUMBER(inp_ncy),AND(inp_ncy>=0,MOD(inp_ncy,1)=0),FALSE)),IF(LEN(inp_noy)=0,TRUE,IF(ISNUMBER(inp_noy),AND(inp_noy>=0,MOD(inp_noy,1)=0),FALSE)),IF(LEN(inp_nox_minus)=0,TRUE,IF(ISNUMBER(inp_nox_minus),AND(inp_nox_minus>=0,MOD(inp_nox_minus,1)=0),FALSE)),IF(LEN(inp_nox_plus)=0,TRUE,IF(ISNUMBER(inp_nox_plus),AND(inp_nox_plus>=0,MOD(inp_nox_plus,1)=0),FALSE)),IF(LEN(inp_noy_minus)=0,TRUE,IF(ISNUMBER(inp_noy_minus),AND(inp_noy_minus>=0,MOD(inp_noy_minus,1)=0),FALSE)),IF(LEN(inp_noy_plus)=0,TRUE,IF(ISNUMBER(inp_noy_plus),AND(inp_noy_plus>=0,MOD(inp_noy_plus,1)=0),FALSE)),IF(LEN(inp_agg)=0,TRUE,IF(ISNUMBER(inp_agg),inp_agg>0,FALSE)),IF(LEN(inp_fc_col)=0,TRUE,IF(ISNUMBER(inp_fc_col),inp_fc_col>0,FALSE)),IF(LEN(inp_fy_col)=0,TRUE,IF(ISNUMBER(inp_fy_col),inp_fy_col>0,FALSE)),IF(LEN(inp_fs_slide)=0,TRUE,IF(ISNUMBER(inp_fs_slide),inp_fs_slide>0,FALSE)),IF(LEN(inp_fs_over)=0,TRUE,IF(ISNUMBER(inp_fs_over),inp_fs_over>0,FALSE)),IF(LEN(inp_scx)=0,TRUE,IF(ISNUMBER(inp_scx),inp_scx>0,FALSE)),IF(LEN(inp_sox)=0,TRUE,IF(ISNUMBER(inp_sox),inp_sox>0,FALSE)),IF(LEN(inp_scy)=0,TRUE,IF(ISNUMBER(inp_scy),inp_scy>0,FALSE)),IF(LEN(inp_soy)=0,TRUE,IF(ISNUMBER(inp_soy),inp_soy>0,FALSE)),IF(LEN(inp_srv_type)=0,TRUE,OR(inp_srv_type="GRAVEDAD",inp_srv_type="SISMO",inp_srv_type="VIENTO",inp_srv_type="OTRO")),IF(LEN(inp_qadm_inc)=0,TRUE,OR(inp_qadm_inc="NO",inp_qadm_inc="SI")),IF(LEN(inp_qadm_basis)=0,TRUE,OR(inp_qadm_basis="BRUTA",inp_qadm_basis="NETA")),IF(LEN(inp_ems_incl)=0,TRUE,OR(inp_ems_incl="SI",inp_ems_incl="NO",inp_ems_incl="NO CONFIRMADO")),IF(LEN(inp_edge_dir)=0,TRUE,OR(inp_edge_dir="NO APLICA",inp_edge_dir="+X",inp_edge_dir="-X",inp_edge_dir="+Y",inp_edge_dir="-Y",inp_edge_dir="+X/+Y",inp_edge_dir="+X/-Y",inp_edge_dir="-X/+Y",inp_edge_dir="-X/-Y")),IF(LEN(inp_rebar_type)=0,TRUE,OR(inp_rebar_type="CORRUGADAS",inp_rebar_type="LISAS",inp_rebar_type="MALLA SOLDADA")),IF(LEN(inp_concrete_type)=0,TRUE,OR(inp_concrete_type="NORMAL",inp_concrete_type="LIVIANO")),IF(LEN(inp_end_inf)=0,TRUE,OR(inp_end_inf="RECTA",inp_end_inf="GANCHO")),IF(LEN(inp_epoxy)=0,TRUE,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(LEN(inp_side_exposure)=0,TRUE,OR(inp_side_exposure="CONTRA SUELO",inp_side_exposure="CONTACTO SUELO",inp_side_exposure="INTERIOR")),IF(LEN(inp_end_sup)=0,TRUE,OR(inp_end_sup="RECTA",inp_end_sup="GANCHO")),IF(LEN(inp_local_detail)=0,TRUE,OR(inp_local_detail="SI",inp_local_detail="NO")),IF(LEN(inp_col_system)=0,TRUE,OR(inp_col_system="IN SITU",inp_col_system="PREFABRICADA")),IF(LEN(inp_end_col)=0,TRUE,OR(inp_end_col="RECTA",inp_end_col="GANCHO")),IF(LEN(inp_joint)=0,TRUE,OR(inp_joint="MONOLITICA",inp_joint="RUGOSA",inp_joint="LISA")),IF(LEN(inp_avf_anchor)=0,TRUE,OR(inp_avf_anchor="SI",inp_avf_anchor="NO")),IF(LEN(inp_passive)=0,TRUE,OR(inp_passive="NO",inp_passive="SI")),IF(LEN(inp_bottom_exposure)=0,TRUE,OR(inp_bottom_exposure="CONTRA SUELO",inp_bottom_exposure="CONTACTO SUELO",inp_bottom_exposure="INTERIOR")),IF(LEN(inp_top_exposure)=0,TRUE,OR(inp_top_exposure="CONTRA SUELO",inp_top_exposure="CONTACTO SUELO",inp_top_exposure="INTERIOR"))),"CUMPLE","DATOS INVÁLIDOS"),"DATOS INVÁLIDOS")` | Nuevas selecciones/números con guardas antes de operaciones; no ocultar datos inválidos. |
| PRESIONES_SERVICIO | `A13` | `Verificacion qmax <= qadm` | `Control adicional de pico según EMS` | Texto de criterio adicional del pico físico; D12 conserva qadm. |
| PRESIONES_SERVICIO | `A57` | `(vacía)` | `Diagnóstico qmax vs qadm` | Diagnóstico visible incluso con selector NO; no gobierna entonces. |
| PRESIONES_SERVICIO | `A58` | `(vacía)` | `Control adicional pico / fuente` | Selector y fundamento trazables; NO por defecto. |
| PRESIONES_SERVICIO | `A59` | `(vacía)` | `Alcance de resistencia pasiva` | No interviene en volteo; no se inventa un brazo de aplicación. |
| PRESIONES_SERVICIO | `B57` | `(vacía)` | `=IF(srv_input_state<>"OK",srv_input_state,IF(g_basis_state<>"OK",g_basis_state,IF(g_qphysical<=g_qadm,"PICO <= QADM","PICO > QADM")))` | Diagnóstico visible incluso con selector NO; no gobierna entonces. |
| PRESIONES_SERVICIO | `B58` | `(vacía)` | `=inp_peak&" / "&IF(LEN(inp_peak_ref)=0,"SIN FUENTE",inp_peak_ref)` | Selector y fundamento trazables; NO por defecto. |
| PRESIONES_SERVICIO | `B59` | `(vacía)` | `SOLO DESLIZAMIENTO` | No interviene en volteo; no se inventa un brazo de aplicación. |
| PRESIONES_SERVICIO | `C57` | `(vacía)` | `-` | Diagnóstico visible incluso con selector NO; no gobierna entonces. |
| PRESIONES_SERVICIO | `C58` | `(vacía)` | `-` | Selector y fundamento trazables; NO por defecto. |
| PRESIONES_SERVICIO | `C59` | `(vacía)` | `-` | No interviene en volteo; no se inventa un brazo de aplicación. |
| PRESIONES_SERVICIO | `D13` | `=IF(srv_input_state<>"OK",srv_input_state,IF(g_basis_state<>"OK",g_basis_state,IF(g_Q<=0,"REQUIERE ANÁLISIS ESPECIAL",IF(D11<0,"REQUIERE ANÁLISIS ESPECIAL",IF(g_qphysical<=g_qadm,"CUMPLE","NO CUMPLE")))))` | `=IF(srv_input_state<>"OK",srv_input_state,IF(inp_peak="NO","NO APLICA",IF(inp_peak<>"SI","DATOS INVÁLIDOS",IF(LEN(inp_peak_ref)=0,"REQUIERE DATOS",IF(g_basis_state<>"OK",g_basis_state,IF(OR(g_Q<=0,D11<0),"REQUIERE ANÁLISIS ESPECIAL",IF(g_qphysical<=g_qadm,"CUMPLE","NO CUMPLE")))))))` | E.05028: pico físico es criterio adicional optativo, no requisito geotécnico universal. |
| PRESIONES_SERVICIO | `D35` | `Este control complementa q física máxima.` | `Control E.050 Art.28 mediante área efectiva; el pico se controla solo si se selecciona SI.` | Jerarquía qadm sin cambiar qmax/qmin/campo físico. |
| PRESIONES_SERVICIO | `D57` | `(vacía)` | `Diagnóstico visible incluso con selector NO; no gobierna entonces.` | Diagnóstico visible incluso con selector NO; no gobierna entonces. |
| PRESIONES_SERVICIO | `D58` | `(vacía)` | `Selector y fundamento trazables; NO por defecto.` | Selector y fundamento trazables; NO por defecto. |
| PRESIONES_SERVICIO | `D59` | `(vacía)` | `No interviene en volteo; no se inventa un brazo de aplicación.` | No interviene en volteo; no se inventa un brazo de aplicación. |
| FLEXION_ACERO | `A30` | `(vacía)` | `FASE 3: GRADO Y MÍNIMO EN UNA O DOS CARAS` | FASE 3: GRADO Y MÍNIMO EN UNA O DOS CARAS |
| FLEXION_ACERO | `A31` | `(vacía)` | `fy nominal normativo` | 9.7.2: clasificación explícita; no modifica inp_fy. |
| FLEXION_ACERO | `A32` | `(vacía)` | `fy nominal convertido MPa` | Conversión interna, no entrada SI; umbral420 sin redondeo binario. |
| FLEXION_ACERO | `A33` | `(vacía)` | `Coherencia fy resistencia / grado` | Advertencia explícita; fy de resistencia nunca se reemplaza. |
| FLEXION_ACERO | `A34` | `(vacía)` | `Estado distribución del mínimo` | DOS CARAS necesita fracción explícita; no se presupone reparto. |
| FLEXION_ACERO | `A35` | `(vacía)` | `Rho mínimo asignado inferior` | Total repartido; piso .0012 solo cuando cara traccionada en DOS CARAS. |
| FLEXION_ACERO | `A36` | `(vacía)` | `Rho mínimo asignado superior` | La suma de mínimos asignados es rho_eff, no 2*rho_eff. |
| FLEXION_ACERO | `A37` | `(vacía)` | `As mínimo total por metro` | 10.5.4 y9.7: total inferior+superior, antes de límites .0012 de caras traccionadas. |
| FLEXION_ACERO | `A45` | `(vacía)` | `REPARTO FIRMADO: MISMO MOMENTO DE CARA, SIN DUPLICAR MU` | REPARTO FIRMADO: MISMO MOMENTO DE CARA, SIN DUPLICAR MU |
| FLEXION_ACERO | `A47` | `(vacía)` | `Estado de parámetros locales` | Eta es una hipótesis estática visible que necesita análisis validado; no se atribuye a E.060. |
| FLEXION_ACERO | `A51` | `(vacía)` | `Lado` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `A52` | `(vacía)` | `X -` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `A53` | `(vacía)` | `X +` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `A54` | `(vacía)` | `Y -` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `A55` | `(vacía)` | `Y +` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `A57` | `(vacía)` | `Error de par local X` | T+−T-=gamma_fMy; no 2*\|gamma_fMy\|. |
| FLEXION_ACERO | `A58` | `(vacía)` | `Error de par local Y` | Para barras Y, par escalar=−gamma_fMx según mano derecha. |
| FLEXION_ACERO | `A59` | `(vacía)` | `Error gamma_f+gamma_v X` | Complementariedad 11.12.6.1; no se añade otro momento aplicado. |
| FLEXION_ACERO | `A60` | `(vacía)` | `Error gamma_f+gamma_v Y` | Momento crítico de eje Y físico; íntegro en flexión+cortante. |
| FLEXION_ACERO | `A61` | `(vacía)` | `Estado equilibrio local` | Control de suma firmada en cada cara y par. No sustituye análisis de compatibilidad de placa. |
| FLEXION_ACERO | `B22` | `=IF(OR(inp_rebar_type="CORRUGADAS",inp_rebar_type="LISAS",inp_rebar_type="MALLA SOLDADA"),IF(inp_rebar_type="LISAS",0.0025,IF(inp_rebar_type="MALLA SOLDADA",IF(fy_mpa>=420,0.0018,""),IF(fy_mpa>=420,0.0018,0.002))),"")` | `=IF(NOT(ISNUMBER(fy_nom_mpa)),"",IF(inp_rebar_type="LISAS",0.0025,IF(inp_rebar_type="CORRUGADAS",IF(fy_nom_mpa>=420,0.0018,0.002),IF(inp_rebar_type="MALLA SOLDADA",IF(fy_nom_mpa>=420,0.0018,""),""))))` | 9.7.2: fy nominal/grado declarado, no inferencia de grado por fy de cálculo redondeado. |
| FLEXION_ACERO | `B31` | `(vacía)` | `=IF(inp_grade="NTP GRADO 420 / ASTM G60",420/0.0980665,IF(inp_grade="OTRO",IF(ISNUMBER(inp_fy_nom),IF(inp_fy_nom>0,inp_fy_nom,""),""),""))` | 9.7.2: clasificación explícita; no modifica inp_fy. |
| FLEXION_ACERO | `B32` | `(vacía)` | `=IF(inp_grade="NTP GRADO 420 / ASTM G60",420,IF(ISNUMBER(fy_nom_kg),fy_nom_kg*0.0980665,""))` | Conversión interna, no entrada SI; umbral420 sin redondeo binario. |
| FLEXION_ACERO | `B33` | `(vacía)` | `=IF(COUNT(inp_fy,fy_nom_kg)<>2,"REQUIERE DATOS",IF(ABS(inp_fy-fy_nom_kg)<=0.00000001,"COINCIDE",IF(inp_fy<fy_nom_kg,"FY RESISTENCIA MENOR QUE NOMINAL","FY RESISTENCIA MAYOR QUE NOMINAL: VERIFICAR CERTIFICADO")))` | Advertencia explícita; fy de resistencia nunca se reemplaza. |
| FLEXION_ACERO | `B34` | `(vacía)` | `=IF(NOT(OR(inp_min_scheme="UNA CARA",inp_min_scheme="DOS CARAS")),"DATOS INVÁLIDOS",IF(inp_min_scheme="UNA CARA",IF(OR(inp_min_face="INFERIOR",inp_min_face="SUPERIOR"),"OK","DATOS INVÁLIDOS"),IF(COUNT(inp_min_frac)<>1,"REQUIERE DATOS",IF(AND(inp_min_frac>0,inp_min_frac<1),"OK","DATOS INVÁLIDOS"))))` | DOS CARAS necesita fracción explícita; no se presupone reparto. |
| FLEXION_ACERO | `B35` | `(vacía)` | `=IF(AND(min_model_state="OK",ISNUMBER(rho_eff)),IF(inp_min_scheme="UNA CARA",IF(inp_min_face="INFERIOR",rho_eff,0),inp_min_frac*rho_eff),"")` | Total repartido; piso .0012 solo cuando cara traccionada en DOS CARAS. |
| FLEXION_ACERO | `B36` | `(vacía)` | `=IF(AND(min_model_state="OK",ISNUMBER(rho_alloc_inf)),rho_eff-rho_alloc_inf,"")` | La suma de mínimos asignados es rho_eff, no 2*rho_eff. |
| FLEXION_ACERO | `B37` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(rho_eff)),rho_eff*100*inp_h*100,"")` | 10.5.4 y9.7: total inferior+superior, antes de límites .0012 de caras traccionadas. |
| FLEXION_ACERO | `B47` | `(vacía)` | `=IF(punz_state<>"OK",punz_state,IF(COUNT(inp_eta_x,inp_eta_y)<>2,"REQUIERE DATOS",IF(AND(MIN(inp_eta_x,inp_eta_y)>=0,MAX(inp_eta_x,inp_eta_y)<=1),"OK","DATOS INVÁLIDOS")))` | Eta es una hipótesis estática visible que necesita análisis validado; no se atribuye a E.060. |
| FLEXION_ACERO | `B51` | `(vacía)` | `M cara total tf m` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `B52:B53` | `(vacía)` | `=IF(struct_state="OK",DIAGRAMAS_X!B7,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `B54:B55` | `(vacía)` | `=IF(struct_state="OK",DIAGRAMAS_Y!B7,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `B57` | `(vacía)` | `=IF(local_model_state="OK",D53-D52-C52,"")` | T+−T-=gamma_fMy; no 2*\|gamma_fMy\|. |
| FLEXION_ACERO | `B58` | `(vacía)` | `=IF(local_model_state="OK",D55-D54-C54,"")` | Para barras Y, par escalar=−gamma_fMx según mano derecha. |
| FLEXION_ACERO | `B59` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B48+(1-PUNZONAMIENTO!B37)*PUNZONAMIENTO!B46-PUNZONAMIENTO!B46,"")` | Complementariedad 11.12.6.1; no se añade otro momento aplicado. |
| FLEXION_ACERO | `B60` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B47+(1-PUNZONAMIENTO!B36)*PUNZONAMIENTO!B45-PUNZONAMIENTO!B45,"")` | Momento crítico de eje Y físico; íntegro en flexión+cortante. |
| FLEXION_ACERO | `B61` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(AND(MAX(ABS(J52),ABS(J53),ABS(J54),ABS(J55),ABS(B57),ABS(B58),ABS(B59),ABS(B60))<=0.00000001),"CUMPLE","NO CUMPLE"))` | Control de suma firmada en cada cara y par. No sustituye análisis de compatibilidad de placa. |
| FLEXION_ACERO | `C31` | `(vacía)` | `kgf/cm2` | 9.7.2: clasificación explícita; no modifica inp_fy. |
| FLEXION_ACERO | `C32` | `(vacía)` | `MPa` | Conversión interna, no entrada SI; umbral420 sin redondeo binario. |
| FLEXION_ACERO | `C33` | `(vacía)` | `-` | Advertencia explícita; fy de resistencia nunca se reemplaza. |
| FLEXION_ACERO | `C34` | `(vacía)` | `-` | DOS CARAS necesita fracción explícita; no se presupone reparto. |
| FLEXION_ACERO | `C35` | `(vacía)` | `-` | Total repartido; piso .0012 solo cuando cara traccionada en DOS CARAS. |
| FLEXION_ACERO | `C36` | `(vacía)` | `-` | La suma de mínimos asignados es rho_eff, no 2*rho_eff. |
| FLEXION_ACERO | `C37` | `(vacía)` | `cm2/m` | 10.5.4 y9.7: total inferior+superior, antes de límites .0012 de caras traccionadas. |
| FLEXION_ACERO | `C47` | `(vacía)` | `-` | Eta es una hipótesis estática visible que necesita análisis validado; no se atribuye a E.060. |
| FLEXION_ACERO | `C51` | `(vacía)` | `Gamma_f Mu tf m` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `C52` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B48,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `C53` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B48,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `C54` | `(vacía)` | `=IF(punz_state="OK",-PUNZONAMIENTO!B47,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `C55` | `(vacía)` | `=IF(punz_state="OK",-PUNZONAMIENTO!B47,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `C57` | `(vacía)` | `tf m` | T+−T-=gamma_fMy; no 2*\|gamma_fMy\|. |
| FLEXION_ACERO | `C58` | `(vacía)` | `tf m` | Para barras Y, par escalar=−gamma_fMx según mano derecha. |
| FLEXION_ACERO | `C59` | `(vacía)` | `tf m` | Complementariedad 11.12.6.1; no se añade otro momento aplicado. |
| FLEXION_ACERO | `C60` | `(vacía)` | `tf m` | Momento crítico de eje Y físico; íntegro en flexión+cortante. |
| FLEXION_ACERO | `C61` | `(vacía)` | `-` | Control de suma firmada en cada cara y par. No sustituye análisis de compatibilidad de placa. |
| FLEXION_ACERO | `D22` | `E.060 9.7.2. Malla fy<420 no tiene valor explícito en tabla; se deja sin cuantía y fuera de alcance.` | `E.0609.7.2: grado nominal declarado; fy de resistencia se conserva.` | Nuevo criterio de cuantía según tipo/grado. |
| FLEXION_ACERO | `D24` | `No cambia la entrada heredada 0.0018; se impone 0.002 para fy=4200kgf/cm2.` | `La comparación usa cuantía total normativa; no duplica mínimo completo por cara.` | 10.5.4: mínimo total separado de mínimos por cara. |
| FLEXION_ACERO | `D31` | `(vacía)` | `9.7.2: clasificación explícita; no modifica inp_fy.` | 9.7.2: clasificación explícita; no modifica inp_fy. |
| FLEXION_ACERO | `D32` | `(vacía)` | `Conversión interna, no entrada SI; umbral420 sin redondeo binario.` | Conversión interna, no entrada SI; umbral420 sin redondeo binario. |
| FLEXION_ACERO | `D33` | `(vacía)` | `Advertencia explícita; fy de resistencia nunca se reemplaza.` | Advertencia explícita; fy de resistencia nunca se reemplaza. |
| FLEXION_ACERO | `D34` | `(vacía)` | `DOS CARAS necesita fracción explícita; no se presupone reparto.` | DOS CARAS necesita fracción explícita; no se presupone reparto. |
| FLEXION_ACERO | `D35` | `(vacía)` | `Total repartido; piso .0012 solo cuando cara traccionada en DOS CARAS.` | Total repartido; piso .0012 solo cuando cara traccionada en DOS CARAS. |
| FLEXION_ACERO | `D36` | `(vacía)` | `La suma de mínimos asignados es rho_eff, no 2*rho_eff.` | La suma de mínimos asignados es rho_eff, no 2*rho_eff. |
| FLEXION_ACERO | `D37` | `(vacía)` | `10.5.4 y9.7: total inferior+superior, antes de límites .0012 de caras traccionadas.` | 10.5.4 y9.7: total inferior+superior, antes de límites .0012 de caras traccionadas. |
| FLEXION_ACERO | `D47` | `(vacía)` | `Eta es una hipótesis estática visible que necesita análisis validado; no se atribuye a E.060.` | Eta es una hipótesis estática visible que necesita análisis validado; no se atribuye a E.060. |
| FLEXION_ACERO | `D51` | `(vacía)` | `T local firmado tf m` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `D52` | `(vacía)` | `=IF(local_model_state="OK",-inp_eta_x*C52,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `D53` | `(vacía)` | `=IF(local_model_state="OK",(1-inp_eta_x)*C53,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `D54` | `(vacía)` | `=IF(local_model_state="OK",-inp_eta_y*C54,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `D55` | `(vacía)` | `=IF(local_model_state="OK",(1-inp_eta_y)*C55,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `D57` | `(vacía)` | `T+−T-=gamma_fMy; no 2*\|gamma_fMy\|.` | T+−T-=gamma_fMy; no 2*\|gamma_fMy\|. |
| FLEXION_ACERO | `D58` | `(vacía)` | `Para barras Y, par escalar=−gamma_fMx según mano derecha.` | Para barras Y, par escalar=−gamma_fMx según mano derecha. |
| FLEXION_ACERO | `D59` | `(vacía)` | `Complementariedad 11.12.6.1; no se añade otro momento aplicado.` | Complementariedad 11.12.6.1; no se añade otro momento aplicado. |
| FLEXION_ACERO | `D60` | `(vacía)` | `Momento crítico de eje Y físico; íntegro en flexión+cortante.` | Momento crítico de eje Y físico; íntegro en flexión+cortante. |
| FLEXION_ACERO | `D61` | `(vacía)` | `Control de suma firmada en cada cara y par. No sustituye análisis de compatibilidad de placa.` | Control de suma firmada en cada cara y par. No sustituye análisis de compatibilidad de placa. |
| FLEXION_ACERO | `E51` | `(vacía)` | `m residual tf m/m` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `E52:E53` | `(vacía)` | `=IF(local_model_state="OK",(B52-D52)/inp_by,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `E54:E55` | `(vacía)` | `=IF(local_model_state="OK",(B54-D54)/inp_bx,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `F51` | `(vacía)` | `M franja tf m` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `F52:F55` | `(vacía)` | `=IF(local_model_state="OK",D52+E52*L52,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `G5:G6` | `=IF(struct_state="OK",IF(OR(B5="Inferior",D5>0),rho_eff*100*inp_h*100,0),"")` | `=IF(AND(struct_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_inf,IF(AND(inp_min_scheme="DOS CARAS",D5>0.000001),0.0012,0))*100*inp_h*100,"")` | 10.5.4: mínimo asignado a cara; piso .0012 cuando DOS CARAS y tracción. Sin duplicar total9.7. |
| FLEXION_ACERO | `G7:G8` | `=IF(struct_state="OK",IF(OR(B7="Inferior",D7>0),rho_eff*100*inp_h*100,0),"")` | `=IF(AND(struct_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_sup,IF(AND(inp_min_scheme="DOS CARAS",D7>0.000001),0.0012,0))*100*inp_h*100,"")` | 10.5.4: mínimo asignado a cara; piso .0012 cuando DOS CARAS y tracción. Sin duplicar total9.7. |
| FLEXION_ACERO | `G51` | `(vacía)` | `M fuera tf m` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `G52:G53` | `(vacía)` | `=IF(local_model_state="OK",E52*(inp_by-L52),"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `G54:G55` | `(vacía)` | `=IF(local_model_state="OK",E54*(inp_bx-L54),"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `H5:H8` | `=IF(struct_state="OK",IF(ISNUMBER(F5),MAX(F5,G5),""),"")` | `=IF(struct_state="OK",IF(COUNT(F5,G5)=2,MAX(F5,G5),""),"")` | Mínimo por cara separado de flexión; mínimo total se verifica con acero real. |
| FLEXION_ACERO | `H51` | `(vacía)` | `Cara franja` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `H52:H55` | `(vacía)` | `=IF(local_model_state="OK",IF(F52>0.000001,"INFERIOR",IF(F52<-0.000001,"SUPERIOR","SIN TRACCIÓN")),"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `I51` | `(vacía)` | `Cara fuera` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `I52:I55` | `(vacía)` | `=IF(local_model_state="OK",IF(G52>0.000001,"INFERIOR",IF(G52<-0.000001,"SUPERIOR","SIN TRACCIÓN")),"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `J51` | `(vacía)` | `Error M cara tf m` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `J52:J55` | `(vacía)` | `=IF(local_model_state="OK",B52-F52-G52,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `K51` | `(vacía)` | `Cara T local` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `K52:K55` | `(vacía)` | `=IF(local_model_state="OK",IF(D52>0.000001,"INFERIOR",IF(D52<-0.000001,"SUPERIOR","SIN TRACCIÓN")),"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `L51` | `(vacía)` | `Ancho franja m` | 13.5.3: componente local y residual suman el momento global de cara. |
| FLEXION_ACERO | `L52` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B56,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `L53` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B56,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `L54` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B55,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| FLEXION_ACERO | `L55` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B55,"")` | Reasignación: m0=(M_cara-T)/W; M_franja=T+m0*b; M_fuera=m0*(W-b). Suma=M_cara. |
| ACERO_DETALLADO | `A85` | `Capa/dirección` | `Lado` | Resumen de cuatro lados; detalle de caras/regiones en filas232:247. |
| ACERO_DETALLADO | `A86` | `INF X` | `X lado -` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `A87` | `INF Y` | `X lado +` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `A88` | `SUP X` | `Y lado -` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `A89` | `SUP Y` | `Y lado +` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `A180` | `(vacía)` | `DISTRIBUCIÓN SUPERIOR X — E.06015.4.4` | DISTRIBUCIÓN SUPERIOR X — E.06015.4.4 |
| ACERO_DETALLADO | `A181` | `(vacía)` | `Dirección` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A182` | `(vacía)` | `As total requerido` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A183` | `(vacía)` | `Ancho franja central` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A184` | `(vacía)` | `Ancho exterior total` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A185` | `(vacía)` | `As central requerido` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A186` | `(vacía)` | `As exterior requerido` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A187` | `(vacía)` | `Barra adoptada` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A188` | `(vacía)` | `Separación central` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A189` | `(vacía)` | `Separación exterior` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A190` | `(vacía)` | `N real central` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A191` | `(vacía)` | `N real exterior` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A192` | `(vacía)` | `As real central` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A193` | `(vacía)` | `As real exterior` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A194` | `(vacía)` | `As central por metro` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A195` | `(vacía)` | `As exterior por metro` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A196` | `(vacía)` | `Franja contenida` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A197` | `(vacía)` | `Estado distribución superior X` | 15.4.4, cantidad y separaciones/ubicación reales. |
| ACERO_DETALLADO | `A202` | `(vacía)` | `DISTRIBUCIÓN SUPERIOR Y — E.06015.4.4` | DISTRIBUCIÓN SUPERIOR Y — E.06015.4.4 |
| ACERO_DETALLADO | `A203` | `(vacía)` | `Dirección` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A204` | `(vacía)` | `As total requerido` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A205` | `(vacía)` | `Ancho franja central` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A206` | `(vacía)` | `Ancho exterior total` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A207` | `(vacía)` | `As central requerido` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A208` | `(vacía)` | `As exterior requerido` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A209` | `(vacía)` | `Barra adoptada` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A210` | `(vacía)` | `Separación central` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A211` | `(vacía)` | `Separación exterior` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A212` | `(vacía)` | `N real central` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A213` | `(vacía)` | `N real exterior` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A214` | `(vacía)` | `As real central` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A215` | `(vacía)` | `As real exterior` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A216` | `(vacía)` | `As central por metro` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A217` | `(vacía)` | `As exterior por metro` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A218` | `(vacía)` | `Franja contenida` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `A219` | `(vacía)` | `Estado distribución superior Y` | 15.4.4, cantidad y separaciones/ubicación reales. |
| ACERO_DETALLADO | `A230` | `(vacía)` | `MOMENTO REGIONAL FIRMADO / CARAS / ARMADO REAL` | MOMENTO REGIONAL FIRMADO / CARAS / ARMADO REAL |
| ACERO_DETALLADO | `A231` | `(vacía)` | `Lado / región` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `A232:A233` | `(vacía)` | `X - franja` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `A234:A235` | `(vacía)` | `X - fuera` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `A236:A237` | `(vacía)` | `X + franja` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `A238:A239` | `(vacía)` | `X + fuera` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `A240:A241` | `(vacía)` | `Y - franja` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `A242:A243` | `(vacía)` | `Y - fuera` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `A244:A245` | `(vacía)` | `Y + franja` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `A246:A247` | `(vacía)` | `Y + fuera` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `A250` | `(vacía)` | `AS TOTAL POR CARA: GLOBAL Y REGIONES LOCALES` | AS TOTAL POR CARA: GLOBAL Y REGIONES LOCALES |
| ACERO_DETALLADO | `A251` | `(vacía)` | `As total INF X` | MAX(global, suma de regiones locales). No suma global+gamma_fMu. |
| ACERO_DETALLADO | `A252` | `(vacía)` | `As total INF Y` | MAX(global, suma de regiones locales). No suma global+gamma_fMu. |
| ACERO_DETALLADO | `A253` | `(vacía)` | `As total SUP X` | MAX(global, suma de regiones locales). No suma global+gamma_fMu. |
| ACERO_DETALLADO | `A254` | `(vacía)` | `As total SUP Y` | MAX(global, suma de regiones locales). No suma global+gamma_fMu. |
| ACERO_DETALLADO | `A260` | `(vacía)` | `MÍNIMO TOTAL Y ACERO REAL ENTRE AMBAS CARAS` | MÍNIMO TOTAL Y ACERO REAL ENTRE AMBAS CARAS |
| ACERO_DETALLADO | `A261` | `(vacía)` | `Dirección` | Mínimo total por dirección. |
| ACERO_DETALLADO | `A262` | `(vacía)` | `X` | 10.5.4: As_inf+As_sup >= As mínimo total; no duplicación del mínimo de9.7. |
| ACERO_DETALLADO | `A263` | `(vacía)` | `Y` | 10.5.4: As_inf+As_sup >= As mínimo total; no duplicación del mínimo de9.7. |
| ACERO_DETALLADO | `A264` | `(vacía)` | `Estado mínimo total` | Pisos por cara comprobados en flexión/regiones; total real aquí. |
| ACERO_DETALLADO | `A266` | `(vacía)` | `N total INF X` | Conteo total confirmado de la cara; no convierte faltante aplicable en cero. |
| ACERO_DETALLADO | `A267` | `(vacía)` | `N total SUP X` | Conteo total confirmado de la cara; no convierte faltante aplicable en cero. |
| ACERO_DETALLADO | `A268` | `(vacía)` | `N total INF Y` | Conteo total confirmado de la cara; no convierte faltante aplicable en cero. |
| ACERO_DETALLADO | `A269` | `(vacía)` | `N total SUP Y` | Conteo total confirmado de la cara; no convierte faltante aplicable en cero. |
| ACERO_DETALLADO | `A282` | `(vacía)` | `Ancho exterior lado -` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A283` | `(vacía)` | `Ancho exterior lado +` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A284` | `(vacía)` | `N real exterior lado -` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A285` | `(vacía)` | `N real exterior lado +` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A286` | `(vacía)` | `As requerido exterior -` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A287` | `(vacía)` | `As requerido exterior +` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A288` | `(vacía)` | `As real exterior -` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A289` | `(vacía)` | `As real exterior +` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A290` | `(vacía)` | `Factibilidad superior X` | No acredita un N que no cabe; ambos lados del exterior. |
| ACERO_DETALLADO | `A294` | `(vacía)` | `Ancho exterior lado -` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A295` | `(vacía)` | `Ancho exterior lado +` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A296` | `(vacía)` | `N real exterior lado -` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A297` | `(vacía)` | `N real exterior lado +` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A298` | `(vacía)` | `As requerido exterior -` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A299` | `(vacía)` | `As requerido exterior +` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A300` | `(vacía)` | `As real exterior -` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A301` | `(vacía)` | `As real exterior +` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `A302` | `(vacía)` | `Factibilidad superior Y` | No acredita un N que no cabe; ambos lados del exterior. |
| ACERO_DETALLADO | `B11` | `=IF(struct_state="OK",MAX(IF(H5>0,D5/H5,0),IF(H6>0,D6/H6,0),IF(H7>0,D7/H7,0),IF(H8>0,D8/H8,0)),"")` | `=IF(AND(struct_state="OK",COUNT(D5:D8,H5:H8)=8),MAX(IF(H5>0,D5/H5,0),IF(H6>0,D6/H6,0),IF(H7>0,D7/H7,0),IF(H8>0,D8/H8,0)),"")` | No calcular D/C con demanda no determinada. |
| ACERO_DETALLADO | `B12` | `=IF(struct_state<>"OK",struct_state,IF(COUNTIF(J5:J8,"NO CUMPLE")=0,"CUMPLE","NO CUMPLE"))` | `=IF(struct_state<>"OK",struct_state,IF(NOT(ISNUMBER(B11)),"REQUIERE DATOS",IF(B11<=1,"CUMPLE","NO CUMPLE")))` | No acreditar acero cuando falta la demanda. |
| ACERO_DETALLADO | `B13` | `=IF(struct_state<>"OK",struct_state,IF(MAX(F5:F8)<=geo_smax,"CUMPLE","NO CUMPLE"))` | `=IF(struct_state<>"OK",struct_state,IF(COUNT(D5:D8)<>4,"REQUIERE DATOS",IF(AND(OR(D5=0,F5<=geo_smax),OR(D6=0,F6<=geo_smax),OR(D7=0,F7<=geo_smax),OR(D8=0,F8<=geo_smax)),"CUMPLE","NO CUMPLE")))` | Espaciamiento de parrilla no requerida no produce NO CUMPLE; un mínimo faltante queda pendiente. |
| ACERO_DETALLADO | `B28` | `=IF(geo_input_state="OK",IF(inp_bx>=inp_by,"LARGA / CUADRADA","CORTA"),"")` | `=IF(struct_state="OK",IF(inp_bx>=inp_by,"LARGA / CUADRADA","CORTA"),"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B29` | `=IF(struct_state="OK",flex_as_req_inf_x*inp_by,"")` | `=As_tot_inf_x` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B32` | `=IF(struct_state="OK",IF(inp_bx>=inp_by,B29,steel_gamma*B29),"")` | `=IF(AND(struct_state="OK",ISNUMBER(B29)),IF(inp_bx>=inp_by,B29,steel_gamma*B29),"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B33` | `=IF(struct_state="OK",B29-B32,"")` | `=IF(AND(struct_state="OK",COUNT(B29,B32)=2),B29-B32,"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B37` | `=inp_ncx` | `=IF(ISNUMBER(inp_ncx),inp_ncx,"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B38` | `=inp_nox` | `=IF(ISNUMBER(inp_nox),inp_nox,"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B41` | `=IF(struct_state="OK",B32/B30,"")` | `=IF(AND(struct_state="OK",ISNUMBER(B32)),B32/B30,"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B42` | `=IF(struct_state="OK",IF(B31>0,B33/B31,0),"")` | `=IF(AND(struct_state="OK",ISNUMBER(B33)),IF(B31>0,B33/B31,0),"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B43` | `=IF(struct_state<>"OK",struct_state,IF(inp_bx>=inp_by,"OK",IF(ABS(inp_yc)+B30/2<=inp_by/2,"OK","FUERA DEL ALCANCE IMPLEMENTADO")))` | `=IF(struct_state<>"OK",struct_state,IF(NOT(AND(ISNUMBER(As_tot_inf_x),As_tot_inf_x>0.000001)),"NO APLICA",IF(inp_bx>=inp_by,"OK",IF(ABS(inp_yc)+B30/2<=inp_by/2,"OK","FUERA DEL ALCANCE IMPLEMENTADO"))))` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B44` | `=IF(struct_state<>"OK",struct_state,IF(B43<>"OK",B43,IF(COUNT(inp_ncx,inp_nox,inp_scx,inp_sox)<>4,"REQUIERE DATOS",IF(NOT(AND(COUNT(inp_ncx,inp_nox,inp_scx,inp_sox)=4,MIN(inp_ncx,inp_nox)>=0,MOD(inp_ncx,1)=0,MOD(inp_nox,1)=0,MIN(inp_scx,inp_sox)>0)),"DATOS INVÁLIDOS",IF(AND(B39>=B32,B40>=B33,inp_scx<=geo_smax,OR(B31=0,inp_sox<=geo_smax),OR(B31>0,inp_nox=0),INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0))*100/inp_scx>=B41,OR(B31=0,INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0))*100/inp_sox>=B42)),zone_x_state,"NO CUMPLE")))))` | `=IF(struct_state<>"OK",struct_state,IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(As_tot_inf_x)),"REQUIERE DATOS",IF(As_tot_inf_x<=0.000001,"NO APLICA",IF(B43<>"OK",B43,IF(COUNT(inp_ncx,inp_nox,inp_scx,inp_sox)<>4,"REQUIERE DATOS",IF(NOT(AND(MIN(inp_ncx,inp_nox)>=0,MOD(inp_ncx,1)=0,MOD(inp_nox,1)=0,MIN(inp_scx,inp_sox)>0)),"DATOS INVÁLIDOS",IF(AND(B39>=B32,B40>=B33,inp_scx<=geo_smax,OR(B31=0,inp_sox<=geo_smax),OR(B31>0,inp_nox=0),INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0))*100/inp_scx>=B41,OR(B31=0,INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0))*100/inp_sox>=B42)),B156,"NO CUMPLE"))))))))` | 15.4.4: lógica idéntica para cada cara y dirección; valores no requeridos no bloquean. |
| ACERO_DETALLADO | `B49` | `=IF(geo_input_state="OK",IF(inp_by>=inp_bx,"LARGA / CUADRADA","CORTA"),"")` | `=IF(struct_state="OK",IF(inp_by>=inp_bx,"LARGA / CUADRADA","CORTA"),"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B50` | `=IF(struct_state="OK",flex_as_req_inf_y*inp_bx,"")` | `=As_tot_inf_y` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B53` | `=IF(struct_state="OK",IF(inp_by>=inp_bx,B50,steel_gamma*B50),"")` | `=IF(AND(struct_state="OK",ISNUMBER(B50)),IF(inp_by>=inp_bx,B50,steel_gamma*B50),"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B54` | `=IF(struct_state="OK",B50-B53,"")` | `=IF(AND(struct_state="OK",COUNT(B50,B53)=2),B50-B53,"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B58` | `=inp_ncy` | `=IF(ISNUMBER(inp_ncy),inp_ncy,"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B59` | `=inp_noy` | `=IF(ISNUMBER(inp_noy),inp_noy,"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B62` | `=IF(struct_state="OK",B53/B51,"")` | `=IF(AND(struct_state="OK",ISNUMBER(B53)),B53/B51,"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B63` | `=IF(struct_state="OK",IF(B52>0,B54/B52,0),"")` | `=IF(AND(struct_state="OK",ISNUMBER(B54)),IF(B52>0,B54/B52,0),"")` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B64` | `=IF(struct_state<>"OK",struct_state,IF(inp_by>=inp_bx,"OK",IF(ABS(inp_xc)+B51/2<=inp_bx/2,"OK","FUERA DEL ALCANCE IMPLEMENTADO")))` | `=IF(struct_state<>"OK",struct_state,IF(NOT(AND(ISNUMBER(As_tot_inf_y),As_tot_inf_y>0.000001)),"NO APLICA",IF(inp_by>=inp_bx,"OK",IF(ABS(inp_xc)+B51/2<=inp_bx/2,"OK","FUERA DEL ALCANCE IMPLEMENTADO"))))` | 15.4.4/10.5.4: distribución por cara, demanda total corregida y conteos reales. |
| ACERO_DETALLADO | `B65` | `=IF(struct_state<>"OK",struct_state,IF(B64<>"OK",B64,IF(COUNT(inp_ncy,inp_noy,inp_scy,inp_soy)<>4,"REQUIERE DATOS",IF(NOT(AND(COUNT(inp_ncy,inp_noy,inp_scy,inp_soy)=4,MIN(inp_ncy,inp_noy)>=0,MOD(inp_ncy,1)=0,MOD(inp_noy,1)=0,MIN(inp_scy,inp_soy)>0)),"DATOS INVÁLIDOS",IF(AND(B60>=B53,B61>=B54,inp_scy<=geo_smax,OR(B52=0,inp_soy<=geo_smax),OR(B52>0,inp_noy=0),INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0))*100/inp_scy>=B62,OR(B52=0,INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0))*100/inp_soy>=B63)),zone_y_state,"NO CUMPLE")))))` | `=IF(struct_state<>"OK",struct_state,IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(As_tot_inf_y)),"REQUIERE DATOS",IF(As_tot_inf_y<=0.000001,"NO APLICA",IF(B64<>"OK",B64,IF(COUNT(inp_ncy,inp_noy,inp_scy,inp_soy)<>4,"REQUIERE DATOS",IF(NOT(AND(MIN(inp_ncy,inp_noy)>=0,MOD(inp_ncy,1)=0,MOD(inp_noy,1)=0,MIN(inp_scy,inp_soy)>0)),"DATOS INVÁLIDOS",IF(AND(B60>=B53,B61>=B54,inp_scy<=geo_smax,OR(B52=0,inp_soy<=geo_smax),OR(B52>0,inp_noy=0),INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0))*100/inp_scy>=B62,OR(B52=0,INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0))*100/inp_soy>=B63)),B168,"NO CUMPLE"))))))))` | 15.4.4: lógica idéntica para cada cara y dirección; valores no requeridos no bloquean. |
| ACERO_DETALLADO | `B85` | `gamma_f Mu tf m` | `T local tf m` | Resumen de cuatro lados; detalle de caras/regiones en filas232:247. |
| ACERO_DETALLADO | `B86` | `=IF(punz_state="OK",PUNZONAMIENTO!B48,"")` | `=IF(local_model_state="OK",FLEXION_ACERO!D52,"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `B87:B88` | `=IF(punz_state="OK",PUNZONAMIENTO!B47,"")` | `=IF(local_model_state="OK",FLEXION_ACERO!D53,"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `B89` | `=IF(punz_state="OK",PUNZONAMIENTO!B47,"")` | `=IF(local_model_state="OK",FLEXION_ACERO!D55,"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `B91` | `=IF(punz_state<>"OK",punz_state,IF(COUNTIF(J86:J89,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(J86:J89,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(J86:J89,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(J86:J89,"REQUIERE DATOS")>0,"REQUIERE DATOS",IF(COUNTIF(J86:J89,"NO APLICA")=4,"NO APLICA","CUMPLE"))))))` | `=IF(punz_state<>"OK",punz_state,IF(local_eq_state<>"CUMPLE",local_eq_state,IF(COUNTIF(Q232:Q247,"NO APLICA")=16,"NO APLICA",IF(COUNTIF(Q232:Q247,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(Q232:Q247,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(Q232:Q247,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(Q232:Q247,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(Q232:Q247,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE"))))))))` | No hay local CUMPLE si faltan reparto validado, N o anclajes; verifica ambas regiones y capas aplicables. |
| ACERO_DETALLADO | `B92` | `INTERIOR / RECTA / 2 CAPAS` | `REPARTO FIRMADO / SIN MU ADICIONAL` | Reasignación de momento físico existente; no solución elástica automática de placa. |
| ACERO_DETALLADO | `B93` | `=IF(local_state="REQUIERE DATOS",IF(inp_local_detail="SI","","inp_local_detail=SI; ")&IF(LEN(inp_rec_lat)=0,"inp_rec_lat; ","")&IF(LEN(inp_epoxy)=0,"inp_epoxy; ","")&IF(LEN(inp_side_exposure)=0,"inp_side_exposure; ","")&IF(LEN(inp_end_inf)=0,"inp_end_inf; ","")&IF(LEN(inp_end_sup)=0,"inp_end_sup; ","")&IF(LEN(inp_agg)=0,"inp_agg; ","")&IF(LEN(inp_ncx)=0,"inp_ncx; ","")&IF(LEN(inp_nox)=0,"inp_nox; ","")&IF(LEN(inp_ncy)=0,"inp_ncy; ","")&IF(LEN(inp_noy)=0,"inp_noy; ","")&IF(LEN(inp_nloc_ix)=0,"inp_nloc_ix; ","")&IF(LEN(inp_nloc_iy)=0,"inp_nloc_iy; ","")&IF(LEN(inp_nloc_sx)=0,"inp_nloc_sx; ","")&IF(LEN(inp_nloc_sy)=0,"inp_nloc_sy; ","")&IF(LEN(inp_ll_ix_m)=0,"inp_ll_ix_m; ","")&IF(LEN(inp_ll_ix_p)=0,"inp_ll_ix_p; ","")&IF(LEN(inp_ll_iy_m)=0,"inp_ll_iy_m; ","")&IF(LEN(inp_ll_iy_p)=0,"inp_ll_iy_p; ","")&IF(LEN(inp_ll_sx_m)=0,"inp_ll_sx_m; ","")&IF(LEN(inp_ll_sx_p)=0,"inp_ll_sx_p; ","")&IF(LEN(inp_ll_sy_m)=0,"inp_ll_sy_m; ","")&IF(LEN(inp_ll_sy_p)=0,"inp_ll_sy_p; ",""),local_state)` | `=IF(local_state="REQUIERE DATOS",IF(local_model_state<>"OK",local_model_state,IF(inp_local_detail="SI","","inp_local_detail=SI; ")&IF(inp_repartition_ok="SI","","inp_repartition_ok=SI; ")&IF(LEN(inp_repartition_ref)=0,"inp_repartition_ref; ","")&IF(LEN(inp_rec_lat)=0,"inp_rec_lat; ","")&IF(LEN(inp_epoxy)=0,"inp_epoxy; ","")&IF(LEN(inp_side_exposure)=0,"inp_side_exposure; ","")&IF(LEN(inp_agg)=0,"inp_agg; ","")&IF(AND(ABS(PUNZONAMIENTO!B48)>0.000001,MAX(I232,I236)>0.000001,LEN(inp_nloc_ix)=0),"inp_nloc_ix; ","")&IF(AND(ABS(PUNZONAMIENTO!B48)>0.000001,MAX(I232,I236)>0.000001,LEN(inp_ll_ix_m)=0),"inp_ll_ix_m; ","")&IF(AND(ABS(PUNZONAMIENTO!B48)>0.000001,MAX(I232,I236)>0.000001,LEN(inp_ll_ix_p)=0),"inp_ll_ix_p; ","")&IF(AND(ABS(PUNZONAMIENTO!B48)>0.000001,MAX(I232,I236)>0.000001,LEN(inp_end_inf)=0),"inp_end_inf; ","")&IF(AND(ABS(PUNZONAMIENTO!B48)>0.000001,MAX(I233,I237)>0.000001,LEN(inp_nloc_sx)=0),"inp_nloc_sx; ","")&IF(AND(ABS(PUNZONAMIENTO!B48)>0.000001,MAX(I233,I237)>0.000001,LEN(inp_ll_sx_m)=0),"inp_ll_sx_m; ","")&IF(AND(ABS(PUNZONAMIENTO!B48)>0.000001,MAX(I233,I237)>0.000001,LEN(inp_ll_sx_p)=0),"inp_ll_sx_p; ","")&IF(AND(ABS(PUNZONAMIENTO!B48)>0.000001,MAX(I233,I237)>0.000001,LEN(inp_end_sup)=0),"inp_end_sup; ","")&IF(AND(ABS(PUNZONAMIENTO!B47)>0.000001,MAX(I240,I244)>0.000001,LEN(inp_nloc_iy)=0),"inp_nloc_iy; ","")&IF(AND(ABS(PUNZONAMIENTO!B47)>0.000001,MAX(I240,I244)>0.000001,LEN(inp_ll_iy_m)=0),"inp_ll_iy_m; ","")&IF(AND(ABS(PUNZONAMIENTO!B47)>0.000001,MAX(I240,I244)>0.000001,LEN(inp_ll_iy_p)=0),"inp_ll_iy_p; ","")&IF(AND(ABS(PUNZONAMIENTO!B47)>0.000001,MAX(I240,I244)>0.000001,LEN(inp_end_inf)=0),"inp_end_inf; ","")&IF(AND(ABS(PUNZONAMIENTO!B47)>0.000001,MAX(I241,I245)>0.000001,LEN(inp_nloc_sy)=0),"inp_nloc_sy; ","")&IF(AND(ABS(PUNZONAMIENTO!B47)>0.000001,MAX(I241,I245)>0.000001,LEN(inp_ll_sy_m)=0),"inp_ll_sy_m; ","")&IF(AND(ABS(PUNZONAMIENTO!B47)>0.000001,MAX(I241,I245)>0.000001,LEN(inp_ll_sy_p)=0),"inp_ll_sy_p; ","")&IF(AND(ABS(PUNZONAMIENTO!B47)>0.000001,MAX(I241,I245)>0.000001,LEN(inp_end_sup)=0),"inp_end_sup; ","")),local_state)` | Diagnóstico condicionado a capas/regiones requeridas; no pide superior solo por magnitud de M. |
| ACERO_DETALLADO | `B152` | `=IF(struct_state="OK",B42*B148,"")` | `=IF(AND(struct_state="OK",ISNUMBER(B42)),B42*B148,"")` | Reutiliza controles físicos de zonas, actualizados a la demanda de cara. |
| ACERO_DETALLADO | `B153` | `=IF(struct_state="OK",B42*B149,"")` | `=IF(AND(struct_state="OK",ISNUMBER(B42)),B42*B149,"")` | Reutiliza controles físicos de zonas, actualizados a la demanda de cara. |
| ACERO_DETALLADO | `B156` | `=IF(struct_state<>"OK",struct_state,IF(B43<>"OK",B43,IF(COUNT(inp_ncx,inp_scx,inp_rec_lat)<>3,"REQUIERE DATOS",IF(NOT(AND(inp_ncx>=1,(inp_ncx-1)*inp_scx<=B30*100-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))-IF(inp_bx>=inp_by,2*inp_rec_lat,0))),"NO CUMPLE",IF(B31=0,"CUMPLE",IF(COUNT(inp_nox_minus,inp_nox_plus,inp_nox,inp_sox)<>4,"REQUIERE DATOS",IF(AND(inp_nox=inp_nox_minus+inp_nox_plus,B154>=B152,B155>=B153,OR(inp_nox_minus=0,(inp_nox_minus-1)*inp_sox<=B148*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))/2),OR(inp_nox_plus=0,(inp_nox_plus-1)*inp_sox<=B149*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))/2)),"CUMPLE","NO CUMPLE")))))))` | `=IF(struct_state<>"OK",struct_state,IF(NOT(ISNUMBER(As_tot_inf_x)),"REQUIERE DATOS",IF(As_tot_inf_x<=0.000001,"NO APLICA",IF(B43<>"OK",B43,IF(COUNT(inp_ncx,inp_scx,inp_rec_lat)<>3,"REQUIERE DATOS",IF(NOT(AND(inp_ncx>=1,(inp_ncx-1)*inp_scx<=B30*100-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))-IF(inp_bx>=inp_by,2*inp_rec_lat,0))),"NO CUMPLE",IF(B31=0,"CUMPLE",IF(COUNT(inp_nox_minus,inp_nox_plus,inp_nox,inp_sox)<>4,"REQUIERE DATOS",IF(AND(inp_nox=inp_nox_minus+inp_nox_plus,B154>=B152,B155>=B153,OR(inp_nox_minus=0,(inp_nox_minus-1)*inp_sox<=B148*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))/2),OR(inp_nox_plus=0,(inp_nox_plus-1)*inp_sox<=B149*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))/2)),"CUMPLE","NO CUMPLE")))))))))` | No se exige una parrilla sin demanda; conteos/posiciones si corresponde. |
| ACERO_DETALLADO | `B164` | `=IF(struct_state="OK",B63*B160,"")` | `=IF(AND(struct_state="OK",ISNUMBER(B63)),B63*B160,"")` | Reutiliza controles físicos de zonas, actualizados a la demanda de cara. |
| ACERO_DETALLADO | `B165` | `=IF(struct_state="OK",B63*B161,"")` | `=IF(AND(struct_state="OK",ISNUMBER(B63)),B63*B161,"")` | Reutiliza controles físicos de zonas, actualizados a la demanda de cara. |
| ACERO_DETALLADO | `B168` | `=IF(struct_state<>"OK",struct_state,IF(B64<>"OK",B64,IF(COUNT(inp_ncy,inp_scy,inp_rec_lat)<>3,"REQUIERE DATOS",IF(NOT(AND(inp_ncy>=1,(inp_ncy-1)*inp_scy<=B51*100-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))-IF(inp_by>=inp_bx,2*inp_rec_lat,0))),"NO CUMPLE",IF(B52=0,"CUMPLE",IF(COUNT(inp_noy_minus,inp_noy_plus,inp_noy,inp_soy)<>4,"REQUIERE DATOS",IF(AND(inp_noy=inp_noy_minus+inp_noy_plus,B166>=B164,B167>=B165,OR(inp_noy_minus=0,(inp_noy_minus-1)*inp_soy<=B160*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))/2),OR(inp_noy_plus=0,(inp_noy_plus-1)*inp_soy<=B161*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))/2)),"CUMPLE","NO CUMPLE")))))))` | `=IF(struct_state<>"OK",struct_state,IF(NOT(ISNUMBER(As_tot_inf_y)),"REQUIERE DATOS",IF(As_tot_inf_y<=0.000001,"NO APLICA",IF(B64<>"OK",B64,IF(COUNT(inp_ncy,inp_scy,inp_rec_lat)<>3,"REQUIERE DATOS",IF(NOT(AND(inp_ncy>=1,(inp_ncy-1)*inp_scy<=B51*100-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))-IF(inp_by>=inp_bx,2*inp_rec_lat,0))),"NO CUMPLE",IF(B52=0,"CUMPLE",IF(COUNT(inp_noy_minus,inp_noy_plus,inp_noy,inp_soy)<>4,"REQUIERE DATOS",IF(AND(inp_noy=inp_noy_minus+inp_noy_plus,B166>=B164,B167>=B165,OR(inp_noy_minus=0,(inp_noy_minus-1)*inp_soy<=B160*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))/2),OR(inp_noy_plus=0,(inp_noy_plus-1)*inp_soy<=B161*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))/2)),"CUMPLE","NO CUMPLE")))))))))` | No se exige una parrilla sin demanda; conteos/posiciones si corresponde. |
| ACERO_DETALLADO | `B173` | `=IF(struct_state="OK",OR(MAX(FLEXION_ACERO!D7:D8)>0,MAX(ABS(ult_mx),ABS(ult_my))>0.000001,IF(punz_state="OK",MAX(ABS(PUNZONAMIENTO!B47),ABS(PUNZONAMIENTO!B48))>0.000001,FALSE)),FALSE)` | `=IF(struct_state="OK",OR(IF(ISNUMBER(As_tot_sup_x),As_tot_sup_x>0.000001,FALSE),IF(ISNUMBER(As_tot_sup_y),As_tot_sup_y>0.000001,FALSE)),FALSE)` | Superior requerido por demanda firmada o mínimo deliberadamente asignado, no gamma absoluto de ambas capas. |
| ACERO_DETALLADO | `B181` | `(vacía)` | `=IF(struct_state="OK",IF(inp_bx>=inp_by,"LARGA / CUADRADA","CORTA"),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B182` | `(vacía)` | `=As_tot_sup_x` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B183` | `(vacía)` | `=IF(struct_state="OK",IF(inp_bx>=inp_by,inp_by,steel_B),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B184` | `(vacía)` | `=IF(struct_state="OK",inp_by-B183,"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B185` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B182)),IF(inp_bx>=inp_by,B182,steel_gamma*B182),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B186` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(B182,B185)=2),B182-B185,"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B187` | `(vacía)` | `=inp_bar_sup_x` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B188` | `(vacía)` | `=inp_sc_sx` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B189` | `(vacía)` | `=inp_so_sx` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B190` | `(vacía)` | `=IF(ISNUMBER(inp_nc_sx),inp_nc_sx,"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B191` | `(vacía)` | `=IF(ISNUMBER(inp_no_sx),inp_no_sx,"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B192` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_nc_sx),inp_nc_sx>=0),inp_nc_sx*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B193` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_no_sx),inp_no_sx>=0),inp_no_sx*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B194` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B185)),B185/B183,"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B195` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B186)),IF(B184>0,B186/B184,0),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B196` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(NOT(AND(ISNUMBER(As_tot_sup_x),As_tot_sup_x>0.000001)),"NO APLICA",IF(inp_bx>=inp_by,"OK",IF(ABS(inp_yc)+B183/2<=inp_by/2,"OK","FUERA DEL ALCANCE IMPLEMENTADO"))))` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B197` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(As_tot_sup_x)),"REQUIERE DATOS",IF(As_tot_sup_x<=0.000001,"NO APLICA",IF(B196<>"OK",B196,IF(COUNT(inp_nc_sx,inp_no_sx,inp_sc_sx,inp_so_sx)<>4,"REQUIERE DATOS",IF(NOT(AND(MIN(inp_nc_sx,inp_no_sx)>=0,MOD(inp_nc_sx,1)=0,MOD(inp_no_sx,1)=0,MIN(inp_sc_sx,inp_so_sx)>0)),"DATOS INVÁLIDOS",IF(AND(B192>=B185,B193>=B186,inp_sc_sx<=geo_smax,OR(B184=0,inp_so_sx<=geo_smax),OR(B184>0,inp_no_sx=0),INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0))*100/inp_sc_sx>=B194,OR(B184=0,INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0))*100/inp_so_sx>=B195)),B290,"NO CUMPLE"))))))))` | 15.4.4, cantidad y separaciones/ubicación reales. |
| ACERO_DETALLADO | `B203` | `(vacía)` | `=IF(struct_state="OK",IF(inp_by>=inp_bx,"LARGA / CUADRADA","CORTA"),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B204` | `(vacía)` | `=As_tot_sup_y` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B205` | `(vacía)` | `=IF(struct_state="OK",IF(inp_by>=inp_bx,inp_bx,steel_B),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B206` | `(vacía)` | `=IF(struct_state="OK",inp_bx-B205,"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B207` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B204)),IF(inp_by>=inp_bx,B204,steel_gamma*B204),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B208` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(B204,B207)=2),B204-B207,"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B209` | `(vacía)` | `=inp_bar_sup_y` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B210` | `(vacía)` | `=inp_sc_sy` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B211` | `(vacía)` | `=inp_so_sy` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B212` | `(vacía)` | `=IF(ISNUMBER(inp_nc_sy),inp_nc_sy,"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B213` | `(vacía)` | `=IF(ISNUMBER(inp_no_sy),inp_no_sy,"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B214` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_nc_sy),inp_nc_sy>=0),inp_nc_sy*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B215` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_no_sy),inp_no_sy>=0),inp_no_sy*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B216` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B207)),B207/B205,"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B217` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B208)),IF(B206>0,B208/B206,0),"")` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B218` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(NOT(AND(ISNUMBER(As_tot_sup_y),As_tot_sup_y>0.000001)),"NO APLICA",IF(inp_by>=inp_bx,"OK",IF(ABS(inp_xc)+B205/2<=inp_bx/2,"OK","FUERA DEL ALCANCE IMPLEMENTADO"))))` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `B219` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(As_tot_sup_y)),"REQUIERE DATOS",IF(As_tot_sup_y<=0.000001,"NO APLICA",IF(B218<>"OK",B218,IF(COUNT(inp_nc_sy,inp_no_sy,inp_sc_sy,inp_so_sy)<>4,"REQUIERE DATOS",IF(NOT(AND(MIN(inp_nc_sy,inp_no_sy)>=0,MOD(inp_nc_sy,1)=0,MOD(inp_no_sy,1)=0,MIN(inp_sc_sy,inp_so_sy)>0)),"DATOS INVÁLIDOS",IF(AND(B214>=B207,B215>=B208,inp_sc_sy<=geo_smax,OR(B206=0,inp_so_sy<=geo_smax),OR(B206>0,inp_no_sy=0),INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0))*100/inp_sc_sy>=B216,OR(B206=0,INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0))*100/inp_so_sy>=B217)),B302,"NO CUMPLE"))))))))` | 15.4.4, cantidad y separaciones/ubicación reales. |
| ACERO_DETALLADO | `B231` | `(vacía)` | `Cara` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `B232` | `(vacía)` | `INF` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B233` | `(vacía)` | `SUP` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B234` | `(vacía)` | `INF` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B235` | `(vacía)` | `SUP` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B236` | `(vacía)` | `INF` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B237` | `(vacía)` | `SUP` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B238` | `(vacía)` | `INF` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B239` | `(vacía)` | `SUP` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B240` | `(vacía)` | `INF` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B241` | `(vacía)` | `SUP` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B242` | `(vacía)` | `INF` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B243` | `(vacía)` | `SUP` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B244` | `(vacía)` | `INF` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B245` | `(vacía)` | `SUP` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B246` | `(vacía)` | `INF` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B247` | `(vacía)` | `SUP` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `B251` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(flex_as_req_inf_x)),IF(local_model_state="OK",IF(ABS(PUNZONAMIENTO!B48)>0.000001,IF(COUNT(I232,I236,I234,I238)=4,MAX(flex_as_req_inf_x*inp_by,MAX(I232,I236)+MAX(I234,I238)),""),flex_as_req_inf_x*inp_by),flex_as_req_inf_x*inp_by),"")` | MAX(global, suma de regiones locales). No suma global+gamma_fMu. |
| ACERO_DETALLADO | `B252` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(flex_as_req_inf_y)),IF(local_model_state="OK",IF(ABS(PUNZONAMIENTO!B47)>0.000001,IF(COUNT(I240,I244,I242,I246)=4,MAX(flex_as_req_inf_y*inp_bx,MAX(I240,I244)+MAX(I242,I246)),""),flex_as_req_inf_y*inp_bx),flex_as_req_inf_y*inp_bx),"")` | MAX(global, suma de regiones locales). No suma global+gamma_fMu. |
| ACERO_DETALLADO | `B253` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(flex_as_req_sup_x)),IF(local_model_state="OK",IF(ABS(PUNZONAMIENTO!B48)>0.000001,IF(COUNT(I233,I237,I235,I239)=4,MAX(flex_as_req_sup_x*inp_by,MAX(I233,I237)+MAX(I235,I239)),""),flex_as_req_sup_x*inp_by),flex_as_req_sup_x*inp_by),"")` | MAX(global, suma de regiones locales). No suma global+gamma_fMu. |
| ACERO_DETALLADO | `B254` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(flex_as_req_sup_y)),IF(local_model_state="OK",IF(ABS(PUNZONAMIENTO!B47)>0.000001,IF(COUNT(I241,I245,I243,I247)=4,MAX(flex_as_req_sup_y*inp_bx,MAX(I241,I245)+MAX(I243,I247)),""),flex_as_req_sup_y*inp_bx),flex_as_req_sup_y*inp_bx),"")` | MAX(global, suma de regiones locales). No suma global+gamma_fMu. |
| ACERO_DETALLADO | `B261` | `(vacía)` | `As min total cm2` | Mínimo total por dirección. |
| ACERO_DETALLADO | `B262` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(rho_eff)),rho_eff*inp_by*100*inp_h*100,"")` | 10.5.4: As_inf+As_sup >= As mínimo total; no duplicación del mínimo de9.7. |
| ACERO_DETALLADO | `B263` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(rho_eff)),rho_eff*inp_bx*100*inp_h*100,"")` | 10.5.4: As_inf+As_sup >= As mínimo total; no duplicación del mínimo de9.7. |
| ACERO_DETALLADO | `B264` | `(vacía)` | `=IF(COUNTIF(F262:F263,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(F262:F263,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(F262:F263,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(F262:F263,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(F262:F263,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))` | Pisos por cara comprobados en flexión/regiones; total real aquí. |
| ACERO_DETALLADO | `B266` | `(vacía)` | `=IF(NOT(ISNUMBER(As_tot_inf_x)),"",IF(As_tot_inf_x<=0.000001,0,IF(COUNT(inp_ncx,inp_nox)=2,inp_ncx+inp_nox,"")))` | Conteo total confirmado de la cara; no convierte faltante aplicable en cero. |
| ACERO_DETALLADO | `B267` | `(vacía)` | `=IF(NOT(ISNUMBER(As_tot_sup_x)),"",IF(As_tot_sup_x<=0.000001,0,IF(COUNT(inp_nc_sx,inp_no_sx)=2,inp_nc_sx+inp_no_sx,"")))` | Conteo total confirmado de la cara; no convierte faltante aplicable en cero. |
| ACERO_DETALLADO | `B268` | `(vacía)` | `=IF(NOT(ISNUMBER(As_tot_inf_y)),"",IF(As_tot_inf_y<=0.000001,0,IF(COUNT(inp_ncy,inp_noy)=2,inp_ncy+inp_noy,"")))` | Conteo total confirmado de la cara; no convierte faltante aplicable en cero. |
| ACERO_DETALLADO | `B269` | `(vacía)` | `=IF(NOT(ISNUMBER(As_tot_sup_y)),"",IF(As_tot_sup_y<=0.000001,0,IF(COUNT(inp_nc_sy,inp_no_sy)=2,inp_nc_sy+inp_no_sy,"")))` | Conteo total confirmado de la cara; no convierte faltante aplicable en cero. |
| ACERO_DETALLADO | `B282` | `(vacía)` | `=IF(struct_state="OK",IF(inp_bx>=inp_by,0,inp_by/2+inp_yc-B183/2),"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B283` | `(vacía)` | `=IF(struct_state="OK",IF(inp_bx>=inp_by,0,inp_by/2-inp_yc-B183/2),"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B284` | `(vacía)` | `=IF(ISNUMBER(inp_no_sx_minus),inp_no_sx_minus,"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B285` | `(vacía)` | `=IF(ISNUMBER(inp_no_sx_plus),inp_no_sx_plus,"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B286` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B195)),B195*B282,"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B287` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B195)),B195*B283,"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B288` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_no_sx_minus)),inp_no_sx_minus*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B289` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_no_sx_plus)),inp_no_sx_plus*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B290` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(NOT(ISNUMBER(As_tot_sup_x)),"REQUIERE DATOS",IF(As_tot_sup_x<=0.000001,"NO APLICA",IF(B196<>"OK",B196,IF(COUNT(inp_nc_sx,inp_sc_sx,inp_rec_lat)<>3,"REQUIERE DATOS",IF(NOT(AND(inp_nc_sx>=1,(inp_nc_sx-1)*inp_sc_sx<=B183*100-INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))-IF(inp_bx>=inp_by,2*inp_rec_lat,0))),"NO CUMPLE",IF(B184=0,"CUMPLE",IF(COUNT(inp_no_sx_minus,inp_no_sx_plus,inp_no_sx,inp_so_sx)<>4,"REQUIERE DATOS",IF(AND(inp_no_sx=inp_no_sx_minus+inp_no_sx_plus,B288>=B286,B289>=B287,OR(inp_no_sx_minus=0,(inp_no_sx_minus-1)*inp_so_sx<=B282*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))/2),OR(inp_no_sx_plus=0,(inp_no_sx_plus-1)*inp_so_sx<=B283*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))/2)),"CUMPLE","NO CUMPLE")))))))))` | No acredita un N que no cabe; ambos lados del exterior. |
| ACERO_DETALLADO | `B294` | `(vacía)` | `=IF(struct_state="OK",IF(inp_by>=inp_bx,0,inp_bx/2+inp_xc-B205/2),"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B295` | `(vacía)` | `=IF(struct_state="OK",IF(inp_by>=inp_bx,0,inp_bx/2-inp_xc-B205/2),"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B296` | `(vacía)` | `=IF(ISNUMBER(inp_no_sy_minus),inp_no_sy_minus,"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B297` | `(vacía)` | `=IF(ISNUMBER(inp_no_sy_plus),inp_no_sy_plus,"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B298` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B217)),B217*B294,"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B299` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B217)),B217*B295,"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B300` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_no_sy_minus)),inp_no_sy_minus*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B301` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_no_sy_plus)),inp_no_sy_plus*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `B302` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(NOT(ISNUMBER(As_tot_sup_y)),"REQUIERE DATOS",IF(As_tot_sup_y<=0.000001,"NO APLICA",IF(B218<>"OK",B218,IF(COUNT(inp_nc_sy,inp_sc_sy,inp_rec_lat)<>3,"REQUIERE DATOS",IF(NOT(AND(inp_nc_sy>=1,(inp_nc_sy-1)*inp_sc_sy<=B205*100-INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))-IF(inp_by>=inp_bx,2*inp_rec_lat,0))),"NO CUMPLE",IF(B206=0,"CUMPLE",IF(COUNT(inp_no_sy_minus,inp_no_sy_plus,inp_no_sy,inp_so_sy)<>4,"REQUIERE DATOS",IF(AND(inp_no_sy=inp_no_sy_minus+inp_no_sy_plus,B300>=B298,B301>=B299,OR(inp_no_sy_minus=0,(inp_no_sy_minus-1)*inp_so_sy<=B294*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))/2),OR(inp_no_sy_plus=0,(inp_no_sy_plus-1)*inp_so_sy<=B295*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))/2)),"CUMPLE","NO CUMPLE")))))))))` | No acredita un N que no cabe; ambos lados del exterior. |
| ACERO_DETALLADO | `C86` | `=IF(punz_state="OK",PUNZONAMIENTO!B56*100,"")` | `=IF(local_model_state="OK",FLEXION_ACERO!L52*100,"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `C87:C88` | `=IF(punz_state="OK",PUNZONAMIENTO!B55*100,"")` | `=IF(local_model_state="OK",FLEXION_ACERO!L53*100,"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `C89` | `=IF(punz_state="OK",PUNZONAMIENTO!B55*100,"")` | `=IF(local_model_state="OK",FLEXION_ACERO!L55*100,"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `C181` | `(vacía)` | `-` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C182` | `(vacía)` | `cm2` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C183:C184` | `(vacía)` | `m` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C185:C186` | `(vacía)` | `cm2` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C187` | `(vacía)` | `-` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C188:C189` | `(vacía)` | `cm` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C190:C191` | `(vacía)` | `-` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C192:C193` | `(vacía)` | `cm2` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C194:C195` | `(vacía)` | `cm2/m` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C196` | `(vacía)` | `-` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C197` | `(vacía)` | `-` | 15.4.4, cantidad y separaciones/ubicación reales. |
| ACERO_DETALLADO | `C203` | `(vacía)` | `-` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C204` | `(vacía)` | `cm2` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C205:C206` | `(vacía)` | `m` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C207:C208` | `(vacía)` | `cm2` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C209` | `(vacía)` | `-` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C210:C211` | `(vacía)` | `cm` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C212:C213` | `(vacía)` | `-` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C214:C215` | `(vacía)` | `cm2` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C216:C217` | `(vacía)` | `cm2/m` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C218` | `(vacía)` | `-` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `C219` | `(vacía)` | `-` | 15.4.4, cantidad y separaciones/ubicación reales. |
| ACERO_DETALLADO | `C231` | `(vacía)` | `Mu firmado tf m` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `C232` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!F52,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C233` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!F52,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C234` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!G52,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C235` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!G52,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C236` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!F53,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C237` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!F53,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C238` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!G53,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C239` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!G53,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C240` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!F54,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C241` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!F54,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C242` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!G54,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C243` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!G54,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C244` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!F55,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C245` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!F55,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C246` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!G55,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C247` | `(vacía)` | `=IF(local_model_state="OK",FLEXION_ACERO!G55,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `C251:C254` | `(vacía)` | `cm2` | MAX(global, suma de regiones locales). No suma global+gamma_fMu. |
| ACERO_DETALLADO | `C261` | `(vacía)` | `As real inf cm2` | Mínimo total por dirección. |
| ACERO_DETALLADO | `C262` | `(vacía)` | `=IF(ISNUMBER(n_total_inf_x),n_total_inf_x*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | 10.5.4: As_inf+As_sup >= As mínimo total; no duplicación del mínimo de9.7. |
| ACERO_DETALLADO | `C263` | `(vacía)` | `=IF(ISNUMBER(n_total_inf_y),n_total_inf_y*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | 10.5.4: As_inf+As_sup >= As mínimo total; no duplicación del mínimo de9.7. |
| ACERO_DETALLADO | `C264` | `(vacía)` | `-` | Pisos por cara comprobados en flexión/regiones; total real aquí. |
| ACERO_DETALLADO | `C266:C269` | `(vacía)` | `barras` | Conteo total confirmado de la cara; no convierte faltante aplicable en cero. |
| ACERO_DETALLADO | `C282:C283` | `(vacía)` | `m` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `C284:C285` | `(vacía)` | `barras` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `C286:C289` | `(vacía)` | `cm2` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `C290` | `(vacía)` | `-` | No acredita un N que no cabe; ambos lados del exterior. |
| ACERO_DETALLADO | `C294:C295` | `(vacía)` | `m` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `C296:C297` | `(vacía)` | `barras` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `C298:C301` | `(vacía)` | `cm2` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `C302` | `(vacía)` | `-` | No acredita un N que no cabe; ambos lados del exterior. |
| ACERO_DETALLADO | `D75` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(inp_epoxy="SIN EPOXI",1,IF(OR(MIN((FLEXION_ACERO!E7)-B75/2,inp_h*100-(FLEXION_ACERO!E7)-B75/2,inp_rec_lat)<3*B75,inp_sep_sup_x-B75<6*B75),1.5,1.2)),"")` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(inp_epoxy="SIN EPOXI",1,IF(OR(MIN((FLEXION_ACERO!E7)-B75/2,inp_h*100-(FLEXION_ACERO!E7)-B75/2,inp_rec_lat)<3*B75,MIN(inp_sep_sup_x,inp_sc_sx,inp_so_sx)-B75<6*B75),1.5,1.2)),"")` | Espaciamiento regional superior participa en cb, psi_e y separación libre. |
| ACERO_DETALLADO | `D76` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(inp_epoxy="SIN EPOXI",1,IF(OR(MIN((FLEXION_ACERO!E8)-B76/2,inp_h*100-(FLEXION_ACERO!E8)-B76/2,inp_rec_lat)<3*B76,inp_sep_sup_y-B76<6*B76),1.5,1.2)),"")` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(inp_epoxy="SIN EPOXI",1,IF(OR(MIN((FLEXION_ACERO!E8)-B76/2,inp_h*100-(FLEXION_ACERO!E8)-B76/2,inp_rec_lat)<3*B76,MIN(inp_sep_sup_y,inp_sc_sy,inp_so_sy)-B76<6*B76),1.5,1.2)),"")` | Espaciamiento regional superior participa en cb, psi_e y separación libre. |
| ACERO_DETALLADO | `D85` | `Mu combinado tf m` | `Mu franja tf m` | Resumen de cuatro lados; detalle de caras/regiones en filas232:247. |
| ACERO_DETALLADO | `D86:D89` | `=IF(punz_state="OK",ABS(B86)+FLEXION_ACERO!D5*C86/100,"")` | `=IF(local_model_state="OK",FLEXION_ACERO!F52,"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `D92` | `Ambas capas resisten conservadoramente la magnitud local más demanda global; sin reparto único entre signos.` | `M_franja+M_fuera=M_cara; T+−T-=gamma_fM. Necesita referencia del análisis que valida el reparto.` | Equilibrio y alcance de redistribución estática explícitos. |
| ACERO_DETALLADO | `D181:D196` | `(vacía)` | `15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0.` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `D197` | `(vacía)` | `15.4.4, cantidad y separaciones/ubicación reales.` | 15.4.4, cantidad y separaciones/ubicación reales. |
| ACERO_DETALLADO | `D203:D218` | `(vacía)` | `15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0.` | 15.4.4: misma lógica para cara inferior/superior. NO APLICA si As requerido=0. |
| ACERO_DETALLADO | `D219` | `(vacía)` | `15.4.4, cantidad y separaciones/ubicación reales.` | 15.4.4, cantidad y separaciones/ubicación reales. |
| ACERO_DETALLADO | `D231` | `(vacía)` | `Mu cara tf m` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `D232` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,C232),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D233` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,-C233),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D234` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,C234),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D235` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,-C235),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D236` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,C236),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D237` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,-C237),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D238` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,C238),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D239` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,-C239),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D240` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,C240),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D241` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,-C241),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D242` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,C242),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D243` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,-C243),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D244` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,C244),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D245` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,-C245),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D246` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,C246),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D247` | `(vacía)` | `=IF(local_model_state="OK",MAX(0,-C247),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `D251:D254` | `(vacía)` | `MAX(global, suma de regiones locales). No suma global+gamma_fMu.` | MAX(global, suma de regiones locales). No suma global+gamma_fMu. |
| ACERO_DETALLADO | `D261` | `(vacía)` | `As real sup cm2` | Mínimo total por dirección. |
| ACERO_DETALLADO | `D262` | `(vacía)` | `=IF(ISNUMBER(n_total_sup_x),n_total_sup_x*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | 10.5.4: As_inf+As_sup >= As mínimo total; no duplicación del mínimo de9.7. |
| ACERO_DETALLADO | `D263` | `(vacía)` | `=IF(ISNUMBER(n_total_sup_y),n_total_sup_y*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | 10.5.4: As_inf+As_sup >= As mínimo total; no duplicación del mínimo de9.7. |
| ACERO_DETALLADO | `D264` | `(vacía)` | `Pisos por cara comprobados en flexión/regiones; total real aquí.` | Pisos por cara comprobados en flexión/regiones; total real aquí. |
| ACERO_DETALLADO | `D266:D269` | `(vacía)` | `Conteo total confirmado de la cara; no convierte faltante aplicable en cero.` | Conteo total confirmado de la cara; no convierte faltante aplicable en cero. |
| ACERO_DETALLADO | `D282:D289` | `(vacía)` | `Ubicación física por ambos extremos de la franja.` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `D290` | `(vacía)` | `No acredita un N que no cabe; ambos lados del exterior.` | No acredita un N que no cabe; ambos lados del exterior. |
| ACERO_DETALLADO | `D294:D301` | `(vacía)` | `Ubicación física por ambos extremos de la franja.` | Ubicación física por ambos extremos de la franja. |
| ACERO_DETALLADO | `D302` | `(vacía)` | `No acredita un N que no cabe; ambos lados del exterior.` | No acredita un N que no cabe; ambos lados del exterior. |
| ACERO_DETALLADO | `E5:E8` | `=IF(struct_state="OK",IF(D5<=0,"No requerido",C5*100/D5),"")` | `=IF(AND(struct_state="OK",ISNUMBER(D5)),IF(D5<=0,"No requerido",C5*100/D5),"")` | No dividir entre una demanda vacía por grado o reparto mínimo pendiente. |
| ACERO_DETALLADO | `E85` | `d cm` | `Cara traccionada` | Resumen de cuatro lados; detalle de caras/regiones en filas232:247. |
| ACERO_DETALLADO | `E86:E89` | `=IF(punz_state="OK",FLEXION_ACERO!E5,"")` | `=IF(local_model_state="OK",FLEXION_ACERO!H52,"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `E231` | `(vacía)` | `Ancho cm` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `E232` | `(vacía)` | `=IF(local_model_state="OK",PUNZONAMIENTO!B56*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E233` | `(vacía)` | `=IF(local_model_state="OK",PUNZONAMIENTO!B56*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E234` | `(vacía)` | `=IF(local_model_state="OK",(inp_by-PUNZONAMIENTO!B56)*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E235` | `(vacía)` | `=IF(local_model_state="OK",(inp_by-PUNZONAMIENTO!B56)*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E236` | `(vacía)` | `=IF(local_model_state="OK",PUNZONAMIENTO!B56*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E237` | `(vacía)` | `=IF(local_model_state="OK",PUNZONAMIENTO!B56*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E238` | `(vacía)` | `=IF(local_model_state="OK",(inp_by-PUNZONAMIENTO!B56)*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E239` | `(vacía)` | `=IF(local_model_state="OK",(inp_by-PUNZONAMIENTO!B56)*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E240` | `(vacía)` | `=IF(local_model_state="OK",PUNZONAMIENTO!B55*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E241` | `(vacía)` | `=IF(local_model_state="OK",PUNZONAMIENTO!B55*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E242` | `(vacía)` | `=IF(local_model_state="OK",(inp_bx-PUNZONAMIENTO!B55)*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E243` | `(vacía)` | `=IF(local_model_state="OK",(inp_bx-PUNZONAMIENTO!B55)*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E244` | `(vacía)` | `=IF(local_model_state="OK",PUNZONAMIENTO!B55*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E245` | `(vacía)` | `=IF(local_model_state="OK",PUNZONAMIENTO!B55*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E246` | `(vacía)` | `=IF(local_model_state="OK",(inp_bx-PUNZONAMIENTO!B55)*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E247` | `(vacía)` | `=IF(local_model_state="OK",(inp_bx-PUNZONAMIENTO!B55)*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `E261` | `(vacía)` | `As real total cm2` | Mínimo total por dirección. |
| ACERO_DETALLADO | `E262:E263` | `(vacía)` | `=IF(COUNT(C262:D262)=2,SUM(C262:D262),"")` | 10.5.4: As_inf+As_sup >= As mínimo total; no duplicación del mínimo de9.7. |
| ACERO_DETALLADO | `F75` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,inp_rec_lat>=0),MIN((FLEXION_ACERO!E7),inp_h*100-(FLEXION_ACERO!E7),inp_rec_lat+B75/2,(inp_sep_sup_x)/2),"")` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,inp_rec_lat>=0),MIN((FLEXION_ACERO!E7),inp_h*100-(FLEXION_ACERO!E7),inp_rec_lat+B75/2,(MIN(inp_sep_sup_x,inp_sc_sx,inp_so_sx))/2),"")` | Espaciamiento regional superior participa en cb, psi_e y separación libre. |
| ACERO_DETALLADO | `F76` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,inp_rec_lat>=0),MIN((FLEXION_ACERO!E8),inp_h*100-(FLEXION_ACERO!E8),inp_rec_lat+B76/2,(inp_sep_sup_y)/2),"")` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,inp_rec_lat>=0),MIN((FLEXION_ACERO!E8),inp_h*100-(FLEXION_ACERO!E8),inp_rec_lat+B76/2,(MIN(inp_sep_sup_y,inp_sc_sy,inp_so_sy))/2),"")` | Espaciamiento regional superior participa en cb, psi_e y separación libre. |
| ACERO_DETALLADO | `F86` | `=IF(punz_state="OK",IF(ABS(B86)<=0.000001,0,IF((inp_fy*E86)^2-4*(inp_fy^2/(2*0.85*inp_fc*C86))*(D86*100000/inp_phi_f)<0,"",MAX(rho_eff*C86*inp_h*100,(inp_fy*E86-SQRT((inp_fy*E86)^2-4*(inp_fy^2/(2*0.85*inp_fc*C86))*(D86*100000/inp_phi_f)))/(2*(inp_fy^2/(2*0.85*inp_fc*C86)))))),"")` | `=IF(local_model_state="OK",IF(E86="SUPERIOR",I233,I232),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `F87` | `=IF(punz_state="OK",IF(ABS(B87)<=0.000001,0,IF((inp_fy*E87)^2-4*(inp_fy^2/(2*0.85*inp_fc*C87))*(D87*100000/inp_phi_f)<0,"",MAX(rho_eff*C87*inp_h*100,(inp_fy*E87-SQRT((inp_fy*E87)^2-4*(inp_fy^2/(2*0.85*inp_fc*C87))*(D87*100000/inp_phi_f)))/(2*(inp_fy^2/(2*0.85*inp_fc*C87)))))),"")` | `=IF(local_model_state="OK",IF(E87="SUPERIOR",I237,I236),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `F88` | `=IF(punz_state="OK",IF(ABS(B88)<=0.000001,0,IF((inp_fy*E88)^2-4*(inp_fy^2/(2*0.85*inp_fc*C88))*(D88*100000/inp_phi_f)<0,"",MAX(rho_eff*C88*inp_h*100,(inp_fy*E88-SQRT((inp_fy*E88)^2-4*(inp_fy^2/(2*0.85*inp_fc*C88))*(D88*100000/inp_phi_f)))/(2*(inp_fy^2/(2*0.85*inp_fc*C88)))))),"")` | `=IF(local_model_state="OK",IF(E88="SUPERIOR",I241,I240),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `F89` | `=IF(punz_state="OK",IF(ABS(B89)<=0.000001,0,IF((inp_fy*E89)^2-4*(inp_fy^2/(2*0.85*inp_fc*C89))*(D89*100000/inp_phi_f)<0,"",MAX(rho_eff*C89*inp_h*100,(inp_fy*E89-SQRT((inp_fy*E89)^2-4*(inp_fy^2/(2*0.85*inp_fc*C89))*(D89*100000/inp_phi_f)))/(2*(inp_fy^2/(2*0.85*inp_fc*C89)))))),"")` | `=IF(local_model_state="OK",IF(E89="SUPERIOR",I245,I244),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `F231` | `(vacía)` | `d cm` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `F232` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E5,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F233` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E7,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F234` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E5,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F235` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E7,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F236` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E5,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F237` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E7,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F238` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E5,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F239` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E7,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F240` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E6,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F241` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E8,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F242` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E6,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F243` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E8,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F244` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E6,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F245` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E8,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F246` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E6,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F247` | `(vacía)` | `=IF(struct_state="OK",FLEXION_ACERO!E8,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `F261` | `(vacía)` | `Estado` | Mínimo total por dirección. |
| ACERO_DETALLADO | `F262:F263` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(min_model_state<>"OK",min_model_state,IF(COUNT(B262:E262)<>4,"REQUIERE DATOS",IF(E262>=B262,"CUMPLE","NO CUMPLE"))))` | 10.5.4: As_inf+As_sup >= As mínimo total; no duplicación del mínimo de9.7. |
| ACERO_DETALLADO | `G86` | `=IF(LEN(inp_nloc_ix)=0,"",inp_nloc_ix)` | `=IF(local_model_state="OK",IF(E86="SUPERIOR",J233,J232),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `G87` | `=IF(LEN(inp_nloc_iy)=0,"",inp_nloc_iy)` | `=IF(local_model_state="OK",IF(E87="SUPERIOR",J237,J236),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `G88` | `=IF(LEN(inp_nloc_sx)=0,"",inp_nloc_sx)` | `=IF(local_model_state="OK",IF(E88="SUPERIOR",J241,J240),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `G89` | `=IF(LEN(inp_nloc_sy)=0,"",inp_nloc_sy)` | `=IF(local_model_state="OK",IF(E89="SUPERIOR",J245,J244),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `G231` | `(vacía)` | `As flex cm2` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `G232:G247` | `(vacía)` | `=IF(local_model_state="OK",IF(E232<=0,0,IF(D232<=0.000001,0,IF((inp_fy*F232)^2-4*(inp_fy^2/(2*0.85*inp_fc*E232))*(D232*100000/inp_phi_f)<0,"",(inp_fy*F232-SQRT((inp_fy*F232)^2-4*(inp_fy^2/(2*0.85*inp_fc*E232))*(D232*100000/inp_phi_f)))/(2*(inp_fy^2/(2*0.85*inp_fc*E232)))))),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H86` | `=IF(AND(punz_state="OK",COUNT(inp_nloc_ix)=1,inp_nloc_ix>=0),inp_nloc_ix*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | `=IF(local_model_state="OK",IF(E86="SUPERIOR",K233,K232),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `H87` | `=IF(AND(punz_state="OK",COUNT(inp_nloc_iy)=1,inp_nloc_iy>=0),inp_nloc_iy*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | `=IF(local_model_state="OK",IF(E87="SUPERIOR",K237,K236),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `H88` | `=IF(AND(punz_state="OK",COUNT(inp_nloc_sx)=1,inp_nloc_sx>=0),inp_nloc_sx*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | `=IF(local_model_state="OK",IF(E88="SUPERIOR",K241,K240),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `H89` | `=IF(AND(punz_state="OK",COUNT(inp_nloc_sy)=1,inp_nloc_sy>=0),inp_nloc_sy*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | `=IF(local_model_state="OK",IF(E89="SUPERIOR",K245,K244),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `H231` | `(vacía)` | `As min cara cm2` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `H232` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_inf,IF(AND(inp_min_scheme="DOS CARAS",D232>0.000001),0.0012,0))*E232*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H233` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_sup,IF(AND(inp_min_scheme="DOS CARAS",D233>0.000001),0.0012,0))*E233*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H234` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_inf,IF(AND(inp_min_scheme="DOS CARAS",D234>0.000001),0.0012,0))*E234*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H235` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_sup,IF(AND(inp_min_scheme="DOS CARAS",D235>0.000001),0.0012,0))*E235*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H236` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_inf,IF(AND(inp_min_scheme="DOS CARAS",D236>0.000001),0.0012,0))*E236*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H237` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_sup,IF(AND(inp_min_scheme="DOS CARAS",D237>0.000001),0.0012,0))*E237*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H238` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_inf,IF(AND(inp_min_scheme="DOS CARAS",D238>0.000001),0.0012,0))*E238*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H239` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_sup,IF(AND(inp_min_scheme="DOS CARAS",D239>0.000001),0.0012,0))*E239*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H240` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_inf,IF(AND(inp_min_scheme="DOS CARAS",D240>0.000001),0.0012,0))*E240*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H241` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_sup,IF(AND(inp_min_scheme="DOS CARAS",D241>0.000001),0.0012,0))*E241*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H242` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_inf,IF(AND(inp_min_scheme="DOS CARAS",D242>0.000001),0.0012,0))*E242*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H243` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_sup,IF(AND(inp_min_scheme="DOS CARAS",D243>0.000001),0.0012,0))*E243*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H244` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_inf,IF(AND(inp_min_scheme="DOS CARAS",D244>0.000001),0.0012,0))*E244*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H245` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_sup,IF(AND(inp_min_scheme="DOS CARAS",D245>0.000001),0.0012,0))*E245*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H246` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_inf,IF(AND(inp_min_scheme="DOS CARAS",D246>0.000001),0.0012,0))*E246*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `H247` | `(vacía)` | `=IF(AND(local_model_state="OK",min_model_state="OK",ISNUMBER(rho_eff)),MAX(rho_alloc_sup,IF(AND(inp_min_scheme="DOS CARAS",D247>0.000001),0.0012,0))*E247*inp_h*100,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `I85` | `ld real min cm` | `ld disponible cm` | Resumen de cuatro lados; detalle de caras/regiones en filas232:247. |
| ACERO_DETALLADO | `I86` | `=IF(AND(punz_state="OK",COUNT(inp_ll_ix_m,inp_ll_ix_p)=2),MIN(inp_ll_ix_m,inp_ll_ix_p),"")` | `=IF(local_model_state="OK",IF(E86="SUPERIOR",L233,L232),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `I87` | `=IF(AND(punz_state="OK",COUNT(inp_ll_iy_m,inp_ll_iy_p)=2),MIN(inp_ll_iy_m,inp_ll_iy_p),"")` | `=IF(local_model_state="OK",IF(E87="SUPERIOR",L237,L236),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `I88` | `=IF(AND(punz_state="OK",COUNT(inp_ll_sx_m,inp_ll_sx_p)=2),MIN(inp_ll_sx_m,inp_ll_sx_p),"")` | `=IF(local_model_state="OK",IF(E88="SUPERIOR",L241,L240),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `I89` | `=IF(AND(punz_state="OK",COUNT(inp_ll_sy_m,inp_ll_sy_p)=2),MIN(inp_ll_sy_m,inp_ll_sy_p),"")` | `=IF(local_model_state="OK",IF(E89="SUPERIOR",L245,L244),"")` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `I231` | `(vacía)` | `As req cm2` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `I232:I247` | `(vacía)` | `=IF(local_model_state="OK",IF(COUNT(G232:H232)=2,MAX(G232:H232),""),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J73` | `=IF(struct_state<>"OK",struct_state,IF(NOT(OR(FLEXION_ACERO!D5>0,AND("inf"="inf",FLEXION_ACERO!H5>0),AND("inf"="sup",OR(MAX(ABS(ult_mx),ABS(ult_my))>0.000001,IF(punz_state="OK",ABS(PUNZONAMIENTO!B48)>0.000001,FALSE))))),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_inf)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_inf<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G73)),MIN(H73:I73)<G73,MIN(inp_sep_inf_x,inp_scx,inp_sox)-B73<MAX(B73,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | `=IF(struct_state<>"OK",struct_state,IF(NOT(AND(ISNUMBER(As_tot_inf_x),As_tot_inf_x>0.000001)),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_inf)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_inf<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G73)),MIN(H73:I73)<G73,MIN(inp_sep_inf_x,inp_scx,inp_sox)-B73<MAX(B73,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | Desarrollo cuando esa cara tiene demanda o mínimo asignado; no exige superiores por \|Mx/My\| aislado. |
| ACERO_DETALLADO | `J74` | `=IF(struct_state<>"OK",struct_state,IF(NOT(OR(FLEXION_ACERO!D6>0,AND("inf"="inf",FLEXION_ACERO!H6>0),AND("inf"="sup",OR(MAX(ABS(ult_mx),ABS(ult_my))>0.000001,IF(punz_state="OK",ABS(PUNZONAMIENTO!B47)>0.000001,FALSE))))),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_inf)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_inf<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G74)),MIN(H74:I74)<G74,MIN(inp_sep_inf_y,inp_scy,inp_soy)-B74<MAX(B74,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | `=IF(struct_state<>"OK",struct_state,IF(NOT(AND(ISNUMBER(As_tot_inf_y),As_tot_inf_y>0.000001)),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_inf)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_inf<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G74)),MIN(H74:I74)<G74,MIN(inp_sep_inf_y,inp_scy,inp_soy)-B74<MAX(B74,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | Desarrollo cuando esa cara tiene demanda o mínimo asignado; no exige superiores por \|Mx/My\| aislado. |
| ACERO_DETALLADO | `J75` | `=IF(struct_state<>"OK",struct_state,IF(NOT(OR(FLEXION_ACERO!D7>0,AND("sup"="inf",FLEXION_ACERO!H7>0),AND("sup"="sup",OR(MAX(ABS(ult_mx),ABS(ult_my))>0.000001,IF(punz_state="OK",ABS(PUNZONAMIENTO!B48)>0.000001,FALSE))))),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_sup)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_sup<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G75)),MIN(H75:I75)<G75,inp_sep_sup_x-B75<MAX(B75,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | `=IF(struct_state<>"OK",struct_state,IF(NOT(AND(ISNUMBER(As_tot_sup_x),As_tot_sup_x>0.000001)),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_sup)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_sup<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G75)),MIN(H75:I75)<G75,MIN(inp_sep_sup_x,inp_sc_sx,inp_so_sx)-B75<MAX(B75,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | Espaciamiento regional superior participa en cb, psi_e y separación libre. |
| ACERO_DETALLADO | `J76` | `=IF(struct_state<>"OK",struct_state,IF(NOT(OR(FLEXION_ACERO!D8>0,AND("sup"="inf",FLEXION_ACERO!H8>0),AND("sup"="sup",OR(MAX(ABS(ult_mx),ABS(ult_my))>0.000001,IF(punz_state="OK",ABS(PUNZONAMIENTO!B47)>0.000001,FALSE))))),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_sup)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_sup<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G76)),MIN(H76:I76)<G76,inp_sep_sup_y-B76<MAX(B76,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | `=IF(struct_state<>"OK",struct_state,IF(NOT(AND(ISNUMBER(As_tot_sup_y),As_tot_sup_y>0.000001)),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_sup)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_sup<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G76)),MIN(H76:I76)<G76,MIN(inp_sep_sup_y,inp_sc_sy,inp_so_sy)-B76<MAX(B76,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | Espaciamiento regional superior participa en cb, psi_e y separación libre. |
| ACERO_DETALLADO | `J85` | `Estado` | `Estado por lado` | Resumen de cuatro lados; detalle de caras/regiones en filas232:247. |
| ACERO_DETALLADO | `J86` | `=IF(punz_state<>"OK",punz_state,IF(ABS(B86)<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",COUNT(inp_nloc_ix,inp_ll_ix_m,inp_ll_ix_p,inp_agg)<>4),"REQUIERE DATOS",IF(OR(inp_nloc_ix<0,MOD(inp_nloc_ix,1)<>0,inp_ll_ix_m<0,inp_ll_ix_p<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(COUNT(inp_ncx,inp_nox)<>2,"REQUIERE DATOS",IF(inp_nloc_ix>inp_ncx+inp_nox,"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(F86)),NOT(ISNUMBER(ld_inf_x))),"REQUIERE DATOS",IF(OR(H86<F86,I86<ld_inf_x,MIN(inp_ll_ix_m,inp_ll_ix_p)<0,F86>rho_max*C86*E86,inp_nloc_ix>INT(C86/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),2.5,4*inp_agg/3))+1,inp_ll_ix_m>H73,inp_ll_ix_p>I73),"NO CUMPLE",IF(J73<>"CUMPLE",J73,"CUMPLE")))))))))` | `=IF(COUNTIF(Q232:Q235,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(Q232:Q235,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(Q232:Q235,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(Q232:Q235,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(Q232:Q235,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `J87` | `=IF(punz_state<>"OK",punz_state,IF(ABS(B87)<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",COUNT(inp_nloc_iy,inp_ll_iy_m,inp_ll_iy_p,inp_agg)<>4),"REQUIERE DATOS",IF(OR(inp_nloc_iy<0,MOD(inp_nloc_iy,1)<>0,inp_ll_iy_m<0,inp_ll_iy_p<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(COUNT(inp_ncy,inp_noy)<>2,"REQUIERE DATOS",IF(inp_nloc_iy>inp_ncy+inp_noy,"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(F87)),NOT(ISNUMBER(ld_inf_y))),"REQUIERE DATOS",IF(OR(H87<F87,I87<ld_inf_y,MIN(inp_ll_iy_m,inp_ll_iy_p)<0,F87>rho_max*C87*E87,inp_nloc_iy>INT(C87/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)),2.5,4*inp_agg/3))+1,inp_ll_iy_m>H74,inp_ll_iy_p>I74),"NO CUMPLE",IF(J74<>"CUMPLE",J74,"CUMPLE")))))))))` | `=IF(COUNTIF(Q236:Q239,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(Q236:Q239,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(Q236:Q239,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(Q236:Q239,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(Q236:Q239,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `J88` | `=IF(punz_state<>"OK",punz_state,IF(ABS(B88)<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",COUNT(inp_nloc_sx,inp_ll_sx_m,inp_ll_sx_p,inp_agg)<>4),"REQUIERE DATOS",IF(OR(inp_nloc_sx<0,MOD(inp_nloc_sx,1)<>0,inp_ll_sx_m<0,inp_ll_sx_p<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(F88)),NOT(ISNUMBER(ld_sup_x))),"REQUIERE DATOS",IF(OR(H88<F88,I88<ld_sup_x,MIN(inp_ll_sx_m,inp_ll_sx_p)<0,F88>rho_max*C88*E88,inp_nloc_sx>INT(C88/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0)),2.5,4*inp_agg/3))+1,inp_ll_sx_m>H75,inp_ll_sx_p>I75),"NO CUMPLE",IF(J75<>"CUMPLE",J75,"CUMPLE")))))))` | `=IF(COUNTIF(Q240:Q243,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(Q240:Q243,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(Q240:Q243,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(Q240:Q243,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(Q240:Q243,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `J89` | `=IF(punz_state<>"OK",punz_state,IF(ABS(B89)<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",COUNT(inp_nloc_sy,inp_ll_sy_m,inp_ll_sy_p,inp_agg)<>4),"REQUIERE DATOS",IF(OR(inp_nloc_sy<0,MOD(inp_nloc_sy,1)<>0,inp_ll_sy_m<0,inp_ll_sy_p<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(F89)),NOT(ISNUMBER(ld_sup_y))),"REQUIERE DATOS",IF(OR(H89<F89,I89<ld_sup_y,MIN(inp_ll_sy_m,inp_ll_sy_p)<0,F89>rho_max*C89*E89,inp_nloc_sy>INT(C89/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0)),2.5,4*inp_agg/3))+1,inp_ll_sy_m>H76,inp_ll_sy_p>I76),"NO CUMPLE",IF(J76<>"CUMPLE",J76,"CUMPLE")))))))` | `=IF(COUNTIF(Q244:Q247,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(Q244:Q247,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(Q244:Q247,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(Q244:Q247,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(Q244:Q247,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))` | Control por lado y signo; cara traccionada del momento regional resultante, no \|Gamma\| repetido en dos caras. |
| ACERO_DETALLADO | `J231` | `(vacía)` | `N real` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `J232` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_ix),ISNUMBER(n_total_inf_x)),inp_nloc_ix,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J233` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_sx),ISNUMBER(n_total_sup_x)),inp_nloc_sx,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J234` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_ix),ISNUMBER(n_total_inf_x)),n_total_inf_x-inp_nloc_ix,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J235` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_sx),ISNUMBER(n_total_sup_x)),n_total_sup_x-inp_nloc_sx,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J236` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_ix),ISNUMBER(n_total_inf_x)),inp_nloc_ix,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J237` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_sx),ISNUMBER(n_total_sup_x)),inp_nloc_sx,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J238` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_ix),ISNUMBER(n_total_inf_x)),n_total_inf_x-inp_nloc_ix,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J239` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_sx),ISNUMBER(n_total_sup_x)),n_total_sup_x-inp_nloc_sx,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J240` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_iy),ISNUMBER(n_total_inf_y)),inp_nloc_iy,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J241` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_sy),ISNUMBER(n_total_sup_y)),inp_nloc_sy,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J242` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_iy),ISNUMBER(n_total_inf_y)),n_total_inf_y-inp_nloc_iy,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J243` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_sy),ISNUMBER(n_total_sup_y)),n_total_sup_y-inp_nloc_sy,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J244` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_iy),ISNUMBER(n_total_inf_y)),inp_nloc_iy,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J245` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_sy),ISNUMBER(n_total_sup_y)),inp_nloc_sy,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J246` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_iy),ISNUMBER(n_total_inf_y)),n_total_inf_y-inp_nloc_iy,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `J247` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_nloc_sy),ISNUMBER(n_total_sup_y)),n_total_sup_y-inp_nloc_sy,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K231` | `(vacía)` | `As real cm2` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `K232` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J232)),J232*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K233` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J233)),J233*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K234` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J234)),J234*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K235` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J235)),J235*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K236` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J236)),J236*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K237` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J237)),J237*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K238` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J238)),J238*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K239` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J239)),J239*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K240` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J240)),J240*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K241` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J241)),J241*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K242` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J242)),J242*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K243` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J243)),J243*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K244` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J244)),J244*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K245` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J245)),J245*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K246` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J246)),J246*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `K247` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(J247)),J247*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L231` | `(vacía)` | `ld disponible cm` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `L232` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_ll_ix_m)),inp_ll_ix_m,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L233` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_ll_sx_m)),inp_ll_sx_m,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L234` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(ACERO_DETALLADO!H73)),ACERO_DETALLADO!H73,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L235` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(ACERO_DETALLADO!H75)),ACERO_DETALLADO!H75,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L236` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_ll_ix_p)),inp_ll_ix_p,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L237` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_ll_sx_p)),inp_ll_sx_p,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L238` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(ACERO_DETALLADO!I73)),ACERO_DETALLADO!I73,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L239` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(ACERO_DETALLADO!I75)),ACERO_DETALLADO!I75,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L240` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_ll_iy_m)),inp_ll_iy_m,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L241` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_ll_sy_m)),inp_ll_sy_m,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L242` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(ACERO_DETALLADO!H74)),ACERO_DETALLADO!H74,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L243` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(ACERO_DETALLADO!H76)),ACERO_DETALLADO!H76,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L244` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_ll_iy_p)),inp_ll_iy_p,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L245` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(inp_ll_sy_p)),inp_ll_sy_p,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L246` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(ACERO_DETALLADO!I74)),ACERO_DETALLADO!I74,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `L247` | `(vacía)` | `=IF(AND(local_model_state="OK",ISNUMBER(ACERO_DETALLADO!I76)),ACERO_DETALLADO!I76,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M231` | `(vacía)` | `ld requerido cm` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `M232` | `(vacía)` | `=ld_inf_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M233` | `(vacía)` | `=ld_sup_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M234` | `(vacía)` | `=ld_inf_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M235` | `(vacía)` | `=ld_sup_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M236` | `(vacía)` | `=ld_inf_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M237` | `(vacía)` | `=ld_sup_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M238` | `(vacía)` | `=ld_inf_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M239` | `(vacía)` | `=ld_sup_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M240` | `(vacía)` | `=ld_inf_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M241` | `(vacía)` | `=ld_sup_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M242` | `(vacía)` | `=ld_inf_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M243` | `(vacía)` | `=ld_sup_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M244` | `(vacía)` | `=ld_inf_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M245` | `(vacía)` | `=ld_sup_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M246` | `(vacía)` | `=ld_inf_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `M247` | `(vacía)` | `=ld_sup_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N231` | `(vacía)` | `N total capa` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `N232` | `(vacía)` | `=n_total_inf_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N233` | `(vacía)` | `=n_total_sup_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N234` | `(vacía)` | `=n_total_inf_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N235` | `(vacía)` | `=n_total_sup_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N236` | `(vacía)` | `=n_total_inf_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N237` | `(vacía)` | `=n_total_sup_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N238` | `(vacía)` | `=n_total_inf_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N239` | `(vacía)` | `=n_total_sup_x` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N240` | `(vacía)` | `=n_total_inf_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N241` | `(vacía)` | `=n_total_sup_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N242` | `(vacía)` | `=n_total_inf_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N243` | `(vacía)` | `=n_total_sup_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N244` | `(vacía)` | `=n_total_inf_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N245` | `(vacía)` | `=n_total_sup_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N246` | `(vacía)` | `=n_total_inf_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `N247` | `(vacía)` | `=n_total_sup_y` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O231` | `(vacía)` | `N máx geométrico` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `O232` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E232<=0,0,MAX(0,INT((E232-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))-IF(E232=inp_by*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O233` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E233<=0,0,MAX(0,INT((E233-INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))-IF(E233=inp_by*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O234` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E234<=0,0,MAX(0,INT((E234-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))-IF(E234=inp_by*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O235` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E235<=0,0,MAX(0,INT((E235-INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))-IF(E235=inp_by*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O236` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E236<=0,0,MAX(0,INT((E236-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))-IF(E236=inp_by*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O237` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E237<=0,0,MAX(0,INT((E237-INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))-IF(E237=inp_by*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O238` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E238<=0,0,MAX(0,INT((E238-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))-IF(E238=inp_by*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O239` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E239<=0,0,MAX(0,INT((E239-INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))-IF(E239=inp_by*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O240` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E240<=0,0,MAX(0,INT((E240-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))-IF(E240=inp_bx*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O241` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E241<=0,0,MAX(0,INT((E241-INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))-IF(E241=inp_bx*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O242` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E242<=0,0,MAX(0,INT((E242-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))-IF(E242=inp_bx*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O243` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E243<=0,0,MAX(0,INT((E243-INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))-IF(E243=inp_bx*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O244` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E244<=0,0,MAX(0,INT((E244-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))-IF(E244=inp_bx*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O245` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E245<=0,0,MAX(0,INT((E245-INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))-IF(E245=inp_bx*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O246` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E246<=0,0,MAX(0,INT((E246-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))-IF(E246=inp_bx*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `O247` | `(vacía)` | `=IF(AND(struct_state="OK",local_model_state="OK",COUNT(inp_rec_lat,inp_agg)=2),IF(E247<=0,0,MAX(0,INT((E247-INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))-IF(E247=inp_bx*100,2*inp_rec_lat,0))/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0)),2.5,4*inp_agg/3))+1)),"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `P231` | `(vacía)` | `As máximo cm2` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `P232:P247` | `(vacía)` | `=IF(local_model_state="OK",rho_max*E232*F232,"")` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q231` | `(vacía)` | `Estado` | 13.5.3/10.5.4: evaluar el signo antes de seleccionar cara y magnitud. |
| ACERO_DETALLADO | `Q232` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C52)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I232)),"NO CUMPLE",IF(I232<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J232,K232,L232,M232,N232,O232)<>6),"REQUIERE DATOS",IF(OR(J232<0,MOD(J232,1)<>0,J232>N232),"DATOS INVÁLIDOS",IF(OR(K232<I232,I232>P232,J232>O232,L232<M232),"NO CUMPLE",IF(ACERO_DETALLADO!J73<>"CUMPLE",ACERO_DETALLADO!J73,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q233` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C52)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I233)),"NO CUMPLE",IF(I233<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J233,K233,L233,M233,N233,O233)<>6),"REQUIERE DATOS",IF(OR(J233<0,MOD(J233,1)<>0,J233>N233),"DATOS INVÁLIDOS",IF(OR(K233<I233,I233>P233,J233>O233,L233<M233),"NO CUMPLE",IF(ACERO_DETALLADO!J75<>"CUMPLE",ACERO_DETALLADO!J75,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q234` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C52)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I234)),"NO CUMPLE",IF(I234<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J234,K234,L234,M234,N234,O234)<>6),"REQUIERE DATOS",IF(OR(J234<0,MOD(J234,1)<>0,J234>N234),"DATOS INVÁLIDOS",IF(OR(K234<I234,I234>P234,J234>O234,L234<M234),"NO CUMPLE",IF(ACERO_DETALLADO!J73<>"CUMPLE",ACERO_DETALLADO!J73,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q235` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C52)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I235)),"NO CUMPLE",IF(I235<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J235,K235,L235,M235,N235,O235)<>6),"REQUIERE DATOS",IF(OR(J235<0,MOD(J235,1)<>0,J235>N235),"DATOS INVÁLIDOS",IF(OR(K235<I235,I235>P235,J235>O235,L235<M235),"NO CUMPLE",IF(ACERO_DETALLADO!J75<>"CUMPLE",ACERO_DETALLADO!J75,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q236` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C53)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I236)),"NO CUMPLE",IF(I236<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J236,K236,L236,M236,N236,O236)<>6),"REQUIERE DATOS",IF(OR(J236<0,MOD(J236,1)<>0,J236>N236),"DATOS INVÁLIDOS",IF(OR(K236<I236,I236>P236,J236>O236,L236<M236),"NO CUMPLE",IF(ACERO_DETALLADO!J73<>"CUMPLE",ACERO_DETALLADO!J73,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q237` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C53)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I237)),"NO CUMPLE",IF(I237<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J237,K237,L237,M237,N237,O237)<>6),"REQUIERE DATOS",IF(OR(J237<0,MOD(J237,1)<>0,J237>N237),"DATOS INVÁLIDOS",IF(OR(K237<I237,I237>P237,J237>O237,L237<M237),"NO CUMPLE",IF(ACERO_DETALLADO!J75<>"CUMPLE",ACERO_DETALLADO!J75,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q238` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C53)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I238)),"NO CUMPLE",IF(I238<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J238,K238,L238,M238,N238,O238)<>6),"REQUIERE DATOS",IF(OR(J238<0,MOD(J238,1)<>0,J238>N238),"DATOS INVÁLIDOS",IF(OR(K238<I238,I238>P238,J238>O238,L238<M238),"NO CUMPLE",IF(ACERO_DETALLADO!J73<>"CUMPLE",ACERO_DETALLADO!J73,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q239` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C53)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I239)),"NO CUMPLE",IF(I239<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J239,K239,L239,M239,N239,O239)<>6),"REQUIERE DATOS",IF(OR(J239<0,MOD(J239,1)<>0,J239>N239),"DATOS INVÁLIDOS",IF(OR(K239<I239,I239>P239,J239>O239,L239<M239),"NO CUMPLE",IF(ACERO_DETALLADO!J75<>"CUMPLE",ACERO_DETALLADO!J75,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q240` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C54)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I240)),"NO CUMPLE",IF(I240<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J240,K240,L240,M240,N240,O240)<>6),"REQUIERE DATOS",IF(OR(J240<0,MOD(J240,1)<>0,J240>N240),"DATOS INVÁLIDOS",IF(OR(K240<I240,I240>P240,J240>O240,L240<M240),"NO CUMPLE",IF(ACERO_DETALLADO!J74<>"CUMPLE",ACERO_DETALLADO!J74,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q241` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C54)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I241)),"NO CUMPLE",IF(I241<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J241,K241,L241,M241,N241,O241)<>6),"REQUIERE DATOS",IF(OR(J241<0,MOD(J241,1)<>0,J241>N241),"DATOS INVÁLIDOS",IF(OR(K241<I241,I241>P241,J241>O241,L241<M241),"NO CUMPLE",IF(ACERO_DETALLADO!J76<>"CUMPLE",ACERO_DETALLADO!J76,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q242` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C54)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I242)),"NO CUMPLE",IF(I242<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J242,K242,L242,M242,N242,O242)<>6),"REQUIERE DATOS",IF(OR(J242<0,MOD(J242,1)<>0,J242>N242),"DATOS INVÁLIDOS",IF(OR(K242<I242,I242>P242,J242>O242,L242<M242),"NO CUMPLE",IF(ACERO_DETALLADO!J74<>"CUMPLE",ACERO_DETALLADO!J74,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q243` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C54)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I243)),"NO CUMPLE",IF(I243<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J243,K243,L243,M243,N243,O243)<>6),"REQUIERE DATOS",IF(OR(J243<0,MOD(J243,1)<>0,J243>N243),"DATOS INVÁLIDOS",IF(OR(K243<I243,I243>P243,J243>O243,L243<M243),"NO CUMPLE",IF(ACERO_DETALLADO!J76<>"CUMPLE",ACERO_DETALLADO!J76,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q244` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C55)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I244)),"NO CUMPLE",IF(I244<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J244,K244,L244,M244,N244,O244)<>6),"REQUIERE DATOS",IF(OR(J244<0,MOD(J244,1)<>0,J244>N244),"DATOS INVÁLIDOS",IF(OR(K244<I244,I244>P244,J244>O244,L244<M244),"NO CUMPLE",IF(ACERO_DETALLADO!J74<>"CUMPLE",ACERO_DETALLADO!J74,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q245` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C55)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I245)),"NO CUMPLE",IF(I245<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J245,K245,L245,M245,N245,O245)<>6),"REQUIERE DATOS",IF(OR(J245<0,MOD(J245,1)<>0,J245>N245),"DATOS INVÁLIDOS",IF(OR(K245<I245,I245>P245,J245>O245,L245<M245),"NO CUMPLE",IF(ACERO_DETALLADO!J76<>"CUMPLE",ACERO_DETALLADO!J76,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q246` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C55)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I246)),"NO CUMPLE",IF(I246<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J246,K246,L246,M246,N246,O246)<>6),"REQUIERE DATOS",IF(OR(J246<0,MOD(J246,1)<>0,J246>N246),"DATOS INVÁLIDOS",IF(OR(K246<I246,I246>P246,J246>O246,L246<M246),"NO CUMPLE",IF(ACERO_DETALLADO!J74<>"CUMPLE",ACERO_DETALLADO!J74,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| ACERO_DETALLADO | `Q247` | `(vacía)` | `=IF(local_model_state<>"OK",local_model_state,IF(ABS(FLEXION_ACERO!C55)<=0.000001,"NO APLICA",IF(min_model_state<>"OK",min_model_state,IF(NOT(ISNUMBER(I247)),"NO CUMPLE",IF(I247<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",inp_repartition_ok<>"SI",LEN(inp_repartition_ref)=0,COUNT(J247,K247,L247,M247,N247,O247)<>6),"REQUIERE DATOS",IF(OR(J247<0,MOD(J247,1)<>0,J247>N247),"DATOS INVÁLIDOS",IF(OR(K247<I247,I247>P247,J247>O247,L247<M247),"NO CUMPLE",IF(ACERO_DETALLADO!J76<>"CUMPLE",ACERO_DETALLADO!J76,"CUMPLE")))))))))` | Mu firmado regional del reparto equilibrado; mínimo asignado por cara; N local o N_total-N_local sin duplicar barras. |
| RESUMEN | `A73` | `q física de servicio` | `Pico físico: control opcional EMS` | No controla si inp_peak=NO; contacto se comprueba separadamente. |
| RESUMEN | `A102` | `(vacía)` | `FASE 3: CONTROLES COMPLEMENTARIOS` | FASE 3: CONTROLES COMPLEMENTARIOS |
| RESUMEN | `A104` | `(vacía)` | `Mínimo real inferior+superior` | E.06010.5.4 /9.7 |
| RESUMEN | `A105` | `(vacía)` | `Distribución superior X` | E.06015.4.4; NO APLICA si no requerido |
| RESUMEN | `A106` | `(vacía)` | `Distribución superior Y` | E.06015.4.4; NO APLICA si no requerido |
| RESUMEN | `A107` | `(vacía)` | `Equilibrio de reparto local` | M cara preservado; gamma_f+gamma_v=1 |
| RESUMEN | `A108` | `(vacía)` | `Datos de grado nominal` | 9.7.2: clasificación independiente de fy resistencia |
| RESUMEN | `A109` | `(vacía)` | `Datos reparto mínimo` | UNA CARA / DOS CARAS; piso .0012 cuando tracción |
| RESUMEN | `B23` | `=IF(COUNTIF(B70:B94,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(B70:B94,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(B70:B94,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(B70:B94,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(B70:B94,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))` | `=IF(COUNTIF(B70:B109,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(B70:B109,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(B70:B109,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(B70:B109,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(B70:B109,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))` | Todas las condiciones F2/F3 necesarias gobiernan; NO APLICA neutral. |
| RESUMEN | `B95` | `=COUNTIF(B70:B94,"NO CUMPLE")` | `=COUNTIF(B70:B94,"NO CUMPLE")+COUNTIF(B104:B109,"NO CUMPLE")` | Contar controles reales, excluyendo contadores y prioridades. |
| RESUMEN | `B96` | `=COUNTIF(B70:B94,"REQUIERE DATOS")` | `=COUNTIF(B70:B94,"REQUIERE DATOS")+COUNTIF(B104:B109,"REQUIERE DATOS")` | Contar controles reales, excluyendo contadores y prioridades. |
| RESUMEN | `B97` | `=COUNTIF(B70:B94,"REQUIERE ANÁLISIS ESPECIAL")` | `=COUNTIF(B70:B94,"REQUIERE ANÁLISIS ESPECIAL")+COUNTIF(B104:B109,"REQUIERE ANÁLISIS ESPECIAL")` | Contar controles reales, excluyendo contadores y prioridades. |
| RESUMEN | `B98` | `=COUNTIF(B70:B94,"FUERA DEL ALCANCE IMPLEMENTADO")` | `=COUNTIF(B70:B94,"FUERA DEL ALCANCE IMPLEMENTADO")+COUNTIF(B104:B109,"FUERA DEL ALCANCE IMPLEMENTADO")` | Contar controles reales, excluyendo contadores y prioridades. |
| RESUMEN | `B104` | `(vacía)` | `=min_real_state` | E.06010.5.4 /9.7 |
| RESUMEN | `B105` | `(vacía)` | `=dist_sup_x_state` | E.06015.4.4; NO APLICA si no requerido |
| RESUMEN | `B106` | `(vacía)` | `=dist_sup_y_state` | E.06015.4.4; NO APLICA si no requerido |
| RESUMEN | `B107` | `(vacía)` | `=local_eq_state` | M cara preservado; gamma_f+gamma_v=1 |
| RESUMEN | `B108` | `(vacía)` | `=IF(ISNUMBER(fy_nom_mpa),"CUMPLE","REQUIERE DATOS")` | 9.7.2: clasificación independiente de fy resistencia |
| RESUMEN | `B109` | `(vacía)` | `=IF(min_model_state="OK","CUMPLE",min_model_state)` | UNA CARA / DOS CARAS; piso .0012 cuando tracción |
| RESUMEN | `C104` | `(vacía)` | `-` | E.06010.5.4 /9.7 |
| RESUMEN | `C105:C106` | `(vacía)` | `-` | E.06015.4.4; NO APLICA si no requerido |
| RESUMEN | `C107` | `(vacía)` | `-` | M cara preservado; gamma_f+gamma_v=1 |
| RESUMEN | `C108` | `(vacía)` | `-` | 9.7.2: clasificación independiente de fy resistencia |
| RESUMEN | `C109` | `(vacía)` | `-` | UNA CARA / DOS CARAS; piso .0012 cuando tracción |
| RESUMEN | `D73` | `15.2.2/3 + EMS` | `Adicional; fuente exigida si SI` | No atribuir qmax<=qadm universal a E.05028. |
| RESUMEN | `D104` | `(vacía)` | `E.06010.5.4 /9.7` | E.06010.5.4 /9.7 |
| RESUMEN | `D105:D106` | `(vacía)` | `E.06015.4.4; NO APLICA si no requerido` | E.06015.4.4; NO APLICA si no requerido |
| RESUMEN | `D107` | `(vacía)` | `M cara preservado; gamma_f+gamma_v=1` | M cara preservado; gamma_f+gamma_v=1 |
| RESUMEN | `D108` | `(vacía)` | `9.7.2: clasificación independiente de fy resistencia` | 9.7.2: clasificación independiente de fy resistencia |
| RESUMEN | `D109` | `(vacía)` | `UNA CARA / DOS CARAS; piso .0012 cuando tracción` | UNA CARA / DOS CARAS; piso .0012 cuando tracción |

## 11. Nombres, nuevas entradas y validaciones

| Nombre nuevo | Destino |
|---|---|
| `As_min_total_pm` | `FLEXION_ACERO!$B$37` |
| `As_tot_inf_x` | `ACERO_DETALLADO!$B$251` |
| `As_tot_inf_y` | `ACERO_DETALLADO!$B$252` |
| `As_tot_sup_x` | `ACERO_DETALLADO!$B$253` |
| `As_tot_sup_y` | `ACERO_DETALLADO!$B$254` |
| `dist_sup_x_state` | `ACERO_DETALLADO!$B$197` |
| `dist_sup_y_state` | `ACERO_DETALLADO!$B$219` |
| `fy_nom_kg` | `FLEXION_ACERO!$B$31` |
| `fy_nom_mpa` | `FLEXION_ACERO!$B$32` |
| `inp_eta_x` | `INGRESO_DATOS!$C$170` |
| `inp_eta_y` | `INGRESO_DATOS!$C$171` |
| `inp_fy_nom` | `INGRESO_DATOS!$C$161` |
| `inp_grade` | `INGRESO_DATOS!$C$160` |
| `inp_min_face` | `INGRESO_DATOS!$C$166` |
| `inp_min_frac` | `INGRESO_DATOS!$C$167` |
| `inp_min_scheme` | `INGRESO_DATOS!$C$165` |
| `inp_nc_sx` | `INGRESO_DATOS!$C$179` |
| `inp_nc_sy` | `INGRESO_DATOS!$C$185` |
| `inp_no_sx` | `INGRESO_DATOS!$C$180` |
| `inp_no_sx_minus` | `INGRESO_DATOS!$C$181` |
| `inp_no_sx_plus` | `INGRESO_DATOS!$C$182` |
| `inp_no_sy` | `INGRESO_DATOS!$C$186` |
| `inp_no_sy_minus` | `INGRESO_DATOS!$C$187` |
| `inp_no_sy_plus` | `INGRESO_DATOS!$C$188` |
| `inp_peak` | `INGRESO_DATOS!$C$156` |
| `inp_peak_ref` | `INGRESO_DATOS!$C$157` |
| `inp_repartition_ok` | `INGRESO_DATOS!$C$173` |
| `inp_repartition_ref` | `INGRESO_DATOS!$C$172` |
| `inp_sc_sx` | `INGRESO_DATOS!$C$177` |
| `inp_sc_sy` | `INGRESO_DATOS!$C$183` |
| `inp_so_sx` | `INGRESO_DATOS!$C$178` |
| `inp_so_sy` | `INGRESO_DATOS!$C$184` |
| `local_eq_state` | `FLEXION_ACERO!$B$61` |
| `local_model_state` | `FLEXION_ACERO!$B$47` |
| `min_model_state` | `FLEXION_ACERO!$B$34` |
| `min_real_state` | `ACERO_DETALLADO!$B$264` |
| `n_total_inf_x` | `ACERO_DETALLADO!$B$266` |
| `n_total_inf_y` | `ACERO_DETALLADO!$B$268` |
| `n_total_sup_x` | `ACERO_DETALLADO!$B$267` |
| `n_total_sup_y` | `ACERO_DETALLADO!$B$269` |
| `rho_alloc_inf` | `FLEXION_ACERO!$B$35` |
| `rho_alloc_sup` | `FLEXION_ACERO!$B$36` |
| `zone_sup_x` | `ACERO_DETALLADO!$B$290` |
| `zone_sup_y` | `ACERO_DETALLADO!$B$302` |

### Nuevas entradas editables: datos vacíos explícitos y valores predeterminados

| Celda | Nombre | Etiqueta | Valor/fórmula inicial | Unidad |
|---|---|---|---|---|
| `INGRESO_DATOS!C170` | `inp_eta_x` | Fracción gamma_fMy al lado - X | `0.5` | - |
| `INGRESO_DATOS!C171` | `inp_eta_y` | Fracción gamma_fMx al lado - Y | `0.5` | - |
| `INGRESO_DATOS!C161` | `inp_fy_nom` | fy nominal declarado si OTRO | `=inp_fy` | kgf/cm2 |
| `INGRESO_DATOS!C160` | `inp_grade` | Clasificación normativa del acero | `OTRO` | - |
| `INGRESO_DATOS!C166` | `inp_min_face` | Cara que recibe mínimo íntegro | `INFERIOR` | - |
| `INGRESO_DATOS!C167` | `inp_min_frac` | Fracción mínima asignada inferior | `(vacía)` | - |
| `INGRESO_DATOS!C165` | `inp_min_scheme` | Distribución del mínimo total | `UNA CARA` | - |
| `INGRESO_DATOS!C179` | `inp_nc_sx` | N real superior X central | `(vacía)` | barras |
| `INGRESO_DATOS!C185` | `inp_nc_sy` | N real superior Y central | `(vacía)` | barras |
| `INGRESO_DATOS!C180` | `inp_no_sx` | N real superior X exterior total | `(vacía)` | barras |
| `INGRESO_DATOS!C181` | `inp_no_sx_minus` | N superior X exterior lado - | `(vacía)` | barras |
| `INGRESO_DATOS!C182` | `inp_no_sx_plus` | N superior X exterior lado + | `(vacía)` | barras |
| `INGRESO_DATOS!C186` | `inp_no_sy` | N real superior Y exterior total | `(vacía)` | barras |
| `INGRESO_DATOS!C187` | `inp_no_sy_minus` | N superior Y exterior lado - | `(vacía)` | barras |
| `INGRESO_DATOS!C188` | `inp_no_sy_plus` | N superior Y exterior lado + | `(vacía)` | barras |
| `INGRESO_DATOS!C156` | `inp_peak` | Control adicional de pico lineal | `NO` | - |
| `INGRESO_DATOS!C157` | `inp_peak_ref` | Fuente de control del pico | `(vacía)` | - |
| `INGRESO_DATOS!C173` | `inp_repartition_ok` | Reparto local validado en análisis | `(vacía)` | - |
| `INGRESO_DATOS!C172` | `inp_repartition_ref` | Referencia del análisis de reparto | `(vacía)` | - |
| `INGRESO_DATOS!C177` | `inp_sc_sx` | Separación central superior X | `=inp_sep_sup_x` | cm |
| `INGRESO_DATOS!C183` | `inp_sc_sy` | Separación central superior Y | `=inp_sep_sup_y` | cm |
| `INGRESO_DATOS!C178` | `inp_so_sx` | Separación exterior superior X | `=inp_sep_sup_x` | cm |
| `INGRESO_DATOS!C184` | `inp_so_sy` | Separación exterior superior Y | `=inp_sep_sup_y` | cm |

Las nuevas entradas se describen por nombre y condición de aplicabilidad. Los conteos superiores vacíos no se necesitan cuando la cara está NO APLICA; las componentes sísmicas y entradas F2 permanecen intactas.

| Validación nueva | Lista / rango |
|---|---|
| `INGRESO_DATOS!C156` | `NO,SI` |
| `INGRESO_DATOS!C160` | `NTP GRADO 420 / ASTM G60,OTRO` |
| `INGRESO_DATOS!C165` | `UNA CARA,DOS CARAS` |
| `INGRESO_DATOS!C166` | `INFERIOR,SUPERIOR` |
| `INGRESO_DATOS!C173` | `SI,NO` |

Las entradas numéricas nuevas se comprueban además mediante `GEOMETRIA!B2627`, módulos locales y RESUMEN: enteros/conteos, no negativos/positivos, selecciones válidas. Pegar texto/negativos no puede evitar los controles por saltar un dropdown. Las reglas CF nuevas usan igualdad exacta: CUMPLE/OK/NO APLICA verde, NO CUMPLE/DATOS INVÁLIDOS/ERROR rojo, pendientes o fuera de alcance amarillo. Se preservan también las reglas anteriores y se comprobó el color efectivo de estados nativos.

### Bloques y extensiones de formato
- `INGRESO_DATOS!A156:H161`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `INGRESO_DATOS!A165:H173`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `INGRESO_DATOS!A177:H188`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `PRESIONES_SERVICIO!A57:H59`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `FLEXION_ACERO!A31:J37`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `FLEXION_ACERO!A47:L47`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `FLEXION_ACERO!A51:L61`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A231:Q247`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A251:J254`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A181:J197`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A282:J290`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A203:J219`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A294:J302`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A266:J269`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A261:J264`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `RESUMEN!A104:H109`: formato de tabla, notas, resultados visibles y alturas ajustadas.

El registro incluye todos los cambios de contenido y nombres/validaciones nuevas. Las vistas auxiliares se conservaron localmente para la auditoría y no forman parte de los entregables publicados.
