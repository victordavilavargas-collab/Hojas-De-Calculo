# CAMBIOS ZAPATA FASE 2 — AUDITORÍA TÉCNICA E.060 / E.050

Fecha: 30/09/2026, America/Lima. Rama `main`, repositorio `victordavilavargas-collab/Hojas-De-Calculo`. Base Git revisada: `5b449d0a7e7075ad603597cd1898922a73f6f54c`. Se verificó el remoto independiente de Excels y se ejecutó pull --ff-only antes de trabajar; el repositorio CSI padre no se modificó.

El objetivo fue corregir y delimitar el motor de cálculo. No se optimizó el caso. Las 15 hojas se auditaron directamente mediante fórmulas, nombres, resultados almacenados e inventario nativo del XLSX; el informe Fase 1 fue solamente una referencia secundaria. La edición y los guardados se realizaron exclusivamente mediante Microsoft Excel COM 16.0. Python/openpyxl se utilizó para lectura y comparación, no para regrabar el XLSX.

## A–B. Archivos, preservación y hashes

| Archivo | Función | SHA256 antes/después |
|---|---|---|
| `trabajo_codex/Diseño de zapata aislada.xlsx` | Base preservada, sin cambios | `24f60a8b5a8b170de9ef528cc7f96120f0b5c651ccdad33acf8a6562965a7060` |
| `trabajo_codex/Diseño de zapata aislada_CORREGIDA_FASE1.xlsx` | Base preservada, sin cambios | `8d66b5590812704f8bdd1173b5583a4bcaaf00d500c1d854d00c42051192ded5` |
| `trabajo_codex/CAMBIOS_ZAPATA_FASE1.md` | Base preservada, sin cambios | `24e6f0077e2f8ba51c8d80b51056834aa8400998d2532d9b83693d426eddbf3d` |
| `trabajo_codex/Diseño de zapata aislada_CORREGIDA_FASE2.xlsx` | Nuevo entregable Fase 2 | `8d92bc7d557dcbb691b1d538e2dd3f96d830e54f69bb1f407a402637b3e2bd01` |

El segundo entregable es `trabajo_codex/CAMBIOS_ZAPATA_FASE2.md`, este documento. Se entregan únicamente XLSX y Markdown. Las copias de ensayo, scripts, PDFs oficiales/auxiliares, gráficos exportados y capturas quedan fuera del commit.

Se conservaron exactamente las entradas heredadas `INGRESO_DATOS!C14:C70` y `CARGAS!C7:C27`: qadm=8.5 tf/m², Bx=By=3.75 m, h=0.50 m, barras y separaciones originales, cargas, momentos, factores y etiquetas de casos. Las nuevas entradas de armado/EMS no conocidas se dejaron vacías; no se inventó un plano, EMS ni factor de seguridad.

## C. Inventario antes/después

| Hoja (orden conservado) | Tamaño F1 → F2 | Fórmulas F1 → F2 | Gráficos | Validaciones F1 → F2 | Reglas CF F1 → F2 | Combinaciones F1 → F2 |
|---|---|---:|---:|---:|---:|---:|
| INGRESO_DATOS | 70×8 → 152×8 | 0 → 4 | 4 | 8 → 23 | 0 → 0 | 19 → 91 |
| BARRAS_PERU | 15×7 → 21×10 | 0 → 0 | 0 | 0 → 0 | 0 → 0 | 1 → 1 |
| CARGAS | 27×8 → 38×8 | 14 → 14 | 0 | 1 → 1 | 6 → 6 | 3 → 4 |
| GEOMETRIA | 2618×11 → 2627×11 | 23420 → 23424 | 0 | 0 → 0 | 4 → 10 | 3 → 9 |
| RESULTANTE | 12×14 → 12×14 | 29 → 29 | 0 | 0 → 0 | 3 → 3 | 5 → 5 |
| PRESIONES_SERVICIO | 15×8 → 55×8 | 10 → 53 | 0 | 0 → 0 | 9 → 24 | 1 → 30 |
| PRESIONES_ULTIMAS | 23×8 → 25×8 | 14 → 15 | 0 | 0 → 0 | 9 → 12 | 1 → 2 |
| DIAGRAMAS_X | 79×12 → 79×12 | 599 → 599 | 3 | 0 → 0 | 3 → 3 | 12 → 12 |
| DIAGRAMAS_Y | 79×12 → 79×12 | 599 → 599 | 3 | 0 → 0 | 3 → 3 | 12 → 12 |
| PUNZONAMIENTO | 58×6 → 66×6 | 53 → 58 | 0 | 0 → 0 | 12 → 18 | 6 → 12 |
| CORTANTE_UNIDIRECCIONAL | 23×8 → 23×10 | 39 → 47 | 0 | 0 → 0 | 12 → 12 | 2 → 2 |
| FLEXION_ACERO | 17×9 → 28×10 | 29 → 37 | 0 | 0 → 0 | 6 → 15 | 2 → 15 |
| ACERO_DETALLADO | 13×10 → 173×10 | 39 → 212 | 0 | 0 → 0 | 12 → 42 | 1 → 114 |
| GRAFICOS | 133×26 → 133×26 | 344 → 344 | 14 | 0 → 0 | 2 → 2 | 3 → 3 |
| RESUMEN | 64×8 → 99×8 | 107 → 136 | 0 | 0 → 0 | 141 → 147 | 15 → 46 |

Se preservan los 168 nombres Fase 1 con sus destinos; total final 324 (156 nuevos). Se conservan los 24 gráficos, sus tipos, series y referencias. Se verificaron anchos, paneles, áreas de impresión, márgenes, opciones, comentarios, validaciones y reglas condicionales anteriores. Sin macros, vínculos externos ni hojas protegidas.

Las alturas se amplían localmente para bloques nuevos/texto visible. Un gráfico de INGRESO_DATOS se desplaza bajo las nuevas entradas para evitar superposición. En INGRESO_DATOS, cuyo PageSetup F1 no estaba serializado, Excel explicitó valores predeterminados portrait/A4/DPI=0 al guardar; no cambió su área de impresión. Las áreas temporales PDF para QA se asignaron solo en aperturas de lectura, sin guardar.

## D–E. Normas oficiales y criterio de vigencia

- [NTE E.060, DS 010-2009-VIVIENDA, texto oficial](https://cdn.www.gob.pe/uploads/document/file/2686419/E.060%20Concreto%20Armado%20DS%20N%C2%B0%20010-2009.pdf). Se aplicaron sus artículos y ecuaciones, sin reemplazarlos por ACI posterior.
- [NTE E.050, RM 406-2018-VIVIENDA, texto oficial](https://cdn.www.gob.pe/uploads/document/file/2366655/54%20E.050%20SUELOS%20Y%20CIMENTACIONES%20RM%20N%C2%B0%20406-2018-VIVIENDA.pdf).
- [Catálogo oficial del RNE](https://www.gob.pe/institucion/vivienda/informes-publicaciones/2309793-reglamento-nacional-de-edificaciones-rne), consultado en esta auditoría. La creación del grupo de actualización E.060 mediante RM 066-2025 no se trató como aprobación de una norma nueva.
- E.020/E.030 no se usaron para reconstruir cargas o combinaciones: las acciones de servicio/últimas son entradas del proyectista. Las opciones 15.2.4/5 actúan exclusivamente sobre servicio. No se infieren factores por nombres de casos.

| Control | Artículo / ecuación | Celdas principales | Decisión técnica |
|---|---|---|---|
| Servicio / resistencia | E.060 15.2.1/2 | `CARGAS!E7:E12/E22:E27; PRESIONES_SERVICIO!B19; PRESIONES_ULTIMAS!D17/B25` | Estados y acciones separados; opciones sísmicas no alteran último. |
| Presión compresiva y contacto | E.060 15.2.3 | `PRESIONES_SERVICIO!D11/D14; PRESIONES_ULTIMAS!D11/D13/D17` | q negativa visible; sin MAX(0,q). Contacto parcial bloqueado. |
| Área efectiva | E.050 28 | `PRESIONES_SERVICIO!B20:B36` | Bx−2|ex|, By−2|ey|, sin reemplazar campo lineal físico. |
| Opciones temporales | E.060 15.2.4/5 | `INGRESO_DATOS!C74:C76; CARGAS!C33:C38` | 1.30 solo SI en SISMO/VIENTO; 0.80 únicamente componentes sísmicas explícitas. |
| Carga inclinada / EMS | E.050 29; E.060 15.2.2 | `PRESIONES_SERVICIO!B37:B39; INGRESO_DATOS!C77:C80` | No se recalcula qadm por c/phi inventados; EMS debe sustentar inclinación. |
| Flexión en caras | E.060 15.4.1/2 | `DIAGRAMAS_X/Y!B7:B9; FLEXION_ACERO!D5:D8` | Voladizos integrados desde cada borde libre; no máximos interiores de viga. |
| Distribución rectangular | E.060 15.4.4.1/2, ecuación 15-1 | `ACERO_DETALLADO!B21:B65/B148:B168` | Dirección larga uniforme; corta gamma_s=2/(beta+1), franja centrada en columna; controles por ambas zonas exteriores. |
| Cuantía mínima y espaciamiento | E.060 10.5.4, 9.7.2/3 | `FLEXION_ACERO!B21:B24; GEOMETRIA!B11` | MAX(normativa,usuario), MIN(3h,40cm,usuario). |
| Flexión simple / límite | E.060 10.2.7.3, 10.3.2/4, 8.5.5 | `FLEXION_ACERO!F5:I8/B25:B27` | Beta1 por fc, Es=200000MPa; As≤0.75As balanceada. Discriminante inválido no crea capacidad ficticia. |
| fc mínimo | E.060 5.1.1 | `FLEXION_ACERO!B28` | fc≥17MPa en zapata y columna, sin cambiar entradas. |
| Cortante unidireccional | E.060 11.12.1.1, 11.3.1.1, 15.5, 9.3.2.3 | `CORTANTE_UNIDIRECCIONAL!C5:J8` | Cortes a d físico de capa traccionada, ambos lados; Vu firmado y magnitud de resistencia separadas; phi=.85. |
| Punzonamiento | E.060 11.12.1.2, 11.12.2.1, 11.12.6, figura 11.12.6; 9.3.2.3 | `PUNZONAMIENTO!B8:B52/B61:B66` | Menor de tres Vc, phi=.85, J y cuatro esfuerzos biaxiales simultáneos; signos conservados. |
| Transferencia local de momento | E.060 13.5.3.1/3 | `PUNZONAMIENTO!B47:B48/B55:B57; ACERO_DETALLADO!B86:J92` | Gamma_f básico; franja c+3h intersectada con zapata real; demanda global+local conservadora; As real por conteo y desarrollo. |
| Desarrollo a tracción | E.060 15.6, 12.1.2, 12.2.1/3, ecuación 12-1 y tabla 12.2 | `ACERO_DETALLADO!B73:J79` | Barras corrugadas rectas continuas; cb real, Ktr=0, lambda=1; ld≥30cm; no reducción por exceso. |
| Altura sobre refuerzo | E.060 15.7 | `GEOMETRIA!B2622:B2625` | Altura sobre coronación de parrilla inferior ≥30cm para zapata sobre suelo. |
| Aplastamiento / conexión | E.060 15.8.1/2, 10.17.1, 9.3.2.4 | `ACERO_DETALLADO!B97:B112/B134:B136` | Phi=.70; menor capacidad de dos superficies; As≥.005Ag; flexocompresión/torsión no certificadas. |
| Desarrollo a compresión | E.060 12.3.1/2; 12.1.2; 15.8.2 | `ACERO_DETALLADO!B114:B126` | Rectas: max(20cm,.24fy/sqrt(fc)db,.043fy db); ambas caras; sin crédito por gancho. |
| Transferencia lateral en junta | E.060 11.7.4/5/6/8/9; 15.8.1.4; 9.3.2.3 | `ACERO_DETALLADO!B128:B132` | Mu concreto según junta; fy≤420MPa; Avf dedicada, anclada y con referencia de plano; límite de concreto. |
| Recubrimientos / separación libre | E.060 7.7.1, 7.6.1, 3.3.2 | `INGRESO_DATOS!C86/C89/C91/C151:C152; ACERO_DETALLADO!B142:B144/B171:B173` | Exposición explícita por cara; contra suelo 7cm, contacto 4/5cm; libre≥db,2.5cm,4/3Dmax. |
| Deslizamiento / volteo | Criterios de ingeniería ingresados; no se atribuyen FS universales al RNE | `PRESIONES_SERVICIO!B43:G55; INGRESO_DATOS!C126:C132` | FS exigido y su fuente son entradas; pasivo no considerado por defecto; cuatro bordes con acciones firmadas. |

## F–H. Hallazgos y correcciones

1. Fase 1 calculaba caras, pero `FLEXION_ACERO!D5:D8` usaba máximos globales de los nombres `diagx/y_m_pos/neg`. Esto incorporaba saltos dentro de la columna. Se corrigieron las fuentes a momentos de caras, calculados desde extremos libres. Los máximos globales se conservan exclusivamente en diagramas/visualización.
2. Faltaba E.050 28: se añadió área efectiva de servicio con sus límites geométricos y q asociada, separada de la presión lineal.
3. No existían opciones visibles 15.2.4/5: se añadieron apagadas por defecto; 0.8 requiere seis componentes sísmicas y conserva la gravedad.
4. `rho=0.0018` no era universal: fy heredado 4200kgf/cm² equivale a **411.8793MPa**, menor que 420MPa. Por ello corresponde **.0020** para corrugadas. No se cambió fy ni rho ingresados; se impone el máximo normativo. Lisas .0025; malla soldada fy≥420MPa .0018; malla menor no recibe un valor inventado. Lisas/mallas quedan fuera del motor de resistencia/desarrollo implementado.
5. Faltaba distribución 15.4.4: se añadió automáticamente para ambos ejes, conteos y As reales en franja central y zonas exteriores, individualmente por lado. No basta sumar acero colocado solamente en un extremo. Se controla que conteos y separaciones quepan físicamente.
6. Cortante tenía peraltes inferiores fijos: cuando hay inversión de demanda neta con contacto bruto todavía compresivo se usa la capa superior traccionada correspondiente. Se conserva integral exacta y se añade Vu firmado.
7. El filtro de borde F1 mezclaba la ubicación de la columna con la del corte. Se separó el perímetro a d/2 realmente contenido de un margen **adicional voluntario** de distancia libre≥d. No se presenta ese margen como artículo de la norma.
8. Se reauditaron, sin reescribir lo correcto, las tres capacidades de punzonamiento, d físico, bo, Vu neto, gamma_f/gamma_v, J y cuatro esquinas. Se corrigió la franja c+3h para columna descentrada mediante intersección de sus límites reales con la zapata.
9. La advertencia genérica de acero local se reemplazó por comprobación de demanda, As requerido, conteo/As real dentro de la franja y anclajes declarados en ambos lados. Cuando falte un dato se muestra REQUIERE DATOS.
10. Se añadió desarrollo de parrillas y conexión, recubrimientos por cara y altura sobre refuerzo. La posición física de la barra decide psi_t; no su nombre. Una columna excéntrica puede exigir acero superior local incluso con Mx/My aplicados iguales a cero; ese acero también requiere terminación, desarrollo y recubrimiento.
11. Se añadieron aplastamiento en ambas superficies, .005Ag atravesando junta, anclaje recto a compresión, transferencia lateral por fricción de concreto y bloqueo explícito de interacción P-Mx-My/torsión/tracción/empalmes no demostrados.
12. Se añadieron EMS/inclinación, base bruta/neta de qadm, deslizamiento y volteo con fuentes de FS del usuario. No se asignaron factores geotécnicos universales ni resistencia pasiva oculta.
13. Se reforzó validación con IF exterior antes de divisiones/MOD y operaciones sobre texto. Los dropdowns no son la única defensa contra pegado inválido. Se protegen también consumidores heredados de presión, grillas y gráficos ante datos faltantes/inválidos.
14. Se sustituyó la mezcla de advertencias e incumplimientos por seis estados diferenciados. RESUMEN conserva una tabla de 25 controles, para que una prioridad global no oculte fallos o pendientes simultáneos.


## L. Mecánica, signos y auditoría dimensional

P interno positivo comprime: `P=inp_sign_p*P_ingresado`. Mx/My son acciones sobre la zapata en ejes globales de mano derecha. El traslado usa Mx−Fy·zh y My+Fx·zh. Para columna (xc,yc), Qx=P·xc+My, Qy=P·yc−Mx; ex=Qx/Q, ey=Qy/Q. Los momentos respecto al origen son Mx−P·yc, My+P·xc. No se cambia esta convención según el nombre de caso.

El campo físico bruto es `q=Q/A+(Pxc+My)x/Iy+(Pyc−Mx)y/Ix`. Servicio utiliza acciones no amplificadas; resistencia utiliza acciones últimas y pesos con factores heredados explícitos. Para el cuerpo de zapata se integra q neta restando pesos uniformes de zapata/relleno, tal como el método F1 auditado. No se mezcla esa q neta estructural con la opción qadm NETA del EMS. Pesos/relleno se modelan uniformes; cargas distribuidas no uniformes no están implementadas.

En E.050 28 `Bx_ef=Bx−2|ex|`, `By_ef=By−2|ey|`, `Aef=Bx_ef*By_ef`. Se usa qef=Q/Aef solo para control geotécnico. Si alguna dimensión≤0 no se divide ni se continúa con un área ficticia. El control qmax físico≤qadm conservado de F1 se identifica como comparación adicional conservadora con el EMS; no se afirma que el Art.28 exija reemplazar q física por qef o que obligue universalmente a controlar el pico lineal.

La opción BRUTA conserva la interpretación F1. NETA exige sigma0 proporcionada por EMS y compara qef−sigma0 (y qmax físico−sigma0) con qadm neta. Es una convención de comparación explícita que el EMS debe autorizar, no una deducción automática de gamma_s·Df ni un nuevo cálculo de capacidad portante. Si la definición del EMS difiere, requiere análisis específico.

| Conversión | Valor exacto utilizado | Uso |
|---|---|---|
| 1kgf | 9.80665N | Fuerzas SI |
| 1tf | 1000kgf = 9806.65N | Capacidades/acciones |
| 1kgf/cm² | 0.0980665MPa = 10tf/m² | Materiales y presión |
| 1MPa | 1/0.0980665kgf/cm² | Norma SI a libro |
| 1tf/m² | .1kgf/cm² = .00980665MPa | Contacto |
| 1tf·m | 100000kgf·cm = 9806.65N·m | Flexión y esfuerzos biaxiales |
| 1m | 100cm = 1000mm | Geometría |
| 1m² | 10000cm² | Ag y franjas |
| 1cm⁴ | 10000mm⁴ | J de sección crítica |
| 1tf/m³ | .001kgf/cm³ | Peso específico |
| K=1/sqrt(.0980665) | 3.193299567810587 | Coeficientes sqrt(fc) |

Entradas y resultados de usuario quedan en tf, tf·m, tf/m², kgf/cm², m, cm, cm² y cm⁴. MPa/N/mm se usan solamente en conversiones normativas transparentes y comprobaciones independientes. No hay entrada nueva obligatoria en unidades SI distintas de las solicitadas.

## Criterios conservadores y alcance implementado

- Peralte de punzonamiento: promedio de los dos peraltes físicos, hipótesis explícita de dos capas ortogonales conservada de F1; flexión/cortante usan su peralte individual. La E.060 no se cita como si escribiera literalmente esa media.
- Esfuerzo biaxial: se conserva máxima magnitud de las cuatro esquinas; las componentes y extremos algebraicos permanecen visibles. No se usa ABS para convertir levantamiento en compresión.
- Margen libre≥d para columna INTERIOR es filtro voluntario de aplicación, separado de la contención normativa del perímetro a d/2. Si falla, queda fuera de alcance aunque exista un perímetro cerrado.
- Gamma_f básico, sin incremento opcional 13.5.3.2. Demanda local se combina por suma de magnitudes con la demanda global de caras y se comprueba conservadoramente en ambas capas. No se acredita automáticamente As global por metro como refuerzo local.
- En desarrollo a tracción se usa Ktr=0 permitido, sin reducción por exceso de acero ni reducción opcional del producto de factores de tabla12.2. Se conservan psi_t, psi_e y psi_s completos, razón (cb+Ktr)/db≤2.5, sqrt(fc)≤8.3MPa^.5 y ld≥30cm.
- Aplastamiento: factor opcional sqrt(A2/A1)=1, conservador, sin inventar geometría A2. La capacidad del concreto no demuestra flexocompresión. Solo el dominio axial en compresión, barras rectas confirmadas y junta lateral comprobada puede producir CUMPLE del conjunto implementado.
- Avf es acero dedicado a cortante por fricción, distinto del acero axial mínimo, con confirmación explícita de anclaje y referencia de plano. Su detalle/anclaje se acepta como dato externo verificado; no se diseña una armadura de cortante completa a partir de una sola área. Declarar junta RUGOSA implica superficie limpia, libre de lechada y rugosidad de amplitud completa aproximadamente 6mm o más, según 11.7.9. No se acredita compresión permanente ni resistencia pasiva por defecto.
- Separación libre usa db,2.5cm,4/3Dmax para barras paralelas de cada parrilla; el cruce ortogonal de las dos capas no se confunde con paquetes o barras paralelas apiladas.


## P–Q. Pruebas independientes y resultados

Se ejecutaron **73 escenarios nativos** en copia descartable y **10857 comprobaciones independientes**, con **0 fallos**. Todos los escenarios tuvieron 0 errores de fórmula y 0 referencias circulares. Las entradas de ensayo nunca se guardaron en el entregable.

La verificación no se limitó a ausencia de errores: incluyó cuadratura de Gauss 2D de presión y ΣF/ΣMx/ΣMy desde acciones originales; cuadratura de voladizos/caras y cortes; As por bisección de capacidad; tres Vc y esfuerzos de punzonamiento calculados en SI; J/gamma, reacción y momentos críticos; distribución por zonas; acero local y desarrollo en SI/mm; aplastamiento, .005Ag y anclajes; fricción de junta y momentos de vuelco respecto a cada borde. Se verificaron estados físicos esperados seleccionados independientemente, entradas preservadas, estructura OOXML y persistencia nativa.

Tolerancia independiente: `abs(a−b)≤max(1e−8,1e−8*max(|a|,|b|))` en las unidades del resultado, implementada con math.isclose(abs_tol=1e−8,rel_tol=1e−8). Las integrales de campos lineales se calculan con Gauss de orden4, exacto para estos polinomios salvo redondeo. El cierre interno de diagramas usa `MAX(1e−8,1e−10*escala de acciones)` para fuerza/momento; no se fuerza el extremo a cero. Se evita activar acero por ruido de magnitud≤1e−6tf·m en transferencias locales.

### Matriz de escenarios: valores numéricos y estados

Guion significa cálculo bloqueado/no aplicable, no cero físico. Las columnas numéricas son resultados nativos contrastados cuando su estado permite cálculo; resultados de casos fuera de alcance no se presentan como diseño certificado.

| Escenario | qmax servicio tf/m² | Aef m² | Mu cara X inf tf·m/m | Mu cara Y inf tf·m/m | Vu punz tf | D/C punz | Equilibrio X/Y | Estado global | Errores |
|---|---:|---:|---:|---:|---:|---:|---|---|---:|
| base-preservada | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.142152 | 0.825378686 | OK/OK | NO CUMPLE | 0 |
| cuadrada-centrada-completa | 11.0731413 | 14.0625 | 14.8775436 | 14.8775436 | 142.251133 | 0.837399934 | OK/OK | CUMPLE | 0 |
| rectangular-X-larga | 11.3720222 | 13.5 | 23.2133648 | 9.33505926 | 141.964097 | 0.835710218 | OK/OK | CUMPLE | 0 |
| rectangular-Y-larga | 11.3720222 | 13.5 | 9.33505926 | 23.2133648 | 141.964097 | 0.835710218 | OK/OK | CUMPLE | 0 |
| columna-rectangular | 11.0731413 | 14.0625 | 12.3322209 | 15.779012 | 140.859796 | 0.771059371 | OK/OK | NO CUMPLE | 0 |
| columna-excentrica-X | 14.3608311 | 12.3173045 | 22.5508477 | 9.33505926 | 141.581382 | 0.83402642 | OK/OK | CUMPLE | 0 |
| columna-excentrica-Y | 14.3608311 | 12.3173045 | 9.33505926 | 22.5508477 | 141.581382 | 0.83402642 | OK/OK | CUMPLE | 0 |
| excentricidad-biaxial | 13.5980871 | 13.0137786 | 14.8519977 | 14.8773927 | 142.107698 | 0.837132551 | OK/OK | CUMPLE | 0 |
| momento-Mx | 11.0731413 | 14.0625 | 14.8775436 | 17.6795663 | 142.251133 | 1.04301521 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| momento-My | 11.0731413 | 14.0625 | 17.6795663 | 14.8775436 | 142.251133 | 1.04301521 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| momento-biaxial | 11.0731413 | 14.0625 | 16.5587572 | 17.1191617 | 142.251133 | 1.12526133 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| signos-inversos | 11.0731413 | 14.0625 | 16.5587572 | 17.1191617 | 142.251133 | 1.12526133 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| contacto-parcial-ultimo | 11.1526948 | 14.0288371 | — | — | — | — | REQUIERE ANÁLISIS ESPECIAL/REQUIERE ANÁLISIS ESPECIAL | REQUIERE ANÁLISIS ESPECIAL | 0 |
| contacto-parcial-servicio | 31.5531413 | 6.58062535 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| levantamiento | -10.2426688 | — | — | — | — | — | REQUIERE ANÁLISIS ESPECIAL/REQUIERE ANÁLISIS ESPECIAL | REQUIERE ANÁLISIS ESPECIAL | 0 |
| P-cero | 3.97955342 | 13.9669938 | — | — | — | — | REQUIERE ANÁLISIS ESPECIAL/REQUIERE ANÁLISIS ESPECIAL | REQUIERE ANÁLISIS ESPECIAL | 0 |
| h-insuficiente | 10.6246948 | 14.0271523 | 14.903098 | 14.9638459 | 145.498731 | 2.60715724 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| separacion-excesiva | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| minimo-gobernante | 11.0731413 | 14.0625 | 0.997555556 | 0.997555556 | 9.53809394 | 0.0561485808 | OK/OK | CUMPLE | 0 |
| cara-X-izquierda | 11.0731413 | 14.0625 | 17.6795663 | 14.8775436 | 142.251133 | 1.04301521 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| cara-X-derecha | 11.0731413 | 14.0625 | 17.6795663 | 14.8775436 | 142.251133 | 1.04301521 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| transferencia-biaxial | 11.0731413 | 14.0625 | 19.3607799 | 21.6023981 | 142.251133 | 1.65986106 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| area-efectiva-E050 | 13.9175858 | 12.88313 | 14.8775436 | 14.8775436 | 142.251133 | 0.837399934 | OK/OK | CUMPLE | 0 |
| dimension-efectiva-X-negativa | 56.6464548 | — | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| dimension-efectiva-Y-negativa | 56.6016036 | — | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| sismo-opciones-apagadas | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| sismo-opciones-activadas | 10.7101174 | 14.0344885 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| sismo-sin-componentes | — | — | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| reduccion-no-sismica | — | — | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | DATOS INVÁLIDOS | 0 |
| incremento-no-temporal | — | — | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | DATOS INVÁLIDOS | 0 |
| barra-inexistente | — | — | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| dimension-cero | — | — | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| dimension-negativa | — | — | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| columna-parcialmente-fuera | — | — | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| columna-fuera | — | — | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| separacion-cero | 11.1526948 | 14.0288371 | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| fy-invalido | — | — | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| fc-invalido | — | — | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| phi-flexion-invalido | 11.1526948 | 14.0288371 | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| phi-cortante-invalido | 11.1526948 | 14.0288371 | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| phi-punzonamiento-invalido | 11.1526948 | 14.0288371 | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| recubrimiento-excesivo | 11.1526948 | 14.0288371 | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| dimensiones-texto | — | — | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| cargas-texto | 11.1526948 | 14.0288371 | — | — | — | — | DATOS INVÁLIDOS/DATOS INVÁLIDOS | DATOS INVÁLIDOS | 0 |
| fy-mayor-420MPa | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| rho-usuario-menor-norma | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| desarrollo-insuficiente | 56.8943222 | 1.94198716 | 9.55895981 | 9.67182945 | 99.7141364 | 0.594316633 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| gancho-inferior | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| falta-recubrimiento-lateral | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| local-sin-acero | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| interfase-minimo-insuficiente | 11.0731413 | 14.0625 | 14.8775436 | 14.8775436 | 142.251133 | 0.837399934 | OK/OK | NO CUMPLE | 0 |
| interfase-anclaje-insuficiente | 11.0731413 | 14.0625 | 14.8775436 | 14.8775436 | 142.251133 | 0.837399934 | OK/OK | NO CUMPLE | 0 |
| pasivo-datos-faltantes | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| qadm-neta | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| qadm-neta-sin-sigma0 | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| borde-bloqueado | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | — | — | OK/OK | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| esquina-bloqueada | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | — | — | OK/OK | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| perimetro-cerrado-pero-filtro-conservador | 27.2205313 | 7.23971091 | 50.140868 | 14.9638459 | — | — | OK/OK | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| concreto-liviano | 11.1526948 | 14.0288371 | — | — | — | — | FUERA DEL ALCANCE IMPLEMENTADO/FUERA DEL ALCANCE IMPLEMENTADO | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| inversion-neta-con-contacto-completo | 11.0731413 | 14.0625 | 2.99266667 | 7.47590301 | 28.6142818 | 0.497430191 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| conteo-central-no-cabe | 11.0731413 | 14.0625 | 14.8775436 | 14.8775436 | 142.251133 | 0.837399934 | OK/OK | NO CUMPLE | 0 |
| acero-exterior-todo-un-lado | 11.3720222 | 13.5 | 23.2133648 | 9.33505926 | 141.964097 | 0.835710218 | OK/OK | NO CUMPLE | 0 |
| anclaje-negativo | 11.0731413 | 14.0625 | 14.8775436 | 14.8775436 | 142.251133 | 0.837399934 | OK/OK | DATOS INVÁLIDOS | 0 |
| fc-menor-17MPa | 11.0731413 | 14.0625 | 14.8775436 | 14.8775436 | 142.251133 | 0.930717991 | OK/OK | NO CUMPLE | 0 |
| fc-columna-menor-17MPa | 11.0731413 | 14.0625 | 14.8775436 | 14.8775436 | 142.251133 | 0.837399934 | OK/OK | NO CUMPLE | 0 |
| recubrimiento-superior-insuficiente | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| recubrimiento-superior-no-aplica | 11.0731413 | 14.0625 | 14.8775436 | 14.8775436 | 142.251133 | 0.837399934 | OK/OK | CUMPLE | 0 |
| exposicion-superior-faltante | 11.1526948 | 14.0288371 | 14.903098 | 14.9638459 | 142.251133 | 0.845608096 | OK/OK | REQUIERE ANÁLISIS ESPECIAL | 0 |
| malla-fy-menor-420MPa | 11.1526948 | 14.0288371 | — | — | — | — | FUERA DEL ALCANCE IMPLEMENTADO/FUERA DEL ALCANCE IMPLEMENTADO | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| malla-fy-mayor-420MPa | 11.1526948 | 14.0288371 | — | — | — | — | FUERA DEL ALCANCE IMPLEMENTADO/FUERA DEL ALCANCE IMPLEMENTADO | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| barra-lisa | 11.1526948 | 14.0288371 | — | — | — | — | FUERA DEL ALCANCE IMPLEMENTADO/FUERA DEL ALCANCE IMPLEMENTADO | FUERA DEL ALCANCE IMPLEMENTADO | 0 |
| columna-excentrica-sin-terminacion-superior | 12.4503845 | 13.4794832 | 14.8519977 | 14.8775436 | 142.166483 | 0.837216337 | OK/OK | REQUIERE DATOS | 0 |
| columna-excentrica-gancho-superior | 12.4503845 | 13.4794832 | 14.8519977 | 14.8775436 | 142.166483 | 0.837216337 | OK/OK | FUERA DEL ALCANCE IMPLEMENTADO | 0 |

Las pruebas cubren los 26 casos mínimos solicitados y límites adicionales. En particular: ambas orientaciones rectangulares; cuadrada; columna rectangular/excéntrica/biaxial; signos; cara izquierda/derecha; contacto parcial en servicio y último; levantamiento/P=0; negativos y texto; barras no existentes; phi no normativos; cuantía, fc≥17MPa y separaciones; desarrollo, ganchos, ausencia de datos y acero local; zonas exteriores individuales y conteos imposibles; EMS neto; sismo apagado/activado/componentes faltantes; borde/esquina; inversión neta con contacto bruto completo; recubrimiento superior aplicable/no aplicable; lisas/mallas; desarrollo superior local en columna excéntrica.

`ACERO_DETALLADO!B93` y `B137` identifican por nombre los datos no declarados de armado local y conexión; cada nombre lleva a una entrada editable descrita en INGRESO_DATOS. En `B135` se identifica el análisis adicional necesario para momentos/tracción/torsión. Se contrastaron los diagnósticos del caso original y los colores efectivos de los cinco resultados principales para todos los escenarios.

### Caso heredado: resultado conservado sin optimizar

| Resultado | Valor final | Celda |
|---|---:|---|
| qmax física tf/m² | 11.1526948 | `PRESIONES_SERVICIO!D10` |
| qmin física tf/m² | 10.9935879 | `PRESIONES_SERVICIO!D11` |
| Área efectiva m² | 14.0288371 | `PRESIONES_SERVICIO!B28` |
| qef bruta tf/m² | 11.0997119 | `PRESIONES_SERVICIO!B29` |
| qadm aplicada tf/m² | 8.5 | `PRESIONES_SERVICIO!B32` |
| Mu cara X tf·m/m | 14.903098 | `FLEXION_ACERO!D5` |
| Mu cara Y tf·m/m | 14.9638459 | `FLEXION_ACERO!D6` |
| As requerido inferior X cm²/m | 10 | `FLEXION_ACERO!H5` |
| As requerido inferior Y cm²/m | 10.0440319 | `FLEXION_ACERO!H6` |
| As colocado inferior X cm²/m | 8.6 | `ACERO_DETALLADO!H5` |
| As colocado inferior Y cm²/m | 8.6 | `ACERO_DETALLADO!H6` |
| phi Vc tf | 173.888938 | `PUNZONAMIENTO!B16` |
| Vu neto tf | 142.142152 | `PUNZONAMIENTO!B14` |
| D/C biaxial | 0.825378686 | `PUNZONAMIENTO!B17` |
| Altura sobre parrilla cm | 39.96 | `GEOMETRIA!B2622` |
| Estado global | NO CUMPLE | `RESUMEN!B23` |

El estado global NO CUMPLE se debe a incumplimientos comprobados del caso; además permanecen controles necesarios en REQUIERE DATOS. Se separan todos en RESUMEN!B70:B94. No se declara cumplimiento integral del proyecto por el resultado de punzonamiento aislado.

## T. Excel 2016, apertura y QA final

Se abrió con Microsoft Excel 16.0 en modo normal, sin ruta de reparación; CalculateFullRebuild, guardado, cierre, reapertura, nuevo recálculo y guardado/cierre, y apertura posterior en solo lectura. Los resultados/entradas críticos de todos los snapshots persistieron. No se solicitó reparación. Se comprobó la caché final y no se encontraron #REF!, #DIV/0!, #VALUE!, #NAME?, #N/A ni #NUM!. Sin referencias circulares, vínculos externos, VBA, _xlfn, _xludf ni funciones modernas prohibidas. Las fórmulas OOXML/COM usan nombres ingleses estándar; Excel español las presenta localizadas automáticamente. Listas y CF se verificaron mediante Excel español/FormulaLocal; el factor sísmico es una lista numérica de rango, evitando ambigüedad decimal.

Se revisaron 27 vistas nativas Fase 2 que abarcan las 15 hojas, comparadas con Fase 1, y los 24 gráficos exportados por Excel. Se preservaron contenido/tipo/referencias de gráficos; el gráfico de As refleja las nuevas demandas de caras. Encabezados, entradas amarillas, resultados verdes y estados exactos rojo/amarillo/verde son visibles. Se corrigieron textos recortados mediante abreviación/espacios de nota combinados, sin ocultar fórmulas o sustituirlas por valores. La revisión PDF auxiliar no modifica la impresión del archivo final.

## R–S. Pendientes, fuera de alcance y decisiones de proyecto

| Tema | Estado / dato necesario | Motivo y alcance |
|---|---|---|
| Contacto parcial/P≤0 | REQUIERE ANÁLISIS ESPECIAL | Falta solucionador compresivo equilibrado ΣF/ΣMx/ΣMy; no se recorta q. |
| BORDE/ESQUINA y proximidad al borde | FUERA DEL ALCANCE IMPLEMENTADO | Orientación editable, pero faltan perímetro abierto mínimo, centroide real, J biaxial y comprobación de secciones alternas. No se reutiliza perímetro interior. |
| Conexión con Mx/My/Mz/tracción | REQUIERE ANÁLISIS ESPECIAL después de completar datos básicos | Faltan coordenadas y disposición de barras verticales, compatibilidad de deformaciones, interacción P-Mx-My, torsión y empalmes 12.17. Acero local horizontal no sustituye esos controles. |
| Ganchos, paquetes, cortes/cambios de armado/sección, empalmes | FUERA DEL ALCANCE IMPLEMENTADO o análisis específico | Solo rectas corrugadas continuas desarrolladas en ambas caras. No se aplican fórmulas de gancho a barras rectas ni desarrollo de compresión por gancho. |
| Concreto liviano/lisas/mallas/prefabricada | FUERA DEL ALCANCE IMPLEMENTADO | Se muestran mínimos de 9.7 donde la tabla aplica, pero no se certifica un motor de resistencia/anclaje ajeno al alcance implementado. |
| qadm y cargas inclinadas | REQUIERE DATOS | Referencia/página EMS, base BRUTA/NETA, sigma0 si neta y confirmación de reducción por inclinación. No se inventan c, phi ni capacidad portante. |
| Acero real y distribución | REQUIERE DATOS si no se declaró | Conteos centrales/exteriores por ambos lados, espaciamientos regionales, detalle concentrado y conteos/longitudes locales deben coincidir con plano real. Las celdas vacías no se llenaron para obtener CUMPLE. |
| Desarrollo / recubrimiento | REQUIERE DATOS | Recubrimiento lateral y exposición, terminación, epoxi, Dmax, longitudes y barras de columna/dowels. Inferior CONTRA SUELO/superior CONTACTO SUELO son hipótesis visibles editables que deben confirmarse. |
| Transferencia lateral | REQUIERE DATOS | Tipo de junta concreto, Avf dedicada, confirmación de anclaje y referencia de plano. Mu de concreto no es mu suelo-zapata. |
| Deslizamiento / volteo | REQUIERE DATOS cuando aplica | FS exigido y fuente de ingeniería, y resistencia pasiva/fuente solo si se decide incluirla. No se atribuye un FS genérico a E.050. Si demanda nula, NO APLICA no impide CUMPLE. |
| Combinaciones/importación/otras cimentaciones | No implementado | Un estado manual; sin 60 combinaciones, envolventes, ETABS/SAP, macros, optimización, pilotes, zapatas combinadas o solver no lineal. |

No se requiere una decisión del usuario para terminar esta auditoría. Para usarla en un proyecto, el responsable debe decidir y documentar las opciones temporales 15.2.4/5, definición EMS de qadm, FS y pasivo, exposiciones reales y plano de armado/conexión. Ninguna elección opcional se activó automáticamente. Los controles implementados pueden producir CUMPLE solo dentro de su dominio y con todos los datos aplicables, demostrado en pruebas axiales y excéntricas completas; esto no elimina los límites arriba identificados.


## I–K. Registro completo de fórmulas/celdas anteriores y nuevas

Comparación directa F1→F2 guardada por Excel. Se agrupan filas consecutivas únicamente si ambos patrones anterior/nuevo se trasladan exactamente con referencias relativas y comparten motivo técnico. Se muestran las fórmulas exactas de la primera celda: cada fila del rango se reconstruye trasladando referencias relativas; nombres/absolutas permanecen. Una celda vacía se distingue de cero. Las unidades y artículos aplicables se identifican en la matriz normativa y en las notas de cada bloque.

6795 celdas con cambio de contenido, consolidadas en 1252 registros; cero cambios fuera del manifiesto. La mayoría corresponde a guardas de las dos grillas de 2601 puntos y consumidores dependientes, no a cambios de acciones.

| Hoja | Celda/rango | Anterior | Nueva | Motivo técnico |
|---|---|---|---|---|
| INGRESO_DATOS | `A25` | `Cuantia minima` | `Cuantía mínima adicional del usuario` | 9.7/10.5.4: rho efectiva = MAX(normativa,usuario). |
| INGRESO_DATOS | `A26` | `Separacion maxima normativa` | `Separación máxima adicional usuario` | 10.5.4: MIN(3h,40cm,usuario). |
| INGRESO_DATOS | `A73` | `(vacía)` | `FASE 2: SERVICIO / EMS` | FASE 2: SERVICIO / EMS |
| INGRESO_DATOS | `A74` | `(vacía)` | `Tipo de caso de servicio` | No infiere casos por nombre. |
| INGRESO_DATOS | `A75` | `(vacía)` | `Incrementar qadm 30%` | 15.2.4: solo SISMO/VIENTO; opción explícita. |
| INGRESO_DATOS | `A76` | `(vacía)` | `Factor sísmico para suelo` | 15.2.5: 0.80 requiere componentes sísmicas CARGAS!C33:C38. |
| INGRESO_DATOS | `A77` | `(vacía)` | `Base de qadm del EMS` | BRUTA conserva interpretación F1. Confirmar con EMS; NETA requiere sigma0. |
| INGRESO_DATOS | `A78` | `(vacía)` | `sigma0 de referencia EMS` | Ingresar solo si qadm es NETA; no se calcula de Df. |
| INGRESO_DATOS | `A79` | `(vacía)` | `EMS contempla carga inclinada` | E.050 art.29; SI exige referencia EMS. |
| INGRESO_DATOS | `A80` | `(vacía)` | `Referencia del EMS / qadm` | Identificar EMS y página que sustenta qadm y carga inclinada. |
| INGRESO_DATOS | `A81` | `(vacía)` | `Orientación del borde libre` | BORDE/ESQUINA se mantienen fuera del alcance de perímetros abiertos. |
| INGRESO_DATOS | `A83` | `(vacía)` | `FASE 2: REFUERZO Y DESARROLLO` | FASE 2: REFUERZO Y DESARROLLO |
| INGRESO_DATOS | `A84` | `(vacía)` | `Tipo de refuerzo` | 9.7.2: cuantía depende de tipo y fy. Desarrollo implementado: corrugadas. |
| INGRESO_DATOS | `A85` | `(vacía)` | `Tipo de concreto` | NORMAL conserva hipótesis F1. Liviano requiere análisis específico. |
| INGRESO_DATOS | `A86` | `(vacía)` | `Recubrimiento lateral real` | Dato faltante: distancia libre al extremo/lado de barras. |
| INGRESO_DATOS | `A87` | `(vacía)` | `Terminación barras inferiores` | RECTA implementada; GANCHO requiere geometría y 12.5. |
| INGRESO_DATOS | `A88` | `(vacía)` | `Revestimiento de barras` | Confirmar SIN EPOXI o EPOXI; afecta psi_e. |
| INGRESO_DATOS | `A89` | `(vacía)` | `Condición del recubrimiento lateral` | 7.7.1: contra suelo 7cm; contacto suelo 4/5cm. |
| INGRESO_DATOS | `A90` | `(vacía)` | `Terminación barras superiores` | Necesaria si la flexión/local requiere parrilla superior. |
| INGRESO_DATOS | `A91` | `(vacía)` | `Diámetro máximo agregado` | 3.3.2 y 7.6: comprobar separación libre >=4/3 Dmáx. |
| INGRESO_DATOS | `A92` | `(vacía)` | `Detalle local concentrado confirmado` | Confirmar conteos dentro de franjas efectivas 13.5.3.3. |
| INGRESO_DATOS | `A93` | `(vacía)` | `N barras locales inferiores X` | Barras X realmente dentro de ancho efectivo en Y. |
| INGRESO_DATOS | `A94` | `(vacía)` | `N barras locales inferiores Y` | Barras Y realmente dentro de ancho efectivo en X. |
| INGRESO_DATOS | `A95` | `(vacía)` | `N barras locales superiores X` | No se asume que la parrilla superior existe. |
| INGRESO_DATOS | `A96` | `(vacía)` | `N barras locales superiores Y` | No se asume que la parrilla superior existe. |
| INGRESO_DATOS | `A97` | `(vacía)` | `Anclaje local inferior X, lado -` | Longitud recta disponible desde cara crítica, lado negativo. |
| INGRESO_DATOS | `A98` | `(vacía)` | `Anclaje local inferior X, lado +` | Longitud recta disponible desde cara crítica, lado positivo. |
| INGRESO_DATOS | `A99` | `(vacía)` | `Anclaje local inferior Y, lado -` | Longitud real declarada; no basta tener As. |
| INGRESO_DATOS | `A100` | `(vacía)` | `Anclaje local inferior Y, lado +` | Longitud real declarada; no basta tener As. |
| INGRESO_DATOS | `A101` | `(vacía)` | `Anclaje local superior X, lado -` | Longitud real declarada. |
| INGRESO_DATOS | `A102` | `(vacía)` | `Anclaje local superior X, lado +` | Longitud real declarada. |
| INGRESO_DATOS | `A103` | `(vacía)` | `Anclaje local superior Y, lado -` | Longitud real declarada. |
| INGRESO_DATOS | `A104` | `(vacía)` | `Anclaje local superior Y, lado +` | Longitud real declarada. |
| INGRESO_DATOS | `A106` | `(vacía)` | `FASE 2: TRANSFERENCIA COLUMNA–ZAPATA` | FASE 2: TRANSFERENCIA COLUMNA–ZAPATA |
| INGRESO_DATOS | `A107` | `(vacía)` | `Sistema columna/pedestal` | Solo columna rectangular construida in situ; otros sistemas bloqueados. |
| INGRESO_DATOS | `A108` | `(vacía)` | `f'c columna/pedestal` | No se asume igual al concreto de la zapata. |
| INGRESO_DATOS | `A109` | `(vacía)` | `fy barras columna/dowels` | Dato de refuerzo a través de la interfase. |
| INGRESO_DATOS | `A110` | `(vacía)` | `Barra longitudinal columna` | BARRAS_PERU; no asumir continuidad. |
| INGRESO_DATOS | `A111` | `(vacía)` | `N total barras de columna` | Entero positivo. |
| INGRESO_DATOS | `A112` | `(vacía)` | `N barras que continúan` | Entero entre cero y N total. |
| INGRESO_DATOS | `A113` | `(vacía)` | `Barra de dowels adicionales` | Ingresar cuando N dowels >0. |
| INGRESO_DATOS | `A114` | `(vacía)` | `N dowels adicionales` | Cero explícito si no existen. |
| INGRESO_DATOS | `A115` | `(vacía)` | `Anclaje columna en zapata` | Longitud recta, sin acreditar gancho a compresión. |
| INGRESO_DATOS | `A116` | `(vacía)` | `Anclaje columna lado superior` | Desarrollo/empalme de lado apoyado. |
| INGRESO_DATOS | `A117` | `(vacía)` | `Anclaje dowels en zapata` | Necesario si hay dowels adicionales. |
| INGRESO_DATOS | `A118` | `(vacía)` | `Anclaje dowels lado superior` | Necesario si hay dowels adicionales. |
| INGRESO_DATOS | `A119` | `(vacía)` | `Terminación columna/dowels` | RECTA implementada para compresión; GANCHO no acredita compresión. |
| INGRESO_DATOS | `A120` | `(vacía)` | `Condición de la junta` | 11.7.4.3; RUGOSA supone limpia y rugosidad >=6mm. |
| INGRESO_DATOS | `A121` | `(vacía)` | `Refuerzo Avf dedicado a cortante` | Área adicional verificada, distribuida y anclada; evita doble uso de barras. |
| INGRESO_DATOS | `A122` | `(vacía)` | `Avf anclado en ambos lados` | 11.7.8; confirmar mediante detalle y capítulo12. |
| INGRESO_DATOS | `A123` | `(vacía)` | `Referencia del detalle de junta` | Plano y verificación de distribución/anclaje Avf. |
| INGRESO_DATOS | `A125` | `(vacía)` | `FASE 2: CRITERIOS DE ESTABILIDAD DEL USUARIO` | FASE 2: CRITERIOS DE ESTABILIDAD DEL USUARIO |
| INGRESO_DATOS | `A126` | `(vacía)` | `FS requerido deslizamiento` | Criterio del diseñador, NO valor atribuido a E.050. |
| INGRESO_DATOS | `A127` | `(vacía)` | `Fuente FS deslizamiento` | Documento/criterio de ingeniería que exige el FS. |
| INGRESO_DATOS | `A128` | `(vacía)` | `Considerar pasivo` | Por defecto NO; no calcula empuje a partir de parámetros inventados. |
| INGRESO_DATOS | `A129` | `(vacía)` | `Resistencia pasiva disponible` | Solo si SI, valor trazable y movilizable proveniente de análisis externo. |
| INGRESO_DATOS | `A130` | `(vacía)` | `Fuente resistencia pasiva` | Datos y análisis que sustentan empuje pasivo. |
| INGRESO_DATOS | `A131` | `(vacía)` | `FS requerido volteo` | Criterio del diseñador, NO valor atribuido a E.050. |
| INGRESO_DATOS | `A132` | `(vacía)` | `Fuente FS volteo` | Momentos respecto a bordes; conserva signo de acciones. |
| INGRESO_DATOS | `A134` | `(vacía)` | `FASE 2: DISTRIBUCIÓN RECTANGULAR Y CONTEOS REALES` | FASE 2: DISTRIBUCIÓN RECTANGULAR Y CONTEOS REALES |
| INGRESO_DATOS | `A135` | `(vacía)` | `Separación central inferior X` | Mismo diámetro X; hereda separación F1 hasta edición explícita. |
| INGRESO_DATOS | `A136` | `(vacía)` | `Separación exterior inferior X` | Mismo diámetro X; no optimiza acero heredado. |
| INGRESO_DATOS | `A137` | `(vacía)` | `N real barras X en franja central` | Conteo del plano dentro de franja; cuadrada: todas las barras X. |
| INGRESO_DATOS | `A138` | `(vacía)` | `N real barras X fuera de franja` | Cero explícito en cuadrada/dirección larga. |
| INGRESO_DATOS | `A139` | `(vacía)` | `Separación central inferior Y` | Mismo diámetro Y; hereda separación F1. |
| INGRESO_DATOS | `A140` | `(vacía)` | `Separación exterior inferior Y` | Mismo diámetro Y; no optimiza acero heredado. |
| INGRESO_DATOS | `A141` | `(vacía)` | `N real barras Y en franja central` | Conteo del plano; cuadrada: todas las barras Y. |
| INGRESO_DATOS | `A142` | `(vacía)` | `N real barras Y fuera de franja` | Cero explícito en cuadrada/dirección larga. |
| INGRESO_DATOS | `A145` | `(vacía)` | `N X exterior lado -Y` | Conteo fuera de franja del lado negativo, si existe. |
| INGRESO_DATOS | `A146` | `(vacía)` | `N X exterior lado +Y` | Ambas zonas deben cumplir; no basta el total exterior. |
| INGRESO_DATOS | `A147` | `(vacía)` | `N Y exterior lado -X` | Conteo fuera de franja del lado negativo, si existe. |
| INGRESO_DATOS | `A148` | `(vacía)` | `N Y exterior lado +X` | N exterior total debe coincidir con suma de ambas zonas. |
| INGRESO_DATOS | `A151` | `(vacía)` | `Exposición de cara inferior` | Hipótesis visible heredada; 7.7.1 determina recubrimiento. |
| INGRESO_DATOS | `A152` | `(vacía)` | `Exposición de cara superior` | Hipótesis visible para suelo sobre zapata; confirmar condición real. |
| INGRESO_DATOS | `B74` | `(vacía)` | `inp_srv_type` | No infiere casos por nombre. |
| INGRESO_DATOS | `B75` | `(vacía)` | `inp_qadm_inc` | 15.2.4: solo SISMO/VIENTO; opción explícita. |
| INGRESO_DATOS | `B76` | `(vacía)` | `inp_eq_factor` | 15.2.5: 0.80 requiere componentes sísmicas CARGAS!C33:C38. |
| INGRESO_DATOS | `B77` | `(vacía)` | `inp_qadm_basis` | BRUTA conserva interpretación F1. Confirmar con EMS; NETA requiere sigma0. |
| INGRESO_DATOS | `B78` | `(vacía)` | `inp_sigma0` | Ingresar solo si qadm es NETA; no se calcula de Df. |
| INGRESO_DATOS | `B79` | `(vacía)` | `inp_ems_incl` | E.050 art.29; SI exige referencia EMS. |
| INGRESO_DATOS | `B80` | `(vacía)` | `inp_ems_ref` | Identificar EMS y página que sustenta qadm y carga inclinada. |
| INGRESO_DATOS | `B81` | `(vacía)` | `inp_edge_dir` | BORDE/ESQUINA se mantienen fuera del alcance de perímetros abiertos. |
| INGRESO_DATOS | `B84` | `(vacía)` | `inp_rebar_type` | 9.7.2: cuantía depende de tipo y fy. Desarrollo implementado: corrugadas. |
| INGRESO_DATOS | `B85` | `(vacía)` | `inp_concrete_type` | NORMAL conserva hipótesis F1. Liviano requiere análisis específico. |
| INGRESO_DATOS | `B86` | `(vacía)` | `inp_rec_lat` | Dato faltante: distancia libre al extremo/lado de barras. |
| INGRESO_DATOS | `B87` | `(vacía)` | `inp_end_inf` | RECTA implementada; GANCHO requiere geometría y 12.5. |
| INGRESO_DATOS | `B88` | `(vacía)` | `inp_epoxy` | Confirmar SIN EPOXI o EPOXI; afecta psi_e. |
| INGRESO_DATOS | `B89` | `(vacía)` | `inp_side_exposure` | 7.7.1: contra suelo 7cm; contacto suelo 4/5cm. |
| INGRESO_DATOS | `B90` | `(vacía)` | `inp_end_sup` | Necesaria si la flexión/local requiere parrilla superior. |
| INGRESO_DATOS | `B91` | `(vacía)` | `inp_agg` | 3.3.2 y 7.6: comprobar separación libre >=4/3 Dmáx. |
| INGRESO_DATOS | `B92` | `(vacía)` | `inp_local_detail` | Confirmar conteos dentro de franjas efectivas 13.5.3.3. |
| INGRESO_DATOS | `B93` | `(vacía)` | `inp_nloc_ix` | Barras X realmente dentro de ancho efectivo en Y. |
| INGRESO_DATOS | `B94` | `(vacía)` | `inp_nloc_iy` | Barras Y realmente dentro de ancho efectivo en X. |
| INGRESO_DATOS | `B95` | `(vacía)` | `inp_nloc_sx` | No se asume que la parrilla superior existe. |
| INGRESO_DATOS | `B96` | `(vacía)` | `inp_nloc_sy` | No se asume que la parrilla superior existe. |
| INGRESO_DATOS | `B97` | `(vacía)` | `inp_ll_ix_m` | Longitud recta disponible desde cara crítica, lado negativo. |
| INGRESO_DATOS | `B98` | `(vacía)` | `inp_ll_ix_p` | Longitud recta disponible desde cara crítica, lado positivo. |
| INGRESO_DATOS | `B99` | `(vacía)` | `inp_ll_iy_m` | Longitud real declarada; no basta tener As. |
| INGRESO_DATOS | `B100` | `(vacía)` | `inp_ll_iy_p` | Longitud real declarada; no basta tener As. |
| INGRESO_DATOS | `B101` | `(vacía)` | `inp_ll_sx_m` | Longitud real declarada. |
| INGRESO_DATOS | `B102` | `(vacía)` | `inp_ll_sx_p` | Longitud real declarada. |
| INGRESO_DATOS | `B103` | `(vacía)` | `inp_ll_sy_m` | Longitud real declarada. |
| INGRESO_DATOS | `B104` | `(vacía)` | `inp_ll_sy_p` | Longitud real declarada. |
| INGRESO_DATOS | `B107` | `(vacía)` | `inp_col_system` | Solo columna rectangular construida in situ; otros sistemas bloqueados. |
| INGRESO_DATOS | `B108` | `(vacía)` | `inp_fc_col` | No se asume igual al concreto de la zapata. |
| INGRESO_DATOS | `B109` | `(vacía)` | `inp_fy_col` | Dato de refuerzo a través de la interfase. |
| INGRESO_DATOS | `B110` | `(vacía)` | `inp_bar_col` | BARRAS_PERU; no asumir continuidad. |
| INGRESO_DATOS | `B111` | `(vacía)` | `inp_n_col` | Entero positivo. |
| INGRESO_DATOS | `B112` | `(vacía)` | `inp_n_continue` | Entero entre cero y N total. |
| INGRESO_DATOS | `B113` | `(vacía)` | `inp_bar_dowel` | Ingresar cuando N dowels >0. |
| INGRESO_DATOS | `B114` | `(vacía)` | `inp_n_dowel` | Cero explícito si no existen. |
| INGRESO_DATOS | `B115` | `(vacía)` | `inp_lcol_foot` | Longitud recta, sin acreditar gancho a compresión. |
| INGRESO_DATOS | `B116` | `(vacía)` | `inp_lcol_above` | Desarrollo/empalme de lado apoyado. |
| INGRESO_DATOS | `B117` | `(vacía)` | `inp_ldow_foot` | Necesario si hay dowels adicionales. |
| INGRESO_DATOS | `B118` | `(vacía)` | `inp_ldow_above` | Necesario si hay dowels adicionales. |
| INGRESO_DATOS | `B119` | `(vacía)` | `inp_end_col` | RECTA implementada para compresión; GANCHO no acredita compresión. |
| INGRESO_DATOS | `B120` | `(vacía)` | `inp_joint` | 11.7.4.3; RUGOSA supone limpia y rugosidad >=6mm. |
| INGRESO_DATOS | `B121` | `(vacía)` | `inp_avf` | Área adicional verificada, distribuida y anclada; evita doble uso de barras. |
| INGRESO_DATOS | `B122` | `(vacía)` | `inp_avf_anchor` | 11.7.8; confirmar mediante detalle y capítulo12. |
| INGRESO_DATOS | `B123` | `(vacía)` | `inp_joint_ref` | Plano y verificación de distribución/anclaje Avf. |
| INGRESO_DATOS | `B126` | `(vacía)` | `inp_fs_slide` | Criterio del diseñador, NO valor atribuido a E.050. |
| INGRESO_DATOS | `B127` | `(vacía)` | `inp_fs_slide_ref` | Documento/criterio de ingeniería que exige el FS. |
| INGRESO_DATOS | `B128` | `(vacía)` | `inp_passive` | Por defecto NO; no calcula empuje a partir de parámetros inventados. |
| INGRESO_DATOS | `B129` | `(vacía)` | `inp_rpassive` | Solo si SI, valor trazable y movilizable proveniente de análisis externo. |
| INGRESO_DATOS | `B130` | `(vacía)` | `inp_rpassive_ref` | Datos y análisis que sustentan empuje pasivo. |
| INGRESO_DATOS | `B131` | `(vacía)` | `inp_fs_over` | Criterio del diseñador, NO valor atribuido a E.050. |
| INGRESO_DATOS | `B132` | `(vacía)` | `inp_fs_over_ref` | Momentos respecto a bordes; conserva signo de acciones. |
| INGRESO_DATOS | `B135` | `(vacía)` | `inp_scx` | Mismo diámetro X; hereda separación F1 hasta edición explícita. |
| INGRESO_DATOS | `B136` | `(vacía)` | `inp_sox` | Mismo diámetro X; no optimiza acero heredado. |
| INGRESO_DATOS | `B137` | `(vacía)` | `inp_ncx` | Conteo del plano dentro de franja; cuadrada: todas las barras X. |
| INGRESO_DATOS | `B138` | `(vacía)` | `inp_nox` | Cero explícito en cuadrada/dirección larga. |
| INGRESO_DATOS | `B139` | `(vacía)` | `inp_scy` | Mismo diámetro Y; hereda separación F1. |
| INGRESO_DATOS | `B140` | `(vacía)` | `inp_soy` | Mismo diámetro Y; no optimiza acero heredado. |
| INGRESO_DATOS | `B141` | `(vacía)` | `inp_ncy` | Conteo del plano; cuadrada: todas las barras Y. |
| INGRESO_DATOS | `B142` | `(vacía)` | `inp_noy` | Cero explícito en cuadrada/dirección larga. |
| INGRESO_DATOS | `B145` | `(vacía)` | `inp_nox_minus` | Conteo fuera de franja del lado negativo, si existe. |
| INGRESO_DATOS | `B146` | `(vacía)` | `inp_nox_plus` | Ambas zonas deben cumplir; no basta el total exterior. |
| INGRESO_DATOS | `B147` | `(vacía)` | `inp_noy_minus` | Conteo fuera de franja del lado negativo, si existe. |
| INGRESO_DATOS | `B148` | `(vacía)` | `inp_noy_plus` | N exterior total debe coincidir con suma de ambas zonas. |
| INGRESO_DATOS | `B151` | `(vacía)` | `inp_bottom_exposure` | Hipótesis visible heredada; 7.7.1 determina recubrimiento. |
| INGRESO_DATOS | `B152` | `(vacía)` | `inp_top_exposure` | Hipótesis visible para suelo sobre zapata; confirmar condición real. |
| INGRESO_DATOS | `C74` | `(vacía)` | `GRAVEDAD` | No infiere casos por nombre. |
| INGRESO_DATOS | `C75` | `(vacía)` | `NO` | 15.2.4: solo SISMO/VIENTO; opción explícita. |
| INGRESO_DATOS | `C76` | `(vacía)` | `1` | 15.2.5: 0.80 requiere componentes sísmicas CARGAS!C33:C38. |
| INGRESO_DATOS | `C77` | `(vacía)` | `BRUTA` | BRUTA conserva interpretación F1. Confirmar con EMS; NETA requiere sigma0. |
| INGRESO_DATOS | `C79` | `(vacía)` | `NO CONFIRMADO` | E.050 art.29; SI exige referencia EMS. |
| INGRESO_DATOS | `C81` | `(vacía)` | `NO APLICA` | BORDE/ESQUINA se mantienen fuera del alcance de perímetros abiertos. |
| INGRESO_DATOS | `C84` | `(vacía)` | `CORRUGADAS` | 9.7.2: cuantía depende de tipo y fy. Desarrollo implementado: corrugadas. |
| INGRESO_DATOS | `C85` | `(vacía)` | `NORMAL` | NORMAL conserva hipótesis F1. Liviano requiere análisis específico. |
| INGRESO_DATOS | `C107` | `(vacía)` | `IN SITU` | Solo columna rectangular construida in situ; otros sistemas bloqueados. |
| INGRESO_DATOS | `C128` | `(vacía)` | `NO` | Por defecto NO; no calcula empuje a partir de parámetros inventados. |
| INGRESO_DATOS | `C135` | `(vacía)` | `=inp_sep_inf_x` | Mismo diámetro X; hereda separación F1 hasta edición explícita. |
| INGRESO_DATOS | `C136` | `(vacía)` | `=inp_sep_inf_x` | Mismo diámetro X; no optimiza acero heredado. |
| INGRESO_DATOS | `C139` | `(vacía)` | `=inp_sep_inf_y` | Mismo diámetro Y; hereda separación F1. |
| INGRESO_DATOS | `C140` | `(vacía)` | `=inp_sep_inf_y` | Mismo diámetro Y; no optimiza acero heredado. |
| INGRESO_DATOS | `C151` | `(vacía)` | `CONTRA SUELO` | Hipótesis visible heredada; 7.7.1 determina recubrimiento. |
| INGRESO_DATOS | `C152` | `(vacía)` | `CONTACTO SUELO` | Hipótesis visible para suelo sobre zapata; confirmar condición real. |
| INGRESO_DATOS | `D74` | `(vacía)` | `-` | No infiere casos por nombre. |
| INGRESO_DATOS | `D75` | `(vacía)` | `-` | 15.2.4: solo SISMO/VIENTO; opción explícita. |
| INGRESO_DATOS | `D76` | `(vacía)` | `-` | 15.2.5: 0.80 requiere componentes sísmicas CARGAS!C33:C38. |
| INGRESO_DATOS | `D77` | `(vacía)` | `-` | BRUTA conserva interpretación F1. Confirmar con EMS; NETA requiere sigma0. |
| INGRESO_DATOS | `D78` | `(vacía)` | `tf/m2` | Ingresar solo si qadm es NETA; no se calcula de Df. |
| INGRESO_DATOS | `D79` | `(vacía)` | `-` | E.050 art.29; SI exige referencia EMS. |
| INGRESO_DATOS | `D80` | `(vacía)` | `-` | Identificar EMS y página que sustenta qadm y carga inclinada. |
| INGRESO_DATOS | `D81` | `(vacía)` | `-` | BORDE/ESQUINA se mantienen fuera del alcance de perímetros abiertos. |
| INGRESO_DATOS | `D84` | `(vacía)` | `-` | 9.7.2: cuantía depende de tipo y fy. Desarrollo implementado: corrugadas. |
| INGRESO_DATOS | `D85` | `(vacía)` | `-` | NORMAL conserva hipótesis F1. Liviano requiere análisis específico. |
| INGRESO_DATOS | `D86` | `(vacía)` | `cm` | Dato faltante: distancia libre al extremo/lado de barras. |
| INGRESO_DATOS | `D87` | `(vacía)` | `-` | RECTA implementada; GANCHO requiere geometría y 12.5. |
| INGRESO_DATOS | `D88` | `(vacía)` | `-` | Confirmar SIN EPOXI o EPOXI; afecta psi_e. |
| INGRESO_DATOS | `D89` | `(vacía)` | `-` | 7.7.1: contra suelo 7cm; contacto suelo 4/5cm. |
| INGRESO_DATOS | `D90` | `(vacía)` | `-` | Necesaria si la flexión/local requiere parrilla superior. |
| INGRESO_DATOS | `D91` | `(vacía)` | `cm` | 3.3.2 y 7.6: comprobar separación libre >=4/3 Dmáx. |
| INGRESO_DATOS | `D92` | `(vacía)` | `-` | Confirmar conteos dentro de franjas efectivas 13.5.3.3. |
| INGRESO_DATOS | `D93` | `(vacía)` | `barras` | Barras X realmente dentro de ancho efectivo en Y. |
| INGRESO_DATOS | `D94` | `(vacía)` | `barras` | Barras Y realmente dentro de ancho efectivo en X. |
| INGRESO_DATOS | `D95:D96` | `(vacía)` | `barras` | No se asume que la parrilla superior existe. |
| INGRESO_DATOS | `D97` | `(vacía)` | `cm` | Longitud recta disponible desde cara crítica, lado negativo. |
| INGRESO_DATOS | `D98` | `(vacía)` | `cm` | Longitud recta disponible desde cara crítica, lado positivo. |
| INGRESO_DATOS | `D99:D100` | `(vacía)` | `cm` | Longitud real declarada; no basta tener As. |
| INGRESO_DATOS | `D101:D104` | `(vacía)` | `cm` | Longitud real declarada. |
| INGRESO_DATOS | `D107` | `(vacía)` | `-` | Solo columna rectangular construida in situ; otros sistemas bloqueados. |
| INGRESO_DATOS | `D108` | `(vacía)` | `kgf/cm2` | No se asume igual al concreto de la zapata. |
| INGRESO_DATOS | `D109` | `(vacía)` | `kgf/cm2` | Dato de refuerzo a través de la interfase. |
| INGRESO_DATOS | `D110` | `(vacía)` | `-` | BARRAS_PERU; no asumir continuidad. |
| INGRESO_DATOS | `D111` | `(vacía)` | `barras` | Entero positivo. |
| INGRESO_DATOS | `D112` | `(vacía)` | `barras` | Entero entre cero y N total. |
| INGRESO_DATOS | `D113` | `(vacía)` | `-` | Ingresar cuando N dowels >0. |
| INGRESO_DATOS | `D114` | `(vacía)` | `barras` | Cero explícito si no existen. |
| INGRESO_DATOS | `D115` | `(vacía)` | `cm` | Longitud recta, sin acreditar gancho a compresión. |
| INGRESO_DATOS | `D116` | `(vacía)` | `cm` | Desarrollo/empalme de lado apoyado. |
| INGRESO_DATOS | `D117:D118` | `(vacía)` | `cm` | Necesario si hay dowels adicionales. |
| INGRESO_DATOS | `D119` | `(vacía)` | `-` | RECTA implementada para compresión; GANCHO no acredita compresión. |
| INGRESO_DATOS | `D120` | `(vacía)` | `-` | 11.7.4.3; RUGOSA supone limpia y rugosidad >=6mm. |
| INGRESO_DATOS | `D121` | `(vacía)` | `cm2` | Área adicional verificada, distribuida y anclada; evita doble uso de barras. |
| INGRESO_DATOS | `D122` | `(vacía)` | `-` | 11.7.8; confirmar mediante detalle y capítulo12. |
| INGRESO_DATOS | `D123` | `(vacía)` | `-` | Plano y verificación de distribución/anclaje Avf. |
| INGRESO_DATOS | `D126` | `(vacía)` | `-` | Criterio del diseñador, NO valor atribuido a E.050. |
| INGRESO_DATOS | `D127` | `(vacía)` | `-` | Documento/criterio de ingeniería que exige el FS. |
| INGRESO_DATOS | `D128` | `(vacía)` | `-` | Por defecto NO; no calcula empuje a partir de parámetros inventados. |
| INGRESO_DATOS | `D129` | `(vacía)` | `tf` | Solo si SI, valor trazable y movilizable proveniente de análisis externo. |
| INGRESO_DATOS | `D130` | `(vacía)` | `-` | Datos y análisis que sustentan empuje pasivo. |
| INGRESO_DATOS | `D131` | `(vacía)` | `-` | Criterio del diseñador, NO valor atribuido a E.050. |
| INGRESO_DATOS | `D132` | `(vacía)` | `-` | Momentos respecto a bordes; conserva signo de acciones. |
| INGRESO_DATOS | `D135` | `(vacía)` | `cm` | Mismo diámetro X; hereda separación F1 hasta edición explícita. |
| INGRESO_DATOS | `D136` | `(vacía)` | `cm` | Mismo diámetro X; no optimiza acero heredado. |
| INGRESO_DATOS | `D137` | `(vacía)` | `barras` | Conteo del plano dentro de franja; cuadrada: todas las barras X. |
| INGRESO_DATOS | `D138` | `(vacía)` | `barras` | Cero explícito en cuadrada/dirección larga. |
| INGRESO_DATOS | `D139` | `(vacía)` | `cm` | Mismo diámetro Y; hereda separación F1. |
| INGRESO_DATOS | `D140` | `(vacía)` | `cm` | Mismo diámetro Y; no optimiza acero heredado. |
| INGRESO_DATOS | `D141` | `(vacía)` | `barras` | Conteo del plano; cuadrada: todas las barras Y. |
| INGRESO_DATOS | `D142` | `(vacía)` | `barras` | Cero explícito en cuadrada/dirección larga. |
| INGRESO_DATOS | `D145` | `(vacía)` | `barras` | Conteo fuera de franja del lado negativo, si existe. |
| INGRESO_DATOS | `D146` | `(vacía)` | `barras` | Ambas zonas deben cumplir; no basta el total exterior. |
| INGRESO_DATOS | `D147` | `(vacía)` | `barras` | Conteo fuera de franja del lado negativo, si existe. |
| INGRESO_DATOS | `D148` | `(vacía)` | `barras` | N exterior total debe coincidir con suma de ambas zonas. |
| INGRESO_DATOS | `D151` | `(vacía)` | `-` | Hipótesis visible heredada; 7.7.1 determina recubrimiento. |
| INGRESO_DATOS | `D152` | `(vacía)` | `-` | Hipótesis visible para suelo sobre zapata; confirmar condición real. |
| INGRESO_DATOS | `E25` | `Editable` | `Se usa MAX(rho norma,rho usuario); ver FLEXION_ACERO!B22:B24.` | No optimizar entrada actual. |
| INGRESO_DATOS | `E26` | `smax = MIN(3h, valor editable)` | `Límite efectivo = MIN(3h,40cm,valor usuario).` | No optimizar entrada actual. |
| INGRESO_DATOS | `E66` | `BORDE/ESQUINA requieren definir perímetro abierto.` | `INTERIOR implementada; BORDE/ESQUINA fuera del alcance hasta probar perímetro abierto.` | No hace cumplimiento ficticio. |
| INGRESO_DATOS | `E74` | `(vacía)` | `No infiere casos por nombre.` | No infiere casos por nombre. |
| INGRESO_DATOS | `E75` | `(vacía)` | `15.2.4: solo SISMO/VIENTO; opción explícita.` | 15.2.4: solo SISMO/VIENTO; opción explícita. |
| INGRESO_DATOS | `E76` | `(vacía)` | `15.2.5: 0.80 requiere componentes sísmicas CARGAS!C33:C38.` | 15.2.5: 0.80 requiere componentes sísmicas CARGAS!C33:C38. |
| INGRESO_DATOS | `E77` | `(vacía)` | `BRUTA conserva interpretación F1. Confirmar con EMS; NETA requiere sigma0.` | BRUTA conserva interpretación F1. Confirmar con EMS; NETA requiere sigma0. |
| INGRESO_DATOS | `E78` | `(vacía)` | `Ingresar solo si qadm es NETA; no se calcula de Df.` | Ingresar solo si qadm es NETA; no se calcula de Df. |
| INGRESO_DATOS | `E79` | `(vacía)` | `E.050 art.29; SI exige referencia EMS.` | E.050 art.29; SI exige referencia EMS. |
| INGRESO_DATOS | `E80` | `(vacía)` | `Identificar EMS y página que sustenta qadm y carga inclinada.` | Identificar EMS y página que sustenta qadm y carga inclinada. |
| INGRESO_DATOS | `E81` | `(vacía)` | `BORDE/ESQUINA se mantienen fuera del alcance de perímetros abiertos.` | BORDE/ESQUINA se mantienen fuera del alcance de perímetros abiertos. |
| INGRESO_DATOS | `E84` | `(vacía)` | `9.7.2: cuantía depende de tipo y fy. Desarrollo implementado: corrugadas.` | 9.7.2: cuantía depende de tipo y fy. Desarrollo implementado: corrugadas. |
| INGRESO_DATOS | `E85` | `(vacía)` | `NORMAL conserva hipótesis F1. Liviano requiere análisis específico.` | NORMAL conserva hipótesis F1. Liviano requiere análisis específico. |
| INGRESO_DATOS | `E86` | `(vacía)` | `Dato faltante: distancia libre al extremo/lado de barras.` | Dato faltante: distancia libre al extremo/lado de barras. |
| INGRESO_DATOS | `E87` | `(vacía)` | `RECTA implementada; GANCHO requiere geometría y 12.5.` | RECTA implementada; GANCHO requiere geometría y 12.5. |
| INGRESO_DATOS | `E88` | `(vacía)` | `Confirmar SIN EPOXI o EPOXI; afecta psi_e.` | Confirmar SIN EPOXI o EPOXI; afecta psi_e. |
| INGRESO_DATOS | `E89` | `(vacía)` | `7.7.1: contra suelo 7cm; contacto suelo 4/5cm.` | 7.7.1: contra suelo 7cm; contacto suelo 4/5cm. |
| INGRESO_DATOS | `E90` | `(vacía)` | `Necesaria si la flexión/local requiere parrilla superior.` | Necesaria si la flexión/local requiere parrilla superior. |
| INGRESO_DATOS | `E91` | `(vacía)` | `3.3.2 y 7.6: comprobar separación libre >=4/3 Dmáx.` | 3.3.2 y 7.6: comprobar separación libre >=4/3 Dmáx. |
| INGRESO_DATOS | `E92` | `(vacía)` | `Confirmar conteos dentro de franjas efectivas 13.5.3.3.` | Confirmar conteos dentro de franjas efectivas 13.5.3.3. |
| INGRESO_DATOS | `E93` | `(vacía)` | `Barras X realmente dentro de ancho efectivo en Y.` | Barras X realmente dentro de ancho efectivo en Y. |
| INGRESO_DATOS | `E94` | `(vacía)` | `Barras Y realmente dentro de ancho efectivo en X.` | Barras Y realmente dentro de ancho efectivo en X. |
| INGRESO_DATOS | `E95:E96` | `(vacía)` | `No se asume que la parrilla superior existe.` | No se asume que la parrilla superior existe. |
| INGRESO_DATOS | `E97` | `(vacía)` | `Longitud recta disponible desde cara crítica, lado negativo.` | Longitud recta disponible desde cara crítica, lado negativo. |
| INGRESO_DATOS | `E98` | `(vacía)` | `Longitud recta disponible desde cara crítica, lado positivo.` | Longitud recta disponible desde cara crítica, lado positivo. |
| INGRESO_DATOS | `E99:E100` | `(vacía)` | `Longitud real declarada; no basta tener As.` | Longitud real declarada; no basta tener As. |
| INGRESO_DATOS | `E101:E104` | `(vacía)` | `Longitud real declarada.` | Longitud real declarada. |
| INGRESO_DATOS | `E107` | `(vacía)` | `Solo columna rectangular construida in situ; otros sistemas bloqueados.` | Solo columna rectangular construida in situ; otros sistemas bloqueados. |
| INGRESO_DATOS | `E108` | `(vacía)` | `No se asume igual al concreto de la zapata.` | No se asume igual al concreto de la zapata. |
| INGRESO_DATOS | `E109` | `(vacía)` | `Dato de refuerzo a través de la interfase.` | Dato de refuerzo a través de la interfase. |
| INGRESO_DATOS | `E110` | `(vacía)` | `BARRAS_PERU; no asumir continuidad.` | BARRAS_PERU; no asumir continuidad. |
| INGRESO_DATOS | `E111` | `(vacía)` | `Entero positivo.` | Entero positivo. |
| INGRESO_DATOS | `E112` | `(vacía)` | `Entero entre cero y N total.` | Entero entre cero y N total. |
| INGRESO_DATOS | `E113` | `(vacía)` | `Ingresar cuando N dowels >0.` | Ingresar cuando N dowels >0. |
| INGRESO_DATOS | `E114` | `(vacía)` | `Cero explícito si no existen.` | Cero explícito si no existen. |
| INGRESO_DATOS | `E115` | `(vacía)` | `Longitud recta, sin acreditar gancho a compresión.` | Longitud recta, sin acreditar gancho a compresión. |
| INGRESO_DATOS | `E116` | `(vacía)` | `Desarrollo/empalme de lado apoyado.` | Desarrollo/empalme de lado apoyado. |
| INGRESO_DATOS | `E117:E118` | `(vacía)` | `Necesario si hay dowels adicionales.` | Necesario si hay dowels adicionales. |
| INGRESO_DATOS | `E119` | `(vacía)` | `RECTA implementada para compresión; GANCHO no acredita compresión.` | RECTA implementada para compresión; GANCHO no acredita compresión. |
| INGRESO_DATOS | `E120` | `(vacía)` | `11.7.4.3; RUGOSA supone limpia y rugosidad >=6mm.` | 11.7.4.3; RUGOSA supone limpia y rugosidad >=6mm. |
| INGRESO_DATOS | `E121` | `(vacía)` | `Área adicional verificada, distribuida y anclada; evita doble uso de barras.` | Área adicional verificada, distribuida y anclada; evita doble uso de barras. |
| INGRESO_DATOS | `E122` | `(vacía)` | `11.7.8; confirmar mediante detalle y capítulo12.` | 11.7.8; confirmar mediante detalle y capítulo12. |
| INGRESO_DATOS | `E123` | `(vacía)` | `Plano y verificación de distribución/anclaje Avf.` | Plano y verificación de distribución/anclaje Avf. |
| INGRESO_DATOS | `E126` | `(vacía)` | `Criterio del diseñador, NO valor atribuido a E.050.` | Criterio del diseñador, NO valor atribuido a E.050. |
| INGRESO_DATOS | `E127` | `(vacía)` | `Documento/criterio de ingeniería que exige el FS.` | Documento/criterio de ingeniería que exige el FS. |
| INGRESO_DATOS | `E128` | `(vacía)` | `Por defecto NO; no calcula empuje a partir de parámetros inventados.` | Por defecto NO; no calcula empuje a partir de parámetros inventados. |
| INGRESO_DATOS | `E129` | `(vacía)` | `Solo si SI, valor trazable y movilizable proveniente de análisis externo.` | Solo si SI, valor trazable y movilizable proveniente de análisis externo. |
| INGRESO_DATOS | `E130` | `(vacía)` | `Datos y análisis que sustentan empuje pasivo.` | Datos y análisis que sustentan empuje pasivo. |
| INGRESO_DATOS | `E131` | `(vacía)` | `Criterio del diseñador, NO valor atribuido a E.050.` | Criterio del diseñador, NO valor atribuido a E.050. |
| INGRESO_DATOS | `E132` | `(vacía)` | `Momentos respecto a bordes; conserva signo de acciones.` | Momentos respecto a bordes; conserva signo de acciones. |
| INGRESO_DATOS | `E135` | `(vacía)` | `Mismo diámetro X; hereda separación F1 hasta edición explícita.` | Mismo diámetro X; hereda separación F1 hasta edición explícita. |
| INGRESO_DATOS | `E136` | `(vacía)` | `Mismo diámetro X; no optimiza acero heredado.` | Mismo diámetro X; no optimiza acero heredado. |
| INGRESO_DATOS | `E137` | `(vacía)` | `Conteo del plano dentro de franja; cuadrada: todas las barras X.` | Conteo del plano dentro de franja; cuadrada: todas las barras X. |
| INGRESO_DATOS | `E138` | `(vacía)` | `Cero explícito en cuadrada/dirección larga.` | Cero explícito en cuadrada/dirección larga. |
| INGRESO_DATOS | `E139` | `(vacía)` | `Mismo diámetro Y; hereda separación F1.` | Mismo diámetro Y; hereda separación F1. |
| INGRESO_DATOS | `E140` | `(vacía)` | `Mismo diámetro Y; no optimiza acero heredado.` | Mismo diámetro Y; no optimiza acero heredado. |
| INGRESO_DATOS | `E141` | `(vacía)` | `Conteo del plano; cuadrada: todas las barras Y.` | Conteo del plano; cuadrada: todas las barras Y. |
| INGRESO_DATOS | `E142` | `(vacía)` | `Cero explícito en cuadrada/dirección larga.` | Cero explícito en cuadrada/dirección larga. |
| INGRESO_DATOS | `E145` | `(vacía)` | `Conteo fuera de franja del lado negativo, si existe.` | Conteo fuera de franja del lado negativo, si existe. |
| INGRESO_DATOS | `E146` | `(vacía)` | `Ambas zonas deben cumplir; no basta el total exterior.` | Ambas zonas deben cumplir; no basta el total exterior. |
| INGRESO_DATOS | `E147` | `(vacía)` | `Conteo fuera de franja del lado negativo, si existe.` | Conteo fuera de franja del lado negativo, si existe. |
| INGRESO_DATOS | `E148` | `(vacía)` | `N exterior total debe coincidir con suma de ambas zonas.` | N exterior total debe coincidir con suma de ambas zonas. |
| INGRESO_DATOS | `E151` | `(vacía)` | `Hipótesis visible heredada; 7.7.1 determina recubrimiento.` | Hipótesis visible heredada; 7.7.1 determina recubrimiento. |
| INGRESO_DATOS | `E152` | `(vacía)` | `Hipótesis visible para suelo sobre zapata; confirmar condición real.` | Hipótesis visible para suelo sobre zapata; confirmar condición real. |
| BARRAS_PERU | `J20` | `(vacía)` | `1` | Opciones numéricas para factor sísmico, independientes del separador decimal local. |
| BARRAS_PERU | `J21` | `(vacía)` | `0.8` | Opciones numéricas para factor sísmico; Excel2016 español. |
| CARGAS | `A31` | `(vacía)` | `COMPONENTES SÍSMICAS DE SERVICIO — ANTES DE REDUCIR` | COMPONENTES SÍSMICAS DE SERVICIO — ANTES DE REDUCIR |
| CARGAS | `A33` | `(vacía)` | `FX sísmico` | E.060 15.2.5: se reduce únicamente la parte sísmica de la combinación. |
| CARGAS | `A34` | `(vacía)` | `FY sísmico` | E.060 15.2.5: se reduce únicamente la parte sísmica de la combinación. |
| CARGAS | `A35` | `(vacía)` | `P sísmico` | E.060 15.2.5: se reduce únicamente la parte sísmica de la combinación. |
| CARGAS | `A36` | `(vacía)` | `MX sísmico` | E.060 15.2.5: se reduce únicamente la parte sísmica de la combinación. |
| CARGAS | `A37` | `(vacía)` | `MY sísmico` | E.060 15.2.5: se reduce únicamente la parte sísmica de la combinación. |
| CARGAS | `A38` | `(vacía)` | `MZ sísmico` | E.060 15.2.5: se reduce únicamente la parte sísmica de la combinación. |
| CARGAS | `D33:D35` | `(vacía)` | `tf` | Unidades de acciones sísmicas. |
| CARGAS | `D36:D38` | `(vacía)` | `tf m` | Unidades de acciones sísmicas. |
| CARGAS | `E7` | `=C7` | `=IF(srv_input_state="OK",C7+IF(inp_eq_factor=1,0,(inp_eq_factor-1)*eq_fx),"")` | E.060 15.2.5: reducir parte sísmica antes del traslado, conservar las otras acciones. |
| CARGAS | `E8` | `=C8` | `=IF(srv_input_state="OK",C8+IF(inp_eq_factor=1,0,(inp_eq_factor-1)*eq_fy),"")` | E.060 15.2.5: reducir parte sísmica antes del traslado, conservar las otras acciones. |
| CARGAS | `E9` | `=inp_sign_p*C9` | `=IF(srv_input_state="OK",inp_sign_p*(C9+IF(inp_eq_factor=1,0,(inp_eq_factor-1)*eq_p)),"")` | E.060 15.2.5: reducir parte sísmica antes del traslado, conservar las otras acciones. |
| CARGAS | `E10` | `=C10+IF(inp_traslado="Si",inp_sign_mx_fy*E8*inp_zh,0)` | `=IF(srv_input_state="OK",C10+IF(inp_eq_factor=1,0,(inp_eq_factor-1)*eq_mx)+IF(inp_traslado="Si",inp_sign_mx_fy*E8*inp_zh,0),"")` | E.060 15.2.5: reducir parte sísmica antes del traslado, conservar las otras acciones. |
| CARGAS | `E11` | `=C11+IF(inp_traslado="Si",inp_sign_my_fx*E7*inp_zh,0)` | `=IF(srv_input_state="OK",C11+IF(inp_eq_factor=1,0,(inp_eq_factor-1)*eq_my)+IF(inp_traslado="Si",inp_sign_my_fx*E7*inp_zh,0),"")` | E.060 15.2.5: reducir parte sísmica antes del traslado, conservar las otras acciones. |
| CARGAS | `E12` | `=C12` | `=IF(srv_input_state="OK",C12+IF(inp_eq_factor=1,0,(inp_eq_factor-1)*eq_mz),"")` | E.060 15.2.5: reducir parte sísmica antes del traslado, conservar las otras acciones. |
| CARGAS | `E22` | `=C22` | `=IF(COUNT(C22:C27)=6,C22,"")` | No multiplicar ni trasladar texto/acciones incompletas. |
| CARGAS | `E23` | `=C23` | `=IF(COUNT(C22:C27)=6,C23,"")` | No multiplicar ni trasladar texto/acciones incompletas. |
| CARGAS | `E24` | `=inp_sign_p*C24` | `=IF(COUNT(C22:C27)=6,inp_sign_p*C24,"")` | No multiplicar ni trasladar texto/acciones incompletas. |
| CARGAS | `E25` | `=C25+IF(inp_traslado="Si",inp_sign_mx_fy*E23*inp_zh,0)` | `=IF(COUNT(C22:C27)=6,C25+IF(inp_traslado="Si",inp_sign_mx_fy*E23*inp_zh,0),"")` | No multiplicar ni trasladar texto/acciones incompletas. |
| CARGAS | `E26` | `=C26+IF(inp_traslado="Si",inp_sign_my_fx*E22*inp_zh,0)` | `=IF(COUNT(C22:C27)=6,C26+IF(inp_traslado="Si",inp_sign_my_fx*E22*inp_zh,0),"")` | No multiplicar ni trasladar texto/acciones incompletas. |
| CARGAS | `E27` | `=C27` | `=IF(COUNT(C22:C27)=6,C27,"")` | No multiplicar ni trasladar texto/acciones incompletas. |
| CARGAS | `E33:E38` | `(vacía)` | `Dato requerido solamente para factor 0.80. Misma convención de los ingresos actuales.` | No se reduce gravedad. |
| GEOMETRIA | `A2621` | `(vacía)` | `ALTURA SOBRE REFUERZO INFERIOR — E.060 15.7` | ALTURA SOBRE REFUERZO INFERIOR — E.060 15.7 |
| GEOMETRIA | `A2622` | `(vacía)` | `Altura disponible sobre parrilla` | Se mide sobre coronación de la barra más alta de la parrilla inferior; conserva orden físico. |
| GEOMETRIA | `A2623` | `(vacía)` | `Altura mínima sobre refuerzo` | E.060 15.7: zapata sobre suelo; no pilotes. |
| GEOMETRIA | `A2624` | `(vacía)` | `Estado altura sobre refuerzo` | No confundir h total con altura encima del acero. |
| GEOMETRIA | `A2625` | `(vacía)` | `Anclaje de columna compatible` | 15.7 también exige peralte compatible con desarrollo de columnas. |
| GEOMETRIA | `A2627` | `(vacía)` | `Estado entradas nuevas Fase 2` | Faltante explícito no equivale a valor negativo/texto/selección inválida. |
| GEOMETRIA | `B11` | `=IF(geo_input_state="OK",MIN(3*inp_h*100,inp_sep_max_usuario),"")` | `=IF(AND(geo_input_state="OK",ISNUMBER(inp_sep_max_usuario),inp_sep_max_usuario>0),MIN(3*inp_h*100,40,inp_sep_max_usuario),"")` | E.060 10.5.4 y 9.7.3: límite normativo absoluto 40cm y 3h, aun si usuario aumenta límite. |
| GEOMETRIA | `B14` | `=IF(AND(COUNT(inp_bx,inp_by,inp_h,inp_cx,inp_cy,inp_xc,inp_yc,inp_rec_inf,inp_rec_sup,inp_fc,inp_fy,inp_n_div_x,inp_n_div_y)=13,MIN(inp_bx,inp_by,inp_h,inp_cx,inp_cy,inp_fc,inp_fy)>0,inp_rec_inf>=0,inp_rec_sup>=0,inp_n_div_x>=4,inp_n_div_x<=50,inp_n_div_y>=4,inp_n_div_y<=50,MOD(inp_n_div_x,1)=0,MOD(inp_n_div_y,1)=0,ABS(inp_xc)+inp_cx/2<=inp_bx/2,ABS(inp_yc)+inp_cy/2<=inp_by/2,OR(inp_sign_p=1,inp_sign_p=-1),OR(inp_order_inf="X inferior / Y superior",inp_order_inf="Y inferior / X superior"),OR(inp_order_sup="X exterior / Y interior",inp_order_sup="Y exterior / X interior"),OR(inp_col_type="INTERIOR",inp_col_type="BORDE",inp_col_type="ESQUINA"),COUNTIF(bar_codes,inp_bar_inf_x)=1,COUNTIF(bar_codes,inp_bar_inf_y)=1,COUNTIF(bar_codes,inp_bar_sup_x)=1,COUNTIF(bar_codes,inp_bar_sup_y)=1),"OK","DATOS / GEOMETRÍA INVÁLIDOS")` | `=IF(COUNT(inp_bx,inp_by,inp_h,inp_cx,inp_cy,inp_xc,inp_yc,inp_rec_inf,inp_rec_sup,inp_fc,inp_fy,inp_n_div_x,inp_n_div_y,inp_gamma_c,inp_gamma_s,inp_hs,inp_df,inp_zh,inp_mu)<>19,"DATOS INVÁLIDOS",IF(AND(AND(COUNT(inp_gamma_c,inp_gamma_s,inp_hs,inp_df,inp_zh,inp_mu)=6,MIN(inp_gamma_c,inp_gamma_s,inp_hs,inp_df,inp_zh,inp_mu)>=0,OR(inp_peso_zapata="Si",inp_peso_zapata="No"),OR(inp_peso_suelo="Si",inp_peso_suelo="No"),OR(inp_traslado="Si",inp_traslado="No"),inp_sign_mx_fy=-1,inp_sign_my_fx=1),COUNT(inp_bx,inp_by,inp_h,inp_cx,inp_cy,inp_xc,inp_yc,inp_rec_inf,inp_rec_sup,inp_fc,inp_fy,inp_n_div_x,inp_n_div_y)=13,MIN(inp_bx,inp_by,inp_h,inp_cx,inp_cy,inp_fc,inp_fy)>0,inp_rec_inf>=0,inp_rec_sup>=0,inp_n_div_x>=4,inp_n_div_x<=50,inp_n_div_y>=4,inp_n_div_y<=50,MOD(inp_n_div_x,1)=0,MOD(inp_n_div_y,1)=0,ABS(inp_xc)+inp_cx/2<=inp_bx/2,ABS(inp_yc)+inp_cy/2<=inp_by/2,OR(inp_sign_p=1,inp_sign_p=-1),OR(inp_order_inf="X inferior / Y superior",inp_order_inf="Y inferior / X superior"),OR(inp_order_sup="X exterior / Y interior",inp_order_sup="Y exterior / X interior"),OR(inp_col_type="INTERIOR",inp_col_type="BORDE",inp_col_type="ESQUINA"),COUNTIF(bar_codes,inp_bar_inf_x)=1,COUNTIF(bar_codes,inp_bar_inf_y)=1,COUNTIF(bar_codes,inp_bar_sup_x)=1,COUNTIF(bar_codes,inp_bar_sup_y)=1),"OK","DATOS / GEOMETRÍA INVÁLIDOS"))` | IF exterior evita MOD/operaciones con texto; validación completa de dominio geométrico. |
| GEOMETRIA | `B2622` | `(vacía)` | `=IF(geo_input_state="OK",inp_h*100-inp_rec_inf-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Se mide sobre coronación de la barra más alta de la parrilla inferior; conserva orden físico. |
| GEOMETRIA | `B2623` | `(vacía)` | `30` | E.060 15.7: zapata sobre suelo; no pilotes. |
| GEOMETRIA | `B2624` | `(vacía)` | `=IF(geo_input_state<>"OK","DATOS INVÁLIDOS",IF(h_above_rebar>=30,"CUMPLE","NO CUMPLE"))` | No confundir h total con altura encima del acero. |
| GEOMETRIA | `B2625` | `(vacía)` | `=iface_anchor_state` | 15.7 también exige peralte compatible con desarrollo de columnas. |
| GEOMETRIA | `B2627` | `(vacía)` | `=IF(AND(IF(LEN(inp_sigma0)=0,TRUE,IF(ISNUMBER(inp_sigma0),inp_sigma0>=0,FALSE)),IF(LEN(inp_rec_lat)=0,TRUE,IF(ISNUMBER(inp_rec_lat),inp_rec_lat>=0,FALSE)),IF(LEN(inp_nloc_ix)=0,TRUE,IF(ISNUMBER(inp_nloc_ix),AND(inp_nloc_ix>=0,MOD(inp_nloc_ix,1)=0),FALSE)),IF(LEN(inp_nloc_iy)=0,TRUE,IF(ISNUMBER(inp_nloc_iy),AND(inp_nloc_iy>=0,MOD(inp_nloc_iy,1)=0),FALSE)),IF(LEN(inp_nloc_sx)=0,TRUE,IF(ISNUMBER(inp_nloc_sx),AND(inp_nloc_sx>=0,MOD(inp_nloc_sx,1)=0),FALSE)),IF(LEN(inp_nloc_sy)=0,TRUE,IF(ISNUMBER(inp_nloc_sy),AND(inp_nloc_sy>=0,MOD(inp_nloc_sy,1)=0),FALSE)),IF(LEN(inp_ll_ix_m)=0,TRUE,IF(ISNUMBER(inp_ll_ix_m),inp_ll_ix_m>=0,FALSE)),IF(LEN(inp_ll_ix_p)=0,TRUE,IF(ISNUMBER(inp_ll_ix_p),inp_ll_ix_p>=0,FALSE)),IF(LEN(inp_ll_iy_m)=0,TRUE,IF(ISNUMBER(inp_ll_iy_m),inp_ll_iy_m>=0,FALSE)),IF(LEN(inp_ll_iy_p)=0,TRUE,IF(ISNUMBER(inp_ll_iy_p),inp_ll_iy_p>=0,FALSE)),IF(LEN(inp_ll_sx_m)=0,TRUE,IF(ISNUMBER(inp_ll_sx_m),inp_ll_sx_m>=0,FALSE)),IF(LEN(inp_ll_sx_p)=0,TRUE,IF(ISNUMBER(inp_ll_sx_p),inp_ll_sx_p>=0,FALSE)),IF(LEN(inp_ll_sy_m)=0,TRUE,IF(ISNUMBER(inp_ll_sy_m),inp_ll_sy_m>=0,FALSE)),IF(LEN(inp_ll_sy_p)=0,TRUE,IF(ISNUMBER(inp_ll_sy_p),inp_ll_sy_p>=0,FALSE)),IF(LEN(inp_n_col)=0,TRUE,IF(ISNUMBER(inp_n_col),AND(inp_n_col>=0,MOD(inp_n_col,1)=0),FALSE)),IF(LEN(inp_n_continue)=0,TRUE,IF(ISNUMBER(inp_n_continue),AND(inp_n_continue>=0,MOD(inp_n_continue,1)=0),FALSE)),IF(LEN(inp_n_dowel)=0,TRUE,IF(ISNUMBER(inp_n_dowel),AND(inp_n_dowel>=0,MOD(inp_n_dowel,1)=0),FALSE)),IF(LEN(inp_lcol_foot)=0,TRUE,IF(ISNUMBER(inp_lcol_foot),inp_lcol_foot>=0,FALSE)),IF(LEN(inp_lcol_above)=0,TRUE,IF(ISNUMBER(inp_lcol_above),inp_lcol_above>=0,FALSE)),IF(LEN(inp_ldow_foot)=0,TRUE,IF(ISNUMBER(inp_ldow_foot),inp_ldow_foot>=0,FALSE)),IF(LEN(inp_ldow_above)=0,TRUE,IF(ISNUMBER(inp_ldow_above),inp_ldow_above>=0,FALSE)),IF(LEN(inp_avf)=0,TRUE,IF(ISNUMBER(inp_avf),inp_avf>=0,FALSE)),IF(LEN(inp_rpassive)=0,TRUE,IF(ISNUMBER(inp_rpassive),inp_rpassive>=0,FALSE)),IF(LEN(inp_ncx)=0,TRUE,IF(ISNUMBER(inp_ncx),AND(inp_ncx>=0,MOD(inp_ncx,1)=0),FALSE)),IF(LEN(inp_nox)=0,TRUE,IF(ISNUMBER(inp_nox),AND(inp_nox>=0,MOD(inp_nox,1)=0),FALSE)),IF(LEN(inp_ncy)=0,TRUE,IF(ISNUMBER(inp_ncy),AND(inp_ncy>=0,MOD(inp_ncy,1)=0),FALSE)),IF(LEN(inp_noy)=0,TRUE,IF(ISNUMBER(inp_noy),AND(inp_noy>=0,MOD(inp_noy,1)=0),FALSE)),IF(LEN(inp_nox_minus)=0,TRUE,IF(ISNUMBER(inp_nox_minus),AND(inp_nox_minus>=0,MOD(inp_nox_minus,1)=0),FALSE)),IF(LEN(inp_nox_plus)=0,TRUE,IF(ISNUMBER(inp_nox_plus),AND(inp_nox_plus>=0,MOD(inp_nox_plus,1)=0),FALSE)),IF(LEN(inp_noy_minus)=0,TRUE,IF(ISNUMBER(inp_noy_minus),AND(inp_noy_minus>=0,MOD(inp_noy_minus,1)=0),FALSE)),IF(LEN(inp_noy_plus)=0,TRUE,IF(ISNUMBER(inp_noy_plus),AND(inp_noy_plus>=0,MOD(inp_noy_plus,1)=0),FALSE)),IF(LEN(inp_agg)=0,TRUE,IF(ISNUMBER(inp_agg),inp_agg>0,FALSE)),IF(LEN(inp_fc_col)=0,TRUE,IF(ISNUMBER(inp_fc_col),inp_fc_col>0,FALSE)),IF(LEN(inp_fy_col)=0,TRUE,IF(ISNUMBER(inp_fy_col),inp_fy_col>0,FALSE)),IF(LEN(inp_fs_slide)=0,TRUE,IF(ISNUMBER(inp_fs_slide),inp_fs_slide>0,FALSE)),IF(LEN(inp_fs_over)=0,TRUE,IF(ISNUMBER(inp_fs_over),inp_fs_over>0,FALSE)),IF(LEN(inp_scx)=0,TRUE,IF(ISNUMBER(inp_scx),inp_scx>0,FALSE)),IF(LEN(inp_sox)=0,TRUE,IF(ISNUMBER(inp_sox),inp_sox>0,FALSE)),IF(LEN(inp_scy)=0,TRUE,IF(ISNUMBER(inp_scy),inp_scy>0,FALSE)),IF(LEN(inp_soy)=0,TRUE,IF(ISNUMBER(inp_soy),inp_soy>0,FALSE)),IF(LEN(inp_srv_type)=0,TRUE,OR(inp_srv_type="GRAVEDAD",inp_srv_type="SISMO",inp_srv_type="VIENTO",inp_srv_type="OTRO")),IF(LEN(inp_qadm_inc)=0,TRUE,OR(inp_qadm_inc="NO",inp_qadm_inc="SI")),IF(LEN(inp_qadm_basis)=0,TRUE,OR(inp_qadm_basis="BRUTA",inp_qadm_basis="NETA")),IF(LEN(inp_ems_incl)=0,TRUE,OR(inp_ems_incl="SI",inp_ems_incl="NO",inp_ems_incl="NO CONFIRMADO")),IF(LEN(inp_edge_dir)=0,TRUE,OR(inp_edge_dir="NO APLICA",inp_edge_dir="+X",inp_edge_dir="-X",inp_edge_dir="+Y",inp_edge_dir="-Y",inp_edge_dir="+X/+Y",inp_edge_dir="+X/-Y",inp_edge_dir="-X/+Y",inp_edge_dir="-X/-Y")),IF(LEN(inp_rebar_type)=0,TRUE,OR(inp_rebar_type="CORRUGADAS",inp_rebar_type="LISAS",inp_rebar_type="MALLA SOLDADA")),IF(LEN(inp_concrete_type)=0,TRUE,OR(inp_concrete_type="NORMAL",inp_concrete_type="LIVIANO")),IF(LEN(inp_end_inf)=0,TRUE,OR(inp_end_inf="RECTA",inp_end_inf="GANCHO")),IF(LEN(inp_epoxy)=0,TRUE,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(LEN(inp_side_exposure)=0,TRUE,OR(inp_side_exposure="CONTRA SUELO",inp_side_exposure="CONTACTO SUELO",inp_side_exposure="INTERIOR")),IF(LEN(inp_end_sup)=0,TRUE,OR(inp_end_sup="RECTA",inp_end_sup="GANCHO")),IF(LEN(inp_local_detail)=0,TRUE,OR(inp_local_detail="SI",inp_local_detail="NO")),IF(LEN(inp_col_system)=0,TRUE,OR(inp_col_system="IN SITU",inp_col_system="PREFABRICADA")),IF(LEN(inp_end_col)=0,TRUE,OR(inp_end_col="RECTA",inp_end_col="GANCHO")),IF(LEN(inp_joint)=0,TRUE,OR(inp_joint="MONOLITICA",inp_joint="RUGOSA",inp_joint="LISA")),IF(LEN(inp_avf_anchor)=0,TRUE,OR(inp_avf_anchor="SI",inp_avf_anchor="NO")),IF(LEN(inp_passive)=0,TRUE,OR(inp_passive="NO",inp_passive="SI")),IF(LEN(inp_bottom_exposure)=0,TRUE,OR(inp_bottom_exposure="CONTRA SUELO",inp_bottom_exposure="CONTACTO SUELO",inp_bottom_exposure="INTERIOR")),IF(LEN(inp_top_exposure)=0,TRUE,OR(inp_top_exposure="CONTRA SUELO",inp_top_exposure="CONTACTO SUELO",inp_top_exposure="INTERIOR"))),"CUMPLE","DATOS INVÁLIDOS")` | Faltante explícito no equivale a valor negativo/texto/selección inválida. |
| GEOMETRIA | `C2622` | `(vacía)` | `cm` | Se mide sobre coronación de la barra más alta de la parrilla inferior; conserva orden físico. |
| GEOMETRIA | `C2623` | `(vacía)` | `cm` | E.060 15.7: zapata sobre suelo; no pilotes. |
| GEOMETRIA | `C2624` | `(vacía)` | `-` | No confundir h total con altura encima del acero. |
| GEOMETRIA | `C2625` | `(vacía)` | `-` | 15.7 también exige peralte compatible con desarrollo de columnas. |
| GEOMETRIA | `C2627` | `(vacía)` | `-` | Faltante explícito no equivale a valor negativo/texto/selección inválida. |
| GEOMETRIA | `D11` | `MIN(3h, editable)` | `MIN(3h,40cm,smax_usuario); E.060 10.5.4` | Límite normativo y criterio más estricto del usuario. |
| GEOMETRIA | `D2622` | `(vacía)` | `Se mide sobre coronación de la barra más alta de la parrilla inferior; conserva orden físico.` | Se mide sobre coronación de la barra más alta de la parrilla inferior; conserva orden físico. |
| GEOMETRIA | `D2623` | `(vacía)` | `E.060 15.7: zapata sobre suelo; no pilotes.` | E.060 15.7: zapata sobre suelo; no pilotes. |
| GEOMETRIA | `D2624` | `(vacía)` | `No confundir h total con altura encima del acero.` | No confundir h total con altura encima del acero. |
| GEOMETRIA | `D2625` | `(vacía)` | `15.7 también exige peralte compatible con desarrollo de columnas.` | 15.7 también exige peralte compatible con desarrollo de columnas. |
| GEOMETRIA | `D2627` | `(vacía)` | `Faltante explícito no equivale a valor negativo/texto/selección inválida.` | Faltante explícito no equivale a valor negativo/texto/selección inválida. |
| GEOMETRIA | `E18:E2618` | `=IF(C18="","",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*D18+res_srv_my_tot/geo_iy*C18)` | `=IF(srv_input_state="OK",IF(C18="","",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*D18+res_srv_my_tot/geo_iy*C18),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GEOMETRIA | `G18:G2618` | `=IF(C18="","",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*D18+res_u_my_tot/geo_iy*C18)` | `=IF(ult_input_state="OK",IF(C18="","",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*D18+res_u_my_tot/geo_iy*C18),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| RESULTANTE | `B5` | `=srv_p` | `=IF(srv_input_state="OK",srv_p,"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `B6` | `=ult_p` | `=IF(ult_input_state="OK",ult_p,"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `C5` | `=geo_w_zapata` | `=IF(srv_input_state="OK",geo_w_zapata,"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `C6` | `=IF(geo_input_state="OK",geo_w_zapata*inp_fwz_u,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",geo_w_zapata*inp_fwz_u,""),"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `D5` | `=geo_w_suelo` | `=IF(srv_input_state="OK",geo_w_suelo,"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `D6` | `=IF(geo_input_state="OK",geo_w_suelo*inp_fws_u,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",geo_w_suelo*inp_fws_u,""),"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `E5` | `=IF(geo_input_state="OK",B5+C5+D5,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",B5+C5+D5,""),"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `E6` | `=IF(geo_input_state="OK",B6+C6+D6,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",B6+C6+D6,""),"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `F5` | `=-srv_mx+srv_p*inp_yc` | `=IF(srv_input_state="OK",-srv_mx+srv_p*inp_yc,"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `F6` | `=-ult_mx+ult_p*inp_yc` | `=IF(ult_input_state="OK",-ult_mx+ult_p*inp_yc,"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `G5` | `=srv_my+srv_p*inp_xc` | `=IF(srv_input_state="OK",srv_my+srv_p*inp_xc,"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `G6` | `=ult_my+ult_p*inp_xc` | `=IF(ult_input_state="OK",ult_my+ult_p*inp_xc,"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `H5` | `=IF(AND(geo_input_state="OK",E5>0),IF(E5<>0,G5/E5,""),"")` | `=IF(srv_input_state="OK",IF(AND(geo_input_state="OK",E5>0),IF(E5<>0,G5/E5,""),""),"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `H6` | `=IF(AND(geo_input_state="OK",E6>0),IF(E6<>0,G6/E6,""),"")` | `=IF(ult_input_state="OK",IF(AND(geo_input_state="OK",E6>0),IF(E6<>0,G6/E6,""),""),"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `I5` | `=IF(AND(geo_input_state="OK",E5>0),IF(E5<>0,F5/E5,""),"")` | `=IF(srv_input_state="OK",IF(AND(geo_input_state="OK",E5>0),IF(E5<>0,F5/E5,""),""),"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `I6` | `=IF(AND(geo_input_state="OK",E6>0),IF(E6<>0,F6/E6,""),"")` | `=IF(ult_input_state="OK",IF(AND(geo_input_state="OK",E6>0),IF(E6<>0,F6/E6,""),""),"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `J5` | `=IF(AND(geo_input_state="OK",E5>0),IF(ABS(H5)<=inp_bx/6,"CUMPLE","NO CUMPLE"),"")` | `=IF(srv_input_state="OK",IF(AND(geo_input_state="OK",E5>0),IF(ABS(H5)<=inp_bx/6,"CUMPLE","NO CUMPLE"),""),"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `J6` | `=IF(AND(geo_input_state="OK",E6>0),IF(ABS(H6)<=inp_bx/6,"CUMPLE","NO CUMPLE"),"")` | `=IF(ult_input_state="OK",IF(AND(geo_input_state="OK",E6>0),IF(ABS(H6)<=inp_bx/6,"CUMPLE","NO CUMPLE"),""),"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `K5` | `=IF(AND(geo_input_state="OK",E5>0),IF(ABS(I5)<=inp_by/6,"CUMPLE","NO CUMPLE"),"")` | `=IF(srv_input_state="OK",IF(AND(geo_input_state="OK",E5>0),IF(ABS(I5)<=inp_by/6,"CUMPLE","NO CUMPLE"),""),"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `K6` | `=IF(AND(geo_input_state="OK",E6>0),IF(ABS(I6)<=inp_by/6,"CUMPLE","NO CUMPLE"),"")` | `=IF(ult_input_state="OK",IF(AND(geo_input_state="OK",E6>0),IF(ABS(I6)<=inp_by/6,"CUMPLE","NO CUMPLE"),""),"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `L5` | `=IF(AND(geo_input_state="OK",E5>0),H5,"")` | `=IF(srv_input_state="OK",IF(AND(geo_input_state="OK",E5>0),H5,""),"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `L6` | `=IF(AND(geo_input_state="OK",E6>0),H6,"")` | `=IF(ult_input_state="OK",IF(AND(geo_input_state="OK",E6>0),H6,""),"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `M5` | `=IF(AND(geo_input_state="OK",E5>0),I5,"")` | `=IF(srv_input_state="OK",IF(AND(geo_input_state="OK",E5>0),I5,""),"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `M6` | `=IF(AND(geo_input_state="OK",E6>0),I6,"")` | `=IF(ult_input_state="OK",IF(AND(geo_input_state="OK",E6>0),I6,""),"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| RESULTANTE | `N5` | `=IF(geo_input_state<>"OK",geo_input_state,IF(E5<=0,"RESULTANTE NO COMPRESIVA",IF(ABS(H5)/(inp_bx/6)+ABS(I5)/(inp_by/6)<=1,"CUMPLE","FUERA DEL NUCLEO")))` | `=IF(srv_input_state="OK",IF(geo_input_state<>"OK",geo_input_state,IF(E5<=0,"RESULTANTE NO COMPRESIVA",IF(ABS(H5)/(inp_bx/6)+ABS(I5)/(inp_by/6)<=1,"CUMPLE","FUERA DEL NUCLEO"))),"")` | E.060 15.2.2: servicio separado; datos sísmicos inválidos no propagan resultados ficticios. |
| RESULTANTE | `N6` | `=IF(geo_input_state<>"OK",geo_input_state,IF(E6<=0,"RESULTANTE NO COMPRESIVA",IF(ABS(H6)/(inp_bx/6)+ABS(I6)/(inp_by/6)<=1,"CUMPLE","FUERA DEL NUCLEO")))` | `=IF(ult_input_state="OK",IF(geo_input_state<>"OK",geo_input_state,IF(E6<=0,"RESULTANTE NO COMPRESIVA",IF(ABS(H6)/(inp_bx/6)+ABS(I6)/(inp_by/6)<=1,"CUMPLE","FUERA DEL NUCLEO"))),"")` | Resultado último bloqueado antes de divisiones/traslados por datos inválidos. |
| PRESIONES_SERVICIO | `A18` | `(vacía)` | `CONTROL GEOTÉCNICO E.050 / OPCIONES E.060` | CONTROL GEOTÉCNICO E.050 / OPCIONES E.060 |
| PRESIONES_SERVICIO | `A19` | `(vacía)` | `Estado de datos de servicio` | 15.2.4/5: opciones visibles; componente sísmica separada; no modifica último. |
| PRESIONES_SERVICIO | `A20` | `(vacía)` | `Q total servicio` | Peso zapata/relleno y P servicio; magnitud compresiva con signo. |
| PRESIONES_SERVICIO | `A21` | `(vacía)` | `Mx de acción respecto a origen` | Mano derecha: Mx aplicado + momento de P descendente. |
| PRESIONES_SERVICIO | `A22` | `(vacía)` | `My de acción respecto a origen` | Mano derecha: My aplicado + P*xc. |
| PRESIONES_SERVICIO | `A23` | `(vacía)` | `ex correspondiente a Bx` | Global: ex=My_origen/Q; E.050 art.28 figura/ejes verificados. |
| PRESIONES_SERVICIO | `A24` | `(vacía)` | `ey correspondiente a By` | Global: ey=-Mx_origen/Q; abs solo en dimensiones efectivas. |
| PRESIONES_SERVICIO | `A25` | `(vacía)` | `Bx efectiva Bx'` | E.050 28.2. Valor <=0 visible; área/presión no se divide. |
| PRESIONES_SERVICIO | `A26` | `(vacía)` | `By efectiva By'` | E.050 28.2; no sustituye el campo físico de q. |
| PRESIONES_SERVICIO | `A27` | `(vacía)` | `Dominio geométrico área efectiva` | E.050 28.2/3. |
| PRESIONES_SERVICIO | `A28` | `(vacía)` | `A efectiva geotécnica` | E.050 art.28; exclusivamente control geotécnico. |
| PRESIONES_SERVICIO | `A29` | `(vacía)` | `Q/Aef bruta` | No se usa como distribución física ni para flexión/cortante. |
| PRESIONES_SERVICIO | `A30` | `(vacía)` | `qadm original EMS` | Se conserva dato original editable, sin optimizar. |
| PRESIONES_SERVICIO | `A31` | `(vacía)` | `Factor de incremento qadm` | E.060 15.2.4: habilitación explícita; estado valida tipo de caso. |
| PRESIONES_SERVICIO | `A32` | `(vacía)` | `qadm aplicada` | Nunca compara la resistencia última con qadm. |
| PRESIONES_SERVICIO | `A33` | `(vacía)` | `Referencia bruta/neta` | qadm NETA: sigma0 debe proceder del EMS; no se inventa. |
| PRESIONES_SERVICIO | `A34` | `(vacía)` | `q efectiva comparable` | Misma base de presión y EMS, E.050 arts.22,27,28. |
| PRESIONES_SERVICIO | `A35` | `(vacía)` | `Control de q efectiva` | Este control complementa q física máxima. |
| PRESIONES_SERVICIO | `A36` | `(vacía)` | `q física máxima comparable` | Campo físico lineal conserva equilibrio; no recorta tracciones. |
| PRESIONES_SERVICIO | `A37` | `(vacía)` | `Resultante horizontal servicio` | Magnitud necesaria para inclinación/deslizamiento. |
| PRESIONES_SERVICIO | `A38` | `(vacía)` | `EMS y carga inclinada` | VERIFICAR QUE LA CAPACIDAD ADMISIBLE DEL EMS CONTEMPLE CARGA INCLINADA — E.050 Art.29. |
| PRESIONES_SERVICIO | `A39` | `(vacía)` | `Referencia EMS` | El dato qadm se conserva, su trazabilidad exige fuente. |
| PRESIONES_SERVICIO | `A42` | `(vacía)` | `ESTABILIDAD — CRITERIOS DE INGENIERÍA / USUARIO` | ESTABILIDAD — CRITERIOS DE INGENIERÍA / USUARIO |
| PRESIONES_SERVICIO | `A43` | `(vacía)` | `Resistencia fricción suelo` | Fricción = mu de usuario × Q; sin reducción sísmica oculta. |
| PRESIONES_SERVICIO | `A44` | `(vacía)` | `Resistencia pasiva habilitada` | Pasivo NO por defecto; solo dato externo trazable. |
| PRESIONES_SERVICIO | `A45` | `(vacía)` | `FS calculado deslizamiento` | No atribuye FS requerido a E.050. |
| PRESIONES_SERVICIO | `A46` | `(vacía)` | `FS requerido / fuente` | Entrada requerida solo si H>0. |
| PRESIONES_SERVICIO | `A47` | `(vacía)` | `Estado deslizamiento` | Criterio de ingeniería explícito; empuje pasivo no automático. |
| PRESIONES_SERVICIO | `A50` | `(vacía)` | `Borde +X` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `A51` | `(vacía)` | `Borde -X` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `A52` | `(vacía)` | `Borde +Y` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `A53` | `(vacía)` | `Borde -Y` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `A55` | `(vacía)` | `Estado volteo` | FS por cada borde; fuente de valor requerido ingresada por diseñador. |
| PRESIONES_SERVICIO | `B19` | `(vacía)` | `=IF(geo_input_state<>"OK","DATOS INVÁLIDOS",IF(NOT(AND(COUNT(CARGAS!C7:C12)=6,COUNT(inp_qadm,inp_eq_factor)=2,inp_qadm>0,OR(inp_srv_type="GRAVEDAD",inp_srv_type="SISMO",inp_srv_type="VIENTO",inp_srv_type="OTRO"),OR(inp_qadm_inc="NO",inp_qadm_inc="SI"),OR(inp_eq_factor=1,inp_eq_factor=0.8),OR(inp_qadm_basis="BRUTA",inp_qadm_basis="NETA"),OR(inp_ems_incl="SI",inp_ems_incl="NO",inp_ems_incl="NO CONFIRMADO"))),"DATOS INVÁLIDOS",IF(AND(inp_qadm_inc="SI",NOT(OR(inp_srv_type="SISMO",inp_srv_type="VIENTO"))),"DATOS INVÁLIDOS",IF(AND(inp_eq_factor=0.8,inp_srv_type<>"SISMO"),"DATOS INVÁLIDOS",IF(AND(inp_eq_factor=0.8,COUNT(CARGAS!C33:C38)<>6),"REQUIERE DATOS","OK")))))` | 15.2.4/5: opciones visibles; componente sísmica separada; no modifica último. |
| PRESIONES_SERVICIO | `B20` | `(vacía)` | `=IF(srv_input_state="OK",res_srv_p_tot,"")` | Peso zapata/relleno y P servicio; magnitud compresiva con signo. |
| PRESIONES_SERVICIO | `B21` | `(vacía)` | `=IF(srv_input_state="OK",srv_mx-srv_p*inp_yc,"")` | Mano derecha: Mx aplicado + momento de P descendente. |
| PRESIONES_SERVICIO | `B22` | `(vacía)` | `=IF(srv_input_state="OK",srv_my+srv_p*inp_xc,"")` | Mano derecha: My aplicado + P*xc. |
| PRESIONES_SERVICIO | `B23` | `(vacía)` | `=IF(AND(srv_input_state="OK",g_Q>0),g_My/g_Q,"")` | Global: ex=My_origen/Q; E.050 art.28 figura/ejes verificados. |
| PRESIONES_SERVICIO | `B24` | `(vacía)` | `=IF(AND(srv_input_state="OK",g_Q>0),-g_Mx/g_Q,"")` | Global: ey=-Mx_origen/Q; abs solo en dimensiones efectivas. |
| PRESIONES_SERVICIO | `B25` | `(vacía)` | `=IF(AND(srv_input_state="OK",g_Q>0),inp_bx-2*ABS(g_ex),"")` | E.050 28.2. Valor <=0 visible; área/presión no se divide. |
| PRESIONES_SERVICIO | `B26` | `(vacía)` | `=IF(AND(srv_input_state="OK",g_Q>0),inp_by-2*ABS(g_ey),"")` | E.050 28.2; no sustituye el campo físico de q. |
| PRESIONES_SERVICIO | `B27` | `(vacía)` | `=IF(srv_input_state<>"OK",srv_input_state,IF(g_Q<=0,"REQUIERE ANÁLISIS ESPECIAL",IF(MIN(g_bx_eff,g_by_eff)<=0,"EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN","OK")))` | E.050 28.2/3. |
| PRESIONES_SERVICIO | `B28` | `(vacía)` | `=IF(g_eff_state="OK",g_bx_eff*g_by_eff,"")` | E.050 art.28; exclusivamente control geotécnico. |
| PRESIONES_SERVICIO | `B29` | `(vacía)` | `=IF(g_eff_state="OK",g_Q/g_Aeff,"")` | No se usa como distribución física ni para flexión/cortante. |
| PRESIONES_SERVICIO | `B30` | `(vacía)` | `=inp_qadm` | Se conserva dato original editable, sin optimizar. |
| PRESIONES_SERVICIO | `B31` | `(vacía)` | `=IF(inp_qadm_inc="SI",1.3,1)` | E.060 15.2.4: habilitación explícita; estado valida tipo de caso. |
| PRESIONES_SERVICIO | `B32` | `(vacía)` | `=IF(srv_input_state="OK",inp_qadm*g_qadm_factor,"")` | Nunca compara la resistencia última con qadm. |
| PRESIONES_SERVICIO | `B33` | `(vacía)` | `=IF(inp_qadm_basis="BRUTA","OK",IF(COUNT(inp_sigma0)<>1,"REQUIERE DATOS",IF(inp_sigma0<0,"DATOS INVÁLIDOS","OK")))` | qadm NETA: sigma0 debe proceder del EMS; no se inventa. |
| PRESIONES_SERVICIO | `B34` | `(vacía)` | `=IF(AND(g_eff_state="OK",g_basis_state="OK"),g_qeff_gross-IF(inp_qadm_basis="NETA",inp_sigma0,0),"")` | Misma base de presión y EMS, E.050 arts.22,27,28. |
| PRESIONES_SERVICIO | `B35` | `(vacía)` | `=IF(g_eff_state<>"OK",g_eff_state,IF(g_basis_state<>"OK",g_basis_state,IF(g_qeff<=g_qadm,"CUMPLE","NO CUMPLE")))` | Este control complementa q física máxima. |
| PRESIONES_SERVICIO | `B36` | `(vacía)` | `=IF(AND(srv_input_state="OK",g_basis_state="OK"),q_srv_max-IF(inp_qadm_basis="NETA",inp_sigma0,0),"")` | Campo físico lineal conserva equilibrio; no recorta tracciones. |
| PRESIONES_SERVICIO | `B37` | `(vacía)` | `=IF(srv_input_state="OK",SQRT(srv_fx^2+srv_fy^2),"")` | Magnitud necesaria para inclinación/deslizamiento. |
| PRESIONES_SERVICIO | `B38` | `(vacía)` | `=IF(srv_input_state<>"OK",srv_input_state,IF(g_H<=0.000000001,"NO APLICA",IF(AND(inp_ems_incl="SI",LEN(inp_ems_ref)>0),"CUMPLE","REQUIERE DATOS")))` | VERIFICAR QUE LA CAPACIDAD ADMISIBLE DEL EMS CONTEMPLE CARGA INCLINADA — E.050 Art.29. |
| PRESIONES_SERVICIO | `B39` | `(vacía)` | `=IF(LEN(inp_ems_ref)>0,inp_ems_ref,"REQUIERE DATOS: IDENTIFICAR EMS / PÁGINA")` | El dato qadm se conserva, su trazabilidad exige fuente. |
| PRESIONES_SERVICIO | `B43` | `(vacía)` | `=IF(AND(srv_input_state="OK",g_Q>0),inp_mu*g_Q,"")` | Fricción = mu de usuario × Q; sin reducción sísmica oculta. |
| PRESIONES_SERVICIO | `B44` | `(vacía)` | `=IF(inp_passive="NO",0,IF(inp_passive="SI",IF(COUNT(inp_rpassive)=1,inp_rpassive,""),""))` | Pasivo NO por defecto; solo dato externo trazable. |
| PRESIONES_SERVICIO | `B45` | `(vacía)` | `=IF(AND(srv_input_state="OK",g_Q>0,g_H>0.000000001,ISNUMBER(slide_Rpass)),(slide_Rfr+slide_Rpass)/g_H,"")` | No atribuye FS requerido a E.050. |
| PRESIONES_SERVICIO | `B46` | `(vacía)` | `=IF(LEN(inp_fs_slide_ref)>0,inp_fs_slide_ref,"REQUIERE DATOS: FUENTE DEL CRITERIO")` | Entrada requerida solo si H>0. |
| PRESIONES_SERVICIO | `B47` | `(vacía)` | `=IF(srv_input_state<>"OK",srv_input_state,IF(g_H<=0.000000001,"NO APLICA",IF(D14<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(NOT(OR(inp_passive="NO",inp_passive="SI")),"DATOS INVÁLIDOS",IF(OR(COUNT(inp_fs_slide)<>1,LEN(inp_fs_slide_ref)=0,AND(inp_passive="SI",OR(COUNT(inp_rpassive)<>1,LEN(inp_rpassive_ref)=0))),"REQUIERE DATOS",IF(OR(inp_fs_slide<=0,slide_Rpass<0),"DATOS INVÁLIDOS",IF(slide_FS>=inp_fs_slide,"CUMPLE","NO CUMPLE")))))))` | Criterio de ingeniería explícito; empuje pasivo no automático. |
| PRESIONES_SERVICIO | `B50` | `(vacía)` | `=IF(srv_input_state="OK",MAX(srv_p,0)*(inp_bx/2-1*inp_xc)+geo_w_total*inp_bx/2+MAX(0,-(1)*(srv_my)),"")` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `B51` | `(vacía)` | `=IF(srv_input_state="OK",MAX(srv_p,0)*(inp_bx/2--1*inp_xc)+geo_w_total*inp_bx/2+MAX(0,-(-1)*(srv_my)),"")` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `B52` | `(vacía)` | `=IF(srv_input_state="OK",MAX(srv_p,0)*(inp_by/2-1*inp_yc)+geo_w_total*inp_by/2+MAX(0,-(1)*(-srv_mx)),"")` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `B53` | `(vacía)` | `=IF(srv_input_state="OK",MAX(srv_p,0)*(inp_by/2--1*inp_yc)+geo_w_total*inp_by/2+MAX(0,-(-1)*(-srv_mx)),"")` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `B55` | `(vacía)` | `=IF(srv_input_state<>"OK",srv_input_state,IF(COUNTIF(G50:G53,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(G50:G53,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(G50:G53,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(G50:G53,"REQUIERE DATOS")>0,"REQUIERE DATOS",IF(COUNTIF(G50:G53,"NO APLICA")=4,"NO APLICA","CUMPLE"))))))` | FS por cada borde; fuente de valor requerido ingresada por diseñador. |
| PRESIONES_SERVICIO | `C19` | `(vacía)` | `-` | 15.2.4/5: opciones visibles; componente sísmica separada; no modifica último. |
| PRESIONES_SERVICIO | `C20` | `(vacía)` | `tf` | Peso zapata/relleno y P servicio; magnitud compresiva con signo. |
| PRESIONES_SERVICIO | `C21` | `(vacía)` | `tf m` | Mano derecha: Mx aplicado + momento de P descendente. |
| PRESIONES_SERVICIO | `C22` | `(vacía)` | `tf m` | Mano derecha: My aplicado + P*xc. |
| PRESIONES_SERVICIO | `C23` | `(vacía)` | `m` | Global: ex=My_origen/Q; E.050 art.28 figura/ejes verificados. |
| PRESIONES_SERVICIO | `C24` | `(vacía)` | `m` | Global: ey=-Mx_origen/Q; abs solo en dimensiones efectivas. |
| PRESIONES_SERVICIO | `C25` | `(vacía)` | `m` | E.050 28.2. Valor <=0 visible; área/presión no se divide. |
| PRESIONES_SERVICIO | `C26` | `(vacía)` | `m` | E.050 28.2; no sustituye el campo físico de q. |
| PRESIONES_SERVICIO | `C27` | `(vacía)` | `-` | E.050 28.2/3. |
| PRESIONES_SERVICIO | `C28` | `(vacía)` | `m2` | E.050 art.28; exclusivamente control geotécnico. |
| PRESIONES_SERVICIO | `C29` | `(vacía)` | `tf/m2` | No se usa como distribución física ni para flexión/cortante. |
| PRESIONES_SERVICIO | `C30` | `(vacía)` | `tf/m2` | Se conserva dato original editable, sin optimizar. |
| PRESIONES_SERVICIO | `C31` | `(vacía)` | `-` | E.060 15.2.4: habilitación explícita; estado valida tipo de caso. |
| PRESIONES_SERVICIO | `C32` | `(vacía)` | `tf/m2` | Nunca compara la resistencia última con qadm. |
| PRESIONES_SERVICIO | `C33` | `(vacía)` | `-` | qadm NETA: sigma0 debe proceder del EMS; no se inventa. |
| PRESIONES_SERVICIO | `C34` | `(vacía)` | `tf/m2` | Misma base de presión y EMS, E.050 arts.22,27,28. |
| PRESIONES_SERVICIO | `C35` | `(vacía)` | `-` | Este control complementa q física máxima. |
| PRESIONES_SERVICIO | `C36` | `(vacía)` | `tf/m2` | Campo físico lineal conserva equilibrio; no recorta tracciones. |
| PRESIONES_SERVICIO | `C37` | `(vacía)` | `tf` | Magnitud necesaria para inclinación/deslizamiento. |
| PRESIONES_SERVICIO | `C38` | `(vacía)` | `-` | VERIFICAR QUE LA CAPACIDAD ADMISIBLE DEL EMS CONTEMPLE CARGA INCLINADA — E.050 Art.29. |
| PRESIONES_SERVICIO | `C39` | `(vacía)` | `-` | El dato qadm se conserva, su trazabilidad exige fuente. |
| PRESIONES_SERVICIO | `C43` | `(vacía)` | `tf` | Fricción = mu de usuario × Q; sin reducción sísmica oculta. |
| PRESIONES_SERVICIO | `C44` | `(vacía)` | `tf` | Pasivo NO por defecto; solo dato externo trazable. |
| PRESIONES_SERVICIO | `C45` | `(vacía)` | `-` | No atribuye FS requerido a E.050. |
| PRESIONES_SERVICIO | `C46` | `(vacía)` | `-` | Entrada requerida solo si H>0. |
| PRESIONES_SERVICIO | `C47` | `(vacía)` | `-` | Criterio de ingeniería explícito; empuje pasivo no automático. |
| PRESIONES_SERVICIO | `C50:C53` | `(vacía)` | `tf m estabilizante` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `C55` | `(vacía)` | `-` | FS por cada borde; fuente de valor requerido ingresada por diseñador. |
| PRESIONES_SERVICIO | `D5:D8` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+B5*6*res_srv_my_tot/(inp_by*inp_bx^2)+C5*6*res_srv_mx_tot/(inp_bx*inp_by^2),"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+B5*6*res_srv_my_tot/(inp_by*inp_bx^2)+C5*6*res_srv_mx_tot/(inp_bx*inp_by^2),""),"")` | Estado de servicio independiente con reducción sísmica explícita. |
| PRESIONES_SERVICIO | `D10` | `=IF(geo_input_state="OK",MAX(D5:D8),"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",MAX(D5:D8),""),"")` | Estado de servicio independiente con reducción sísmica explícita. |
| PRESIONES_SERVICIO | `D11` | `=IF(geo_input_state="OK",MIN(D5:D8),"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",MIN(D5:D8),""),"")` | Estado de servicio independiente con reducción sísmica explícita. |
| PRESIONES_SERVICIO | `D13` | `=IF(D14<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS DE CONTACTO PARCIAL",IF(D10<=D12,"CUMPLE","NO CUMPLE"))` | `=IF(srv_input_state<>"OK",srv_input_state,IF(g_basis_state<>"OK",g_basis_state,IF(g_Q<=0,"REQUIERE ANÁLISIS ESPECIAL",IF(D11<0,"REQUIERE ANÁLISIS ESPECIAL",IF(g_qphysical<=g_qadm,"CUMPLE","NO CUMPLE")))))` | E.060 15.2.2/3/4 y EMS: no dar CUMPLE a contacto no resuelto. |
| PRESIONES_SERVICIO | `D14` | `=IF(geo_input_state<>"OK",geo_input_state,IF(res_srv_p_tot<=0,"RESULTANTE NO COMPRESIVA",IF(D11<0,"PÉRDIDA PARCIAL DE CONTACTO","CONTACTO COMPLETO")))` | `=IF(srv_input_state<>"OK",srv_input_state,IF(g_Q<=0,"REQUIERE ANÁLISIS ESPECIAL",IF(D11<0,"PÉRDIDA PARCIAL DE CONTACTO","CONTACTO COMPLETO")))` | Mantener signo y bloqueo: no MAX(0,q). |
| PRESIONES_SERVICIO | `D15` | `=IF(D14<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS DE CONTACTO PARCIAL","")` | `=IF(srv_input_state<>"OK",srv_input_state,IF(D14<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS DE CONTACTO PARCIAL",IF(g_incl_result="REQUIERE DATOS","VERIFICAR QUE LA CAPACIDAD ADMISIBLE DEL EMS CONTEMPLE CARGA INCLINADA — E.050 Art.29","")))` | Indicar condición inclinada y pérdida de contacto. |
| PRESIONES_SERVICIO | `D19` | `(vacía)` | `15.2.4/5: opciones visibles; componente sísmica separada; no modifica último.` | 15.2.4/5: opciones visibles; componente sísmica separada; no modifica último. |
| PRESIONES_SERVICIO | `D20` | `(vacía)` | `Peso zapata/relleno y P servicio; magnitud compresiva con signo.` | Peso zapata/relleno y P servicio; magnitud compresiva con signo. |
| PRESIONES_SERVICIO | `D21` | `(vacía)` | `Mano derecha: Mx aplicado + momento de P descendente.` | Mano derecha: Mx aplicado + momento de P descendente. |
| PRESIONES_SERVICIO | `D22` | `(vacía)` | `Mano derecha: My aplicado + P*xc.` | Mano derecha: My aplicado + P*xc. |
| PRESIONES_SERVICIO | `D23` | `(vacía)` | `Global: ex=My_origen/Q; E.050 art.28 figura/ejes verificados.` | Global: ex=My_origen/Q; E.050 art.28 figura/ejes verificados. |
| PRESIONES_SERVICIO | `D24` | `(vacía)` | `Global: ey=-Mx_origen/Q; abs solo en dimensiones efectivas.` | Global: ey=-Mx_origen/Q; abs solo en dimensiones efectivas. |
| PRESIONES_SERVICIO | `D25` | `(vacía)` | `E.050 28.2. Valor <=0 visible; área/presión no se divide.` | E.050 28.2. Valor <=0 visible; área/presión no se divide. |
| PRESIONES_SERVICIO | `D26` | `(vacía)` | `E.050 28.2; no sustituye el campo físico de q.` | E.050 28.2; no sustituye el campo físico de q. |
| PRESIONES_SERVICIO | `D27` | `(vacía)` | `E.050 28.2/3.` | E.050 28.2/3. |
| PRESIONES_SERVICIO | `D28` | `(vacía)` | `E.050 art.28; exclusivamente control geotécnico.` | E.050 art.28; exclusivamente control geotécnico. |
| PRESIONES_SERVICIO | `D29` | `(vacía)` | `No se usa como distribución física ni para flexión/cortante.` | No se usa como distribución física ni para flexión/cortante. |
| PRESIONES_SERVICIO | `D30` | `(vacía)` | `Se conserva dato original editable, sin optimizar.` | Se conserva dato original editable, sin optimizar. |
| PRESIONES_SERVICIO | `D31` | `(vacía)` | `E.060 15.2.4: habilitación explícita; estado valida tipo de caso.` | E.060 15.2.4: habilitación explícita; estado valida tipo de caso. |
| PRESIONES_SERVICIO | `D32` | `(vacía)` | `Nunca compara la resistencia última con qadm.` | Nunca compara la resistencia última con qadm. |
| PRESIONES_SERVICIO | `D33` | `(vacía)` | `qadm NETA: sigma0 debe proceder del EMS; no se inventa.` | qadm NETA: sigma0 debe proceder del EMS; no se inventa. |
| PRESIONES_SERVICIO | `D34` | `(vacía)` | `Misma base de presión y EMS, E.050 arts.22,27,28.` | Misma base de presión y EMS, E.050 arts.22,27,28. |
| PRESIONES_SERVICIO | `D35` | `(vacía)` | `Este control complementa q física máxima.` | Este control complementa q física máxima. |
| PRESIONES_SERVICIO | `D36` | `(vacía)` | `Campo físico lineal conserva equilibrio; no recorta tracciones.` | Campo físico lineal conserva equilibrio; no recorta tracciones. |
| PRESIONES_SERVICIO | `D37` | `(vacía)` | `Magnitud necesaria para inclinación/deslizamiento.` | Magnitud necesaria para inclinación/deslizamiento. |
| PRESIONES_SERVICIO | `D38` | `(vacía)` | `VERIFICAR QUE LA CAPACIDAD ADMISIBLE DEL EMS CONTEMPLE CARGA INCLINADA — E.050 Art.29.` | VERIFICAR QUE LA CAPACIDAD ADMISIBLE DEL EMS CONTEMPLE CARGA INCLINADA — E.050 Art.29. |
| PRESIONES_SERVICIO | `D39` | `(vacía)` | `El dato qadm se conserva, su trazabilidad exige fuente.` | El dato qadm se conserva, su trazabilidad exige fuente. |
| PRESIONES_SERVICIO | `D43` | `(vacía)` | `Fricción = mu de usuario × Q; sin reducción sísmica oculta.` | Fricción = mu de usuario × Q; sin reducción sísmica oculta. |
| PRESIONES_SERVICIO | `D44` | `(vacía)` | `Pasivo NO por defecto; solo dato externo trazable.` | Pasivo NO por defecto; solo dato externo trazable. |
| PRESIONES_SERVICIO | `D45` | `(vacía)` | `No atribuye FS requerido a E.050.` | No atribuye FS requerido a E.050. |
| PRESIONES_SERVICIO | `D46` | `(vacía)` | `Entrada requerida solo si H>0.` | Entrada requerida solo si H>0. |
| PRESIONES_SERVICIO | `D47` | `(vacía)` | `Criterio de ingeniería explícito; empuje pasivo no automático.` | Criterio de ingeniería explícito; empuje pasivo no automático. |
| PRESIONES_SERVICIO | `D50` | `(vacía)` | `=IF(srv_input_state="OK",MAX(-srv_p,0)*(inp_bx/2-1*inp_xc)+MAX(0,(1)*(srv_my)),"")` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `D51` | `(vacía)` | `=IF(srv_input_state="OK",MAX(-srv_p,0)*(inp_bx/2--1*inp_xc)+MAX(0,(-1)*(srv_my)),"")` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `D52` | `(vacía)` | `=IF(srv_input_state="OK",MAX(-srv_p,0)*(inp_by/2-1*inp_yc)+MAX(0,(1)*(-srv_mx)),"")` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `D53` | `(vacía)` | `=IF(srv_input_state="OK",MAX(-srv_p,0)*(inp_by/2--1*inp_yc)+MAX(0,(-1)*(-srv_mx)),"")` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `D55` | `(vacía)` | `FS por cada borde; fuente de valor requerido ingresada por diseñador.` | FS por cada borde; fuente de valor requerido ingresada por diseñador. |
| PRESIONES_SERVICIO | `E50:E53` | `(vacía)` | `tf m volcantes` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `F50:F53` | `(vacía)` | `=IF(AND(srv_input_state="OK",D50>0),B50/D50,"")` | Momento tomado respecto al borde real de zapata. Los pesos actúan en centro; P en xc/yc; signos conservados. |
| PRESIONES_SERVICIO | `G50` | `(vacía)` | `=IF(srv_input_state<>"OK",srv_input_state,IF(D50=0,"NO APLICA",IF(D14<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(inp_fs_over)<>1,LEN(inp_fs_over_ref)=0),"REQUIERE DATOS",IF(inp_fs_over<=0,"DATOS INVÁLIDOS",IF(F50>=inp_fs_over,"CUMPLE","NO CUMPLE"))))))` | Sin solicitación volcantes no se exige FS; no divide por cero. |
| PRESIONES_SERVICIO | `G51` | `(vacía)` | `=IF(srv_input_state<>"OK",srv_input_state,IF(D51=0,"NO APLICA",IF(D14<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(inp_fs_over)<>1,LEN(inp_fs_over_ref)=0),"REQUIERE DATOS",IF(inp_fs_over<=0,"DATOS INVÁLIDOS",IF(F51>=inp_fs_over,"CUMPLE","NO CUMPLE"))))))` | Sin solicitación volcantes no se exige FS; no divide por cero. |
| PRESIONES_SERVICIO | `G52` | `(vacía)` | `=IF(srv_input_state<>"OK",srv_input_state,IF(D52=0,"NO APLICA",IF(D14<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(inp_fs_over)<>1,LEN(inp_fs_over_ref)=0),"REQUIERE DATOS",IF(inp_fs_over<=0,"DATOS INVÁLIDOS",IF(F52>=inp_fs_over,"CUMPLE","NO CUMPLE"))))))` | Sin solicitación volcantes no se exige FS; no divide por cero. |
| PRESIONES_SERVICIO | `G53` | `(vacía)` | `=IF(srv_input_state<>"OK",srv_input_state,IF(D53=0,"NO APLICA",IF(D14<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL",IF(OR(COUNT(inp_fs_over)<>1,LEN(inp_fs_over_ref)=0),"REQUIERE DATOS",IF(inp_fs_over<=0,"DATOS INVÁLIDOS",IF(F53>=inp_fs_over,"CUMPLE","NO CUMPLE"))))))` | Sin solicitación volcantes no se exige FS; no divide por cero. |
| PRESIONES_ULTIMAS | `A25` | `(vacía)` | `Estado de acciones y pesos últimos` | E.060 15.2.1; exclusivamente estado último. |
| PRESIONES_ULTIMAS | `B25` | `(vacía)` | `=IF(geo_input_state<>"OK","DATOS INVÁLIDOS",IF(COUNT(CARGAS!C22:C27)<>6,"DATOS INVÁLIDOS",IF(COUNT(inp_fwz_u,inp_fws_u)<>2,"DATOS INVÁLIDOS",IF(MIN(inp_fwz_u,inp_fws_u)<0,"DATOS INVÁLIDOS","OK"))))` | E.060 15.2.1; exclusivamente estado último. |
| PRESIONES_ULTIMAS | `C25` | `(vacía)` | `-` | E.060 15.2.1; exclusivamente estado último. |
| PRESIONES_ULTIMAS | `D5:D8` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+B5*6*res_u_my_tot/(inp_by*inp_bx^2)+C5*6*res_u_mx_tot/(inp_bx*inp_by^2),"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+B5*6*res_u_my_tot/(inp_by*inp_bx^2)+C5*6*res_u_mx_tot/(inp_bx*inp_by^2),""),"")` | Presión última solo para seis acciones y pesos válidos. |
| PRESIONES_ULTIMAS | `D10` | `=IF(geo_input_state="OK",MAX(D5:D8),"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",MAX(D5:D8),""),"")` | Presión última solo para seis acciones y pesos válidos. |
| PRESIONES_ULTIMAS | `D11` | `=IF(geo_input_state="OK",MIN(D5:D8),"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",MIN(D5:D8),""),"")` | Presión última solo para seis acciones y pesos válidos. |
| PRESIONES_ULTIMAS | `D13` | `=IF(geo_input_state<>"OK",geo_input_state,IF(res_u_p_tot<=0,"RESULTANTE NO COMPRESIVA",IF(D11<0,"PÉRDIDA PARCIAL DE CONTACTO","CONTACTO COMPLETO")))` | `=IF(ult_input_state<>"OK",ult_input_state,IF(res_u_p_tot<=0,"REQUIERE ANÁLISIS ESPECIAL",IF(D11<0,"PÉRDIDA PARCIAL DE CONTACTO","CONTACTO COMPLETO")))` | Sin carga válida no produce presión ni contacto ficticios. |
| PRESIONES_ULTIMAS | `D17` | `=IF(geo_input_state<>"OK",geo_input_state,IF(OR(COUNT(ult_p,ult_mx,ult_my)<3,COUNT(srv_p,srv_mx,srv_my)<3,COUNT(punz_d_x,punz_d_y)<2,inp_phi_p<>0.85,inp_phi_v<>0.85),"REVISAR DATOS / PHI E.060",IF(MIN(punz_d_x,punz_d_y)<=0,"PERALTE EFECTIVO NO POSITIVO",IF(ult_p<=0,"LEVANTAMIENTO / TRACCIÓN: NO DISEÑAR",IF(D13<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS DE CONTACTO PARCIAL","OK")))))` | `=IF(geo_input_state<>"OK","DATOS INVÁLIDOS",IF(NOT(AND(COUNT(inp_fc,inp_fy,inp_phi_f,inp_phi_v,inp_phi_p,inp_rho_min,inp_sep_max_usuario,inp_sep_inf_x,inp_sep_inf_y,inp_sep_sup_x,inp_sep_sup_y,inp_fwz_u,inp_fws_u)=13,MIN(inp_fc,inp_fy,inp_sep_max_usuario,inp_sep_inf_x,inp_sep_inf_y,inp_sep_sup_x,inp_sep_sup_y)>0,inp_rho_min>=0,MIN(inp_fwz_u,inp_fws_u)>=0,inp_phi_f=0.9,inp_phi_v=0.85,inp_phi_p=0.85)),"DATOS INVÁLIDOS",IF(COUNT(CARGAS!C22:C27)<>6,"DATOS INVÁLIDOS",IF(OR(inp_concrete_type<>"NORMAL",inp_rebar_type<>"CORRUGADAS"),"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNT(punz_d_x,punz_d_y)<2,"DATOS INVÁLIDOS",IF(MIN(punz_d_x,punz_d_y)<=0,"DATOS INVÁLIDOS",IF(ult_p<=0,"REQUIERE ANÁLISIS ESPECIAL",IF(D13<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS ESPECIAL","OK"))))))))` | Resistencia solo acciones amplificadas. Sin IFERROR/ceros para divisiones o phi incorrectos. |
| PRESIONES_ULTIMAS | `D25` | `(vacía)` | `E.060 15.2.1; exclusivamente estado último.` | E.060 15.2.1; exclusivamente estado último. |
| DIAGRAMAS_X | `B7` | `=IF(struct_state="OK",$J$7*((inp_xc-inp_cx/2)+inp_bx/2)^2/2+$J$8*((inp_xc-inp_cx/2)+inp_bx/2)^3/6-ult_p*MAX(0,(inp_xc-inp_cx/2)-inp_xc),"")` | `=IF(struct_state="OK",$J$7*(inp_bx/2+inp_xc-inp_cx/2)^2/2+$J$8*(inp_bx/2+inp_xc-inp_cx/2)^3/6,"")` | 15.4.1: fuerzas sobre el voladizo exterior izquierdo/inferior; exacto, sin P dentro de columna. |
| DIAGRAMAS_X | `B8` | `=IF(struct_state="OK",$J$7*((inp_xc+inp_cx/2)+inp_bx/2)^2/2+$J$8*((inp_xc+inp_cx/2)+inp_bx/2)^3/6-ult_p*MAX(0,(inp_xc+inp_cx/2)-inp_xc)+ $J$9,"")` | `=IF(struct_state="OK",($J$7+$J$8*inp_bx)*(inp_bx/2-inp_xc-inp_cx/2)^2/2-$J$8*(inp_bx/2-inp_xc-inp_cx/2)^3/6,"")` | 15.4.1: integrar desde extremo libre derecho/superior; evita cancelación de grandes términos P y M. |
| DIAGRAMAS_X | `B9` | `=IF(struct_state="OK",MAX(B4,B5)/inp_by,"")` | `=IF(struct_state="OK",MAX(ABS(B7),ABS(B8))/inp_by,"")` | E.060 15.4.2(a): máximo solo en caras de columna; B4/B5 globales conservados para gráficos. |
| DIAGRAMAS_X | `D7:D8` | `Formula ligada a tabla inferior` | `Mu exacto en cara; E.060 15.4.1/2(a).` | Identificar fuente normativa. |
| DIAGRAMAS_X | `J6` | `=IF(struct_state<>"OK",struct_state,IF(AND(ABS(J4)<=MAX(0.000001,0.001*ABS(ult_p)),ABS(J5)<=MAX(0.000001,0.001*MAX(ABS(ult_my),ABS(ult_p*inp_bx)))),"OK","ERROR"))` | `=IF(struct_state<>"OK",struct_state,IF(AND(ABS(J4)<=MAX(0.00000001,0.0000000001*ABS(ult_p)),ABS(J5)<=MAX(0.00000001,0.0000000001*MAX(ABS($J$9),ABS(ult_p*inp_bx)))),"OK","ERROR"))` | Cierre analítico: tolerancia absoluta1e-8 y relativa1e-10, compatible con doble precisión Excel. |
| DIAGRAMAS_Y | `B7` | `=IF(struct_state="OK",$J$7*((inp_yc-inp_cy/2)+inp_by/2)^2/2+$J$8*((inp_yc-inp_cy/2)+inp_by/2)^3/6-ult_p*MAX(0,(inp_yc-inp_cy/2)-inp_yc),"")` | `=IF(struct_state="OK",$J$7*(inp_by/2+inp_yc-inp_cy/2)^2/2+$J$8*(inp_by/2+inp_yc-inp_cy/2)^3/6,"")` | 15.4.1: fuerzas sobre el voladizo exterior izquierdo/inferior; exacto, sin P dentro de columna. |
| DIAGRAMAS_Y | `B8` | `=IF(struct_state="OK",$J$7*((inp_yc+inp_cy/2)+inp_by/2)^2/2+$J$8*((inp_yc+inp_cy/2)+inp_by/2)^3/6-ult_p*MAX(0,(inp_yc+inp_cy/2)-inp_yc)+ $J$9,"")` | `=IF(struct_state="OK",($J$7+$J$8*inp_by)*(inp_by/2-inp_yc-inp_cy/2)^2/2-$J$8*(inp_by/2-inp_yc-inp_cy/2)^3/6,"")` | 15.4.1: integrar desde extremo libre derecho/superior; evita cancelación de grandes términos P y M. |
| DIAGRAMAS_Y | `B9` | `=IF(struct_state="OK",MAX(B4,B5)/inp_bx,"")` | `=IF(struct_state="OK",MAX(ABS(B7),ABS(B8))/inp_bx,"")` | E.060 15.4.2(a): máximo solo en caras de columna; B4/B5 globales conservados para gráficos. |
| DIAGRAMAS_Y | `D7:D8` | `Formula ligada a tabla inferior` | `Mu exacto en cara; E.060 15.4.1/2(a).` | Identificar fuente normativa. |
| DIAGRAMAS_Y | `J6` | `=IF(struct_state<>"OK",struct_state,IF(AND(ABS(J4)<=MAX(0.000001,0.001*ABS(ult_p)),ABS(J5)<=MAX(0.000001,0.001*MAX(ABS((-ult_mx)),ABS(ult_p*inp_by)))),"OK","ERROR"))` | `=IF(struct_state<>"OK",struct_state,IF(AND(ABS(J4)<=MAX(0.00000001,0.0000000001*ABS(ult_p)),ABS(J5)<=MAX(0.00000001,0.0000000001*MAX(ABS($J$9),ABS(ult_p*inp_by)))),"OK","ERROR"))` | Cierre analítico: tolerancia absoluta1e-8 y relativa1e-10, compatible con doble precisión Excel. |
| PUNZONAMIENTO | `A61` | `(vacía)` | `GEOMETRÍA DEL PERÍMETRO Y ALCANCE` | GEOMETRÍA DEL PERÍMETRO Y ALCANCE |
| PUNZONAMIENTO | `A62` | `(vacía)` | `Margen X para d/2` | 11.12.1.2: margen real desde perímetro a borde, d/2 por lado. |
| PUNZONAMIENTO | `A63` | `(vacía)` | `Margen Y para d/2` | No usar lado mayor de columna en ambos ejes. |
| PUNZONAMIENTO | `A64` | `(vacía)` | `Perímetro cerrado contenido` | Condición geométrica, no garantía de que sea sección crítica mínima. |
| PUNZONAMIENTO | `A65` | `(vacía)` | `Filtro conservador de dominio` | Margen voluntario libre >=d; NO se atribuye a la norma. Cerca de borde exige perímetros alternativos. |
| PUNZONAMIENTO | `A66` | `(vacía)` | `Tipo / orientación` | BORDE y ESQUINA mantienen bloqueo; no se reutilizan J interiores. |
| PUNZONAMIENTO | `B11` | `=IF(geo_input_state="OK",IF(AND(geo_input_state="OK",inp_col_type="INTERIOR",MIN(B8:B9)>0,geo_min_edge_dist>=MAX(inp_cx,inp_cy)/2+B10/100),2*(B4+B10)+2*(B5+B10),""),"")` | `=IF(geo_input_state<>"OK","",IF(NOT(ISNUMBER(B10)),"",IF(AND(B10>0,inp_col_type="INTERIOR",punz_geom_state="OK",punz_domain="OK"),2*((B4+B10)+(B5+B10)),"")))` | 11.12.1.2: bo cerrado d/2, solo geometría contenida y alcance conservador explícito. |
| PUNZONAMIENTO | `B19` | `=IF(inp_col_type<>"INTERIOR","BORDE/ESQUINA: REQUIERE GEOMETRÍA DE PERÍMETRO ABIERTO",IF(NOT(ISNUMBER(B11)),"BORDE LIBRE PRÓXIMO: REVISAR PERÍMETRO MÍNIMO",""))` | `=IF(geo_input_state<>"OK","DATOS INVÁLIDOS",IF(inp_col_type<>"INTERIOR","FUERA DEL ALCANCE IMPLEMENTADO: PERÍMETRO ABIERTO",IF(punz_domain<>"OK","REQUIERE REVISIÓN DE PERÍMETROS ALTERNATIVOS CERCA DE BORDE","")))` | Distinguir geometría de condición conservadora voluntaria. |
| PUNZONAMIENTO | `B28` | `=IF(struct_state<>"OK",struct_state,IF(NOT(ISNUMBER(B11)),"REQUIERE GEOMETRÍA DE PERÍMETRO CRÍTICO","OK"))` | `=IF(struct_state<>"OK",struct_state,IF(inp_col_type<>"INTERIOR","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(punz_geom_state<>"OK",punz_domain<>"OK"),"FUERA DEL ALCANCE IMPLEMENTADO","OK")))` | Sin perímetro/J abiertos probados, no afirmar cumplimiento. |
| PUNZONAMIENTO | `B55` | `=IF(B28="OK",MIN(inp_bx,inp_cx+3*inp_h),"")` | `=IF(punz_state="OK",MIN(inp_bx/2,inp_xc+inp_cx/2+1.5*inp_h)-MAX(-inp_bx/2,inp_xc-inp_cx/2-1.5*inp_h),"")` | 13.5.3.1: intersección física de franja c+3h con zapata, respecto a columna descentrada. |
| PUNZONAMIENTO | `B56` | `=IF(B28="OK",MIN(inp_by,inp_cy+3*inp_h),"")` | `=IF(punz_state="OK",MIN(inp_by/2,inp_yc+inp_cy/2+1.5*inp_h)-MAX(-inp_by/2,inp_yc-inp_cy/2-1.5*inp_h),"")` | 13.5.3.1: ancho disponible real, no MIN(ancho total,c+3h) con centro incorrecto. |
| PUNZONAMIENTO | `B57` | `=IF(B28<>"OK",B28,IF(MAX(ABS(B47),ABS(B48))>0.000001,"ADVERTENCIA: VERIFICAR REFUERZO LOCAL γf Mu (13.5.3.3)","SIN MOMENTO TRANSFERIDO"))` | `=local_state` | E.060 13.5.3: resultado de comprobación real de acero local, no advertencia genérica. |
| PUNZONAMIENTO | `B62` | `(vacía)` | `=IF(AND(geo_input_state="OK",ISNUMBER(B10),B10>0),inp_bx/2-ABS(inp_xc)-inp_cx/2-B10/200,"")` | 11.12.1.2: margen real desde perímetro a borde, d/2 por lado. |
| PUNZONAMIENTO | `B63` | `(vacía)` | `=IF(AND(geo_input_state="OK",ISNUMBER(B10),B10>0),inp_by/2-ABS(inp_yc)-inp_cy/2-B10/200,"")` | No usar lado mayor de columna en ambos ejes. |
| PUNZONAMIENTO | `B64` | `(vacía)` | `=IF(COUNT(B62:B63)<2,"DATOS INVÁLIDOS",IF(MIN(B62:B63)>=0,"OK","FUERA DEL ALCANCE IMPLEMENTADO"))` | Condición geométrica, no garantía de que sea sección crítica mínima. |
| PUNZONAMIENTO | `B65` | `(vacía)` | `=IF(COUNT(B62:B63)<2,"DATOS INVÁLIDOS",IF(geo_min_edge_dist>=B10/100,"OK","FUERA DEL ALCANCE IMPLEMENTADO"))` | Margen voluntario libre >=d; NO se atribuye a la norma. Cerca de borde exige perímetros alternativos. |
| PUNZONAMIENTO | `B66` | `(vacía)` | `=inp_col_type&" / "&inp_edge_dir` | BORDE y ESQUINA mantienen bloqueo; no se reutilizan J interiores. |
| PUNZONAMIENTO | `C62` | `(vacía)` | `m` | 11.12.1.2: margen real desde perímetro a borde, d/2 por lado. |
| PUNZONAMIENTO | `C63` | `(vacía)` | `m` | No usar lado mayor de columna en ambos ejes. |
| PUNZONAMIENTO | `C64` | `(vacía)` | `-` | Condición geométrica, no garantía de que sea sección crítica mínima. |
| PUNZONAMIENTO | `C65` | `(vacía)` | `-` | Margen voluntario libre >=d; NO se atribuye a la norma. Cerca de borde exige perímetros alternativos. |
| PUNZONAMIENTO | `C66` | `(vacía)` | `-` | BORDE y ESQUINA mantienen bloqueo; no se reutilizan J interiores. |
| PUNZONAMIENTO | `D62` | `(vacía)` | `11.12.1.2: margen real desde perímetro a borde, d/2 por lado.` | 11.12.1.2: margen real desde perímetro a borde, d/2 por lado. |
| PUNZONAMIENTO | `D63` | `(vacía)` | `No usar lado mayor de columna en ambos ejes.` | No usar lado mayor de columna en ambos ejes. |
| PUNZONAMIENTO | `D64` | `(vacía)` | `Condición geométrica, no garantía de que sea sección crítica mínima.` | Condición geométrica, no garantía de que sea sección crítica mínima. |
| PUNZONAMIENTO | `D65` | `(vacía)` | `Margen voluntario libre >=d; NO se atribuye a la norma. Cerca de borde exige perímetros alternativos.` | Margen voluntario libre >=d; NO se atribuye a la norma. Cerca de borde exige perímetros alternativos. |
| PUNZONAMIENTO | `D66` | `(vacía)` | `BORDE y ESQUINA mantienen bloqueo; no se reutilizan J interiores.` | BORDE y ESQUINA mantienen bloqueo; no se reutilizan J interiores. |
| CORTANTE_UNIDIRECCIONAL | `C5:C6` | `=IF(struct_state="OK",MAX(0,B5-punz_d_x/100),"")` | `=IF(struct_state="OK",MAX(0,B5-J5/100),"")` | Sección a d desde cara y capacidad con d físico coherente con el signo. |
| CORTANTE_UNIDIRECCIONAL | `C7:C8` | `=IF(struct_state="OK",MAX(0,B7-punz_d_y/100),"")` | `=IF(struct_state="OK",MAX(0,B7-J7/100),"")` | Sección a d desde cara y capacidad con d físico coherente con el signo. |
| CORTANTE_UNIDIRECCIONAL | `G5:G6` | `=IF(struct_state="OK",inp_phi_v*0.17*PUNZONAMIENTO!$B$22*SQRT(inp_fc)*100*punz_d_x/1000,"")` | `=IF(struct_state="OK",inp_phi_v*0.17*PUNZONAMIENTO!$B$22*SQRT(inp_fc)*100*J5/1000,"")` | Sección a d desde cara y capacidad con d físico coherente con el signo. |
| CORTANTE_UNIDIRECCIONAL | `G7:G8` | `=IF(struct_state="OK",inp_phi_v*0.17*PUNZONAMIENTO!$B$22*SQRT(inp_fc)*100*punz_d_y/1000,"")` | `=IF(struct_state="OK",inp_phi_v*0.17*PUNZONAMIENTO!$B$22*SQRT(inp_fc)*100*J7/1000,"")` | Sección a d desde cara y capacidad con d físico coherente con el signo. |
| CORTANTE_UNIDIRECCIONAL | `I4` | `(vacía)` | `Vu firmado tf/m` | E.060 15.5: conservar signo además de magnitud. |
| CORTANTE_UNIDIRECCIONAL | `I5:I8` | `(vacía)` | `=IF(struct_state="OK",E5*C5,"")` | Integral firmada tf/m; F muestra magnitud necesaria para comparar capacidad, no borra signo original. |
| CORTANTE_UNIDIRECCIONAL | `J4` | `(vacía)` | `d utilizado cm` | Dirección X/Y y capa traccionada según cara crítica. |
| CORTANTE_UNIDIRECCIONAL | `J5` | `(vacía)` | `=IF(struct_state="OK",IF(DIAGRAMAS_X!B7<0,FLEXION_ACERO!E7,punz_d_x),"")` | 15.5.2: d de dirección/capa realmente traccionada; inversión usa capa superior. |
| CORTANTE_UNIDIRECCIONAL | `J6` | `(vacía)` | `=IF(struct_state="OK",IF(DIAGRAMAS_X!B8<0,FLEXION_ACERO!E7,punz_d_x),"")` | 15.5.2: d de dirección/capa realmente traccionada; inversión usa capa superior. |
| CORTANTE_UNIDIRECCIONAL | `J7` | `(vacía)` | `=IF(struct_state="OK",IF(DIAGRAMAS_Y!B7<0,FLEXION_ACERO!E8,punz_d_y),"")` | 15.5.2: d de dirección/capa realmente traccionada; inversión usa capa superior. |
| CORTANTE_UNIDIRECCIONAL | `J8` | `(vacía)` | `=IF(struct_state="OK",IF(DIAGRAMAS_Y!B8<0,FLEXION_ACERO!E8,punz_d_y),"")` | 15.5.2: d de dirección/capa realmente traccionada; inversión usa capa superior. |
| FLEXION_ACERO | `A20` | `(vacía)` | `MÍNIMOS Y CAPACIDAD — E.060 9.7, 10.3, 10.5` | MÍNIMOS Y CAPACIDAD — E.060 9.7, 10.3, 10.5 |
| FLEXION_ACERO | `A21` | `(vacía)` | `fy convertido a MPa` | 1 kgf/cm2 = 0.0980665 MPa exacto. |
| FLEXION_ACERO | `A22` | `(vacía)` | `Cuantía mínima normativa` | E.060 9.7.2. Malla fy<420 no tiene valor explícito en tabla; se deja sin cuantía y fuera de alcance. |
| FLEXION_ACERO | `A23` | `(vacía)` | `Cuantía mínima efectiva` | No admite que rho_usuario menor reduzca mínimo normativo. |
| FLEXION_ACERO | `A24` | `(vacía)` | `Cuantía ingresada vs norma` | No cambia la entrada heredada 0.0018; se impone 0.002 para fy=4200kgf/cm2. |
| FLEXION_ACERO | `A25` | `(vacía)` | `Beta1 del bloque rectangular` | E.060 10.2.7.3: interpolación 28–56MPa. |
| FLEXION_ACERO | `A26` | `(vacía)` | `Rho balanceada` | E.060 10.2/10.3.2; Es=200000MPa según 8.5.5, convertido exactamente. |
| FLEXION_ACERO | `A27` | `(vacía)` | `Rho máxima implementada` | E.060 10.3.4; sección simple sin acreditar acero a compresión. |
| FLEXION_ACERO | `A28` | `(vacía)` | `Resistencia mínima del concreto` | E.060 5.1.1: fc mínimo17MPa en concreto estructural, ambas superficies. |
| FLEXION_ACERO | `B14` | `=IF(struct_state="OK",-diagx_m_neg/inp_by,"")` | `=IF(struct_state="OK",-D7,"")` | Demanda negativa normativa en caras X. |
| FLEXION_ACERO | `B15` | `=IF(struct_state="OK",-diagy_m_neg/inp_bx,"")` | `=IF(struct_state="OK",-D8,"")` | Demanda negativa normativa en caras Y. |
| FLEXION_ACERO | `B16` | `=IF(struct_state<>"OK",struct_state,IF(MAX(D7:D8)>0.000001,"REQUIERE ACERO SUPERIOR POR INVERSIÓN DE MOMENTO","SIN DEMANDA NEGATIVA GLOBAL"))` | `=IF(struct_state<>"OK",struct_state,IF(MAX(D7:D8)>0.000001,"REQUIERE ACERO SUPERIOR","SIN INVERSIÓN EN CARAS"))` | Texto abreviado visible; el acero superior local se comprueba separadamente. |
| FLEXION_ACERO | `B17` | `=PUNZONAMIENTO!B57` | `=local_state` | Separar acero global de acero local por transferencia. |
| FLEXION_ACERO | `B21` | `(vacía)` | `=IF(ISNUMBER(inp_fy),inp_fy*0.0980665,"")` | 1 kgf/cm2 = 0.0980665 MPa exacto. |
| FLEXION_ACERO | `B22` | `(vacía)` | `=IF(OR(inp_rebar_type="CORRUGADAS",inp_rebar_type="LISAS",inp_rebar_type="MALLA SOLDADA"),IF(inp_rebar_type="LISAS",0.0025,IF(inp_rebar_type="MALLA SOLDADA",IF(fy_mpa>=420,0.0018,""),IF(fy_mpa>=420,0.0018,0.002))),"")` | E.060 9.7.2. Malla fy<420 no tiene valor explícito en tabla; se deja sin cuantía y fuera de alcance. |
| FLEXION_ACERO | `B23` | `(vacía)` | `=IF(AND(ISNUMBER(rho_norm),ISNUMBER(inp_rho_min),inp_rho_min>=0),MAX(rho_norm,inp_rho_min),"")` | No admite que rho_usuario menor reduzca mínimo normativo. |
| FLEXION_ACERO | `B24` | `(vacía)` | `=IF(COUNT(rho_norm,inp_rho_min)<2,"DATOS INVÁLIDOS",IF(inp_rho_min<rho_norm,"DEBAJO DEL MÍNIMO: SE USA RHO NORMATIVA","OK"))` | No cambia la entrada heredada 0.0018; se impone 0.002 para fy=4200kgf/cm2. |
| FLEXION_ACERO | `B25` | `(vacía)` | `=IF(ISNUMBER(inp_fc),MAX(0.65,MIN(0.85,0.85-(inp_fc*0.0980665-28)*0.2/28)),"")` | E.060 10.2.7.3: interpolación 28–56MPa. |
| FLEXION_ACERO | `B26` | `(vacía)` | `=IF(AND(ISNUMBER(inp_fc),ISNUMBER(inp_fy),inp_fc>0,inp_fy>0),0.85*flex_beta1*inp_fc/inp_fy*(0.003/(0.003+inp_fy/(200000/0.0980665))),"")` | E.060 10.2/10.3.2; Es=200000MPa según 8.5.5, convertido exactamente. |
| FLEXION_ACERO | `B27` | `(vacía)` | `=IF(ISNUMBER(rho_bal),0.75*rho_bal,"")` | E.060 10.3.4; sección simple sin acreditar acero a compresión. |
| FLEXION_ACERO | `B28` | `(vacía)` | `=IF(NOT(ISNUMBER(inp_fc)),"DATOS INVÁLIDOS",IF(inp_fc*0.0980665<17,"NO CUMPLE",IF(COUNT(inp_fc_col)<>1,"REQUIERE DATOS",IF(inp_fc_col*0.0980665>=17,"CUMPLE","NO CUMPLE"))))` | E.060 5.1.1: fc mínimo17MPa en concreto estructural, ambas superficies. |
| FLEXION_ACERO | `C21` | `(vacía)` | `MPa` | 1 kgf/cm2 = 0.0980665 MPa exacto. |
| FLEXION_ACERO | `C22` | `(vacía)` | `-` | E.060 9.7.2. Malla fy<420 no tiene valor explícito en tabla; se deja sin cuantía y fuera de alcance. |
| FLEXION_ACERO | `C23` | `(vacía)` | `-` | No admite que rho_usuario menor reduzca mínimo normativo. |
| FLEXION_ACERO | `C24` | `(vacía)` | `-` | No cambia la entrada heredada 0.0018; se impone 0.002 para fy=4200kgf/cm2. |
| FLEXION_ACERO | `C25` | `(vacía)` | `-` | E.060 10.2.7.3: interpolación 28–56MPa. |
| FLEXION_ACERO | `C26` | `(vacía)` | `-` | E.060 10.2/10.3.2; Es=200000MPa según 8.5.5, convertido exactamente. |
| FLEXION_ACERO | `C27` | `(vacía)` | `-` | E.060 10.3.4; sección simple sin acreditar acero a compresión. |
| FLEXION_ACERO | `C28` | `(vacía)` | `-` | E.060 5.1.1: fc mínimo17MPa en concreto estructural, ambas superficies. |
| FLEXION_ACERO | `D5` | `=IF(struct_state="OK",diagx_m_pos/inp_by,"")` | `=IF(struct_state="OK",MAX(0,DIAGRAMAS_X!B7,DIAGRAMAS_X!B8)/inp_by,"")` | E.060 15.4.2(a): caras críticas exactas con signo, positivo inferior/negativo superior. |
| FLEXION_ACERO | `D6` | `=IF(struct_state="OK",diagy_m_pos/inp_bx,"")` | `=IF(struct_state="OK",MAX(0,DIAGRAMAS_Y!B7,DIAGRAMAS_Y!B8)/inp_bx,"")` | E.060 15.4.2(a): caras críticas exactas con signo, positivo inferior/negativo superior. |
| FLEXION_ACERO | `D7` | `=IF(struct_state="OK",diagx_m_neg/inp_by,"")` | `=IF(struct_state="OK",MAX(0,-DIAGRAMAS_X!B7,-DIAGRAMAS_X!B8)/inp_by,"")` | E.060 15.4.2(a): caras críticas exactas con signo, positivo inferior/negativo superior. |
| FLEXION_ACERO | `D8` | `=IF(struct_state="OK",diagy_m_neg/inp_bx,"")` | `=IF(struct_state="OK",MAX(0,-DIAGRAMAS_Y!B7,-DIAGRAMAS_Y!B8)/inp_bx,"")` | E.060 15.4.2(a): caras críticas exactas con signo, positivo inferior/negativo superior. |
| FLEXION_ACERO | `D21` | `(vacía)` | `1 kgf/cm2 = 0.0980665 MPa exacto.` | 1 kgf/cm2 = 0.0980665 MPa exacto. |
| FLEXION_ACERO | `D22` | `(vacía)` | `E.060 9.7.2. Malla fy<420 no tiene valor explícito en tabla; se deja sin cuantía y fuera de alcance.` | E.060 9.7.2. Malla fy<420 no tiene valor explícito en tabla; se deja sin cuantía y fuera de alcance. |
| FLEXION_ACERO | `D23` | `(vacía)` | `No admite que rho_usuario menor reduzca mínimo normativo.` | No admite que rho_usuario menor reduzca mínimo normativo. |
| FLEXION_ACERO | `D24` | `(vacía)` | `No cambia la entrada heredada 0.0018; se impone 0.002 para fy=4200kgf/cm2.` | No cambia la entrada heredada 0.0018; se impone 0.002 para fy=4200kgf/cm2. |
| FLEXION_ACERO | `D25` | `(vacía)` | `E.060 10.2.7.3: interpolación 28–56MPa.` | E.060 10.2.7.3: interpolación 28–56MPa. |
| FLEXION_ACERO | `D26` | `(vacía)` | `E.060 10.2/10.3.2; Es=200000MPa según 8.5.5, convertido exactamente.` | E.060 10.2/10.3.2; Es=200000MPa según 8.5.5, convertido exactamente. |
| FLEXION_ACERO | `D27` | `(vacía)` | `E.060 10.3.4; sección simple sin acreditar acero a compresión.` | E.060 10.3.4; sección simple sin acreditar acero a compresión. |
| FLEXION_ACERO | `D28` | `(vacía)` | `E.060 5.1.1: fc mínimo17MPa en concreto estructural, ambas superficies.` | E.060 5.1.1: fc mínimo17MPa en concreto estructural, ambas superficies. |
| FLEXION_ACERO | `F5:F8` | `=IF(struct_state="OK",IF(D5<=0,0,IF((inp_fy*E5)^2-4*(inp_fy^2/(2*0.85*inp_fc*100))*(D5*100000/inp_phi_f)<0,999,(inp_fy*E5-SQRT((inp_fy*E5)^2-4*(inp_fy^2/(2*0.85*inp_fc*100))*(D5*100000/inp_phi_f)))/(2*(inp_fy^2/(2*0.85*inp_fc*100))))),"")` | `=IF(struct_state="OK",IF(D5<=0,0,IF((inp_fy*E5)^2-4*(inp_fy^2/(2*0.85*inp_fc*100))*(D5*100000/inp_phi_f)<0,"",(inp_fy*E5-SQRT((inp_fy*E5)^2-4*(inp_fy^2/(2*0.85*inp_fc*100))*(D5*100000/inp_phi_f)))/(2*(inp_fy^2/(2*0.85*inp_fc*100))))),"")` | E.060 10.2: sección simple; imposible se deja vacío y estado NO CUMPLE, sin 999. |
| FLEXION_ACERO | `G5:G8` | `=IF(struct_state="OK",IF(OR(B5="Inferior",D5>0),inp_rho_min*100*inp_h*100,0),"")` | `=IF(struct_state="OK",IF(OR(B5="Inferior",D5>0),rho_eff*100*inp_h*100,0),"")` | E.060 10.5.4 y 9.7.2; mínimo íntegro en cara correspondiente, no repartir entre caras. |
| FLEXION_ACERO | `H5:H8` | `=IF(struct_state="OK",IF(F5=999,999,MAX(F5,G5)),"")` | `=IF(struct_state="OK",IF(ISNUMBER(F5),MAX(F5,G5),""),"")` | No presenta As mínimo como solución cuando flexión no tiene raíz resistente. |
| FLEXION_ACERO | `I5:I8` | `=IF(struct_state<>"OK",struct_state,IF(E5<=0,"PERALTE NO POSITIVO",IF(F5=999,"REVISAR SECCION","VER DETALLADO")))` | `=IF(struct_state<>"OK",struct_state,IF(NOT(ISNUMBER(H5)),"NO CUMPLE",IF(H5>rho_max*100*E5,"NO CUMPLE","VER DETALLADO")))` | E.060 10.3.4: verificar As<=0.75Asb antes de acreditar resistencia. |
| ACERO_DETALLADO | `A20` | `(vacía)` | `DISTRIBUCIÓN RECTANGULAR — E.060 15.4.4` | DISTRIBUCIÓN RECTANGULAR — E.060 15.4.4 |
| ACERO_DETALLADO | `A21` | `(vacía)` | `Lado largo` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `A22` | `(vacía)` | `Lado corto` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `A23` | `(vacía)` | `Beta largo/corto` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `A24` | `(vacía)` | `Gamma s` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `A27` | `(vacía)` | `DISTRIBUCIÓN INFERIOR X` | DISTRIBUCIÓN INFERIOR X |
| ACERO_DETALLADO | `A28` | `(vacía)` | `Dirección` | Distribuir X sobre Y y viceversa. |
| ACERO_DETALLADO | `A29` | `(vacía)` | `As total requerido` | As por metro × ancho perpendicular completo. |
| ACERO_DETALLADO | `A30` | `(vacía)` | `Ancho franja central` | Corta: ancho igual lado corto, centrado en eje columna. |
| ACERO_DETALLADO | `A31` | `(vacía)` | `Ancho exterior total` | Zonas de ambos lados, suma de anchos. |
| ACERO_DETALLADO | `A32` | `(vacía)` | `As central requerido` | 15.4.4.2: gamma_s As; larga/cuadrada totalidad uniforme. |
| ACERO_DETALLADO | `A33` | `(vacía)` | `As exterior requerido` | (1-gamma_s) As, no uniforme central arbitrario. |
| ACERO_DETALLADO | `A34` | `(vacía)` | `Barra y diámetro adoptados` | Se mantiene diámetro global; separación regional editable. |
| ACERO_DETALLADO | `A35` | `(vacía)` | `Separación central adoptada` | Entrada visible, no se cambia para lograr cumplimiento. |
| ACERO_DETALLADO | `A36` | `(vacía)` | `Separación exterior adoptada` | Si zona exterior no existe, no aplica. |
| ACERO_DETALLADO | `A37` | `(vacía)` | `N real central` | Conteo declarado del plano, no estimación continua. |
| ACERO_DETALLADO | `A38` | `(vacía)` | `N real exterior` | Conteo fuera de franja, cero explícito si no existe. |
| ACERO_DETALLADO | `A39` | `(vacía)` | `As colocado central` | Acero real = número × área comercial. |
| ACERO_DETALLADO | `A40` | `(vacía)` | `As colocado exterior` | No usa area equivalente por metro para contar barras. |
| ACERO_DETALLADO | `A41` | `(vacía)` | `As central por metro requerido` | Concentración de la dirección corta. |
| ACERO_DETALLADO | `A42` | `(vacía)` | `As exterior por metro requerido` | Cero solo si región inexistente. |
| ACERO_DETALLADO | `A43` | `(vacía)` | `Franja contenida` | No se recorta una franja centrada normativa que sale de la zapata. |
| ACERO_DETALLADO | `A44` | `(vacía)` | `Estado distribución X` | Combina cantidad real y separación/densidad, manteniendo mínimo; 15.4.4. |
| ACERO_DETALLADO | `A48` | `(vacía)` | `DISTRIBUCIÓN INFERIOR Y` | DISTRIBUCIÓN INFERIOR Y |
| ACERO_DETALLADO | `A49` | `(vacía)` | `Dirección` | Distribuir X sobre Y y viceversa. |
| ACERO_DETALLADO | `A50` | `(vacía)` | `As total requerido` | As por metro × ancho perpendicular completo. |
| ACERO_DETALLADO | `A51` | `(vacía)` | `Ancho franja central` | Corta: ancho igual lado corto, centrado en eje columna. |
| ACERO_DETALLADO | `A52` | `(vacía)` | `Ancho exterior total` | Zonas de ambos lados, suma de anchos. |
| ACERO_DETALLADO | `A53` | `(vacía)` | `As central requerido` | 15.4.4.2: gamma_s As; larga/cuadrada totalidad uniforme. |
| ACERO_DETALLADO | `A54` | `(vacía)` | `As exterior requerido` | (1-gamma_s) As, no uniforme central arbitrario. |
| ACERO_DETALLADO | `A55` | `(vacía)` | `Barra y diámetro adoptados` | Se mantiene diámetro global; separación regional editable. |
| ACERO_DETALLADO | `A56` | `(vacía)` | `Separación central adoptada` | Entrada visible, no se cambia para lograr cumplimiento. |
| ACERO_DETALLADO | `A57` | `(vacía)` | `Separación exterior adoptada` | Si zona exterior no existe, no aplica. |
| ACERO_DETALLADO | `A58` | `(vacía)` | `N real central` | Conteo declarado del plano, no estimación continua. |
| ACERO_DETALLADO | `A59` | `(vacía)` | `N real exterior` | Conteo fuera de franja, cero explícito si no existe. |
| ACERO_DETALLADO | `A60` | `(vacía)` | `As colocado central` | Acero real = número × área comercial. |
| ACERO_DETALLADO | `A61` | `(vacía)` | `As colocado exterior` | No usa area equivalente por metro para contar barras. |
| ACERO_DETALLADO | `A62` | `(vacía)` | `As central por metro requerido` | Concentración de la dirección corta. |
| ACERO_DETALLADO | `A63` | `(vacía)` | `As exterior por metro requerido` | Cero solo si región inexistente. |
| ACERO_DETALLADO | `A64` | `(vacía)` | `Franja contenida` | No se recorta una franja centrada normativa que sale de la zapata. |
| ACERO_DETALLADO | `A65` | `(vacía)` | `Estado distribución Y` | Combina cantidad real y separación/densidad, manteniendo mínimo; 15.4.4. |
| ACERO_DETALLADO | `A70` | `(vacía)` | `DESARROLLO DE PARRILLAS — E.060 15.6 / 12.2` | DESARROLLO DE PARRILLAS — E.060 15.6 / 12.2 |
| ACERO_DETALLADO | `A72` | `(vacía)` | `Parrilla` | 12.2.3: Ktr=0; sin reducción por acero en exceso. |
| ACERO_DETALLADO | `A73` | `(vacía)` | `INF X` | Punto de desarrollo: ambas caras de columna y barra continua en toda la longitud. |
| ACERO_DETALLADO | `A74` | `(vacía)` | `INF Y` | Punto de desarrollo: ambas caras de columna y barra continua en toda la longitud. |
| ACERO_DETALLADO | `A75` | `(vacía)` | `SUP X` | Punto de desarrollo: ambas caras de columna y barra continua en toda la longitud. |
| ACERO_DETALLADO | `A76` | `(vacía)` | `SUP Y` | Punto de desarrollo: ambas caras de columna y barra continua en toda la longitud. |
| ACERO_DETALLADO | `A78` | `(vacía)` | `Estado de desarrollo global` | Secciones de cambios de sección/refuerzo no modeladas; barras rectas continuas. |
| ACERO_DETALLADO | `A79` | `(vacía)` | `Hipótesis de desarrollo` | 12.2.3 permite Ktr=0. Sin reducción por exceso. Ganchos/paquetes/cortes/empalmes requieren detalle especial. |
| ACERO_DETALLADO | `A83` | `(vacía)` | `ACERO LOCAL DE TRANSFERENCIA — E.060 13.5.3` | ACERO LOCAL DE TRANSFERENCIA — E.060 13.5.3 |
| ACERO_DETALLADO | `A85` | `(vacía)` | `Capa/dirección` | Franja efectiva real; no se acredita por As global por metro. |
| ACERO_DETALLADO | `A86` | `(vacía)` | `INF X` | Ambas capas se comprueban conservadoramente para transferencia no balanceada, ambos signos. |
| ACERO_DETALLADO | `A87` | `(vacía)` | `INF Y` | Ambas capas se comprueban conservadoramente para transferencia no balanceada, ambos signos. |
| ACERO_DETALLADO | `A88` | `(vacía)` | `SUP X` | Ambas capas se comprueban conservadoramente para transferencia no balanceada, ambos signos. |
| ACERO_DETALLADO | `A89` | `(vacía)` | `SUP Y` | Ambas capas se comprueban conservadoramente para transferencia no balanceada, ambos signos. |
| ACERO_DETALLADO | `A91` | `(vacía)` | `Estado acero local` | No permite convertir advertencia F1 en CUMPLE sin conteo y desarrollo comprobados. |
| ACERO_DETALLADO | `A92` | `(vacía)` | `Alcance local implementado` | Ambas capas resisten conservadoramente la magnitud local más demanda global; sin reparto único entre signos. |
| ACERO_DETALLADO | `A93` | `(vacía)` | `Datos faltantes de acero local` | Nombres exactos vinculados a entradas editables. |
| ACERO_DETALLADO | `A95` | `(vacía)` | `TRANSFERENCIA COLUMNA–ZAPATA — E.060 15.8` | TRANSFERENCIA COLUMNA–ZAPATA — E.060 15.8 |
| ACERO_DETALLADO | `A97` | `(vacía)` | `Datos básicos interfase` | No presume fc/fy ni continuidad de barras; explícitamente IN SITU. |
| ACERO_DETALLADO | `A98` | `(vacía)` | `Ag columna / A1` | Área bruta de columna rectangular. |
| ACERO_DETALLADO | `A99` | `(vacía)` | `Pu de interfase` | Se conserva signo; no se toma ABS como conversión. |
| ACERO_DETALLADO | `A100` | `(vacía)` | `Phi aplastamiento` | E.060 9.3.2.4; sin aumento opcional sqrt(A2/A1). |
| ACERO_DETALLADO | `A101` | `(vacía)` | `phi Rn zapata` | 10.17.1: factor A2/A1=1 conservador, no geometría inventada. |
| ACERO_DETALLADO | `A102` | `(vacía)` | `phi Rn columna` | 10.17.1: capacidad de ambas superficies. |
| ACERO_DETALLADO | `A103` | `(vacía)` | `Capacidad axial por aplastamiento` | 15.8.1.1: mínimo de ambas superficies. |
| ACERO_DETALLADO | `A104` | `(vacía)` | `Exceso axial compresión` | MAX positivo calcula solo exceso; no cambia signo de Pu. |
| ACERO_DETALLADO | `A105` | `(vacía)` | `As mínimo a través de junta` | E.060 15.8.2.1, columna/pedestal construido en obra. |
| ACERO_DETALLADO | `A106` | `(vacía)` | `As axial compresión requerida` | 15.8.1.2(a) y 9.3.2.2(b); no acredita flexocompresión. |
| ACERO_DETALLADO | `A107` | `(vacía)` | `As axial tracción requerida` | 15.8.1.2(b); magnitud de tracción con Pu firmado visible. |
| ACERO_DETALLADO | `A108` | `(vacía)` | `As mínimo/axial requerido` | No pretende cubrir momentos, cortante ni desarrollo. |
| ACERO_DETALLADO | `A109` | `(vacía)` | `As barras que continúan` | N confirmado que atraviesa la junta, no N total de columna. |
| ACERO_DETALLADO | `A110` | `(vacía)` | `As dowels adicionales` | Cero solo cuando el usuario declara N dowels=0. |
| ACERO_DETALLADO | `A111` | `(vacía)` | `As real a través de junta` | 15.8.2.1: suma de continuas y adicionales confirmadas. |
| ACERO_DETALLADO | `A112` | `(vacía)` | `Estado cantidad de refuerzo` | Control cantidad, independiente del anclaje y la flexocompresión. |
| ACERO_DETALLADO | `A114` | `(vacía)` | `db columna` | Diámetro de barras realmente continuas o adicionales. |
| ACERO_DETALLADO | `A115` | `(vacía)` | `ldc recta requerida` | 12.3.1/2: mínimo20cm, sin factores de reducción por exceso/confinamiento. Se usa menor fc de ambos lados. |
| ACERO_DETALLADO | `A116` | `(vacía)` | `ldc disponible en zapata` | Longitud real recta ingresada desde cara de junta; no cero por falta de datos. |
| ACERO_DETALLADO | `A117` | `(vacía)` | `ldc disponible lado columna` | No acredita empalme 12.17 para fuerzas sísmicas/momentos. |
| ACERO_DETALLADO | `A118` | `(vacía)` | `Máximo geométrico en zapata` | Longitud dentro de altura, compatible con fondo/recubrimiento. |
| ACERO_DETALLADO | `A119` | `(vacía)` | `Estado anclaje columna` | 12.1/12.3 y15.7: el gancho no desarrolla compresión. |
| ACERO_DETALLADO | `A120` | `(vacía)` | `db dowels` | Diámetro de barras realmente continuas o adicionales. |
| ACERO_DETALLADO | `A121` | `(vacía)` | `ldc recta requerida` | 12.3.1/2: mínimo20cm, sin factores de reducción por exceso/confinamiento. Se usa menor fc de ambos lados. |
| ACERO_DETALLADO | `A122` | `(vacía)` | `ldc disponible en zapata` | Longitud real recta ingresada desde cara de junta; no cero por falta de datos. |
| ACERO_DETALLADO | `A123` | `(vacía)` | `ldc disponible lado columna` | No acredita empalme 12.17 para fuerzas sísmicas/momentos. |
| ACERO_DETALLADO | `A124` | `(vacía)` | `Máximo geométrico en zapata` | Longitud dentro de altura, compatible con fondo/recubrimiento. |
| ACERO_DETALLADO | `A125` | `(vacía)` | `Estado anclaje dowels` | 12.1/12.3 y15.7: el gancho no desarrolla compresión. |
| ACERO_DETALLADO | `A126` | `(vacía)` | `Estado desarrollo de interfase` | Anclaje recto a compresión calculado. Tracción/flexocompresión y empalmes12.17 requieren detalle específico. |
| ACERO_DETALLADO | `A128` | `(vacía)` | `H último en junta` | Resultante lateral; no se mezcla con H de servicio. |
| ACERO_DETALLADO | `A129` | `(vacía)` | `Mu de fricción de junta` | 11.7.4.3: NORMAL. No es mu suelo-concreto. |
| ACERO_DETALLADO | `A130` | `(vacía)` | `Avf requerida lateral` | 11.7.4.1/6: fy<=420MPa; no acredita compresión permanente como reducción. |
| ACERO_DETALLADO | `A131` | `(vacía)` | `phi Vn límite de junta` | 11.7.5: límite concreto menor entre 0.2fcAc y5.5MPaAc. |
| ACERO_DETALLADO | `A132` | `(vacía)` | `Estado transferencia lateral` | 11.7.8: Avf dedicada, distribuida y anclada; referencia de plano obligatoria. |
| ACERO_DETALLADO | `A134` | `(vacía)` | `Estado de momentos/axial` | 15.8.1.3/12.17: flexocompresión biaxial, torsión y empalmes no se certifican con reparto axial uniforme. |
| ACERO_DETALLADO | `A135` | `(vacía)` | `Detalle requerido de momentos` | Si momentos/tracción: faltan coordenadas de barras, compatibilidad de deformaciones, interacción P-Mx-My y empalmes 12.17. Acero local horizontal no sustituye conexión vertical. |
| ACERO_DETALLADO | `A136` | `(vacía)` | `Estado conjunto de interfase` | Solo puede CUMPLE para dominio axial implementado con todas las verificaciones aplicables. |
| ACERO_DETALLADO | `A137` | `(vacía)` | `Datos faltantes de conexión` | Consultar asimismo B135 si existe flexocompresión/tracción/torsión. |
| ACERO_DETALLADO | `A140` | `(vacía)` | `RECUBRIMIENTO Y ESPACIAMIENTO — E.060 7.6 / 7.7` | RECUBRIMIENTO Y ESPACIAMIENTO — E.060 7.6 / 7.7 |
| ACERO_DETALLADO | `A142` | `(vacía)` | `Recubrimiento lateral mínimo` | 7.7.1: construido en sitio; fuego/exposición agresiva no se determinan sin información. |
| ACERO_DETALLADO | `A143` | `(vacía)` | `Estado recubrimiento` | 7.7.1: inferior, superior si se requiere y lateral; exposiciones son entradas explícitas. |
| ACERO_DETALLADO | `A144` | `(vacía)` | `Estado separaciones libres` | 7.6.1 y3.3.2: distancia libre paralela >=db,2.5cm,4/3Dmáx; cruces ortogonales no son barras paralelas superpuestas. |
| ACERO_DETALLADO | `A146` | `(vacía)` | `CONTEOS REALES Y ZONAS EXTERIORES — E.060 15.4.4` | CONTEOS REALES Y ZONAS EXTERIORES — E.060 15.4.4 |
| ACERO_DETALLADO | `A148` | `(vacía)` | `Ancho exterior X lado -` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A149` | `(vacía)` | `Ancho exterior X lado +` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A150` | `(vacía)` | `N real exterior X lado -` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A151` | `(vacía)` | `N real exterior X lado +` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A152` | `(vacía)` | `As requerido exterior lado -` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A153` | `(vacía)` | `As requerido exterior lado +` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A154` | `(vacía)` | `As real exterior lado -` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A155` | `(vacía)` | `As real exterior lado +` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A156` | `(vacía)` | `Factibilidad de conteos X` | No acredita un N que no cabe con la separación adoptada; comprueba ambas zonas exteriores. |
| ACERO_DETALLADO | `A160` | `(vacía)` | `Ancho exterior Y lado -` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A161` | `(vacía)` | `Ancho exterior Y lado +` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A162` | `(vacía)` | `N real exterior Y lado -` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A163` | `(vacía)` | `N real exterior Y lado +` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A164` | `(vacía)` | `As requerido exterior lado -` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A165` | `(vacía)` | `As requerido exterior lado +` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A166` | `(vacía)` | `As real exterior lado -` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A167` | `(vacía)` | `As real exterior lado +` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `A168` | `(vacía)` | `Factibilidad de conteos Y` | No acredita un N que no cabe con la separación adoptada; comprueba ambas zonas exteriores. |
| ACERO_DETALLADO | `A171` | `(vacía)` | `Recubrimiento mínimo inferior` | 7.7.1: condición seleccionada; no se optimiza el valor heredado. |
| ACERO_DETALLADO | `A172` | `(vacía)` | `Recubrimiento mínimo superior` | 7.7.1: condición seleccionada; no se optimiza el valor heredado. |
| ACERO_DETALLADO | `A173` | `(vacía)` | `Refuerzo superior requerido` | También considera momento de reacción crítica con columna descentrada, aun sin momento aplicado. |
| ACERO_DETALLADO | `B13` | `=IF(MAX(F5:F8)<=geo_smax,"CUMPLE","NO CUMPLE")` | `=IF(struct_state<>"OK",struct_state,IF(MAX(F5:F8)<=geo_smax,"CUMPLE","NO CUMPLE"))` | No devolver cumplimiento de separación con entradas inválidas. |
| ACERO_DETALLADO | `B21` | `(vacía)` | `=IF(struct_state="OK",MAX(inp_bx,inp_by),"")` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `B22` | `(vacía)` | `=IF(struct_state="OK",MIN(inp_bx,inp_by),"")` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `B23` | `(vacía)` | `=IF(struct_state="OK",B21/B22,"")` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `B24` | `(vacía)` | `=IF(struct_state="OK",2/(B23+1),"")` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `B28` | `(vacía)` | `=IF(geo_input_state="OK",IF(inp_bx>=inp_by,"LARGA / CUADRADA","CORTA"),"")` | Distribuir X sobre Y y viceversa. |
| ACERO_DETALLADO | `B29` | `(vacía)` | `=IF(struct_state="OK",flex_as_req_inf_x*inp_by,"")` | As por metro × ancho perpendicular completo. |
| ACERO_DETALLADO | `B30` | `(vacía)` | `=IF(struct_state="OK",IF(inp_bx>=inp_by,inp_by,steel_B),"")` | Corta: ancho igual lado corto, centrado en eje columna. |
| ACERO_DETALLADO | `B31` | `(vacía)` | `=IF(struct_state="OK",inp_by-B30,"")` | Zonas de ambos lados, suma de anchos. |
| ACERO_DETALLADO | `B32` | `(vacía)` | `=IF(struct_state="OK",IF(inp_bx>=inp_by,B29,steel_gamma*B29),"")` | 15.4.4.2: gamma_s As; larga/cuadrada totalidad uniforme. |
| ACERO_DETALLADO | `B33` | `(vacía)` | `=IF(struct_state="OK",B29-B32,"")` | (1-gamma_s) As, no uniforme central arbitrario. |
| ACERO_DETALLADO | `B34` | `(vacía)` | `=inp_bar_inf_x` | Se mantiene diámetro global; separación regional editable. |
| ACERO_DETALLADO | `B35` | `(vacía)` | `=inp_scx` | Entrada visible, no se cambia para lograr cumplimiento. |
| ACERO_DETALLADO | `B36` | `(vacía)` | `=inp_sox` | Si zona exterior no existe, no aplica. |
| ACERO_DETALLADO | `B37` | `(vacía)` | `=inp_ncx` | Conteo declarado del plano, no estimación continua. |
| ACERO_DETALLADO | `B38` | `(vacía)` | `=inp_nox` | Conteo fuera de franja, cero explícito si no existe. |
| ACERO_DETALLADO | `B39` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_ncx),inp_ncx>=0),inp_ncx*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | Acero real = número × área comercial. |
| ACERO_DETALLADO | `B40` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_nox),inp_nox>=0),inp_nox*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | No usa area equivalente por metro para contar barras. |
| ACERO_DETALLADO | `B41` | `(vacía)` | `=IF(struct_state="OK",B32/B30,"")` | Concentración de la dirección corta. |
| ACERO_DETALLADO | `B42` | `(vacía)` | `=IF(struct_state="OK",IF(B31>0,B33/B31,0),"")` | Cero solo si región inexistente. |
| ACERO_DETALLADO | `B43` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(inp_bx>=inp_by,"OK",IF(ABS(inp_yc)+B30/2<=inp_by/2,"OK","FUERA DEL ALCANCE IMPLEMENTADO")))` | No se recorta una franja centrada normativa que sale de la zapata. |
| ACERO_DETALLADO | `B44` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(B43<>"OK",B43,IF(COUNT(inp_ncx,inp_nox,inp_scx,inp_sox)<>4,"REQUIERE DATOS",IF(NOT(AND(COUNT(inp_ncx,inp_nox,inp_scx,inp_sox)=4,MIN(inp_ncx,inp_nox)>=0,MOD(inp_ncx,1)=0,MOD(inp_nox,1)=0,MIN(inp_scx,inp_sox)>0)),"DATOS INVÁLIDOS",IF(AND(B39>=B32,B40>=B33,inp_scx<=geo_smax,OR(B31=0,inp_sox<=geo_smax),OR(B31>0,inp_nox=0),INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0))*100/inp_scx>=B41,OR(B31=0,INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0))*100/inp_sox>=B42)),zone_x_state,"NO CUMPLE")))))` | 15.4.4: no basta suma de N exterior; verificar lado -/+, recubrimiento y que conteos caben físicamente. |
| ACERO_DETALLADO | `B49` | `(vacía)` | `=IF(geo_input_state="OK",IF(inp_by>=inp_bx,"LARGA / CUADRADA","CORTA"),"")` | Distribuir X sobre Y y viceversa. |
| ACERO_DETALLADO | `B50` | `(vacía)` | `=IF(struct_state="OK",flex_as_req_inf_y*inp_bx,"")` | As por metro × ancho perpendicular completo. |
| ACERO_DETALLADO | `B51` | `(vacía)` | `=IF(struct_state="OK",IF(inp_by>=inp_bx,inp_bx,steel_B),"")` | Corta: ancho igual lado corto, centrado en eje columna. |
| ACERO_DETALLADO | `B52` | `(vacía)` | `=IF(struct_state="OK",inp_bx-B51,"")` | Zonas de ambos lados, suma de anchos. |
| ACERO_DETALLADO | `B53` | `(vacía)` | `=IF(struct_state="OK",IF(inp_by>=inp_bx,B50,steel_gamma*B50),"")` | 15.4.4.2: gamma_s As; larga/cuadrada totalidad uniforme. |
| ACERO_DETALLADO | `B54` | `(vacía)` | `=IF(struct_state="OK",B50-B53,"")` | (1-gamma_s) As, no uniforme central arbitrario. |
| ACERO_DETALLADO | `B55` | `(vacía)` | `=inp_bar_inf_y` | Se mantiene diámetro global; separación regional editable. |
| ACERO_DETALLADO | `B56` | `(vacía)` | `=inp_scy` | Entrada visible, no se cambia para lograr cumplimiento. |
| ACERO_DETALLADO | `B57` | `(vacía)` | `=inp_soy` | Si zona exterior no existe, no aplica. |
| ACERO_DETALLADO | `B58` | `(vacía)` | `=inp_ncy` | Conteo declarado del plano, no estimación continua. |
| ACERO_DETALLADO | `B59` | `(vacía)` | `=inp_noy` | Conteo fuera de franja, cero explícito si no existe. |
| ACERO_DETALLADO | `B60` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_ncy),inp_ncy>=0),inp_ncy*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Acero real = número × área comercial. |
| ACERO_DETALLADO | `B61` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_noy),inp_noy>=0),inp_noy*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | No usa area equivalente por metro para contar barras. |
| ACERO_DETALLADO | `B62` | `(vacía)` | `=IF(struct_state="OK",B53/B51,"")` | Concentración de la dirección corta. |
| ACERO_DETALLADO | `B63` | `(vacía)` | `=IF(struct_state="OK",IF(B52>0,B54/B52,0),"")` | Cero solo si región inexistente. |
| ACERO_DETALLADO | `B64` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(inp_by>=inp_bx,"OK",IF(ABS(inp_xc)+B51/2<=inp_bx/2,"OK","FUERA DEL ALCANCE IMPLEMENTADO")))` | No se recorta una franja centrada normativa que sale de la zapata. |
| ACERO_DETALLADO | `B65` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(B64<>"OK",B64,IF(COUNT(inp_ncy,inp_noy,inp_scy,inp_soy)<>4,"REQUIERE DATOS",IF(NOT(AND(COUNT(inp_ncy,inp_noy,inp_scy,inp_soy)=4,MIN(inp_ncy,inp_noy)>=0,MOD(inp_ncy,1)=0,MOD(inp_noy,1)=0,MIN(inp_scy,inp_soy)>0)),"DATOS INVÁLIDOS",IF(AND(B60>=B53,B61>=B54,inp_scy<=geo_smax,OR(B52=0,inp_soy<=geo_smax),OR(B52>0,inp_noy=0),INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0))*100/inp_scy>=B62,OR(B52=0,INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0))*100/inp_soy>=B63)),zone_y_state,"NO CUMPLE")))))` | 15.4.4: no basta suma de N exterior; verificar lado -/+, recubrimiento y que conteos caben físicamente. |
| ACERO_DETALLADO | `B72` | `(vacía)` | `db cm` | 12.2.3: Ktr=0; sin reducción por acero en exceso. |
| ACERO_DETALLADO | `B73` | `(vacía)` | `=IF(struct_state="OK",INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | Diámetro cm del catálogo, no convertir área en diámetro. |
| ACERO_DETALLADO | `B74` | `(vacía)` | `=IF(struct_state="OK",INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Diámetro cm del catálogo, no convertir área en diámetro. |
| ACERO_DETALLADO | `B75` | `(vacía)` | `=IF(struct_state="OK",INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | Diámetro cm del catálogo, no convertir área en diámetro. |
| ACERO_DETALLADO | `B76` | `(vacía)` | `=IF(struct_state="OK",INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | Diámetro cm del catálogo, no convertir área en diámetro. |
| ACERO_DETALLADO | `B78` | `(vacía)` | `=IF(COUNTIF(J73:J76,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(J73:J76,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(J73:J76,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(J73:J76,"REQUIERE DATOS")>0,"REQUIERE DATOS",IF(COUNTIF(J73:J76,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL","CUMPLE")))))` | Secciones de cambios de sección/refuerzo no modeladas; barras rectas continuas. |
| ACERO_DETALLADO | `B79` | `(vacía)` | `Ktr=0; rectas continuas` | 12.2.3 permite Ktr=0. Sin reducción por exceso. Ganchos/paquetes/cortes/empalmes requieren detalle especial. |
| ACERO_DETALLADO | `B85` | `(vacía)` | `gamma_f Mu tf m` | Franja efectiva real; no se acredita por As global por metro. |
| ACERO_DETALLADO | `B86` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B48,"")` | γfM crítico firmado de Fase1, auditado; barX↔My, barY↔Mx. |
| ACERO_DETALLADO | `B87:B88` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B47,"")` | γfM crítico firmado de Fase1, auditado; barX↔My, barY↔Mx. |
| ACERO_DETALLADO | `B89` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B47,"")` | γfM crítico firmado de Fase1, auditado; barX↔My, barY↔Mx. |
| ACERO_DETALLADO | `B91` | `(vacía)` | `=IF(punz_state<>"OK",punz_state,IF(COUNTIF(J86:J89,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(J86:J89,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(J86:J89,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(J86:J89,"REQUIERE DATOS")>0,"REQUIERE DATOS",IF(COUNTIF(J86:J89,"NO APLICA")=4,"NO APLICA","CUMPLE"))))))` | No permite convertir advertencia F1 en CUMPLE sin conteo y desarrollo comprobados. |
| ACERO_DETALLADO | `B92` | `(vacía)` | `INTERIOR / RECTA / 2 CAPAS` | Ambas capas resisten conservadoramente la magnitud local más demanda global; sin reparto único entre signos. |
| ACERO_DETALLADO | `B93` | `(vacía)` | `=IF(local_state="REQUIERE DATOS",IF(inp_local_detail="SI","","inp_local_detail=SI; ")&IF(LEN(inp_rec_lat)=0,"inp_rec_lat; ","")&IF(LEN(inp_epoxy)=0,"inp_epoxy; ","")&IF(LEN(inp_side_exposure)=0,"inp_side_exposure; ","")&IF(LEN(inp_end_inf)=0,"inp_end_inf; ","")&IF(LEN(inp_end_sup)=0,"inp_end_sup; ","")&IF(LEN(inp_agg)=0,"inp_agg; ","")&IF(LEN(inp_ncx)=0,"inp_ncx; ","")&IF(LEN(inp_nox)=0,"inp_nox; ","")&IF(LEN(inp_ncy)=0,"inp_ncy; ","")&IF(LEN(inp_noy)=0,"inp_noy; ","")&IF(LEN(inp_nloc_ix)=0,"inp_nloc_ix; ","")&IF(LEN(inp_nloc_iy)=0,"inp_nloc_iy; ","")&IF(LEN(inp_nloc_sx)=0,"inp_nloc_sx; ","")&IF(LEN(inp_nloc_sy)=0,"inp_nloc_sy; ","")&IF(LEN(inp_ll_ix_m)=0,"inp_ll_ix_m; ","")&IF(LEN(inp_ll_ix_p)=0,"inp_ll_ix_p; ","")&IF(LEN(inp_ll_iy_m)=0,"inp_ll_iy_m; ","")&IF(LEN(inp_ll_iy_p)=0,"inp_ll_iy_p; ","")&IF(LEN(inp_ll_sx_m)=0,"inp_ll_sx_m; ","")&IF(LEN(inp_ll_sx_p)=0,"inp_ll_sx_p; ","")&IF(LEN(inp_ll_sy_m)=0,"inp_ll_sy_m; ","")&IF(LEN(inp_ll_sy_p)=0,"inp_ll_sy_p; ",""),local_state)` | Lista de datos locales de detalle no declarados; no se inventan conteos/anclajes. |
| ACERO_DETALLADO | `B97` | `(vacía)` | `=IF(geo_input_state<>"OK","DATOS INVÁLIDOS",IF(inp_col_system<>"IN SITU","FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNT(inp_fc_col,inp_fy_col,inp_n_col,inp_n_continue,inp_n_dowel)<>5,"REQUIERE DATOS",IF(OR(MIN(inp_fc_col,inp_fy_col)<=0,MIN(inp_n_col,inp_n_continue,inp_n_dowel)<0,inp_n_continue>inp_n_col,MOD(inp_n_col,1)<>0,MOD(inp_n_continue,1)<>0,MOD(inp_n_dowel,1)<>0),"DATOS INVÁLIDOS",IF(COUNTIF(bar_codes,inp_bar_col)<>1,"REQUIERE DATOS",IF(AND(inp_n_dowel>0,COUNTIF(bar_codes,inp_bar_dowel)<>1),"REQUIERE DATOS","OK"))))))` | No presume fc/fy ni continuidad de barras; explícitamente IN SITU. |
| ACERO_DETALLADO | `B98` | `(vacía)` | `=IF(geo_input_state="OK",inp_cx*inp_cy*10000,"")` | Área bruta de columna rectangular. |
| ACERO_DETALLADO | `B99` | `(vacía)` | `=ult_p` | Se conserva signo; no se toma ABS como conversión. |
| ACERO_DETALLADO | `B100` | `(vacía)` | `0.7` | E.060 9.3.2.4; sin aumento opcional sqrt(A2/A1). |
| ACERO_DETALLADO | `B101` | `(vacía)` | `=IF(iface_data_state="OK",phi_bearing*0.85*inp_fc*iface_Ag/1000,"")` | 10.17.1: factor A2/A1=1 conservador, no geometría inventada. |
| ACERO_DETALLADO | `B102` | `(vacía)` | `=IF(iface_data_state="OK",phi_bearing*0.85*inp_fc_col*iface_Ag/1000,"")` | 10.17.1: capacidad de ambas superficies. |
| ACERO_DETALLADO | `B103` | `(vacía)` | `=IF(iface_data_state="OK",MIN(bearing_foot,bearing_col),"")` | 15.8.1.1: mínimo de ambas superficies. |
| ACERO_DETALLADO | `B104` | `(vacía)` | `=IF(AND(iface_data_state="OK",ult_input_state="OK"),MAX(0,ult_p-bearing_min),"")` | MAX positivo calcula solo exceso; no cambia signo de Pu. |
| ACERO_DETALLADO | `B105` | `(vacía)` | `=IF(geo_input_state="OK",0.005*iface_Ag,"")` | E.060 15.8.2.1, columna/pedestal construido en obra. |
| ACERO_DETALLADO | `B106` | `(vacía)` | `=IF(AND(iface_data_state="OK",ult_input_state="OK"),bearing_excess*1000/(0.7*inp_fy_col),"")` | 15.8.1.2(a) y 9.3.2.2(b); no acredita flexocompresión. |
| ACERO_DETALLADO | `B107` | `(vacía)` | `=IF(AND(iface_data_state="OK",ult_input_state="OK"),MAX(0,-ult_p)*1000/(0.9*inp_fy_col),"")` | 15.8.1.2(b); magnitud de tracción con Pu firmado visible. |
| ACERO_DETALLADO | `B108` | `(vacía)` | `=IF(AND(iface_data_state="OK",ult_input_state="OK"),MAX(iface_Asmin,iface_Ascomp,iface_Astens),"")` | No pretende cubrir momentos, cortante ni desarrollo. |
| ACERO_DETALLADO | `B109` | `(vacía)` | `=IF(iface_data_state="OK",inp_n_continue*INDEX(bar_area_cm2,MATCH(inp_bar_col,bar_codes,0)),"")` | N confirmado que atraviesa la junta, no N total de columna. |
| ACERO_DETALLADO | `B110` | `(vacía)` | `=IF(iface_data_state="OK",IF(inp_n_dowel=0,0,inp_n_dowel*INDEX(bar_area_cm2,MATCH(inp_bar_dowel,bar_codes,0))),"")` | Cero solo cuando el usuario declara N dowels=0. |
| ACERO_DETALLADO | `B111` | `(vacía)` | `=IF(iface_data_state="OK",iface_Ascont+iface_Asdow,"")` | 15.8.2.1: suma de continuas y adicionales confirmadas. |
| ACERO_DETALLADO | `B112` | `(vacía)` | `=IF(iface_data_state<>"OK",iface_data_state,IF(ult_input_state<>"OK",ult_input_state,IF(iface_Asreal>=iface_Asreq,"CUMPLE","NO CUMPLE")))` | Control cantidad, independiente del anclaje y la flexocompresión. |
| ACERO_DETALLADO | `B114` | `(vacía)` | `=IF(iface_data_state="OK",IF(inp_n_continue=0,0,INDEX(bar_diam_cm,MATCH(inp_bar_col,bar_codes,0))),"")` | Diámetro de barras realmente continuas o adicionales. |
| ACERO_DETALLADO | `B115` | `(vacía)` | `=IF(iface_data_state="OK",IF(inp_n_continue=0,0,MAX(20,0.24*(inp_fy_col*0.0980665)/MIN(SQRT(MIN(inp_fc,inp_fc_col)*0.0980665),8.3)*B114,0.043*(inp_fy_col*0.0980665)*B114)),"")` | 12.3.1/2: mínimo20cm, sin factores de reducción por exceso/confinamiento. Se usa menor fc de ambos lados. |
| ACERO_DETALLADO | `B116` | `(vacía)` | `=IF(LEN(inp_lcol_foot)=0,"",inp_lcol_foot)` | Longitud real recta ingresada desde cara de junta; no cero por falta de datos. |
| ACERO_DETALLADO | `B117` | `(vacía)` | `=IF(LEN(inp_lcol_above)=0,"",inp_lcol_above)` | No acredita empalme 12.17 para fuerzas sísmicas/momentos. |
| ACERO_DETALLADO | `B118` | `(vacía)` | `=IF(iface_data_state="OK",inp_h*100-inp_rec_inf-B114/2,"")` | Longitud dentro de altura, compatible con fondo/recubrimiento. |
| ACERO_DETALLADO | `B119` | `(vacía)` | `=IF(iface_data_state<>"OK",iface_data_state,IF(inp_n_continue=0,"NO APLICA",IF(OR(COUNT(inp_lcol_foot,inp_lcol_above)<>2,LEN(inp_end_col)=0),"REQUIERE DATOS",IF(inp_end_col<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(MIN(inp_lcol_foot,inp_lcol_above)<0,"DATOS INVÁLIDOS",IF(AND(inp_lcol_foot>=B115,inp_lcol_above>=B115,inp_lcol_foot<=B118),"CUMPLE","NO CUMPLE"))))))` | 12.1/12.3 y15.7: el gancho no desarrolla compresión. |
| ACERO_DETALLADO | `B120` | `(vacía)` | `=IF(iface_data_state="OK",IF(inp_n_dowel=0,0,INDEX(bar_diam_cm,MATCH(inp_bar_dowel,bar_codes,0))),"")` | Diámetro de barras realmente continuas o adicionales. |
| ACERO_DETALLADO | `B121` | `(vacía)` | `=IF(iface_data_state="OK",IF(inp_n_dowel=0,0,MAX(20,0.24*(inp_fy_col*0.0980665)/MIN(SQRT(MIN(inp_fc,inp_fc_col)*0.0980665),8.3)*B120,0.043*(inp_fy_col*0.0980665)*B120)),"")` | 12.3.1/2: mínimo20cm, sin factores de reducción por exceso/confinamiento. Se usa menor fc de ambos lados. |
| ACERO_DETALLADO | `B122` | `(vacía)` | `=IF(LEN(inp_ldow_foot)=0,"",inp_ldow_foot)` | Longitud real recta ingresada desde cara de junta; no cero por falta de datos. |
| ACERO_DETALLADO | `B123` | `(vacía)` | `=IF(LEN(inp_ldow_above)=0,"",inp_ldow_above)` | No acredita empalme 12.17 para fuerzas sísmicas/momentos. |
| ACERO_DETALLADO | `B124` | `(vacía)` | `=IF(iface_data_state="OK",inp_h*100-inp_rec_inf-B120/2,"")` | Longitud dentro de altura, compatible con fondo/recubrimiento. |
| ACERO_DETALLADO | `B125` | `(vacía)` | `=IF(iface_data_state<>"OK",iface_data_state,IF(inp_n_dowel=0,"NO APLICA",IF(OR(COUNT(inp_ldow_foot,inp_ldow_above)<>2,LEN(inp_end_col)=0),"REQUIERE DATOS",IF(inp_end_col<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(MIN(inp_ldow_foot,inp_ldow_above)<0,"DATOS INVÁLIDOS",IF(AND(inp_ldow_foot>=B121,inp_ldow_above>=B121,inp_ldow_foot<=B124),"CUMPLE","NO CUMPLE"))))))` | 12.1/12.3 y15.7: el gancho no desarrolla compresión. |
| ACERO_DETALLADO | `B126` | `(vacía)` | `=IF(iface_data_state<>"OK",iface_data_state,IF(ult_input_state<>"OK",ult_input_state,IF(COUNTIF(B119:B125,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(OR(ult_p<0,MAX(ABS(ult_mx),ABS(ult_my))>0.000001),"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(B119:B125,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(B119:B125,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(B119:B125,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))))` | Anclaje recto a compresión calculado. Tracción/flexocompresión y empalmes12.17 requieren detalle específico. |
| ACERO_DETALLADO | `B128` | `(vacía)` | `=IF(ult_input_state="OK",SQRT(ult_fx^2+ult_fy^2),"")` | Resultante lateral; no se mezcla con H de servicio. |
| ACERO_DETALLADO | `B129` | `(vacía)` | `=IF(inp_joint="MONOLITICA",1.4,IF(inp_joint="RUGOSA",1,IF(inp_joint="LISA",0.6,"")))` | 11.7.4.3: NORMAL. No es mu suelo-concreto. |
| ACERO_DETALLADO | `B130` | `(vacía)` | `=IF(AND(iface_data_state="OK",ult_input_state="OK",ISNUMBER(iface_mu),iface_mu>0),iface_H*1000/(0.85*iface_mu*MIN(inp_fy_col,420/0.0980665)),"")` | 11.7.4.1/6: fy<=420MPa; no acredita compresión permanente como reducción. |
| ACERO_DETALLADO | `B131` | `(vacía)` | `=IF(iface_data_state="OK",0.85*MIN(0.2*MIN(inp_fc,inp_fc_col),5.5/0.0980665)*iface_Ag/1000,"")` | 11.7.5: límite concreto menor entre 0.2fcAc y5.5MPaAc. |
| ACERO_DETALLADO | `B132` | `(vacía)` | `=IF(ult_input_state<>"OK",ult_input_state,IF(iface_H<=0.000000001,"NO APLICA",IF(iface_data_state<>"OK",iface_data_state,IF(OR(COUNT(inp_avf)<>1,NOT(ISNUMBER(iface_mu)),LEN(inp_avf_anchor)=0,LEN(inp_joint_ref)=0),"REQUIERE DATOS",IF(inp_avf<0,"DATOS INVÁLIDOS",IF(AND(inp_avf>=iface_Avf_req,iface_H<=iface_Vlimit,inp_avf_anchor="SI"),"CUMPLE","NO CUMPLE"))))))` | 11.7.8: Avf dedicada, distribuida y anclada; referencia de plano obligatoria. |
| ACERO_DETALLADO | `B134` | `(vacía)` | `=IF(ult_input_state<>"OK",ult_input_state,IF(MAX(ABS(ult_mx),ABS(ult_my),ABS(ult_mz))>0.000001,"REQUIERE ANÁLISIS ESPECIAL",IF(ult_p<0,"REQUIERE ANÁLISIS ESPECIAL","CUMPLE")))` | 15.8.1.3/12.17: flexocompresión biaxial, torsión y empalmes no se certifican con reparto axial uniforme. |
| ACERO_DETALLADO | `B135` | `(vacía)` | `P-Mx-My / empalmes: análisis especial` | Si momentos/tracción: faltan coordenadas de barras, compatibilidad de deformaciones, interacción P-Mx-My y empalmes 12.17. Acero local horizontal no sustituye conexión vertical. |
| ACERO_DETALLADO | `B136` | `(vacía)` | `=IF(iface_data_state<>"OK",iface_data_state,IF(OR(iface_Asstate="DATOS INVÁLIDOS",iface_anchor_state="DATOS INVÁLIDOS",iface_lateral_state="DATOS INVÁLIDOS"),"DATOS INVÁLIDOS",IF(OR(iface_Asstate="NO CUMPLE",iface_anchor_state="NO CUMPLE",iface_lateral_state="NO CUMPLE"),"NO CUMPLE",IF(OR(iface_anchor_state="FUERA DEL ALCANCE IMPLEMENTADO",iface_lateral_state="FUERA DEL ALCANCE IMPLEMENTADO"),"FUERA DEL ALCANCE IMPLEMENTADO",IF(iface_moment_state<>"CUMPLE",iface_moment_state,IF(OR(iface_Asstate="REQUIERE DATOS",iface_anchor_state="REQUIERE DATOS",iface_lateral_state="REQUIERE DATOS"),"REQUIERE DATOS","CUMPLE"))))))` | Solo puede CUMPLE para dominio axial implementado con todas las verificaciones aplicables. |
| ACERO_DETALLADO | `B137` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(iface_state="REQUIERE DATOS",IF(LEN(inp_fc_col)=0,"inp_fc_col; ","")&IF(LEN(inp_fy_col)=0,"inp_fy_col; ","")&IF(LEN(inp_bar_col)=0,"inp_bar_col; ","")&IF(LEN(inp_n_col)=0,"inp_n_col; ","")&IF(LEN(inp_n_continue)=0,"inp_n_continue; ","")&IF(LEN(inp_n_dowel)=0,"inp_n_dowel; ","")&IF(LEN(inp_lcol_foot)=0,"inp_lcol_foot; ","")&IF(LEN(inp_lcol_above)=0,"inp_lcol_above; ","")&IF(LEN(inp_end_col)=0,"inp_end_col; ","")&IF(LEN(inp_joint)=0,"inp_joint; ","")&IF(AND(ISNUMBER(inp_n_dowel),inp_n_dowel>0,LEN(inp_bar_dowel)=0),"inp_bar_dowel; ","")&IF(AND(ISNUMBER(inp_n_dowel),inp_n_dowel>0,LEN(inp_ldow_foot)=0),"inp_ldow_foot; ","")&IF(AND(ISNUMBER(inp_n_dowel),inp_n_dowel>0,LEN(inp_ldow_above)=0),"inp_ldow_above; ","")&IF(AND(OR(ult_fx<>0,ult_fy<>0),LEN(inp_avf)=0),"inp_avf; ","")&IF(AND(OR(ult_fx<>0,ult_fy<>0),LEN(inp_avf_anchor)=0),"inp_avf_anchor; ","")&IF(AND(OR(ult_fx<>0,ult_fy<>0),LEN(inp_joint_ref)=0),"inp_joint_ref; ",""),iface_state))` | Lista explícita de entradas no declaradas, no verificación ficticia de conexión. |
| ACERO_DETALLADO | `B142` | `(vacía)` | `=IF(geo_input_state="OK",IF(inp_side_exposure="CONTRA SUELO",7,IF(inp_side_exposure="CONTACTO SUELO",IF(MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)))>=1.905,5,4),IF(inp_side_exposure="INTERIOR",2,""))),"")` | 7.7.1: construido en sitio; fuego/exposición agresiva no se determinan sin información. |
| ACERO_DETALLADO | `B143` | `(vacía)` | `=IF(geo_input_state<>"OK","DATOS INVÁLIDOS",IF(OR(COUNT(inp_rec_lat)<>1,LEN(inp_side_exposure)=0,LEN(inp_bottom_exposure)=0,AND(top_rebar_needed,LEN(inp_top_exposure)=0)),"REQUIERE DATOS",IF(OR(COUNT(cover_min_lat,cover_min_bottom)<>2,AND(top_rebar_needed,COUNT(cover_min_top)<>1)),"DATOS INVÁLIDOS",IF(AND(inp_rec_lat>=cover_min_lat,inp_rec_inf>=cover_min_bottom,IF(top_rebar_needed,inp_rec_sup>=cover_min_top,TRUE)),"CUMPLE","NO CUMPLE"))))` | 7.7.1: inferior, superior si se requiere y lateral; exposiciones son entradas explícitas. |
| ACERO_DETALLADO | `B144` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(COUNT(inp_agg)<>1,"REQUIERE DATOS",IF(inp_agg<=0,"DATOS INVÁLIDOS",IF(AND(MIN(inp_sep_inf_x,inp_scx,inp_sox)-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))>=MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),2.5,4*inp_agg/3),MIN(inp_sep_inf_y,inp_scy,inp_soy)-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))>=MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)),2.5,4*inp_agg/3)),"CUMPLE","NO CUMPLE"))))` | 7.6.1 y3.3.2: distancia libre paralela >=db,2.5cm,4/3Dmáx; cruces ortogonales no son barras paralelas superpuestas. |
| ACERO_DETALLADO | `B148` | `(vacía)` | `=IF(struct_state="OK",IF(inp_bx>=inp_by,0,inp_by/2+inp_yc-B30/2),"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B149` | `(vacía)` | `=IF(struct_state="OK",IF(inp_bx>=inp_by,0,inp_by/2-inp_yc-B30/2),"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B150` | `(vacía)` | `=IF(ISNUMBER(inp_nox_minus),inp_nox_minus,"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B151` | `(vacía)` | `=IF(ISNUMBER(inp_nox_plus),inp_nox_plus,"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B152` | `(vacía)` | `=IF(struct_state="OK",B42*B148,"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B153` | `(vacía)` | `=IF(struct_state="OK",B42*B149,"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B154` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_nox_minus)),inp_nox_minus*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B155` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_nox_plus)),inp_nox_plus*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B156` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(B43<>"OK",B43,IF(COUNT(inp_ncx,inp_scx,inp_rec_lat)<>3,"REQUIERE DATOS",IF(NOT(AND(inp_ncx>=1,(inp_ncx-1)*inp_scx<=B30*100-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))-IF(inp_bx>=inp_by,2*inp_rec_lat,0))),"NO CUMPLE",IF(B31=0,"CUMPLE",IF(COUNT(inp_nox_minus,inp_nox_plus,inp_nox,inp_sox)<>4,"REQUIERE DATOS",IF(AND(inp_nox=inp_nox_minus+inp_nox_plus,B154>=B152,B155>=B153,OR(inp_nox_minus=0,(inp_nox_minus-1)*inp_sox<=B148*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))/2),OR(inp_nox_plus=0,(inp_nox_plus-1)*inp_sox<=B149*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))/2)),"CUMPLE","NO CUMPLE")))))))` | No acredita un N que no cabe con la separación adoptada; comprueba ambas zonas exteriores. |
| ACERO_DETALLADO | `B160` | `(vacía)` | `=IF(struct_state="OK",IF(inp_by>=inp_bx,0,inp_bx/2+inp_xc-B51/2),"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B161` | `(vacía)` | `=IF(struct_state="OK",IF(inp_by>=inp_bx,0,inp_bx/2-inp_xc-B51/2),"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B162` | `(vacía)` | `=IF(ISNUMBER(inp_noy_minus),inp_noy_minus,"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B163` | `(vacía)` | `=IF(ISNUMBER(inp_noy_plus),inp_noy_plus,"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B164` | `(vacía)` | `=IF(struct_state="OK",B63*B160,"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B165` | `(vacía)` | `=IF(struct_state="OK",B63*B161,"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B166` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_noy_minus)),inp_noy_minus*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B167` | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(inp_noy_plus)),inp_noy_plus*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `B168` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(B64<>"OK",B64,IF(COUNT(inp_ncy,inp_scy,inp_rec_lat)<>3,"REQUIERE DATOS",IF(NOT(AND(inp_ncy>=1,(inp_ncy-1)*inp_scy<=B51*100-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))-IF(inp_by>=inp_bx,2*inp_rec_lat,0))),"NO CUMPLE",IF(B52=0,"CUMPLE",IF(COUNT(inp_noy_minus,inp_noy_plus,inp_noy,inp_soy)<>4,"REQUIERE DATOS",IF(AND(inp_noy=inp_noy_minus+inp_noy_plus,B166>=B164,B167>=B165,OR(inp_noy_minus=0,(inp_noy_minus-1)*inp_soy<=B160*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))/2),OR(inp_noy_plus=0,(inp_noy_plus-1)*inp_soy<=B161*100-inp_rec_lat-INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))/2)),"CUMPLE","NO CUMPLE")))))))` | No acredita un N que no cabe con la separación adoptada; comprueba ambas zonas exteriores. |
| ACERO_DETALLADO | `B171` | `(vacía)` | `=IF(geo_input_state="OK",IF(inp_bottom_exposure="CONTRA SUELO",7,IF(inp_bottom_exposure="CONTACTO SUELO",IF(MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)))>=1.905,5,4),IF(inp_bottom_exposure="INTERIOR",2,""))),"")` | 7.7.1: condición seleccionada; no se optimiza el valor heredado. |
| ACERO_DETALLADO | `B172` | `(vacía)` | `=IF(geo_input_state="OK",IF(inp_top_exposure="CONTRA SUELO",7,IF(inp_top_exposure="CONTACTO SUELO",IF(MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0)),INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0)))>=1.905,5,4),IF(inp_top_exposure="INTERIOR",2,""))),"")` | 7.7.1: condición seleccionada; no se optimiza el valor heredado. |
| ACERO_DETALLADO | `B173` | `(vacía)` | `=IF(struct_state="OK",OR(MAX(FLEXION_ACERO!D7:D8)>0,MAX(ABS(ult_mx),ABS(ult_my))>0.000001,IF(punz_state="OK",MAX(ABS(PUNZONAMIENTO!B47),ABS(PUNZONAMIENTO!B48))>0.000001,FALSE)),FALSE)` | También considera momento de reacción crítica con columna descentrada, aun sin momento aplicado. |
| ACERO_DETALLADO | `C21:C22` | `(vacía)` | `m` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `C23:C24` | `(vacía)` | `-` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `C28` | `(vacía)` | `-` | Distribuir X sobre Y y viceversa. |
| ACERO_DETALLADO | `C29` | `(vacía)` | `cm2` | As por metro × ancho perpendicular completo. |
| ACERO_DETALLADO | `C30` | `(vacía)` | `m` | Corta: ancho igual lado corto, centrado en eje columna. |
| ACERO_DETALLADO | `C31` | `(vacía)` | `m` | Zonas de ambos lados, suma de anchos. |
| ACERO_DETALLADO | `C32` | `(vacía)` | `cm2` | 15.4.4.2: gamma_s As; larga/cuadrada totalidad uniforme. |
| ACERO_DETALLADO | `C33` | `(vacía)` | `cm2` | (1-gamma_s) As, no uniforme central arbitrario. |
| ACERO_DETALLADO | `C34` | `(vacía)` | `-` | Se mantiene diámetro global; separación regional editable. |
| ACERO_DETALLADO | `C35` | `(vacía)` | `cm` | Entrada visible, no se cambia para lograr cumplimiento. |
| ACERO_DETALLADO | `C36` | `(vacía)` | `cm` | Si zona exterior no existe, no aplica. |
| ACERO_DETALLADO | `C37` | `(vacía)` | `barras` | Conteo declarado del plano, no estimación continua. |
| ACERO_DETALLADO | `C38` | `(vacía)` | `barras` | Conteo fuera de franja, cero explícito si no existe. |
| ACERO_DETALLADO | `C39` | `(vacía)` | `cm2` | Acero real = número × área comercial. |
| ACERO_DETALLADO | `C40` | `(vacía)` | `cm2` | No usa area equivalente por metro para contar barras. |
| ACERO_DETALLADO | `C41` | `(vacía)` | `cm2/m` | Concentración de la dirección corta. |
| ACERO_DETALLADO | `C42` | `(vacía)` | `cm2/m` | Cero solo si región inexistente. |
| ACERO_DETALLADO | `C43` | `(vacía)` | `-` | No se recorta una franja centrada normativa que sale de la zapata. |
| ACERO_DETALLADO | `C44` | `(vacía)` | `-` | Combina cantidad real y separación/densidad, manteniendo mínimo; 15.4.4. |
| ACERO_DETALLADO | `C49` | `(vacía)` | `-` | Distribuir X sobre Y y viceversa. |
| ACERO_DETALLADO | `C50` | `(vacía)` | `cm2` | As por metro × ancho perpendicular completo. |
| ACERO_DETALLADO | `C51` | `(vacía)` | `m` | Corta: ancho igual lado corto, centrado en eje columna. |
| ACERO_DETALLADO | `C52` | `(vacía)` | `m` | Zonas de ambos lados, suma de anchos. |
| ACERO_DETALLADO | `C53` | `(vacía)` | `cm2` | 15.4.4.2: gamma_s As; larga/cuadrada totalidad uniforme. |
| ACERO_DETALLADO | `C54` | `(vacía)` | `cm2` | (1-gamma_s) As, no uniforme central arbitrario. |
| ACERO_DETALLADO | `C55` | `(vacía)` | `-` | Se mantiene diámetro global; separación regional editable. |
| ACERO_DETALLADO | `C56` | `(vacía)` | `cm` | Entrada visible, no se cambia para lograr cumplimiento. |
| ACERO_DETALLADO | `C57` | `(vacía)` | `cm` | Si zona exterior no existe, no aplica. |
| ACERO_DETALLADO | `C58` | `(vacía)` | `barras` | Conteo declarado del plano, no estimación continua. |
| ACERO_DETALLADO | `C59` | `(vacía)` | `barras` | Conteo fuera de franja, cero explícito si no existe. |
| ACERO_DETALLADO | `C60` | `(vacía)` | `cm2` | Acero real = número × área comercial. |
| ACERO_DETALLADO | `C61` | `(vacía)` | `cm2` | No usa area equivalente por metro para contar barras. |
| ACERO_DETALLADO | `C62` | `(vacía)` | `cm2/m` | Concentración de la dirección corta. |
| ACERO_DETALLADO | `C63` | `(vacía)` | `cm2/m` | Cero solo si región inexistente. |
| ACERO_DETALLADO | `C64` | `(vacía)` | `-` | No se recorta una franja centrada normativa que sale de la zapata. |
| ACERO_DETALLADO | `C65` | `(vacía)` | `-` | Combina cantidad real y separación/densidad, manteniendo mínimo; 15.4.4. |
| ACERO_DETALLADO | `C72` | `(vacía)` | `psi_t` | 12.2.3: Ktr=0; sin reducción por acero en exceso. |
| ACERO_DETALLADO | `C73` | `(vacía)` | `=IF(struct_state="OK",IF(IF(inp_order_inf="X inferior / Y superior",inp_rec_inf+B73/2,inp_rec_inf+INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))+B73/2)>=30,1.3,1),"")` | Tabla12.2: superior por >=30cm concreto fresco debajo, no por nombre de parrilla. |
| ACERO_DETALLADO | `C74` | `(vacía)` | `=IF(struct_state="OK",IF(IF(inp_order_inf="Y inferior / X superior",inp_rec_inf+B74/2,inp_rec_inf+INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))+B74/2)>=30,1.3,1),"")` | Tabla12.2: superior por >=30cm concreto fresco debajo, no por nombre de parrilla. |
| ACERO_DETALLADO | `C75:C76` | `(vacía)` | `=IF(struct_state="OK",IF(FLEXION_ACERO!E7>=30,1.3,1),"")` | Tabla12.2: superior por >=30cm concreto fresco debajo, no por nombre de parrilla. |
| ACERO_DETALLADO | `C78` | `(vacía)` | `-` | Secciones de cambios de sección/refuerzo no modeladas; barras rectas continuas. |
| ACERO_DETALLADO | `C79` | `(vacía)` | `-` | 12.2.3 permite Ktr=0. Sin reducción por exceso. Ganchos/paquetes/cortes/empalmes requieren detalle especial. |
| ACERO_DETALLADO | `C85` | `(vacía)` | `Ancho cm` | Franja efectiva real; no se acredita por As global por metro. |
| ACERO_DETALLADO | `C86` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B56*100,"")` | Ancho efectivo 13.5.3.1; limitado a zapata y centro columna. |
| ACERO_DETALLADO | `C87:C88` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B55*100,"")` | Ancho efectivo 13.5.3.1; limitado a zapata y centro columna. |
| ACERO_DETALLADO | `C89` | `(vacía)` | `=IF(punz_state="OK",PUNZONAMIENTO!B55*100,"")` | Ancho efectivo 13.5.3.1; limitado a zapata y centro columna. |
| ACERO_DETALLADO | `C91` | `(vacía)` | `-` | No permite convertir advertencia F1 en CUMPLE sin conteo y desarrollo comprobados. |
| ACERO_DETALLADO | `C92` | `(vacía)` | `-` | Ambas capas resisten conservadoramente la magnitud local más demanda global; sin reparto único entre signos. |
| ACERO_DETALLADO | `C97` | `(vacía)` | `-` | No presume fc/fy ni continuidad de barras; explícitamente IN SITU. |
| ACERO_DETALLADO | `C98` | `(vacía)` | `cm2` | Área bruta de columna rectangular. |
| ACERO_DETALLADO | `C99` | `(vacía)` | `tf` | Se conserva signo; no se toma ABS como conversión. |
| ACERO_DETALLADO | `C100` | `(vacía)` | `-` | E.060 9.3.2.4; sin aumento opcional sqrt(A2/A1). |
| ACERO_DETALLADO | `C101` | `(vacía)` | `tf` | 10.17.1: factor A2/A1=1 conservador, no geometría inventada. |
| ACERO_DETALLADO | `C102` | `(vacía)` | `tf` | 10.17.1: capacidad de ambas superficies. |
| ACERO_DETALLADO | `C103` | `(vacía)` | `tf` | 15.8.1.1: mínimo de ambas superficies. |
| ACERO_DETALLADO | `C104` | `(vacía)` | `tf` | MAX positivo calcula solo exceso; no cambia signo de Pu. |
| ACERO_DETALLADO | `C105` | `(vacía)` | `cm2` | E.060 15.8.2.1, columna/pedestal construido en obra. |
| ACERO_DETALLADO | `C106` | `(vacía)` | `cm2` | 15.8.1.2(a) y 9.3.2.2(b); no acredita flexocompresión. |
| ACERO_DETALLADO | `C107` | `(vacía)` | `cm2` | 15.8.1.2(b); magnitud de tracción con Pu firmado visible. |
| ACERO_DETALLADO | `C108` | `(vacía)` | `cm2` | No pretende cubrir momentos, cortante ni desarrollo. |
| ACERO_DETALLADO | `C109` | `(vacía)` | `cm2` | N confirmado que atraviesa la junta, no N total de columna. |
| ACERO_DETALLADO | `C110` | `(vacía)` | `cm2` | Cero solo cuando el usuario declara N dowels=0. |
| ACERO_DETALLADO | `C111` | `(vacía)` | `cm2` | 15.8.2.1: suma de continuas y adicionales confirmadas. |
| ACERO_DETALLADO | `C112` | `(vacía)` | `-` | Control cantidad, independiente del anclaje y la flexocompresión. |
| ACERO_DETALLADO | `C114` | `(vacía)` | `cm` | Diámetro de barras realmente continuas o adicionales. |
| ACERO_DETALLADO | `C115` | `(vacía)` | `cm` | 12.3.1/2: mínimo20cm, sin factores de reducción por exceso/confinamiento. Se usa menor fc de ambos lados. |
| ACERO_DETALLADO | `C116` | `(vacía)` | `cm` | Longitud real recta ingresada desde cara de junta; no cero por falta de datos. |
| ACERO_DETALLADO | `C117` | `(vacía)` | `cm` | No acredita empalme 12.17 para fuerzas sísmicas/momentos. |
| ACERO_DETALLADO | `C118` | `(vacía)` | `cm` | Longitud dentro de altura, compatible con fondo/recubrimiento. |
| ACERO_DETALLADO | `C119` | `(vacía)` | `-` | 12.1/12.3 y15.7: el gancho no desarrolla compresión. |
| ACERO_DETALLADO | `C120` | `(vacía)` | `cm` | Diámetro de barras realmente continuas o adicionales. |
| ACERO_DETALLADO | `C121` | `(vacía)` | `cm` | 12.3.1/2: mínimo20cm, sin factores de reducción por exceso/confinamiento. Se usa menor fc de ambos lados. |
| ACERO_DETALLADO | `C122` | `(vacía)` | `cm` | Longitud real recta ingresada desde cara de junta; no cero por falta de datos. |
| ACERO_DETALLADO | `C123` | `(vacía)` | `cm` | No acredita empalme 12.17 para fuerzas sísmicas/momentos. |
| ACERO_DETALLADO | `C124` | `(vacía)` | `cm` | Longitud dentro de altura, compatible con fondo/recubrimiento. |
| ACERO_DETALLADO | `C125` | `(vacía)` | `-` | 12.1/12.3 y15.7: el gancho no desarrolla compresión. |
| ACERO_DETALLADO | `C126` | `(vacía)` | `-` | Anclaje recto a compresión calculado. Tracción/flexocompresión y empalmes12.17 requieren detalle específico. |
| ACERO_DETALLADO | `C128` | `(vacía)` | `tf` | Resultante lateral; no se mezcla con H de servicio. |
| ACERO_DETALLADO | `C129` | `(vacía)` | `-` | 11.7.4.3: NORMAL. No es mu suelo-concreto. |
| ACERO_DETALLADO | `C130` | `(vacía)` | `cm2` | 11.7.4.1/6: fy<=420MPa; no acredita compresión permanente como reducción. |
| ACERO_DETALLADO | `C131` | `(vacía)` | `tf` | 11.7.5: límite concreto menor entre 0.2fcAc y5.5MPaAc. |
| ACERO_DETALLADO | `C132` | `(vacía)` | `-` | 11.7.8: Avf dedicada, distribuida y anclada; referencia de plano obligatoria. |
| ACERO_DETALLADO | `C134` | `(vacía)` | `-` | 15.8.1.3/12.17: flexocompresión biaxial, torsión y empalmes no se certifican con reparto axial uniforme. |
| ACERO_DETALLADO | `C135` | `(vacía)` | `-` | Si momentos/tracción: faltan coordenadas de barras, compatibilidad de deformaciones, interacción P-Mx-My y empalmes 12.17. Acero local horizontal no sustituye conexión vertical. |
| ACERO_DETALLADO | `C136` | `(vacía)` | `-` | Solo puede CUMPLE para dominio axial implementado con todas las verificaciones aplicables. |
| ACERO_DETALLADO | `C142` | `(vacía)` | `cm` | 7.7.1: construido en sitio; fuego/exposición agresiva no se determinan sin información. |
| ACERO_DETALLADO | `C143` | `(vacía)` | `-` | 7.7.1: inferior, superior si se requiere y lateral; exposiciones son entradas explícitas. |
| ACERO_DETALLADO | `C144` | `(vacía)` | `-` | 7.6.1 y3.3.2: distancia libre paralela >=db,2.5cm,4/3Dmáx; cruces ortogonales no son barras paralelas superpuestas. |
| ACERO_DETALLADO | `C148:C149` | `(vacía)` | `m` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `C150:C151` | `(vacía)` | `barras` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `C152:C155` | `(vacía)` | `cm2` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `C156` | `(vacía)` | `-` | No acredita un N que no cabe con la separación adoptada; comprueba ambas zonas exteriores. |
| ACERO_DETALLADO | `C160:C161` | `(vacía)` | `m` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `C162:C163` | `(vacía)` | `barras` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `C164:C167` | `(vacía)` | `cm2` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `C168` | `(vacía)` | `-` | No acredita un N que no cabe con la separación adoptada; comprueba ambas zonas exteriores. |
| ACERO_DETALLADO | `C171:C172` | `(vacía)` | `cm` | 7.7.1: condición seleccionada; no se optimiza el valor heredado. |
| ACERO_DETALLADO | `C173` | `(vacía)` | `-` | También considera momento de reacción crítica con columna descentrada, aun sin momento aplicado. |
| ACERO_DETALLADO | `D21:D24` | `(vacía)` | `E.060 15.4.4; independiente de cuál eje es más largo.` | E.060 15.4.4; independiente de cuál eje es más largo. |
| ACERO_DETALLADO | `D28` | `(vacía)` | `Distribuir X sobre Y y viceversa.` | Distribuir X sobre Y y viceversa. |
| ACERO_DETALLADO | `D29` | `(vacía)` | `As por metro × ancho perpendicular completo.` | As por metro × ancho perpendicular completo. |
| ACERO_DETALLADO | `D30` | `(vacía)` | `Corta: ancho igual lado corto, centrado en eje columna.` | Corta: ancho igual lado corto, centrado en eje columna. |
| ACERO_DETALLADO | `D31` | `(vacía)` | `Zonas de ambos lados, suma de anchos.` | Zonas de ambos lados, suma de anchos. |
| ACERO_DETALLADO | `D32` | `(vacía)` | `15.4.4.2: gamma_s As; larga/cuadrada totalidad uniforme.` | 15.4.4.2: gamma_s As; larga/cuadrada totalidad uniforme. |
| ACERO_DETALLADO | `D33` | `(vacía)` | `(1-gamma_s) As, no uniforme central arbitrario.` | (1-gamma_s) As, no uniforme central arbitrario. |
| ACERO_DETALLADO | `D34` | `(vacía)` | `Se mantiene diámetro global; separación regional editable.` | Se mantiene diámetro global; separación regional editable. |
| ACERO_DETALLADO | `D35` | `(vacía)` | `Entrada visible, no se cambia para lograr cumplimiento.` | Entrada visible, no se cambia para lograr cumplimiento. |
| ACERO_DETALLADO | `D36` | `(vacía)` | `Si zona exterior no existe, no aplica.` | Si zona exterior no existe, no aplica. |
| ACERO_DETALLADO | `D37` | `(vacía)` | `Conteo declarado del plano, no estimación continua.` | Conteo declarado del plano, no estimación continua. |
| ACERO_DETALLADO | `D38` | `(vacía)` | `Conteo fuera de franja, cero explícito si no existe.` | Conteo fuera de franja, cero explícito si no existe. |
| ACERO_DETALLADO | `D39` | `(vacía)` | `Acero real = número × área comercial.` | Acero real = número × área comercial. |
| ACERO_DETALLADO | `D40` | `(vacía)` | `No usa area equivalente por metro para contar barras.` | No usa area equivalente por metro para contar barras. |
| ACERO_DETALLADO | `D41` | `(vacía)` | `Concentración de la dirección corta.` | Concentración de la dirección corta. |
| ACERO_DETALLADO | `D42` | `(vacía)` | `Cero solo si región inexistente.` | Cero solo si región inexistente. |
| ACERO_DETALLADO | `D43` | `(vacía)` | `No se recorta una franja centrada normativa que sale de la zapata.` | No se recorta una franja centrada normativa que sale de la zapata. |
| ACERO_DETALLADO | `D44` | `(vacía)` | `Combina cantidad real y separación/densidad, manteniendo mínimo; 15.4.4.` | Combina cantidad real y separación/densidad, manteniendo mínimo; 15.4.4. |
| ACERO_DETALLADO | `D49` | `(vacía)` | `Distribuir X sobre Y y viceversa.` | Distribuir X sobre Y y viceversa. |
| ACERO_DETALLADO | `D50` | `(vacía)` | `As por metro × ancho perpendicular completo.` | As por metro × ancho perpendicular completo. |
| ACERO_DETALLADO | `D51` | `(vacía)` | `Corta: ancho igual lado corto, centrado en eje columna.` | Corta: ancho igual lado corto, centrado en eje columna. |
| ACERO_DETALLADO | `D52` | `(vacía)` | `Zonas de ambos lados, suma de anchos.` | Zonas de ambos lados, suma de anchos. |
| ACERO_DETALLADO | `D53` | `(vacía)` | `15.4.4.2: gamma_s As; larga/cuadrada totalidad uniforme.` | 15.4.4.2: gamma_s As; larga/cuadrada totalidad uniforme. |
| ACERO_DETALLADO | `D54` | `(vacía)` | `(1-gamma_s) As, no uniforme central arbitrario.` | (1-gamma_s) As, no uniforme central arbitrario. |
| ACERO_DETALLADO | `D55` | `(vacía)` | `Se mantiene diámetro global; separación regional editable.` | Se mantiene diámetro global; separación regional editable. |
| ACERO_DETALLADO | `D56` | `(vacía)` | `Entrada visible, no se cambia para lograr cumplimiento.` | Entrada visible, no se cambia para lograr cumplimiento. |
| ACERO_DETALLADO | `D57` | `(vacía)` | `Si zona exterior no existe, no aplica.` | Si zona exterior no existe, no aplica. |
| ACERO_DETALLADO | `D58` | `(vacía)` | `Conteo declarado del plano, no estimación continua.` | Conteo declarado del plano, no estimación continua. |
| ACERO_DETALLADO | `D59` | `(vacía)` | `Conteo fuera de franja, cero explícito si no existe.` | Conteo fuera de franja, cero explícito si no existe. |
| ACERO_DETALLADO | `D60` | `(vacía)` | `Acero real = número × área comercial.` | Acero real = número × área comercial. |
| ACERO_DETALLADO | `D61` | `(vacía)` | `No usa area equivalente por metro para contar barras.` | No usa area equivalente por metro para contar barras. |
| ACERO_DETALLADO | `D62` | `(vacía)` | `Concentración de la dirección corta.` | Concentración de la dirección corta. |
| ACERO_DETALLADO | `D63` | `(vacía)` | `Cero solo si región inexistente.` | Cero solo si región inexistente. |
| ACERO_DETALLADO | `D64` | `(vacía)` | `No se recorta una franja centrada normativa que sale de la zapata.` | No se recorta una franja centrada normativa que sale de la zapata. |
| ACERO_DETALLADO | `D65` | `(vacía)` | `Combina cantidad real y separación/densidad, manteniendo mínimo; 15.4.4.` | Combina cantidad real y separación/densidad, manteniendo mínimo; 15.4.4. |
| ACERO_DETALLADO | `D72` | `(vacía)` | `psi_e` | 12.2.3: Ktr=0; sin reducción por acero en exceso. |
| ACERO_DETALLADO | `D73` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(inp_epoxy="SIN EPOXI",1,IF(OR(MIN((IF(inp_order_inf="X inferior / Y superior",inp_rec_inf+B73/2,inp_rec_inf+INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))+B73/2))-B73/2,inp_h*100-(IF(inp_order_inf="X inferior / Y superior",inp_rec_inf+B73/2,inp_rec_inf+INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))+B73/2))-B73/2,inp_rec_lat)<3*B73,MIN(inp_sep_inf_x,inp_scx,inp_sox)-B73<6*B73),1.5,1.2)),"")` | Tabla12.2: recubrimiento libre real de la capa, tratamiento y espaciamiento declarados. |
| ACERO_DETALLADO | `D74` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(inp_epoxy="SIN EPOXI",1,IF(OR(MIN((IF(inp_order_inf="Y inferior / X superior",inp_rec_inf+B74/2,inp_rec_inf+INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))+B74/2))-B74/2,inp_h*100-(IF(inp_order_inf="Y inferior / X superior",inp_rec_inf+B74/2,inp_rec_inf+INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))+B74/2))-B74/2,inp_rec_lat)<3*B74,MIN(inp_sep_inf_y,inp_scy,inp_soy)-B74<6*B74),1.5,1.2)),"")` | Tabla12.2: recubrimiento libre real de la capa, tratamiento y espaciamiento declarados. |
| ACERO_DETALLADO | `D75` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(inp_epoxy="SIN EPOXI",1,IF(OR(MIN((FLEXION_ACERO!E7)-B75/2,inp_h*100-(FLEXION_ACERO!E7)-B75/2,inp_rec_lat)<3*B75,inp_sep_sup_x-B75<6*B75),1.5,1.2)),"")` | Tabla12.2: recubrimiento libre real de la capa, tratamiento y espaciamiento declarados. |
| ACERO_DETALLADO | `D76` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,OR(inp_epoxy="SIN EPOXI",inp_epoxy="EPOXI")),IF(inp_epoxy="SIN EPOXI",1,IF(OR(MIN((FLEXION_ACERO!E8)-B76/2,inp_h*100-(FLEXION_ACERO!E8)-B76/2,inp_rec_lat)<3*B76,inp_sep_sup_y-B76<6*B76),1.5,1.2)),"")` | Tabla12.2: recubrimiento libre real de la capa, tratamiento y espaciamiento declarados. |
| ACERO_DETALLADO | `D78` | `(vacía)` | `Secciones de cambios de sección/refuerzo no modeladas; barras rectas continuas.` | Secciones de cambios de sección/refuerzo no modeladas; barras rectas continuas. |
| ACERO_DETALLADO | `D79` | `(vacía)` | `12.2.3 permite Ktr=0. Sin reducción por exceso. Ganchos/paquetes/cortes/empalmes requieren detalle especial.` | 12.2.3 permite Ktr=0. Sin reducción por exceso. Ganchos/paquetes/cortes/empalmes requieren detalle especial. |
| ACERO_DETALLADO | `D85` | `(vacía)` | `Mu combinado tf m` | Franja efectiva real; no se acredita por As global por metro. |
| ACERO_DETALLADO | `D86:D89` | `(vacía)` | `=IF(punz_state="OK",ABS(B86)+FLEXION_ACERO!D5*C86/100,"")` | Suma magnitudes del Mu local y Mu normativo global; criterio conservador explícito. |
| ACERO_DETALLADO | `D91` | `(vacía)` | `No permite convertir advertencia F1 en CUMPLE sin conteo y desarrollo comprobados.` | No permite convertir advertencia F1 en CUMPLE sin conteo y desarrollo comprobados. |
| ACERO_DETALLADO | `D92` | `(vacía)` | `Ambas capas resisten conservadoramente la magnitud local más demanda global; sin reparto único entre signos.` | Ambas capas resisten conservadoramente la magnitud local más demanda global; sin reparto único entre signos. |
| ACERO_DETALLADO | `D97` | `(vacía)` | `No presume fc/fy ni continuidad de barras; explícitamente IN SITU.` | No presume fc/fy ni continuidad de barras; explícitamente IN SITU. |
| ACERO_DETALLADO | `D98` | `(vacía)` | `Área bruta de columna rectangular.` | Área bruta de columna rectangular. |
| ACERO_DETALLADO | `D99` | `(vacía)` | `Se conserva signo; no se toma ABS como conversión.` | Se conserva signo; no se toma ABS como conversión. |
| ACERO_DETALLADO | `D100` | `(vacía)` | `E.060 9.3.2.4; sin aumento opcional sqrt(A2/A1).` | E.060 9.3.2.4; sin aumento opcional sqrt(A2/A1). |
| ACERO_DETALLADO | `D101` | `(vacía)` | `10.17.1: factor A2/A1=1 conservador, no geometría inventada.` | 10.17.1: factor A2/A1=1 conservador, no geometría inventada. |
| ACERO_DETALLADO | `D102` | `(vacía)` | `10.17.1: capacidad de ambas superficies.` | 10.17.1: capacidad de ambas superficies. |
| ACERO_DETALLADO | `D103` | `(vacía)` | `15.8.1.1: mínimo de ambas superficies.` | 15.8.1.1: mínimo de ambas superficies. |
| ACERO_DETALLADO | `D104` | `(vacía)` | `MAX positivo calcula solo exceso; no cambia signo de Pu.` | MAX positivo calcula solo exceso; no cambia signo de Pu. |
| ACERO_DETALLADO | `D105` | `(vacía)` | `E.060 15.8.2.1, columna/pedestal construido en obra.` | E.060 15.8.2.1, columna/pedestal construido en obra. |
| ACERO_DETALLADO | `D106` | `(vacía)` | `15.8.1.2(a) y 9.3.2.2(b); no acredita flexocompresión.` | 15.8.1.2(a) y 9.3.2.2(b); no acredita flexocompresión. |
| ACERO_DETALLADO | `D107` | `(vacía)` | `15.8.1.2(b); magnitud de tracción con Pu firmado visible.` | 15.8.1.2(b); magnitud de tracción con Pu firmado visible. |
| ACERO_DETALLADO | `D108` | `(vacía)` | `No pretende cubrir momentos, cortante ni desarrollo.` | No pretende cubrir momentos, cortante ni desarrollo. |
| ACERO_DETALLADO | `D109` | `(vacía)` | `N confirmado que atraviesa la junta, no N total de columna.` | N confirmado que atraviesa la junta, no N total de columna. |
| ACERO_DETALLADO | `D110` | `(vacía)` | `Cero solo cuando el usuario declara N dowels=0.` | Cero solo cuando el usuario declara N dowels=0. |
| ACERO_DETALLADO | `D111` | `(vacía)` | `15.8.2.1: suma de continuas y adicionales confirmadas.` | 15.8.2.1: suma de continuas y adicionales confirmadas. |
| ACERO_DETALLADO | `D112` | `(vacía)` | `Control cantidad, independiente del anclaje y la flexocompresión.` | Control cantidad, independiente del anclaje y la flexocompresión. |
| ACERO_DETALLADO | `D114` | `(vacía)` | `Diámetro de barras realmente continuas o adicionales.` | Diámetro de barras realmente continuas o adicionales. |
| ACERO_DETALLADO | `D115` | `(vacía)` | `12.3.1/2: mínimo20cm, sin factores de reducción por exceso/confinamiento. Se usa menor fc de ambos lados.` | 12.3.1/2: mínimo20cm, sin factores de reducción por exceso/confinamiento. Se usa menor fc de ambos lados. |
| ACERO_DETALLADO | `D116` | `(vacía)` | `Longitud real recta ingresada desde cara de junta; no cero por falta de datos.` | Longitud real recta ingresada desde cara de junta; no cero por falta de datos. |
| ACERO_DETALLADO | `D117` | `(vacía)` | `No acredita empalme 12.17 para fuerzas sísmicas/momentos.` | No acredita empalme 12.17 para fuerzas sísmicas/momentos. |
| ACERO_DETALLADO | `D118` | `(vacía)` | `Longitud dentro de altura, compatible con fondo/recubrimiento.` | Longitud dentro de altura, compatible con fondo/recubrimiento. |
| ACERO_DETALLADO | `D119` | `(vacía)` | `12.1/12.3 y15.7: el gancho no desarrolla compresión.` | 12.1/12.3 y15.7: el gancho no desarrolla compresión. |
| ACERO_DETALLADO | `D120` | `(vacía)` | `Diámetro de barras realmente continuas o adicionales.` | Diámetro de barras realmente continuas o adicionales. |
| ACERO_DETALLADO | `D121` | `(vacía)` | `12.3.1/2: mínimo20cm, sin factores de reducción por exceso/confinamiento. Se usa menor fc de ambos lados.` | 12.3.1/2: mínimo20cm, sin factores de reducción por exceso/confinamiento. Se usa menor fc de ambos lados. |
| ACERO_DETALLADO | `D122` | `(vacía)` | `Longitud real recta ingresada desde cara de junta; no cero por falta de datos.` | Longitud real recta ingresada desde cara de junta; no cero por falta de datos. |
| ACERO_DETALLADO | `D123` | `(vacía)` | `No acredita empalme 12.17 para fuerzas sísmicas/momentos.` | No acredita empalme 12.17 para fuerzas sísmicas/momentos. |
| ACERO_DETALLADO | `D124` | `(vacía)` | `Longitud dentro de altura, compatible con fondo/recubrimiento.` | Longitud dentro de altura, compatible con fondo/recubrimiento. |
| ACERO_DETALLADO | `D125` | `(vacía)` | `12.1/12.3 y15.7: el gancho no desarrolla compresión.` | 12.1/12.3 y15.7: el gancho no desarrolla compresión. |
| ACERO_DETALLADO | `D126` | `(vacía)` | `Anclaje recto a compresión calculado. Tracción/flexocompresión y empalmes12.17 requieren detalle específico.` | Anclaje recto a compresión calculado. Tracción/flexocompresión y empalmes12.17 requieren detalle específico. |
| ACERO_DETALLADO | `D128` | `(vacía)` | `Resultante lateral; no se mezcla con H de servicio.` | Resultante lateral; no se mezcla con H de servicio. |
| ACERO_DETALLADO | `D129` | `(vacía)` | `11.7.4.3: NORMAL. No es mu suelo-concreto.` | 11.7.4.3: NORMAL. No es mu suelo-concreto. |
| ACERO_DETALLADO | `D130` | `(vacía)` | `11.7.4.1/6: fy<=420MPa; no acredita compresión permanente como reducción.` | 11.7.4.1/6: fy<=420MPa; no acredita compresión permanente como reducción. |
| ACERO_DETALLADO | `D131` | `(vacía)` | `11.7.5: límite concreto menor entre 0.2fcAc y5.5MPaAc.` | 11.7.5: límite concreto menor entre 0.2fcAc y5.5MPaAc. |
| ACERO_DETALLADO | `D132` | `(vacía)` | `11.7.8: Avf dedicada, distribuida y anclada; referencia de plano obligatoria.` | 11.7.8: Avf dedicada, distribuida y anclada; referencia de plano obligatoria. |
| ACERO_DETALLADO | `D134` | `(vacía)` | `15.8.1.3/12.17: flexocompresión biaxial, torsión y empalmes no se certifican con reparto axial uniforme.` | 15.8.1.3/12.17: flexocompresión biaxial, torsión y empalmes no se certifican con reparto axial uniforme. |
| ACERO_DETALLADO | `D135` | `(vacía)` | `Si momentos/tracción: faltan coordenadas de barras, compatibilidad de deformaciones, interacción P-Mx-My y empalmes 12.17. Acero local horizontal no sustituye conexión vertical.` | Si momentos/tracción: faltan coordenadas de barras, compatibilidad de deformaciones, interacción P-Mx-My y empalmes 12.17. Acero local horizontal no sustituye conexión vertical. |
| ACERO_DETALLADO | `D136` | `(vacía)` | `Solo puede CUMPLE para dominio axial implementado con todas las verificaciones aplicables.` | Solo puede CUMPLE para dominio axial implementado con todas las verificaciones aplicables. |
| ACERO_DETALLADO | `D142` | `(vacía)` | `7.7.1: construido en sitio; fuego/exposición agresiva no se determinan sin información.` | 7.7.1: construido en sitio; fuego/exposición agresiva no se determinan sin información. |
| ACERO_DETALLADO | `D143` | `(vacía)` | `7.7.1: inferior, superior si se requiere y lateral; exposiciones son entradas explícitas.` | 7.7.1: inferior, superior si se requiere y lateral; exposiciones son entradas explícitas. |
| ACERO_DETALLADO | `D144` | `(vacía)` | `7.6.1 y3.3.2: distancia libre paralela >=db,2.5cm,4/3Dmáx; cruces ortogonales no son barras paralelas superpuestas.` | 7.6.1 y3.3.2: distancia libre paralela >=db,2.5cm,4/3Dmáx; cruces ortogonales no son barras paralelas superpuestas. |
| ACERO_DETALLADO | `D148:D155` | `(vacía)` | `Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral.` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `D156` | `(vacía)` | `No acredita un N que no cabe con la separación adoptada; comprueba ambas zonas exteriores.` | No acredita un N que no cabe con la separación adoptada; comprueba ambas zonas exteriores. |
| ACERO_DETALLADO | `D160:D167` | `(vacía)` | `Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral.` | Cantidad/ubicación por zona; extremos deben respetar recubrimiento lateral. |
| ACERO_DETALLADO | `D168` | `(vacía)` | `No acredita un N que no cabe con la separación adoptada; comprueba ambas zonas exteriores.` | No acredita un N que no cabe con la separación adoptada; comprueba ambas zonas exteriores. |
| ACERO_DETALLADO | `D171:D172` | `(vacía)` | `7.7.1: condición seleccionada; no se optimiza el valor heredado.` | 7.7.1: condición seleccionada; no se optimiza el valor heredado. |
| ACERO_DETALLADO | `D173` | `(vacía)` | `También considera momento de reacción crítica con columna descentrada, aun sin momento aplicado.` | También considera momento de reacción crítica con columna descentrada, aun sin momento aplicado. |
| ACERO_DETALLADO | `E72` | `(vacía)` | `psi_s` | 12.2.3: Ktr=0; sin reducción por acero en exceso. |
| ACERO_DETALLADO | `E73:E76` | `(vacía)` | `=IF(struct_state="OK",IF(B73<=1.905,0.8,1),"")` | Tabla12.2: diámetro <=3/4 pulgadas. |
| ACERO_DETALLADO | `E85` | `(vacía)` | `d cm` | Franja efectiva real; no se acredita por As global por metro. |
| ACERO_DETALLADO | `E86:E89` | `(vacía)` | `=IF(punz_state="OK",FLEXION_ACERO!E5,"")` | Peralte real de la capa correspondiente. |
| ACERO_DETALLADO | `F72` | `(vacía)` | `cb cm` | 12.2.3: Ktr=0; sin reducción por acero en exceso. |
| ACERO_DETALLADO | `F73` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,inp_rec_lat>=0),MIN((IF(inp_order_inf="X inferior / Y superior",inp_rec_inf+B73/2,inp_rec_inf+INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))+B73/2)),inp_h*100-(IF(inp_order_inf="X inferior / Y superior",inp_rec_inf+B73/2,inp_rec_inf+INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))+B73/2)),inp_rec_lat+B73/2,(MIN(inp_sep_inf_x,inp_scx,inp_sox))/2),"")` | cb: centro a superficie más próxima, coordenada física según capa, o mitad del espaciamiento; 12.2.3. |
| ACERO_DETALLADO | `F74` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,inp_rec_lat>=0),MIN((IF(inp_order_inf="Y inferior / X superior",inp_rec_inf+B74/2,inp_rec_inf+INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))+B74/2)),inp_h*100-(IF(inp_order_inf="Y inferior / X superior",inp_rec_inf+B74/2,inp_rec_inf+INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))+B74/2)),inp_rec_lat+B74/2,(MIN(inp_sep_inf_y,inp_scy,inp_soy))/2),"")` | cb: centro a superficie más próxima, coordenada física según capa, o mitad del espaciamiento; 12.2.3. |
| ACERO_DETALLADO | `F75` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,inp_rec_lat>=0),MIN((FLEXION_ACERO!E7),inp_h*100-(FLEXION_ACERO!E7),inp_rec_lat+B75/2,(inp_sep_sup_x)/2),"")` | cb: centro a superficie más próxima, coordenada física según capa, o mitad del espaciamiento; 12.2.3. |
| ACERO_DETALLADO | `F76` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1,inp_rec_lat>=0),MIN((FLEXION_ACERO!E8),inp_h*100-(FLEXION_ACERO!E8),inp_rec_lat+B76/2,(inp_sep_sup_y)/2),"")` | cb: centro a superficie más próxima, coordenada física según capa, o mitad del espaciamiento; 12.2.3. |
| ACERO_DETALLADO | `F85` | `(vacía)` | `As req cm2` | Franja efectiva real; no se acredita por As global por metro. |
| ACERO_DETALLADO | `F86:F89` | `(vacía)` | `=IF(punz_state="OK",IF(ABS(B86)<=0.000001,0,IF((inp_fy*E86)^2-4*(inp_fy^2/(2*0.85*inp_fc*C86))*(D86*100000/inp_phi_f)<0,"",MAX(rho_eff*C86*inp_h*100,(inp_fy*E86-SQRT((inp_fy*E86)^2-4*(inp_fy^2/(2*0.85*inp_fc*C86))*(D86*100000/inp_phi_f)))/(2*(inp_fy^2/(2*0.85*inp_fc*C86)))))),"")` | 13.5.3.3 y 10.2: acero requerido dentro del ancho efectivo; sin excepción de aumento γf. |
| ACERO_DETALLADO | `G72` | `(vacía)` | `ld req cm` | 12.2.3: Ktr=0; sin reducción por acero en exceso. |
| ACERO_DETALLADO | `G73:G76` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(D73,F73)=2,F73>0),MAX(30,(inp_fy*0.0980665)*C73*D73*E73/(1.1*MIN(SQRT(inp_fc*0.0980665),8.3)*MIN(2.5,F73/B73))*B73),"")` | 12-1, Ktr=0. No se aplica reducción opcional del producto de factores de tabla12.2. |
| ACERO_DETALLADO | `G85` | `(vacía)` | `N real` | Franja efectiva real; no se acredita por As global por metro. |
| ACERO_DETALLADO | `G86` | `(vacía)` | `=IF(LEN(inp_nloc_ix)=0,"",inp_nloc_ix)` | Conteo real declarado; un dato faltante no se presenta como cero. |
| ACERO_DETALLADO | `G87` | `(vacía)` | `=IF(LEN(inp_nloc_iy)=0,"",inp_nloc_iy)` | Conteo real declarado; un dato faltante no se presenta como cero. |
| ACERO_DETALLADO | `G88` | `(vacía)` | `=IF(LEN(inp_nloc_sx)=0,"",inp_nloc_sx)` | Conteo real declarado; un dato faltante no se presenta como cero. |
| ACERO_DETALLADO | `G89` | `(vacía)` | `=IF(LEN(inp_nloc_sy)=0,"",inp_nloc_sy)` | Conteo real declarado; un dato faltante no se presenta como cero. |
| ACERO_DETALLADO | `H5:H8` | `=IF(struct_state="OK",IF(D5<=0,0,C5*100/F5),"")` | `=IF(AND(struct_state="OK",ISNUMBER(F5),F5>0,ISNUMBER(D5)),IF(D5<=0,0,C5*100/F5),"")` | Separación cero bloqueada por struct_state antes de dividir. |
| ACERO_DETALLADO | `H72` | `(vacía)` | `ld disp - cm` | 12.2.3: Ktr=0; sin reducción por acero en exceso. |
| ACERO_DETALLADO | `H73` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1),(inp_bx/2+inp_xc-inp_cx/2)*100-inp_rec_lat,"")` | Longitud recta desde cara a extremo de barra; resta recubrimiento lateral. |
| ACERO_DETALLADO | `H74` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1),(inp_by/2+inp_yc-inp_cy/2)*100-inp_rec_lat,"")` | Longitud recta desde cara a extremo de barra; resta recubrimiento lateral. |
| ACERO_DETALLADO | `H75` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1),(inp_bx/2+inp_xc-inp_cx/2)*100-inp_rec_lat,"")` | Longitud recta desde cara a extremo de barra; resta recubrimiento lateral. |
| ACERO_DETALLADO | `H76` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1),(inp_by/2+inp_yc-inp_cy/2)*100-inp_rec_lat,"")` | Longitud recta desde cara a extremo de barra; resta recubrimiento lateral. |
| ACERO_DETALLADO | `H85` | `(vacía)` | `As real cm2` | Franja efectiva real; no se acredita por As global por metro. |
| ACERO_DETALLADO | `H86` | `(vacía)` | `=IF(AND(punz_state="OK",COUNT(inp_nloc_ix)=1,inp_nloc_ix>=0),inp_nloc_ix*INDEX(bar_area_cm2,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | Acero real por conteo, distinto del cálculo global por metro. |
| ACERO_DETALLADO | `H87` | `(vacía)` | `=IF(AND(punz_state="OK",COUNT(inp_nloc_iy)=1,inp_nloc_iy>=0),inp_nloc_iy*INDEX(bar_area_cm2,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Acero real por conteo, distinto del cálculo global por metro. |
| ACERO_DETALLADO | `H88` | `(vacía)` | `=IF(AND(punz_state="OK",COUNT(inp_nloc_sx)=1,inp_nloc_sx>=0),inp_nloc_sx*INDEX(bar_area_cm2,MATCH(inp_bar_sup_x,bar_codes,0)),"")` | Acero real por conteo, distinto del cálculo global por metro. |
| ACERO_DETALLADO | `H89` | `(vacía)` | `=IF(AND(punz_state="OK",COUNT(inp_nloc_sy)=1,inp_nloc_sy>=0),inp_nloc_sy*INDEX(bar_area_cm2,MATCH(inp_bar_sup_y,bar_codes,0)),"")` | Acero real por conteo, distinto del cálculo global por metro. |
| ACERO_DETALLADO | `I5:I8` | `=IF(struct_state="OK",IF(D5<=0,1,H5/D5),"")` | `=IF(AND(struct_state="OK",ISNUMBER(D5),ISNUMBER(H5)),IF(D5<=0,1,H5/D5),"")` | No confundir As vacío por sección imposible con cero demanda. |
| ACERO_DETALLADO | `I72` | `(vacía)` | `ld disp + cm` | 12.2.3: Ktr=0; sin reducción por acero en exceso. |
| ACERO_DETALLADO | `I73` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1),(inp_bx/2-inp_xc-inp_cx/2)*100-inp_rec_lat,"")` | Longitud recta desde cara a extremo de barra; resta recubrimiento lateral. |
| ACERO_DETALLADO | `I74` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1),(inp_by/2-inp_yc-inp_cy/2)*100-inp_rec_lat,"")` | Longitud recta desde cara a extremo de barra; resta recubrimiento lateral. |
| ACERO_DETALLADO | `I75` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1),(inp_bx/2-inp_xc-inp_cx/2)*100-inp_rec_lat,"")` | Longitud recta desde cara a extremo de barra; resta recubrimiento lateral. |
| ACERO_DETALLADO | `I76` | `(vacía)` | `=IF(AND(struct_state="OK",COUNT(inp_rec_lat)=1),(inp_by/2-inp_yc-inp_cy/2)*100-inp_rec_lat,"")` | Longitud recta desde cara a extremo de barra; resta recubrimiento lateral. |
| ACERO_DETALLADO | `I85` | `(vacía)` | `ld real min cm` | Franja efectiva real; no se acredita por As global por metro. |
| ACERO_DETALLADO | `I86` | `(vacía)` | `=IF(AND(punz_state="OK",COUNT(inp_ll_ix_m,inp_ll_ix_p)=2),MIN(inp_ll_ix_m,inp_ll_ix_p),"")` | Mínima longitud local declarada de ambos lados. |
| ACERO_DETALLADO | `I87` | `(vacía)` | `=IF(AND(punz_state="OK",COUNT(inp_ll_iy_m,inp_ll_iy_p)=2),MIN(inp_ll_iy_m,inp_ll_iy_p),"")` | Mínima longitud local declarada de ambos lados. |
| ACERO_DETALLADO | `I88` | `(vacía)` | `=IF(AND(punz_state="OK",COUNT(inp_ll_sx_m,inp_ll_sx_p)=2),MIN(inp_ll_sx_m,inp_ll_sx_p),"")` | Mínima longitud local declarada de ambos lados. |
| ACERO_DETALLADO | `I89` | `(vacía)` | `=IF(AND(punz_state="OK",COUNT(inp_ll_sy_m,inp_ll_sy_p)=2),MIN(inp_ll_sy_m,inp_ll_sy_p),"")` | Mínima longitud local declarada de ambos lados. |
| ACERO_DETALLADO | `J5:J8` | `=IF(struct_state<>"OK",struct_state,IF(D5<=0,"CUMPLE",IF(AND(H5>=D5,F5<=G5),"CUMPLE","NO CUMPLE")))` | `=IF(struct_state<>"OK",struct_state,IF(FLEXION_ACERO!I5="NO CUMPLE","NO CUMPLE",IF(D5<=0,"NO APLICA",IF(AND(H5>=D5,F5<=G5),"CUMPLE","NO CUMPLE"))))` | Separar parrilla no requerida de incumplimiento. |
| ACERO_DETALLADO | `J72` | `(vacía)` | `Estado` | 12.2.3: Ktr=0; sin reducción por acero en exceso. |
| ACERO_DETALLADO | `J73` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(NOT(OR(FLEXION_ACERO!D5>0,AND("inf"="inf",FLEXION_ACERO!H5>0),AND("inf"="sup",OR(MAX(ABS(ult_mx),ABS(ult_my))>0.000001,IF(punz_state="OK",ABS(PUNZONAMIENTO!B48)>0.000001,FALSE))))),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_inf)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_inf<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G73)),MIN(H73:I73)<G73,MIN(inp_sep_inf_x,inp_scx,inp_sox)-B73<MAX(B73,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | 15.6.2: desarrollar a ambos lados de cara; agrega 7.6.1 y 3.3.2 sin acreditar ganchos. |
| ACERO_DETALLADO | `J74` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(NOT(OR(FLEXION_ACERO!D6>0,AND("inf"="inf",FLEXION_ACERO!H6>0),AND("inf"="sup",OR(MAX(ABS(ult_mx),ABS(ult_my))>0.000001,IF(punz_state="OK",ABS(PUNZONAMIENTO!B47)>0.000001,FALSE))))),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_inf)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_inf<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G74)),MIN(H74:I74)<G74,MIN(inp_sep_inf_y,inp_scy,inp_soy)-B74<MAX(B74,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | 15.6.2: desarrollar a ambos lados de cara; agrega 7.6.1 y 3.3.2 sin acreditar ganchos. |
| ACERO_DETALLADO | `J75` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(NOT(OR(FLEXION_ACERO!D7>0,AND("sup"="inf",FLEXION_ACERO!H7>0),AND("sup"="sup",OR(MAX(ABS(ult_mx),ABS(ult_my))>0.000001,IF(punz_state="OK",ABS(PUNZONAMIENTO!B48)>0.000001,FALSE))))),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_sup)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_sup<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G75)),MIN(H75:I75)<G75,inp_sep_sup_x-B75<MAX(B75,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | 15.6.2: desarrollar a ambos lados de cara; agrega 7.6.1 y 3.3.2 sin acreditar ganchos. |
| ACERO_DETALLADO | `J76` | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(NOT(OR(FLEXION_ACERO!D8>0,AND("sup"="inf",FLEXION_ACERO!H8>0),AND("sup"="sup",OR(MAX(ABS(ult_mx),ABS(ult_my))>0.000001,IF(punz_state="OK",ABS(PUNZONAMIENTO!B47)>0.000001,FALSE))))),"NO APLICA",IF(OR(COUNT(inp_rec_lat,inp_agg)<>2,LEN(inp_epoxy)=0,LEN(inp_end_sup)=0,LEN(inp_side_exposure)=0),"REQUIERE DATOS",IF(inp_end_sup<>"RECTA","FUERA DEL ALCANCE IMPLEMENTADO",IF(OR(inp_rec_lat<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(G76)),MIN(H76:I76)<G76,inp_sep_sup_y-B76<MAX(B76,2.5,4*inp_agg/3)),"NO CUMPLE","CUMPLE"))))))` | 15.6.2: desarrollar a ambos lados de cara; agrega 7.6.1 y 3.3.2 sin acreditar ganchos. |
| ACERO_DETALLADO | `J85` | `(vacía)` | `Estado` | Franja efectiva real; no se acredita por As global por metro. |
| ACERO_DETALLADO | `J86` | `(vacía)` | `=IF(punz_state<>"OK",punz_state,IF(ABS(B86)<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",COUNT(inp_nloc_ix,inp_ll_ix_m,inp_ll_ix_p,inp_agg)<>4),"REQUIERE DATOS",IF(OR(inp_nloc_ix<0,MOD(inp_nloc_ix,1)<>0,inp_ll_ix_m<0,inp_ll_ix_p<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(COUNT(inp_ncx,inp_nox)<>2,"REQUIERE DATOS",IF(inp_nloc_ix>inp_ncx+inp_nox,"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(F86)),NOT(ISNUMBER(ld_inf_x))),"REQUIERE DATOS",IF(OR(H86<F86,I86<ld_inf_x,MIN(inp_ll_ix_m,inp_ll_ix_p)<0,F86>rho_max*C86*E86,inp_nloc_ix>INT(C86/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),2.5,4*inp_agg/3))+1,inp_ll_ix_m>H73,inp_ll_ix_p>I73),"NO CUMPLE",IF(J73<>"CUMPLE",J73,"CUMPLE")))))))))` | 13.5.3.3: refuerzo y desarrollo local; conteos y longitudes insuficientes no acreditan conexión. |
| ACERO_DETALLADO | `J87` | `(vacía)` | `=IF(punz_state<>"OK",punz_state,IF(ABS(B87)<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",COUNT(inp_nloc_iy,inp_ll_iy_m,inp_ll_iy_p,inp_agg)<>4),"REQUIERE DATOS",IF(OR(inp_nloc_iy<0,MOD(inp_nloc_iy,1)<>0,inp_ll_iy_m<0,inp_ll_iy_p<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(COUNT(inp_ncy,inp_noy)<>2,"REQUIERE DATOS",IF(inp_nloc_iy>inp_ncy+inp_noy,"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(F87)),NOT(ISNUMBER(ld_inf_y))),"REQUIERE DATOS",IF(OR(H87<F87,I87<ld_inf_y,MIN(inp_ll_iy_m,inp_ll_iy_p)<0,F87>rho_max*C87*E87,inp_nloc_iy>INT(C87/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)),2.5,4*inp_agg/3))+1,inp_ll_iy_m>H74,inp_ll_iy_p>I74),"NO CUMPLE",IF(J74<>"CUMPLE",J74,"CUMPLE")))))))))` | 13.5.3.3: refuerzo y desarrollo local; conteos y longitudes insuficientes no acreditan conexión. |
| ACERO_DETALLADO | `J88` | `(vacía)` | `=IF(punz_state<>"OK",punz_state,IF(ABS(B88)<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",COUNT(inp_nloc_sx,inp_ll_sx_m,inp_ll_sx_p,inp_agg)<>4),"REQUIERE DATOS",IF(OR(inp_nloc_sx<0,MOD(inp_nloc_sx,1)<>0,inp_ll_sx_m<0,inp_ll_sx_p<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(F88)),NOT(ISNUMBER(ld_sup_x))),"REQUIERE DATOS",IF(OR(H88<F88,I88<ld_sup_x,MIN(inp_ll_sx_m,inp_ll_sx_p)<0,F88>rho_max*C88*E88,inp_nloc_sx>INT(C88/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0)),2.5,4*inp_agg/3))+1,inp_ll_sx_m>H75,inp_ll_sx_p>I75),"NO CUMPLE",IF(J75<>"CUMPLE",J75,"CUMPLE")))))))` | 13.5.3.3: refuerzo y desarrollo local; conteos y longitudes insuficientes no acreditan conexión. |
| ACERO_DETALLADO | `J89` | `(vacía)` | `=IF(punz_state<>"OK",punz_state,IF(ABS(B89)<=0.000001,"NO APLICA",IF(OR(inp_local_detail<>"SI",COUNT(inp_nloc_sy,inp_ll_sy_m,inp_ll_sy_p,inp_agg)<>4),"REQUIERE DATOS",IF(OR(inp_nloc_sy<0,MOD(inp_nloc_sy,1)<>0,inp_ll_sy_m<0,inp_ll_sy_p<0,inp_agg<=0),"DATOS INVÁLIDOS",IF(OR(NOT(ISNUMBER(F89)),NOT(ISNUMBER(ld_sup_y))),"REQUIERE DATOS",IF(OR(H89<F89,I89<ld_sup_y,MIN(inp_ll_sy_m,inp_ll_sy_p)<0,F89>rho_max*C89*E89,inp_nloc_sy>INT(C89/MAX(INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0)),2.5,4*inp_agg/3))+1,inp_ll_sy_m>H76,inp_ll_sy_p>I76),"NO CUMPLE",IF(J76<>"CUMPLE",J76,"CUMPLE")))))))` | 13.5.3.3: refuerzo y desarrollo local; conteos y longitudes insuficientes no acreditan conexión. |
| GRAFICOS | `B12` | `=IF(geo_input_state="OK",q_srv_px_py,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",q_srv_px_py,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `B13` | `=IF(geo_input_state="OK",q_srv_px_my,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",q_srv_px_my,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `B14` | `=IF(geo_input_state="OK",q_srv_mx_py,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",q_srv_mx_py,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `B15` | `=IF(geo_input_state="OK",q_srv_mx_my,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",q_srv_mx_my,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `C12:C15` | `=IF(geo_input_state="OK",inp_qadm,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",g_qadm,""),"")` | Gráfico muestra qadm aplicada explícitamente, incluyendo 15.2.4 solo si habilitado. |
| GRAFICOS | `D12` | `=IF(geo_input_state="OK",q_u_px_py,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",q_u_px_py,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `D13` | `=IF(geo_input_state="OK",q_u_px_my,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",q_u_px_my,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `D14` | `=IF(geo_input_state="OK",q_u_mx_py,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",q_u_mx_py,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `D15` | `=IF(geo_input_state="OK",q_u_mx_my,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",q_u_mx_my,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `E4` | `=IF(geo_input_state="OK",res_srv_ex,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_ex,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `F4` | `=IF(geo_input_state="OK",res_srv_ey,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_ey,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `G4` | `=IF(geo_input_state="OK",res_u_ex,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_ex,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `H4` | `=IF(geo_input_state="OK",res_u_ey,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_ey,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `K5:K15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*K$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*K$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `K21:K31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*K$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*K$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `L5:L15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*L$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*L$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `L21:L31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*L$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*L$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `M5:M15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*M$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*M$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `M21:M31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*M$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*M$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `N5:N15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*N$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*N$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `N21:N31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*N$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*N$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `O5:O15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*O$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*O$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `O21:O31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*O$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*O$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `P5:P15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*P$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*P$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `P21:P31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*P$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*P$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `Q5:Q15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*Q$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*Q$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `Q21:Q31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*Q$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*Q$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `R5:R15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*R$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*R$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `R21:R31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*R$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*R$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `S5:S15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*S$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*S$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `S21:S31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*S$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*S$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `T5:T15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*T$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*T$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `T21:T31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*T$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*T$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| GRAFICOS | `U5:U15` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*U$4,"")` | `=IF(srv_input_state="OK",IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*U$4,""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| GRAFICOS | `U21:U31` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*U$20,"")` | `=IF(ult_input_state="OK",IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*U$20,""),"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| RESUMEN | `A68` | `(vacía)` | `FASE 2: AUDITORÍA NORMATIVA Y DATOS PENDIENTES` | FASE 2: AUDITORÍA NORMATIVA Y DATOS PENDIENTES |
| RESUMEN | `A70` | `(vacía)` | `Datos geométricos` | Geom. y signos |
| RESUMEN | `A71` | `(vacía)` | `Datos de servicio` | 15.2.2/4/5 |
| RESUMEN | `A72` | `(vacía)` | `Estado de resistencia` | 15.2.1; φ/materiales |
| RESUMEN | `A73` | `(vacía)` | `q física de servicio` | 15.2.2/3 + EMS |
| RESUMEN | `A74` | `(vacía)` | `Área efectiva geotécnica` | E.050 28 |
| RESUMEN | `A75` | `(vacía)` | `Contacto de servicio` | 15.2.3 |
| RESUMEN | `A76` | `(vacía)` | `EMS / inclinación` | E.050 29 |
| RESUMEN | `A77` | `(vacía)` | `Fuente del EMS` | E.060 15.2.2; E.050 22 |
| RESUMEN | `A78` | `(vacía)` | `Equilibrio X` | ∑F y∑My |
| RESUMEN | `A79` | `(vacía)` | `Equilibrio Y` | ∑F y∑Mx |
| RESUMEN | `A80` | `(vacía)` | `Punzonamiento` | 11.12; cuatro esquinas |
| RESUMEN | `A81` | `(vacía)` | `Cortante unidireccional` | 11.12.1.1/15.5 |
| RESUMEN | `A82` | `(vacía)` | `Acero global inferior/superior` | 15.4.2 en caras |
| RESUMEN | `A83` | `(vacía)` | `Distribución rectangular X` | 15.4.4.1/2 |
| RESUMEN | `A84` | `(vacía)` | `Distribución rectangular Y` | 15.4.4.1/2 |
| RESUMEN | `A85` | `(vacía)` | `Desarrollo de parrillas` | 15.6/12.2 |
| RESUMEN | `A86` | `(vacía)` | `Acero local por momentos` | 13.5.3.1/3 |
| RESUMEN | `A87` | `(vacía)` | `Altura sobre refuerzo` | Artículo 15.7 |
| RESUMEN | `A88` | `(vacía)` | `Transferencia columna–zapata` | 15.8 /10.17/12.3/11.7 |
| RESUMEN | `A89` | `(vacía)` | `Deslizamiento` | Criterio del usuario |
| RESUMEN | `A90` | `(vacía)` | `Volteo` | Criterio del usuario |
| RESUMEN | `A91` | `(vacía)` | `Recubrimiento` | 7.7.1 |
| RESUMEN | `A92` | `(vacía)` | `Separación libre` | 7.6.1 y3.3.2 |
| RESUMEN | `A93` | `(vacía)` | `Datos adicionales Fase 2` | Dominio de entradas nuevas |
| RESUMEN | `A94` | `(vacía)` | `fc mínimo normativo` | E.060 5.1.1: >=17MPa |
| RESUMEN | `A95` | `(vacía)` | `Controles NO CUMPLE` | Incumplimientos comprobados, separados de verificaciones pendientes. |
| RESUMEN | `A96` | `(vacía)` | `Controles REQUIERE DATOS` | No se ocultaron en NO CUMPLE. |
| RESUMEN | `A97` | `(vacía)` | `Controles ANÁLISIS ESPECIAL` | Contacto parcial, flexocompresión/empalmes específicos. |
| RESUMEN | `A98` | `(vacía)` | `Controles FUERA DE ALCANCE` | No recicla perímetros ni desarrollo ajenos al dominio. |
| RESUMEN | `A99` | `(vacía)` | `Prioridad de estado global` | La tabla anterior conserva simultáneamente incumplimientos y pendientes. |
| RESUMEN | `B10` | `=res_srv_p_tot` | `=IF(srv_input_state="OK",res_srv_p_tot,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B11` | `=res_srv_mx_tot` | `=IF(srv_input_state="OK",res_srv_mx_tot,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B12` | `=res_srv_my_tot` | `=IF(srv_input_state="OK",res_srv_my_tot,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B13` | `=res_srv_ex` | `=IF(srv_input_state="OK",res_srv_ex,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B14` | `=res_srv_ey` | `=IF(srv_input_state="OK",res_srv_ey,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B15` | `=q_srv_max` | `=IF(srv_input_state="OK",q_srv_max,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B16` | `=q_srv_min` | `=IF(srv_input_state="OK",q_srv_min,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B18` | `=q_u_max` | `=IF(ult_input_state="OK",q_u_max,"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| RESUMEN | `B19` | `=q_u_min` | `=IF(ult_input_state="OK",q_u_min,"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| RESUMEN | `B23` | `=IF(OR(PRESIONES_SERVICIO!D14<>"CONTACTO COMPLETO",struct_state<>"OK"),"REQUIERE REVISIÓN DE CONTACTO / DATOS",IF(punz_state<>"OK",punz_state,IF(AND(q_srv_max<=inp_qadm,punz_result="CUMPLE",cort_result="CUMPLE",acero_result="CUMPLE",acero_sep_result="CUMPLE",geo_col_inside_status="CUMPLE",eq_x="OK",eq_y="OK"),IF(PUNZONAMIENTO!B57="SIN MOMENTO TRANSFERIDO","CUMPLE","ADVERTENCIA: VERIFICAR REFUERZO LOCAL γf Mu"),"NO CUMPLE")))` | `=IF(COUNTIF(B70:B94,"DATOS INVÁLIDOS")>0,"DATOS INVÁLIDOS",IF(COUNTIF(B70:B94,"FUERA DEL ALCANCE IMPLEMENTADO")>0,"FUERA DEL ALCANCE IMPLEMENTADO",IF(COUNTIF(B70:B94,"REQUIERE ANÁLISIS ESPECIAL")>0,"REQUIERE ANÁLISIS ESPECIAL",IF(COUNTIF(B70:B94,"NO CUMPLE")>0,"NO CUMPLE",IF(COUNTIF(B70:B94,"REQUIERE DATOS")>0,"REQUIERE DATOS","CUMPLE")))))` | Estado global no convierte limitaciones necesarias en CUMPLE; tablas mantienen fallos/pendientes separados. |
| RESUMEN | `B28` | `=IF(q_srv_max>inp_qadm,"ACTIVA","")` | `=IF(srv_input_state="OK",IF(q_srv_max>inp_qadm,"ACTIVA",""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B29` | `=IF(q_srv_min<0,"ACTIVA","")` | `=IF(srv_input_state="OK",IF(q_srv_min<0,"ACTIVA",""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B30` | `=IF(res_srv_nucleo<>"CUMPLE","ACTIVA","")` | `=IF(srv_input_state="OK",IF(res_srv_nucleo<>"CUMPLE","ACTIVA",""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B38` | `=IF(OR(srv_p<=0,ult_p<=0),"ACTIVA","")` | `=IF(srv_input_state="OK",IF(OR(srv_p<=0,ult_p<=0),"ACTIVA",""),"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `B62` | `=PUNZONAMIENTO!B57` | `=local_state` | Estado real del módulo local de momentos, no advertencia sin cálculo. |
| RESUMEN | `B70` | `(vacía)` | `=IF(geo_input_state="OK","CUMPLE","DATOS INVÁLIDOS")` | Geom. y signos |
| RESUMEN | `B71` | `(vacía)` | `=IF(srv_input_state="OK","CUMPLE",srv_input_state)` | 15.2.2/4/5 |
| RESUMEN | `B72` | `(vacía)` | `=IF(struct_state="OK","CUMPLE",struct_state)` | 15.2.1; φ/materiales |
| RESUMEN | `B73` | `(vacía)` | `=q_srv_qadm_status` | 15.2.2/3 + EMS |
| RESUMEN | `B74` | `(vacía)` | `=IF(g_eff_state="EXCENTRICIDAD FUERA DEL DOMINIO DE CIMENTACIÓN","REQUIERE ANÁLISIS ESPECIAL",g_eff_result)` | E.050 28 |
| RESUMEN | `B75` | `(vacía)` | `=IF(srv_input_state<>"OK",srv_input_state,IF(PRESIONES_SERVICIO!D14="CONTACTO COMPLETO","CUMPLE","REQUIERE ANÁLISIS ESPECIAL"))` | 15.2.3 |
| RESUMEN | `B76` | `(vacía)` | `=g_incl_result` | E.050 29 |
| RESUMEN | `B77` | `(vacía)` | `=IF(LEN(inp_ems_ref)>0,"CUMPLE","REQUIERE DATOS")` | E.060 15.2.2; E.050 22 |
| RESUMEN | `B78` | `(vacía)` | `=IF(eq_x="OK","CUMPLE",IF(eq_x="ERROR","NO CUMPLE",eq_x))` | ∑F y∑My |
| RESUMEN | `B79` | `(vacía)` | `=IF(eq_y="OK","CUMPLE",IF(eq_y="ERROR","NO CUMPLE",eq_y))` | ∑F y∑Mx |
| RESUMEN | `B80` | `(vacía)` | `=punz_result` | 11.12; cuatro esquinas |
| RESUMEN | `B81` | `(vacía)` | `=cort_result` | 11.12.1.1/15.5 |
| RESUMEN | `B82` | `(vacía)` | `=acero_result` | 15.4.2 en caras |
| RESUMEN | `B83` | `(vacía)` | `=dist_x_state` | 15.4.4.1/2 |
| RESUMEN | `B84` | `(vacía)` | `=dist_y_state` | 15.4.4.1/2 |
| RESUMEN | `B85` | `(vacía)` | `=ld_state` | 15.6/12.2 |
| RESUMEN | `B86` | `(vacía)` | `=local_state` | 13.5.3.1/3 |
| RESUMEN | `B87` | `(vacía)` | `=hmin_state` | Artículo 15.7 |
| RESUMEN | `B88` | `(vacía)` | `=iface_state` | 15.8 /10.17/12.3/11.7 |
| RESUMEN | `B89` | `(vacía)` | `=slide_state` | Criterio del usuario |
| RESUMEN | `B90` | `(vacía)` | `=over_state` | Criterio del usuario |
| RESUMEN | `B91` | `(vacía)` | `=cover_state` | 7.7.1 |
| RESUMEN | `B92` | `(vacía)` | `=clear_spacing_state` | 7.6.1 y3.3.2 |
| RESUMEN | `B93` | `(vacía)` | `=extra_input_state` | Dominio de entradas nuevas |
| RESUMEN | `B94` | `(vacía)` | `=fcmin_state` | E.060 5.1.1: >=17MPa |
| RESUMEN | `B95` | `(vacía)` | `=COUNTIF(B70:B94,"NO CUMPLE")` | Incumplimientos comprobados, separados de verificaciones pendientes. |
| RESUMEN | `B96` | `(vacía)` | `=COUNTIF(B70:B94,"REQUIERE DATOS")` | No se ocultaron en NO CUMPLE. |
| RESUMEN | `B97` | `(vacía)` | `=COUNTIF(B70:B94,"REQUIERE ANÁLISIS ESPECIAL")` | Contacto parcial, flexocompresión/empalmes específicos. |
| RESUMEN | `B98` | `(vacía)` | `=COUNTIF(B70:B94,"FUERA DEL ALCANCE IMPLEMENTADO")` | No recicla perímetros ni desarrollo ajenos al dominio. |
| RESUMEN | `B99` | `(vacía)` | `INVÁLIDOS > FUERA ALCANCE > ANÁLISIS ESPECIAL > NO CUMPLE > REQUIERE DATOS > CUMPLE` | La tabla anterior conserva simultáneamente incumplimientos y pendientes. |
| RESUMEN | `C70` | `(vacía)` | `-` | Geom. y signos |
| RESUMEN | `C71` | `(vacía)` | `-` | 15.2.2/4/5 |
| RESUMEN | `C72` | `(vacía)` | `-` | 15.2.1; φ/materiales |
| RESUMEN | `C73` | `(vacía)` | `-` | 15.2.2/3 + EMS |
| RESUMEN | `C74` | `(vacía)` | `-` | E.050 28 |
| RESUMEN | `C75` | `(vacía)` | `-` | 15.2.3 |
| RESUMEN | `C76` | `(vacía)` | `-` | E.050 29 |
| RESUMEN | `C77` | `(vacía)` | `-` | E.060 15.2.2; E.050 22 |
| RESUMEN | `C78` | `(vacía)` | `-` | ∑F y∑My |
| RESUMEN | `C79` | `(vacía)` | `-` | ∑F y∑Mx |
| RESUMEN | `C80` | `(vacía)` | `-` | 11.12; cuatro esquinas |
| RESUMEN | `C81` | `(vacía)` | `-` | 11.12.1.1/15.5 |
| RESUMEN | `C82` | `(vacía)` | `-` | 15.4.2 en caras |
| RESUMEN | `C83:C84` | `(vacía)` | `-` | 15.4.4.1/2 |
| RESUMEN | `C85` | `(vacía)` | `-` | 15.6/12.2 |
| RESUMEN | `C86` | `(vacía)` | `-` | 13.5.3.1/3 |
| RESUMEN | `C87` | `(vacía)` | `-` | Artículo 15.7 |
| RESUMEN | `C88` | `(vacía)` | `-` | 15.8 /10.17/12.3/11.7 |
| RESUMEN | `C89:C90` | `(vacía)` | `-` | Criterio del usuario |
| RESUMEN | `C91` | `(vacía)` | `-` | 7.7.1 |
| RESUMEN | `C92` | `(vacía)` | `-` | 7.6.1 y3.3.2 |
| RESUMEN | `C93` | `(vacía)` | `-` | Dominio de entradas nuevas |
| RESUMEN | `C94` | `(vacía)` | `-` | E.060 5.1.1: >=17MPa |
| RESUMEN | `C95` | `(vacía)` | `-` | Incumplimientos comprobados, separados de verificaciones pendientes. |
| RESUMEN | `C96` | `(vacía)` | `-` | No se ocultaron en NO CUMPLE. |
| RESUMEN | `C97` | `(vacía)` | `-` | Contacto parcial, flexocompresión/empalmes específicos. |
| RESUMEN | `C98` | `(vacía)` | `-` | No recicla perímetros ni desarrollo ajenos al dominio. |
| RESUMEN | `C99` | `(vacía)` | `-` | La tabla anterior conserva simultáneamente incumplimientos y pendientes. |
| RESUMEN | `D13:D14` | `=res_srv_nucleo` | `=IF(srv_input_state="OK",res_srv_nucleo,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `D15` | `=q_srv_qadm_status` | `=IF(srv_input_state="OK",q_srv_qadm_status,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `D16` | `=q_srv_uplift_status` | `=IF(srv_input_state="OK",q_srv_uplift_status,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `D19` | `=q_u_uplift_status` | `=IF(ult_input_state="OK",q_u_uplift_status,"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| RESUMEN | `D70` | `(vacía)` | `Geom. y signos` | Geom. y signos |
| RESUMEN | `D71` | `(vacía)` | `15.2.2/4/5` | 15.2.2/4/5 |
| RESUMEN | `D72` | `(vacía)` | `15.2.1; φ/materiales` | 15.2.1; φ/materiales |
| RESUMEN | `D73` | `(vacía)` | `15.2.2/3 + EMS` | 15.2.2/3 + EMS |
| RESUMEN | `D74` | `(vacía)` | `E.050 28` | E.050 28 |
| RESUMEN | `D75` | `(vacía)` | `15.2.3` | 15.2.3 |
| RESUMEN | `D76` | `(vacía)` | `E.050 29` | E.050 29 |
| RESUMEN | `D77` | `(vacía)` | `E.060 15.2.2; E.050 22` | E.060 15.2.2; E.050 22 |
| RESUMEN | `D78` | `(vacía)` | `∑F y∑My` | ∑F y∑My |
| RESUMEN | `D79` | `(vacía)` | `∑F y∑Mx` | ∑F y∑Mx |
| RESUMEN | `D80` | `(vacía)` | `11.12; cuatro esquinas` | 11.12; cuatro esquinas |
| RESUMEN | `D81` | `(vacía)` | `11.12.1.1/15.5` | 11.12.1.1/15.5 |
| RESUMEN | `D82` | `(vacía)` | `15.4.2 en caras` | 15.4.2 en caras |
| RESUMEN | `D83:D84` | `(vacía)` | `15.4.4.1/2` | 15.4.4.1/2 |
| RESUMEN | `D85` | `(vacía)` | `15.6/12.2` | 15.6/12.2 |
| RESUMEN | `D86` | `(vacía)` | `13.5.3.1/3` | 13.5.3.1/3 |
| RESUMEN | `D87` | `(vacía)` | `Artículo 15.7` | Artículo 15.7 |
| RESUMEN | `D88` | `(vacía)` | `15.8 /10.17/12.3/11.7` | 15.8 /10.17/12.3/11.7 |
| RESUMEN | `D89:D90` | `(vacía)` | `Criterio del usuario` | Criterio del usuario |
| RESUMEN | `D91` | `(vacía)` | `7.7.1` | 7.7.1 |
| RESUMEN | `D92` | `(vacía)` | `7.6.1 y3.3.2` | 7.6.1 y3.3.2 |
| RESUMEN | `D93` | `(vacía)` | `Dominio de entradas nuevas` | Dominio de entradas nuevas |
| RESUMEN | `D94` | `(vacía)` | `E.060 5.1.1: >=17MPa` | E.060 5.1.1: >=17MPa |
| RESUMEN | `D95` | `(vacía)` | `Incumplimientos comprobados, separados de verificaciones pendientes.` | Incumplimientos comprobados, separados de verificaciones pendientes. |
| RESUMEN | `D96` | `(vacía)` | `No se ocultaron en NO CUMPLE.` | No se ocultaron en NO CUMPLE. |
| RESUMEN | `D97` | `(vacía)` | `Contacto parcial, flexocompresión/empalmes específicos.` | Contacto parcial, flexocompresión/empalmes específicos. |
| RESUMEN | `D98` | `(vacía)` | `No recicla perímetros ni desarrollo ajenos al dominio.` | No recicla perímetros ni desarrollo ajenos al dominio. |
| RESUMEN | `D99` | `(vacía)` | `La tabla anterior conserva simultáneamente incumplimientos y pendientes.` | La tabla anterior conserva simultáneamente incumplimientos y pendientes. |
| RESUMEN | `F5` | `=res_u_p_tot` | `=IF(ult_input_state="OK",res_u_p_tot,"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| RESUMEN | `F6` | `=res_u_mx_tot` | `=IF(ult_input_state="OK",res_u_mx_tot,"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| RESUMEN | `F7` | `=res_u_my_tot` | `=IF(ult_input_state="OK",res_u_my_tot,"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| RESUMEN | `F8` | `=res_srv_nucleo` | `=IF(srv_input_state="OK",res_srv_nucleo,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `F9` | `=res_u_nucleo` | `=IF(ult_input_state="OK",res_u_nucleo,"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |
| RESUMEN | `H8` | `=res_srv_nucleo` | `=IF(srv_input_state="OK",res_srv_nucleo,"")` | Bloquear consumidores físicos de servicio cuando opciones/componentes no son válidos; no cero ficticio. |
| RESUMEN | `H9` | `=res_u_nucleo` | `=IF(ult_input_state="OK",res_u_nucleo,"")` | Bloquear presión/consumidores últimos con acciones o factores inválidos. |

## M–O. Nombres, nuevas entradas y validaciones

| Nombre nuevo | Destino |
|---|---|
| `bearing_col` | `ACERO_DETALLADO!$B$102` |
| `bearing_excess` | `ACERO_DETALLADO!$B$104` |
| `bearing_foot` | `ACERO_DETALLADO!$B$101` |
| `bearing_min` | `ACERO_DETALLADO!$B$103` |
| `clear_spacing_state` | `ACERO_DETALLADO!$B$144` |
| `cover_min_bottom` | `ACERO_DETALLADO!$B$171` |
| `cover_min_lat` | `ACERO_DETALLADO!$B$142` |
| `cover_min_top` | `ACERO_DETALLADO!$B$172` |
| `cover_state` | `ACERO_DETALLADO!$B$143` |
| `dist_x_state` | `ACERO_DETALLADO!$B$44` |
| `dist_y_state` | `ACERO_DETALLADO!$B$65` |
| `eq_fx` | `CARGAS!$C$33` |
| `eq_fy` | `CARGAS!$C$34` |
| `eq_mx` | `CARGAS!$C$36` |
| `eq_my` | `CARGAS!$C$37` |
| `eq_mz` | `CARGAS!$C$38` |
| `eq_p` | `CARGAS!$C$35` |
| `extra_input_state` | `GEOMETRIA!$B$2627` |
| `fac_sismo_opciones` | `BARRAS_PERU!$J$20:$J$21` |
| `fcmin_state` | `FLEXION_ACERO!$B$28` |
| `flex_beta1` | `FLEXION_ACERO!$B$25` |
| `fy_mpa` | `FLEXION_ACERO!$B$21` |
| `g_Aeff` | `PRESIONES_SERVICIO!$B$28` |
| `g_basis_state` | `PRESIONES_SERVICIO!$B$33` |
| `g_bx_eff` | `PRESIONES_SERVICIO!$B$25` |
| `g_by_eff` | `PRESIONES_SERVICIO!$B$26` |
| `g_eff_result` | `PRESIONES_SERVICIO!$B$35` |
| `g_eff_state` | `PRESIONES_SERVICIO!$B$27` |
| `g_ems_state` | `PRESIONES_SERVICIO!$B$39` |
| `g_ex` | `PRESIONES_SERVICIO!$B$23` |
| `g_ey` | `PRESIONES_SERVICIO!$B$24` |
| `g_H` | `PRESIONES_SERVICIO!$B$37` |
| `g_incl_result` | `PRESIONES_SERVICIO!$B$38` |
| `g_Mx` | `PRESIONES_SERVICIO!$B$21` |
| `g_My` | `PRESIONES_SERVICIO!$B$22` |
| `g_Q` | `PRESIONES_SERVICIO!$B$20` |
| `g_qadm` | `PRESIONES_SERVICIO!$B$32` |
| `g_qadm_factor` | `PRESIONES_SERVICIO!$B$31` |
| `g_qeff` | `PRESIONES_SERVICIO!$B$34` |
| `g_qeff_gross` | `PRESIONES_SERVICIO!$B$29` |
| `g_qphysical` | `PRESIONES_SERVICIO!$B$36` |
| `h_above_rebar` | `GEOMETRIA!$B$2622` |
| `h_col_anchor_state` | `GEOMETRIA!$B$2625` |
| `hmin_state` | `GEOMETRIA!$B$2624` |
| `iface_Ag` | `ACERO_DETALLADO!$B$98` |
| `iface_anchor_state` | `ACERO_DETALLADO!$B$126` |
| `iface_Ascomp` | `ACERO_DETALLADO!$B$106` |
| `iface_Ascont` | `ACERO_DETALLADO!$B$109` |
| `iface_Asdow` | `ACERO_DETALLADO!$B$110` |
| `iface_Asmin` | `ACERO_DETALLADO!$B$105` |
| `iface_Asreal` | `ACERO_DETALLADO!$B$111` |
| `iface_Asreq` | `ACERO_DETALLADO!$B$108` |
| `iface_Asstate` | `ACERO_DETALLADO!$B$112` |
| `iface_Astens` | `ACERO_DETALLADO!$B$107` |
| `iface_Avf_req` | `ACERO_DETALLADO!$B$130` |
| `iface_data_state` | `ACERO_DETALLADO!$B$97` |
| `iface_H` | `ACERO_DETALLADO!$B$128` |
| `iface_lateral_state` | `ACERO_DETALLADO!$B$132` |
| `iface_moment_state` | `ACERO_DETALLADO!$B$134` |
| `iface_mu` | `ACERO_DETALLADO!$B$129` |
| `iface_state` | `ACERO_DETALLADO!$B$136` |
| `iface_Vlimit` | `ACERO_DETALLADO!$B$131` |
| `inp_agg` | `INGRESO_DATOS!$C$91` |
| `inp_avf` | `INGRESO_DATOS!$C$121` |
| `inp_avf_anchor` | `INGRESO_DATOS!$C$122` |
| `inp_bar_col` | `INGRESO_DATOS!$C$110` |
| `inp_bar_dowel` | `INGRESO_DATOS!$C$113` |
| `inp_bottom_exposure` | `INGRESO_DATOS!$C$151` |
| `inp_col_system` | `INGRESO_DATOS!$C$107` |
| `inp_concrete_type` | `INGRESO_DATOS!$C$85` |
| `inp_edge_dir` | `INGRESO_DATOS!$C$81` |
| `inp_ems_incl` | `INGRESO_DATOS!$C$79` |
| `inp_ems_ref` | `INGRESO_DATOS!$C$80` |
| `inp_end_col` | `INGRESO_DATOS!$C$119` |
| `inp_end_inf` | `INGRESO_DATOS!$C$87` |
| `inp_end_sup` | `INGRESO_DATOS!$C$90` |
| `inp_epoxy` | `INGRESO_DATOS!$C$88` |
| `inp_eq_factor` | `INGRESO_DATOS!$C$76` |
| `inp_fc_col` | `INGRESO_DATOS!$C$108` |
| `inp_fs_over` | `INGRESO_DATOS!$C$131` |
| `inp_fs_over_ref` | `INGRESO_DATOS!$C$132` |
| `inp_fs_slide` | `INGRESO_DATOS!$C$126` |
| `inp_fs_slide_ref` | `INGRESO_DATOS!$C$127` |
| `inp_fy_col` | `INGRESO_DATOS!$C$109` |
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
| `inp_local_detail` | `INGRESO_DATOS!$C$92` |
| `inp_n_col` | `INGRESO_DATOS!$C$111` |
| `inp_n_continue` | `INGRESO_DATOS!$C$112` |
| `inp_n_dowel` | `INGRESO_DATOS!$C$114` |
| `inp_ncx` | `INGRESO_DATOS!$C$137` |
| `inp_ncy` | `INGRESO_DATOS!$C$141` |
| `inp_nloc_ix` | `INGRESO_DATOS!$C$93` |
| `inp_nloc_iy` | `INGRESO_DATOS!$C$94` |
| `inp_nloc_sx` | `INGRESO_DATOS!$C$95` |
| `inp_nloc_sy` | `INGRESO_DATOS!$C$96` |
| `inp_nox` | `INGRESO_DATOS!$C$138` |
| `inp_nox_minus` | `INGRESO_DATOS!$C$145` |
| `inp_nox_plus` | `INGRESO_DATOS!$C$146` |
| `inp_noy` | `INGRESO_DATOS!$C$142` |
| `inp_noy_minus` | `INGRESO_DATOS!$C$147` |
| `inp_noy_plus` | `INGRESO_DATOS!$C$148` |
| `inp_passive` | `INGRESO_DATOS!$C$128` |
| `inp_qadm_basis` | `INGRESO_DATOS!$C$77` |
| `inp_qadm_inc` | `INGRESO_DATOS!$C$75` |
| `inp_rebar_type` | `INGRESO_DATOS!$C$84` |
| `inp_rec_lat` | `INGRESO_DATOS!$C$86` |
| `inp_rpassive` | `INGRESO_DATOS!$C$129` |
| `inp_rpassive_ref` | `INGRESO_DATOS!$C$130` |
| `inp_scx` | `INGRESO_DATOS!$C$135` |
| `inp_scy` | `INGRESO_DATOS!$C$139` |
| `inp_side_exposure` | `INGRESO_DATOS!$C$89` |
| `inp_sigma0` | `INGRESO_DATOS!$C$78` |
| `inp_sox` | `INGRESO_DATOS!$C$136` |
| `inp_soy` | `INGRESO_DATOS!$C$140` |
| `inp_srv_type` | `INGRESO_DATOS!$C$74` |
| `inp_top_exposure` | `INGRESO_DATOS!$C$152` |
| `ld_inf_x` | `ACERO_DETALLADO!$G$73` |
| `ld_inf_y` | `ACERO_DETALLADO!$G$74` |
| `ld_state` | `ACERO_DETALLADO!$B$78` |
| `ld_sup_x` | `ACERO_DETALLADO!$G$75` |
| `ld_sup_y` | `ACERO_DETALLADO!$G$76` |
| `local_state` | `ACERO_DETALLADO!$B$91` |
| `over_state` | `PRESIONES_SERVICIO!$B$55` |
| `phi_bearing` | `ACERO_DETALLADO!$B$100` |
| `punz_domain` | `PUNZONAMIENTO!$B$65` |
| `punz_geom_state` | `PUNZONAMIENTO!$B$64` |
| `rho_bal` | `FLEXION_ACERO!$B$26` |
| `rho_eff` | `FLEXION_ACERO!$B$23` |
| `rho_max` | `FLEXION_ACERO!$B$27` |
| `rho_norm` | `FLEXION_ACERO!$B$22` |
| `slide_FS` | `PRESIONES_SERVICIO!$B$45` |
| `slide_Rfr` | `PRESIONES_SERVICIO!$B$43` |
| `slide_Rpass` | `PRESIONES_SERVICIO!$B$44` |
| `slide_state` | `PRESIONES_SERVICIO!$B$47` |
| `srv_input_state` | `PRESIONES_SERVICIO!$B$19` |
| `steel_B` | `ACERO_DETALLADO!$B$22` |
| `steel_beta` | `ACERO_DETALLADO!$B$23` |
| `steel_gamma` | `ACERO_DETALLADO!$B$24` |
| `steel_L` | `ACERO_DETALLADO!$B$21` |
| `top_rebar_needed` | `ACERO_DETALLADO!$B$173` |
| `ult_input_state` | `PRESIONES_ULTIMAS!$B$25` |
| `zone_x_state` | `ACERO_DETALLADO!$B$156` |
| `zone_y_state` | `ACERO_DETALLADO!$B$168` |

### Nuevas entradas editables: datos vacíos explícitos y valores predeterminados

| Celda | Nombre | Etiqueta | Valor/fórmula inicial | Unidad |
|---|---|---|---|---|
| `INGRESO_DATOS!C91` | `inp_agg` | Diámetro máximo agregado | `(vacía)` | cm |
| `INGRESO_DATOS!C121` | `inp_avf` | Refuerzo Avf dedicado a cortante | `(vacía)` | cm2 |
| `INGRESO_DATOS!C122` | `inp_avf_anchor` | Avf anclado en ambos lados | `(vacía)` | - |
| `INGRESO_DATOS!C110` | `inp_bar_col` | Barra longitudinal columna | `(vacía)` | - |
| `INGRESO_DATOS!C113` | `inp_bar_dowel` | Barra de dowels adicionales | `(vacía)` | - |
| `INGRESO_DATOS!C151` | `inp_bottom_exposure` | Exposición de cara inferior | `CONTRA SUELO` | - |
| `INGRESO_DATOS!C107` | `inp_col_system` | Sistema columna/pedestal | `IN SITU` | - |
| `INGRESO_DATOS!C85` | `inp_concrete_type` | Tipo de concreto | `NORMAL` | - |
| `INGRESO_DATOS!C81` | `inp_edge_dir` | Orientación del borde libre | `NO APLICA` | - |
| `INGRESO_DATOS!C79` | `inp_ems_incl` | EMS contempla carga inclinada | `NO CONFIRMADO` | - |
| `INGRESO_DATOS!C80` | `inp_ems_ref` | Referencia del EMS / qadm | `(vacía)` | - |
| `INGRESO_DATOS!C119` | `inp_end_col` | Terminación columna/dowels | `(vacía)` | - |
| `INGRESO_DATOS!C87` | `inp_end_inf` | Terminación barras inferiores | `(vacía)` | - |
| `INGRESO_DATOS!C90` | `inp_end_sup` | Terminación barras superiores | `(vacía)` | - |
| `INGRESO_DATOS!C88` | `inp_epoxy` | Revestimiento de barras | `(vacía)` | - |
| `INGRESO_DATOS!C76` | `inp_eq_factor` | Factor sísmico para suelo | `1` | - |
| `INGRESO_DATOS!C108` | `inp_fc_col` | f'c columna/pedestal | `(vacía)` | kgf/cm2 |
| `INGRESO_DATOS!C131` | `inp_fs_over` | FS requerido volteo | `(vacía)` | - |
| `INGRESO_DATOS!C132` | `inp_fs_over_ref` | Fuente FS volteo | `(vacía)` | - |
| `INGRESO_DATOS!C126` | `inp_fs_slide` | FS requerido deslizamiento | `(vacía)` | - |
| `INGRESO_DATOS!C127` | `inp_fs_slide_ref` | Fuente FS deslizamiento | `(vacía)` | - |
| `INGRESO_DATOS!C109` | `inp_fy_col` | fy barras columna/dowels | `(vacía)` | kgf/cm2 |
| `INGRESO_DATOS!C120` | `inp_joint` | Condición de la junta | `(vacía)` | - |
| `INGRESO_DATOS!C123` | `inp_joint_ref` | Referencia del detalle de junta | `(vacía)` | - |
| `INGRESO_DATOS!C116` | `inp_lcol_above` | Anclaje columna lado superior | `(vacía)` | cm |
| `INGRESO_DATOS!C115` | `inp_lcol_foot` | Anclaje columna en zapata | `(vacía)` | cm |
| `INGRESO_DATOS!C118` | `inp_ldow_above` | Anclaje dowels lado superior | `(vacía)` | cm |
| `INGRESO_DATOS!C117` | `inp_ldow_foot` | Anclaje dowels en zapata | `(vacía)` | cm |
| `INGRESO_DATOS!C97` | `inp_ll_ix_m` | Anclaje local inferior X, lado - | `(vacía)` | cm |
| `INGRESO_DATOS!C98` | `inp_ll_ix_p` | Anclaje local inferior X, lado + | `(vacía)` | cm |
| `INGRESO_DATOS!C99` | `inp_ll_iy_m` | Anclaje local inferior Y, lado - | `(vacía)` | cm |
| `INGRESO_DATOS!C100` | `inp_ll_iy_p` | Anclaje local inferior Y, lado + | `(vacía)` | cm |
| `INGRESO_DATOS!C101` | `inp_ll_sx_m` | Anclaje local superior X, lado - | `(vacía)` | cm |
| `INGRESO_DATOS!C102` | `inp_ll_sx_p` | Anclaje local superior X, lado + | `(vacía)` | cm |
| `INGRESO_DATOS!C103` | `inp_ll_sy_m` | Anclaje local superior Y, lado - | `(vacía)` | cm |
| `INGRESO_DATOS!C104` | `inp_ll_sy_p` | Anclaje local superior Y, lado + | `(vacía)` | cm |
| `INGRESO_DATOS!C92` | `inp_local_detail` | Detalle local concentrado confirmado | `(vacía)` | - |
| `INGRESO_DATOS!C111` | `inp_n_col` | N total barras de columna | `(vacía)` | barras |
| `INGRESO_DATOS!C112` | `inp_n_continue` | N barras que continúan | `(vacía)` | barras |
| `INGRESO_DATOS!C114` | `inp_n_dowel` | N dowels adicionales | `(vacía)` | barras |
| `INGRESO_DATOS!C137` | `inp_ncx` | N real barras X en franja central | `(vacía)` | barras |
| `INGRESO_DATOS!C141` | `inp_ncy` | N real barras Y en franja central | `(vacía)` | barras |
| `INGRESO_DATOS!C93` | `inp_nloc_ix` | N barras locales inferiores X | `(vacía)` | barras |
| `INGRESO_DATOS!C94` | `inp_nloc_iy` | N barras locales inferiores Y | `(vacía)` | barras |
| `INGRESO_DATOS!C95` | `inp_nloc_sx` | N barras locales superiores X | `(vacía)` | barras |
| `INGRESO_DATOS!C96` | `inp_nloc_sy` | N barras locales superiores Y | `(vacía)` | barras |
| `INGRESO_DATOS!C138` | `inp_nox` | N real barras X fuera de franja | `(vacía)` | barras |
| `INGRESO_DATOS!C145` | `inp_nox_minus` | N X exterior lado -Y | `(vacía)` | barras |
| `INGRESO_DATOS!C146` | `inp_nox_plus` | N X exterior lado +Y | `(vacía)` | barras |
| `INGRESO_DATOS!C142` | `inp_noy` | N real barras Y fuera de franja | `(vacía)` | barras |
| `INGRESO_DATOS!C147` | `inp_noy_minus` | N Y exterior lado -X | `(vacía)` | barras |
| `INGRESO_DATOS!C148` | `inp_noy_plus` | N Y exterior lado +X | `(vacía)` | barras |
| `INGRESO_DATOS!C128` | `inp_passive` | Considerar pasivo | `NO` | - |
| `INGRESO_DATOS!C77` | `inp_qadm_basis` | Base de qadm del EMS | `BRUTA` | - |
| `INGRESO_DATOS!C75` | `inp_qadm_inc` | Incrementar qadm 30% | `NO` | - |
| `INGRESO_DATOS!C84` | `inp_rebar_type` | Tipo de refuerzo | `CORRUGADAS` | - |
| `INGRESO_DATOS!C86` | `inp_rec_lat` | Recubrimiento lateral real | `(vacía)` | cm |
| `INGRESO_DATOS!C129` | `inp_rpassive` | Resistencia pasiva disponible | `(vacía)` | tf |
| `INGRESO_DATOS!C130` | `inp_rpassive_ref` | Fuente resistencia pasiva | `(vacía)` | - |
| `INGRESO_DATOS!C135` | `inp_scx` | Separación central inferior X | `=inp_sep_inf_x` | cm |
| `INGRESO_DATOS!C139` | `inp_scy` | Separación central inferior Y | `=inp_sep_inf_y` | cm |
| `INGRESO_DATOS!C89` | `inp_side_exposure` | Condición del recubrimiento lateral | `(vacía)` | - |
| `INGRESO_DATOS!C78` | `inp_sigma0` | sigma0 de referencia EMS | `(vacía)` | tf/m2 |
| `INGRESO_DATOS!C136` | `inp_sox` | Separación exterior inferior X | `=inp_sep_inf_x` | cm |
| `INGRESO_DATOS!C140` | `inp_soy` | Separación exterior inferior Y | `=inp_sep_inf_y` | cm |
| `INGRESO_DATOS!C74` | `inp_srv_type` | Tipo de caso de servicio | `GRAVEDAD` | - |
| `INGRESO_DATOS!C152` | `inp_top_exposure` | Exposición de cara superior | `CONTACTO SUELO` | - |

`CARGAS!C33:C38` son seis componentes sísmicas, vacías por defecto. Se necesitan solo con factor .8. Se mantienen todos los ingresos originales; las nuevas celdas de detalle se identifican por nombre y descripción al lado de la entrada.

| Validación nueva | Lista / rango |
|---|---|
| `INGRESO_DATOS!C74` | `GRAVEDAD,SISMO,VIENTO,OTRO` |
| `INGRESO_DATOS!C75` | `NO,SI` |
| `INGRESO_DATOS!C77` | `BRUTA,NETA` |
| `INGRESO_DATOS!C79` | `SI,NO,NO CONFIRMADO` |
| `INGRESO_DATOS!C81` | `NO APLICA,+X,-X,+Y,-Y,+X/+Y,+X/-Y,-X/+Y,-X/-Y` |
| `INGRESO_DATOS!C84` | `CORRUGADAS,LISAS,MALLA SOLDADA` |
| `INGRESO_DATOS!C85` | `NORMAL,LIVIANO` |
| `INGRESO_DATOS!C87` | `RECTA,GANCHO` |
| `INGRESO_DATOS!C88` | `SIN EPOXI,EPOXI` |
| `INGRESO_DATOS!C89` | `CONTRA SUELO,CONTACTO SUELO,INTERIOR` |
| `INGRESO_DATOS!C90` | `RECTA,GANCHO` |
| `INGRESO_DATOS!C92` | `SI,NO` |
| `INGRESO_DATOS!C107` | `IN SITU,PREFABRICADA` |
| `INGRESO_DATOS!C110` | `=bar_codes` |
| `INGRESO_DATOS!C113` | `=bar_codes` |
| `INGRESO_DATOS!C119` | `RECTA,GANCHO` |
| `INGRESO_DATOS!C120` | `MONOLITICA,RUGOSA,LISA` |
| `INGRESO_DATOS!C122` | `SI,NO` |
| `INGRESO_DATOS!C128` | `NO,SI` |
| `INGRESO_DATOS!C151` | `CONTRA SUELO,CONTACTO SUELO,INTERIOR` |
| `INGRESO_DATOS!C152` | `CONTRA SUELO,CONTACTO SUELO,INTERIOR` |
| `INGRESO_DATOS!C76` | `=fac_sismo_opciones` |

Las entradas numéricas nuevas se comprueban además mediante `GEOMETRIA!B2627`, módulos locales y RESUMEN: enteros/conteos, no negativos/positivos, selecciones válidas. Pegar texto/negativos no puede evitar los controles por saltar un dropdown. Las reglas CF nuevas usan igualdad exacta: CUMPLE/OK/NO APLICA verde, NO CUMPLE/DATOS INVÁLIDOS/ERROR rojo, pendientes o fuera de alcance amarillo. Se preservan también las reglas anteriores y se comprobó el color efectivo de estados nativos.

### Bloques y extensiones de formato
- `INGRESO_DATOS!A74:H132`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `CARGAS!A32:H38`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `PRESIONES_SERVICIO!A19:H39`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `FLEXION_ACERO!A21:I27`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `FLEXION_ACERO!A28:I28`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `PUNZONAMIENTO!A62:F66`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `INGRESO_DATOS!A135:H142`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `INGRESO_DATOS!A145:H148`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `INGRESO_DATOS!A151:H152`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `PRESIONES_ULTIMAS!A25:H25`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A28:J44`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A49:J65`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A148:J156`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A160:J168`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A72:J79`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `GEOMETRIA!A2622:J2625`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A85:J92`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A93:J93`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A137:J137`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A97:J136`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `PRESIONES_SERVICIO!A43:H55`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A142:J144`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `ACERO_DETALLADO!A171:J173`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `RESUMEN!A70:H99`: formato de tabla, notas, resultados visibles y alturas ajustadas.
- `GEOMETRIA!A2627:J2627`: formato de tabla, notas, resultados visibles y alturas ajustadas.

El registro incluye todos los cambios de contenido y nombres/validaciones nuevas. Las vistas auxiliares se conservaron localmente para la auditoría y no forman parte de los entregables publicados.
