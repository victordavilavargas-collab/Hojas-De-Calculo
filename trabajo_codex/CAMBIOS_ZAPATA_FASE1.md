# CAMBIOS ZAPATA FASE 1 - NTE E.060

Fecha: 30/09/2026, America/Lima. Corrección de un estado actual, sin ampliación a múltiples combinaciones.

## A-B. Archivos y repositorio

Origen, sin sobrescribir: `C:\Herramientas CSI\Excels\trabajo_codex\Diseño de zapata aislada.xlsx`.

Salida: `C:\Herramientas CSI\Excels\trabajo_codex\Diseño de zapata aislada_CORREGIDA_FASE1.xlsx`.

Repositorio: `victordavilavargas-collab/Hojas-De-Calculo`, rama `main`. La carpeta local heredaba inicialmente el repositorio CSI padre; el usuario autorizó crear un repositorio independiente en Excels. Se verificó que el original local y origin/main tenían el mismo blob Git `c904d8e2defdb2585578686ce5435c4de5a31743`. Se ejecutó pull del remoto correcto antes de crear y editar la copia.

SHA256 del original antes/después: `24f60a8b5a8b170de9ef528cc7f96120f0b5c651ccdad33acf8a6562965a7060`. La copia se editó y guardó exclusivamente mediante Microsoft Excel COM 16.0. openpyxl se utilizó solo para lectura, inventario y comparación; no regrabó el libro.

## C. Auditoría previa de estructura completa

Se inspeccionaron todas las hojas, entradas, fórmulas, resultados, vínculos entre hojas, nombres, validaciones, formato condicional, combinaciones de celdas, protección, impresión, gráficos y objetos antes de modificar fórmulas. El inventario previo y las vistas nativas se obtuvieron del original abierto en solo lectura y se cerró sin guardar.

| Hoja | Tamaño original | Fórmulas originales | Gráficos | Validaciones | Reglas CF | Rangos combinados | Protección |
|---|---:|---:|---:|---:|---:|---:|---|
| INGRESO_DATOS | 61 × 8 | 0 | 4 | 4 | 0 | 6 | False |
| BARRAS_PERU | 15 × 7 | 0 | 0 | 0 | 0 | 1 | False |
| CARGAS | 27 × 8 | 14 | 0 | 1 | 6 | 3 | False |
| GEOMETRIA | 2618 × 11 | 23419 | 0 | 0 | 4 | 3 | False |
| RESULTANTE | 12 × 14 | 29 | 0 | 0 | 3 | 5 | False |
| PRESIONES_SERVICIO | 15 × 8 | 10 | 0 | 0 | 6 | 1 | False |
| PRESIONES_ULTIMAS | 15 × 8 | 8 | 0 | 0 | 6 | 1 | False |
| DIAGRAMAS_X | 64 × 12 | 567 | 3 | 0 | 0 | 2 | False |
| DIAGRAMAS_Y | 64 × 12 | 567 | 3 | 0 | 0 | 2 | False |
| PUNZONAMIENTO | 19 × 6 | 16 | 0 | 0 | 3 | 2 | False |
| CORTANTE_UNIDIRECCIONAL | 13 × 8 | 31 | 0 | 0 | 3 | 2 | False |
| FLEXION_ACERO | 12 × 9 | 25 | 0 | 0 | 0 | 2 | False |
| ACERO_DETALLADO | 13 × 10 | 39 | 0 | 0 | 6 | 1 | False |
| GRAFICOS | 133 × 26 | 344 | 14 | 0 | 2 | 3 | False |
| RESUMEN | 38 × 8 | 59 | 0 | 0 | 12 | 4 | False |

Se conservaron las 15 hojas y su orden, los 24 gráficos y los 147 nombres definidos originales. Se añadieron 21 nombres para entradas/resultados de Fase 1. Sin imágenes embebidas, macros, hojas protegidas ni vínculos externos. Los atributos Locked originales no restringen edición porque ninguna hoja está protegida. Se conservaron dimensiones de columnas, comentarios, áreas de impresión, márgenes, opciones de impresión y paneles inmovilizados. En DIAGRAMAS_X, cuya configuración de página no estaba serializada en el original, el guardado nativo de Excel explicitó valores predeterminados: portrait, A4 (paperSize=9) y DPI=0. Las áreas y ajustes de exportación PDF para revisión se asignaron solamente en sesiones de lectura sin guardar.

### Entradas principales identificadas directamente

| Hoja / rango | Contenido |
|---|---|
| INGRESO_DATOS!C14:C26 | Materiales, pesos específicos, qadm, recubrimientos, φ, cuantía y separación máxima |
| INGRESO_DATOS!C30:C38 | Bx, By, h, desplante, pesos activados, altura de relleno y nx/ny |
| INGRESO_DATOS!C42:C50 | Columna, ubicación, traslado horizontal y convención P |
| INGRESO_DATOS!C54:C61 | Barras y separaciones adoptadas; preservadas |
| CARGAS!C7:C12 | Acciones de servicio originales, preservadas |
| CARGAS!C22:C27 | Acciones últimas originales, preservadas |
| INGRESO_DATOS!C65:C70 | Nuevas capas, tipo columna, identificación de caso y factores explícitos de pesos últimos |

### Celdas de cálculo y vínculos principales

`GEOMETRIA!B4:B14`, grilla `C18:K2618`; `RESULTANTE!B5:N6`; presiones en `PRESIONES_SERVICIO!D5:D15` y `PRESIONES_ULTIMAS!D5:D23`; tablas `DIAGRAMAS_X/Y!A14:L64` y extremos exactos `A70:D79`; punzonamiento `PUNZONAMIENTO!B4:B58`; cortante `CORTANTE_UNIDIRECCIONAL!B5:H8/B15:B23`; flexión `FLEXION_ACERO!D5:I8`; detalle `ACERO_DETALLADO!D5:J8`; resultados `RESUMEN!B23/A42:H64`. Todos los vínculos son fórmulas; no se reemplazaron por resultados estáticos.

## D. Problemas encontrados antes de editar

1. `PUNZONAMIENTO!B15` usaba una sola expresión `0.53*SQRT(inp_fc)*B11*B10/1000`, propia del orden de capacidad de cortante como viga, en lugar de la menor de las tres expresiones bidireccionales.
2. El punzonamiento omitía los dos momentos y γf/γv, Jcx/Jcy y los esfuerzos locales.
3. `B8/B9` ignoraban superposición física de barras; ambos peraltes eran 41.865 cm.
4. `B13/B14` mezclaban presión bruta con Pu de columna, omitían pesos descendentes interiores y recortaban signos mediante MAX.
5. `CARGAS!E9/E24` usaban ABS de P: una tracción podía convertirse en compresión.
6. GEOMETRIA, DIAGRAMAS y mapas GRAFICOS truncaban q negativa con MAX(0,q), sin reequilibrio.
7. Los diagramas distribuían P en la huella de columna, integraban numéricamente y omitían el momento concentrado; M de extremo tenía aproximadamente -0.22791 tf·m en X y +0.76969 tf·m en Y. Las caras se obtenían por búsqueda aproximada y podían ocultar falta de referencia mediante IFERROR(...,0).
8. Cortante utilizaba el mismo d mínimo para ambas direcciones y la presión del borde como promedio del voladizo crítico, sin integrar la pendiente.
9. Núcleo central biaxial comprobaba excentricidades por separado, sin sumar sus ratios.
10. El signo de primer momento de presión en Y y el traslado de Fy no correspondían a momentos de acciones sobre zapata según mano derecha.
11. Residuos de redondeo del momento negativo podían activar acero superior mínimo ficticio.
12. Las reglas antiguas por búsqueda de CUMPLE también podían coincidir con NO CUMPLE; se añadieron reglas exactas con prioridad y colores verificados.

## E, G-H. Criterio mecánico, unidades y signos

### Signos

`INGRESO_DATOS!C50` es `SIGNO_COMPRESION_P`, con validación +1/-1, valor inicial +1 para preservar el significado de las cargas positivas originales. `CARGAS!E9=inp_sign_p*C9`, `E24=inp_sign_p*C24`. P interno positivo comprime y P negativo conserva levantamiento/tracción y bloquea diseño. No se aplica ABS a la conversión de P. ABS se conserva legítimamente para magnitudes de cortante/momento y tolerancias de equilibrio.

Mx y My se interpretan como **acciones aplicadas sobre la zapata en ejes globales de mano derecha**. No son reacciones de apoyo sin convertir. `C48=-1` corrige el aporte `Mx=-Fy*zh`; `C49=+1` conserva `My=+Fx*zh`. Si se utilizan resultados de otra convención, el usuario debe convertirlos a estas acciones antes de ingresarlos. La importación automática está excluida de esta fase.

Para columna ubicada en (xc,yc), los primeros momentos del campo de presión son `Qx=Pu*xc+My` y `Qy=Pu*yc-Mx`. Por eso `RESULTANTE!F5/F6=-Mx+P*yc` y `G5/G6=My+P*xc`. Se rotularon F/G como primeros momentos de q; el equilibrio físico es `∫y*q dA-P*yc+Mx=0`, `-∫x*q dA+P*xc+My=0`. Las presiones brutas originales del caso centrado mantienen qmax/qmin: cambia el lado físico de mayor presión en Y.

### Método neto

Para servicio se conservan los pesos brutos activados. Para el estado último se explicitan los factores de pesos `C69/C70`, valor inicial 1, exactamente equivalente al original; **deben corresponder a la combinación última elegida**. `RESULTANTE!C6/D6` aplican esos factores. El libro no determina combinaciones ni factores de mayoración automáticamente.

La reacción bruta es `qbruto=(Pu+Wz,u+Ws,u)/A + Qx*x/Iy + Qy*y/Ix`. Para resistencia del cuerpo de zapata se emplea exclusivamente `qneto=qbruto-(Wz,u+Ws,u)/A = Pu/A+Qx*x/Iy+Qy*y/Ix`. Estos pesos se consideran uniformes y sus contribuciones ascendentes/descendentes se cancelan; no vuelven a incorporarse en Vu. Los factores modifican presión bruta y contacto, pero la prueba con pesos 1.4/1.7 confirmó invariancia de la demanda neta en contacto completo.

`PRESIONES_ULTIMAS!D20:D23` muestran q0 neta, gradientes y peso uniforme restado. `PUNZONAMIENTO!B13/B12/B30/B14` muestran qu media dentro de perímetro, área, reacción interior y `Vu=Pu-qu_neta*Acrit` sin recortar a cero. La integración rectangular del campo lineal es exacta por simetría alrededor de la columna.

Si qmin bruto <0 se conserva el valor negativo, se muestra **PÉRDIDA PARCIAL DE CONTACTO** y se bloquean cálculos dependientes con **REQUIERE ANÁLISIS DE CONTACTO PARCIAL**. No se implementó un solucionador de contacto parcial ni se presenta una grilla truncada como equilibrada.

## I. Capacidad de punzonamiento

Fuente principal: [NTE E.060, DS 010-2009-VIVIENDA, documento oficial](https://cdn.www.gob.pe/uploads/document/file/2686419/E.060%20Concreto%20Armado%20DS%20N%C2%B0%20010-2009.pdf), 11.12.1.1/2, 11.12.2.1, figura 11.12.6 y 13.5.3. No se sustituyó por otra edición ACI. También se revisaron 15.4 y 15.5 para secciones de flexión y cortante en zapatas.

Se mantienen kgf/cm² y cm. `1 kgf/cm²=0.0980665 MPa`, `1 tf=9806.65 N`. La conversión exacta común es `K=1/SQRT(0.0980665)=3.193299567810587`, visible en `B22`. Los coeficientes equivalentes son:

| Expresión SI | Coeficiente kgf/cm²-cm | Celda |
|---|---:|---|
| 0.17 | 0.5428609265277998 | B23 |
| 0.083 | 0.2650438641282787 | B24 |
| 0.33 | 1.0537888573774938 | B25 |

```text
Vc1 = 0.17*K*(1+2/β)*sqrt(fc)*bo*d/1000  [tf]
Vc2 = 0.083*K*(αs*d/bo+2)*sqrt(fc)*bo*d/1000 [tf]
Vc3 = 0.33*K*sqrt(fc)*bo*d/1000 [tf]
Vc = MIN(Vc1,Vc2,Vc3); φ=0.85; φVc=φ*Vc
```

β es lado largo/corto de columna. αs=40/30/20 según INTERIOR/BORDE/ESQUINA. La entrada de tipo está en `C66`, por defecto INTERIOR. BORDE/ESQUINA conservan sus parámetros pero no reutilizan el perímetro interior: falta especificar geometría/orientación del perímetro abierto y sus centroides/J. Se bloquean. Para INTERIOR se exige peralte positivo y distancia mínima al borde ≥ d+mitad del lado mayor de columna, como filtro conservador de aplicabilidad. Cerca de un borde libre se requiere evaluar los perímetros mínimos alternativos; no se certifica el completo automáticamente. `bo=2[(cx+d)+(cy+d)]`, a d/2 de caras, solamente dentro del dominio aceptado.

## J. Transferencia Mx/My y esfuerzos de punzonamiento

`B31=bx=cx+d`, `B32=by=cy+d`, en cm; `B33=Ac=bo*d`. Propiedades de sección crítica conforme figura 11.12.6:

```text
Jcx = d*by^3/6 + by*d^3/6 + d*bx*by^2/2 [cm4]
Jcy = d*bx^3/6 + bx*d^3/6 + d*by*bx^2/2 [cm4]
γfx = 1/(1+(2/3)*sqrt(by/bx)); γvx=1-γfx
γfy = 1/(1+(2/3)*sqrt(bx/by)); γvy=1-γfy
```

Se usó el γf básico de 13.5.3.1; no se incrementó mediante la excepción de 13.5.3.2. El benchmark cuadrado da γf=0.6 y γv=0.4; el caso rectangular tiene factores diferentes por eje.

Los momentos en el corte se calculan respecto al centroide del perímetro coincidente con columna interior:

```text
Mx,crit = Mx + gy*Acrit*(by/100)^2/12 [tf m]
My,crit = My - gx*Acrit*(bx/100)^2/12 [tf m]
vu(x,y)=Vu*1000/Ac - γvx*Mx,crit*100000*y/Jcx
                    + γvy*My,crit*100000*x/Jcy [kgf/cm2]
```

`B45/B46` incluyen la reacción neta interior, `B47/B48` presentan γf Mu por flexión; `B49:B52` evalúan las cuatro esquinas (±bx/2,±by/2) con ambos momentos simultáneos. `B38` es máxima **magnitud**, `B39` conserva mínimo con signo y `B58` máximo algebraico. Se compara conservadoramente la máxima magnitud con `B40=φVc*1000/Ac`; `B17=B38/B40`. Para Vu positivo y sin inversión el máximo absoluto coincide con el máximo algebraico pedido. La prueba biaxial 60/40 da D/C>1 pese a que Vu solo sí cumpliría.

El diseño global de acero por metro no demuestra por sí solo la concentración/anclaje de γf Mu exigida en 13.5.3.3. Se muestran momentos y anchos efectivos (cx/cy+3h, limitados al ancho de zapata) y una advertencia explícita en `B55:B57`, FLEXION y RESUMEN. Si todos los controles globales cumplieran, el resultado final seguiría en ADVERTENCIA mientras haya transferencia local pendiente; no se inventó un reparto local de acero.

## K. Peraltes efectivos

`C65` define X inferior/Y superior o la opción inversa. Para X inferior:

```text
dx=h*100-r_inf-dbX/2
dy=h*100-r_inf-dbX-dbY/2
d_punzonamiento=(dx+dy)/2
```

Con opción inversa se permutan los términos de superposición. El promedio representa el peralte de las dos capas ortogonales en el procedimiento bidireccional; la E.060 define d hasta refuerzo traccionado, y se adopta explícitamente este criterio de sección para dos capas. No se toma el mayor para aumentar capacidad. Flexión y cortante X/Y usan el valor físico individual. `C68` define cuál barra superior queda exterior, para E7/E8 de FLEXION cuando exista inversión.

## L-M. Corrección de DIAGRAMAS_X y DIAGRAMAS_Y

Se conservó la tabla de 51 filas y los 3 gráficos de cada hoja. Cada grilla tiene dos puntos coincidentes en la columna, antes/después de las acciones concentradas. nx/ny siguen editables entre 4 y 50; el extremo libre se alcanza aunque la división sea menor que 50. Los extremos de demanda se calculan con raíces y límites analíticos fuera de la tabla, por lo que no dependen de que una estación coincida con un máximo.

Para longitud L, `t=s+L/2`, centro de columna sc, `w_neta=a+b*t`:

```text
V=a*t+b*t^2/2-Pu*H(s-sc)
M=a*t^2/2+b*t^3/6-Pu*MAX(0,s-sc)+Mc*H(s-sc)
X: Mc=My; Y: Mc=-Mx
```

La idealización de P y M concentrados en el centro de la columna produce envolventes globales conservadoras cerca de su eje; las caras se muestran por integración exacta independiente de esa grilla. No se modela una distribución adicional de tensiones de contacto columna-zapata. MAX(0,s-sc) es la función de Macaulay de brazo geométrico, no un truncamiento de q. Los residuos <MAX(1E-8 tf m,1E-10*|Pu*L|) se normalizan solo en la **selección de demanda**, para evitar acero superior ficticio; los valores del diagrama y sus errores de cierre permanecen crudos.

## N. Equilibrio y cortante unidireccional

`DIAGRAMAS_X/Y!J4` = V final; `J5` = M final; `J6` = OK/ERROR. Se exige error ≤MAX(1E-6 tf,0.001|Pu|) y momento ≤MAX(1E-6 tf m,0.001 MAX(|Mc|,|Pu*L|)). El último punto no se fija a cero: se obtiene con la misma ley integral que los demás. También se comprobó cierre por cuadratura de Gauss independiente y se mantienen ambas comprobaciones en RESUMEN!B58:H60.

Cortante: corte a dx/dy desde la cara, integración de presión lineal neta sobre el voladizo exterior, resultados por metro. Capacidad como viga con 0.17 MPa convertido rigurosamente, φ=0.85 y b=100 cm. Se muestran por separado Vu, φVc, D/C y estado X/Y. La fórmula clásica de As por raíz cuadrática se preservó y se contrastó con una solución independiente por bisección de capacidad resistente.

## O. Benchmark y casos independientes

Con fc=210 kgf/cm², columna 40×40 cm, h=50 cm, recubrimiento=7.5 cm y barras 1/2 pulgada superpuestas:

| Resultado | Valor |
|---|---:|
| dx cm | 41.86500000 |
| dy cm | 40.59500000 |
| d medio cm | 41.23000000 |
| bo cm | 324.92000000 |
| Vc1 tf | 316.16170504 |
| Vc2 tf | 364.07198712 |
| Vc3 tf | 204.57522091 |
| Vc gobernante tf | 204.57522091 |
| φVc tf | 173.88893777 |
| Vu neto tf | 142.14215192 |
| vu_max kgf/cm² | 10.71359993 |
| φvn kgf/cm² | 12.98022364 |
| D/C biaxial actual | 0.82537869 |

Control manual con d=41.865 cm (un único nivel idealizado): Vc=209.349825 tf y φVc=177.947351 tf, próximos a 209/178 tf de referencia. **No se impuso ese peralte al libro**: el promedio real de capas es 41.23 cm, y por ello el resultado es 204.575/173.889 tf. El valor previo φVc≈89.498 tf provenía del coeficiente incorrecto de punzonamiento.

| Prueba nativa en copia descartable | Punzonamiento | Equilibrio X | Equilibrio Y | Errores Excel |
|---|---|---|---|---:|
| base | CUMPLE | OK | OK | 0 |
| benchmark-sin-momentos | CUMPLE | OK | OK | 0 |
| biaxial-60-40 | NO CUMPLE | OK | OK | 0 |
| biaxial-signos-inversos | NO CUMPLE | OK | OK | 0 |
| rectangular-descentrada | CUMPLE | OK | OK | 0 |
| gobierna-Vc1 | CUMPLE | OK | OK | 0 |
| gobierna-Vc2 | CUMPLE | OK | OK | 0 |
| capas-y-inferior | CUMPLE | OK | OK | 0 |
| compresion-con-signo-menos | CUMPLE | OK | OK | 0 |
| levantamiento-real | LEVANTAMIENTO / TRACCIÓN: NO DISEÑAR | LEVANTAMIENTO / TRACCIÓN: NO DISEÑAR | LEVANTAMIENTO / TRACCIÓN: NO DISEÑAR | 0 |
| contacto-parcial | REQUIERE ANÁLISIS DE CONTACTO PARCIAL | REQUIERE ANÁLISIS DE CONTACTO PARCIAL | REQUIERE ANÁLISIS DE CONTACTO PARCIAL | 0 |
| borde | REQUIERE GEOMETRÍA DE PERÍMETRO CRÍTICO | OK | OK | 0 |
| esquina | REQUIERE GEOMETRÍA DE PERÍMETRO CRÍTICO | OK | OK | 0 |
| interior-proximo-borde | REQUIERE GEOMETRÍA DE PERÍMETRO CRÍTICO | OK | OK | 0 |
| grilla-10-17 | CUMPLE | OK | OK | 0 |
| pesos-factorizados | CUMPLE | OK | OK | 0 |
| dimension-cero | DATOS / GEOMETRÍA INVÁLIDOS | DATOS / GEOMETRÍA INVÁLIDOS | DATOS / GEOMETRÍA INVÁLIDOS | 0 |
| barra-no-valida | DATOS / GEOMETRÍA INVÁLIDOS | DATOS / GEOMETRÍA INVÁLIDOS | DATOS / GEOMETRÍA INVÁLIDOS | 0 |
| peralte-no-positivo | PERALTE EFECTIVO NO POSITIVO | PERALTE EFECTIVO NO POSITIVO | PERALTE EFECTIVO NO POSITIVO | 0 |
| phi-no-E060 | REVISAR DATOS / PHI E.060 | REVISAR DATOS / PHI E.060 | REVISAR DATOS / PHI E.060 | 0 |

Verificación independiente: 1998 aserciones, 0 fallos. Incluye conversión SI de capacidades, cuadratura del área/perímetro crítico y de las franjas, momentos residuales, cuatro esfuerzos biaxiales, raíces/extremos, As por bisección, signo P, bloqueo físico, colores efectivos de Excel, nombres y persistencia guardado/recalculado/reabierto. Las pruebas cambian solo `prueba-descartable.xlsx`, y no se entregan ni guardan sus datos en el libro final.

### Estado del caso original preservado

- qmax servicio tf/m²: **11.15269476** (`PRESIONES_SERVICIO!D10`).

- qmin servicio tf/m²: **10.99358791** (`PRESIONES_SERVICIO!D11`).

- ERROR_FUERZAS_X tf: **0.00000000** (`DIAGRAMAS_X!J4`).

- ERROR_MOMENTOS_X tf m: **-0.00000000** (`DIAGRAMAS_X!J5`).

- ERROR_FUERZAS_Y tf: **-0.00000000** (`DIAGRAMAS_Y!J4`).

- ERROR_MOMENTOS_Y tf m: **-0.00000000** (`DIAGRAMAS_Y!J5`).

- D/C cortante X: **0.47673805** (`CORTANTE_UNIDIRECCIONAL!B17`).

- D/C cortante Y: **0.49852583** (`CORTANTE_UNIDIRECCIONAL!B22`).

- As requerido inferior X cm²/m: **12.21922571** (`FLEXION_ACERO!H5`).

- As requerido inferior Y cm²/m: **12.68199027** (`FLEXION_ACERO!H6`).

- As colocado X cm²/m: **8.60000000** (`ACERO_DETALLADO!H5`).

- As colocado Y cm²/m: **8.60000000** (`ACERO_DETALLADO!H6`).

- Resultado global: **NO CUMPLE** (`RESUMEN!B23`).

## P. Errores, compatibilidad, reapertura y preservación visual

Sin #REF!, #DIV/0!, #VALUE!, #NAME?, #N/A, #NUM! ni referencias circulares en el archivo final y las 20 pruebas. Durante la prueba de entradas inválidas se detectaron #VALUE! por AND sin cortocircuito y #N/A por una barra inexistente: se resolvieron con IF externo y comprobación del catálogo, sin IFERROR(...,0). Se corrigieron también las funciones de reglas CF a través de FormulaLocal de Excel español; sin _xlfn/_xludf en fórmulas de celda ni reglas CF.

Se ejecutó CalculateFullRebuild, guardado, cierre, apertura normal sin solicitud de reparación, recálculo, otro guardado/cierre y nueva apertura; las entradas y resultados críticos permanecieron iguales. Tras restaurar la posición inicial de RESUMEN y sus paneles se repitió recálculo/guardado y una última apertura normal en solo lectura; sus resultados coinciden con la caché del archivo final. Los procesos Excel creados para estas tareas se cerraron con Quit y liberación COM. Dos instancias ocultas que persistieron se identificaron por PID, se verificó que tenían cero libros abiertos y se cerraron; al final no quedaron procesos EXCEL. No se usaron instancias CSI.

Se revisaron vistas nativas de las 15 hojas y los 24 gráficos frente al original. Se conservan barras de encabezado, colores base, anchos, gráficos y disposición general. Se prolonga el formato original para resultados y entradas nuevas. Se ajustaron localmente alturas/wrap para textos nuevos. Se combinan únicamente rangos nuevos o espacios de advertencia necesarios. Se desplazó un gráfico preexistente que estaba debajo de INGRESO_DATOS y coincidía con el bloque C65:C70; no se eliminó ni cambió su contenido. La posición exacta antes/después se muestra en el inventario siguiente.

- INGRESO_DATOS, gráfico 2, Chart 6: antes `{'height': 198.42520141601562, 'name': 'Chart 6', 'width': 340.157470703125, 'series': 1, 'left': 172.8000030517578, 'top': 1654.800048828125}`; después `{'top': 1838.4000244140625, 'width': 340.157470703125, 'series': 1, 'height': 198.42520141601562, 'name': 'Chart 6', 'left': 172.8000030517578}`. Movimiento de anclaje debido a filas/textos nuevos; misma cantidad de series.

- DIAGRAMAS_X, gráfico 2, Chart 2: antes `{'height': 198.42520141601562, 'name': 'Chart 2', 'width': 396.85040283203125, 'series': 1, 'left': 1047.5999755859375, 'top': 361.20001220703125}`; después `{'top': 381.6000061035156, 'width': 396.85040283203125, 'series': 1, 'height': 198.42520141601562, 'name': 'Chart 2', 'left': 1047.5999755859375}`. Movimiento de anclaje debido a filas/textos nuevos; misma cantidad de series.

- DIAGRAMAS_X, gráfico 3, Chart 3: antes `{'height': 198.42520141601562, 'name': 'Chart 3', 'width': 396.85040283203125, 'series': 1, 'left': 1047.5999755859375, 'top': 606.0}`; después `{'top': 626.4000244140625, 'width': 396.85040283203125, 'series': 1, 'height': 198.42520141601562, 'name': 'Chart 3', 'left': 1047.5999755859375}`. Movimiento de anclaje debido a filas/textos nuevos; misma cantidad de series.

- DIAGRAMAS_Y, gráfico 2, Chart 2: antes `{'height': 198.42520141601562, 'name': 'Chart 2', 'width': 396.85040283203125, 'series': 1, 'left': 1047.5999755859375, 'top': 361.20001220703125}`; después `{'top': 381.6000061035156, 'width': 396.85040283203125, 'series': 1, 'height': 198.42520141601562, 'name': 'Chart 2', 'left': 1047.5999755859375}`. Movimiento de anclaje debido a filas/textos nuevos; misma cantidad de series.

- DIAGRAMAS_Y, gráfico 3, Chart 3: antes `{'height': 198.42520141601562, 'name': 'Chart 3', 'width': 396.85040283203125, 'series': 1, 'left': 1047.5999755859375, 'top': 606.0}`; después `{'top': 626.4000244140625, 'width': 396.85040283203125, 'series': 1, 'height': 198.42520141601562, 'name': 'Chart 3', 'left': 1047.5999755859375}`. Movimiento de anclaje debido a filas/textos nuevos; misma cantidad de series.

## Q. Limitaciones pendientes, expresamente visibles

- Contacto exclusivamente a compresión parcial: no implementado; bloqueado sin recortar q.
- BORDE/ESQUINA y perímetro interior cercano a borde: falta definir e investigar geometría abierta, centroide/J y superficies mínimas. No se aplica perímetro completo para certificar.
- Refuerzo local de γf Mu: momentos y anchos efectivos calculados, pero concentración, reparto/anclaje de conexión requieren detalle estructural. Se conserva advertencia y no se convierte en CUMPLE global.
- Factores de peso propio/relleno último y convención de acciones deben corresponder al caso ingresado. No se infiere una combinación a partir del nombre.
- Diseño global por metro y acciones concentradas es el alcance conservado; no se certifican anclajes, aplastamiento, deslizamiento ni todo el proyecto de cimentación mediante esta Fase 1. Las entradas manuales de dimensiones y acero no se optimizan.

## R. Reservado para Fase 2

60 combinaciones, envolventes automáticas de esas combinaciones, importación ETABS/SAP2000, macros/botones, dashboard nuevo, optimización de dimensiones y diseño de otros sistemas de cimentación. No se añadió ninguna de esas funciones.

## F. Registro auditable de celdas y fórmulas anteriores/nuevas

Este registro se obtuvo comparando el OOXML original y el final guardado por Excel. Los grupos de filas contiguas se consolidan solo cuando **tanto fórmula anterior como nueva** mantienen el mismo patrón de referencias relativas. Se muestran la primera celda del rango y ambas fórmulas exactas de esa celda; las referencias relativas se trasladan a cada fila del rango. Fórmulas absolutas y nombres se conservan. Un cambio sin fórmula se indica como valor/texto. La columna técnica detalla la causa. Los rangos de formato/nombres/validación se documentan después de la tabla.

| Hoja | Celda/rango | Anterior (primera celda) | Nueva (primera celda) | Justificación |
|---|---|---|---|---|
| INGRESO_DATOS | A50 | `Convertir carga vertical a compresion positiva` | `Signo de P ingresado en compresión` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| INGRESO_DATOS | A64 | `(vacía)` | `DISPOSICIÓN Y CASO ACTUAL` | Entradas nuevas de Fase 1 sin desplazar las existentes. |
| INGRESO_DATOS | A65 | `(vacía)` | `Parrilla inferior: dirección más baja` | Entradas nuevas de Fase 1 sin desplazar las existentes. |
| INGRESO_DATOS | A66 | `(vacía)` | `Tipo de columna` | Entradas nuevas de Fase 1 sin desplazar las existentes. |
| INGRESO_DATOS | A67 | `(vacía)` | `Caso / combinación última actual` | Entradas nuevas de Fase 1 sin desplazar las existentes. |
| INGRESO_DATOS | A68 | `(vacía)` | `Parrilla superior: dirección exterior` | Entradas nuevas de Fase 1 sin desplazar las existentes. |
| INGRESO_DATOS | A69 | `(vacía)` | `Factor peso zapata, estado último` | Entradas nuevas de Fase 1 sin desplazar las existentes. |
| INGRESO_DATOS | A70 | `(vacía)` | `Factor peso relleno, estado último` | Entradas nuevas de Fase 1 sin desplazar las existentes. |
| INGRESO_DATOS | B50 | `convP` | `SIGNO_COMPRESION_P` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| INGRESO_DATOS | C48 | `1` | `-1` | Ejes globales de mano derecha: acción horizontal Fy a altura zh aporta Mx=-Fy*zh. My=+Fx*zh. Se hace explícita la convención de acciones sobre la zapata. |
| INGRESO_DATOS | C50 | `Si` | `1` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| INGRESO_DATOS | C65 | `(vacía)` | `X inferior / Y superior` | Entrada editable de Fase 1. |
| INGRESO_DATOS | C66 | `(vacía)` | `INTERIOR` | Entrada editable de Fase 1. |
| INGRESO_DATOS | C67 | `(vacía)` | `CARGAS_ULTIMAS - caso actual` | Entrada editable de Fase 1. |
| INGRESO_DATOS | C68 | `(vacía)` | `X exterior / Y interior` | Entrada editable de Fase 1. |
| INGRESO_DATOS | C69:C70 | `(vacía)` | `1` | Entrada editable de Fase 1. |
| INGRESO_DATOS | D50 | `Si/No` | `+1 / -1` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| INGRESO_DATOS | D65:D70 | `(vacía)` | `-` | Unidad de nueva entrada. |
| INGRESO_DATOS | E48 | `Convencion SAP2000` | `Acción sobre zapata: Mx = Mx ingreso - Fy*zh.` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| INGRESO_DATOS | E49 | `Convencion SAP2000` | `Acción sobre zapata: My = My ingreso + Fx*zh.` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| INGRESO_DATOS | E50 | `Usa ABS(P) si P es negativo` | `P interno = signo × P; tracción conserva signo negativo.` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| INGRESO_DATOS | E65 | `(vacía)` | `Barra X debajo de Y; opción inversa editable.` | Descripción de nueva entrada. |
| INGRESO_DATOS | E66 | `(vacía)` | `BORDE/ESQUINA requieren definir perímetro abierto.` | Descripción de nueva entrada. |
| INGRESO_DATOS | E67 | `(vacía)` | `Identificador editable; las acciones se ingresan en CARGAS.` | Descripción de nueva entrada. |
| INGRESO_DATOS | E68 | `(vacía)` | `X más próxima a cara superior; opción inversa editable.` | Descripción de nueva entrada. |
| INGRESO_DATOS | E69:E70 | `(vacía)` | `Confirmar el factor de la combinación actual; original utilizaba 1.` | Descripción de nueva entrada. |
| CARGAS | E4 | `Las cargas verticales se transforman con ABS(P) si se activa convP.` | `P positivo en compresión según SIGNO_COMPRESION_P. Mx/My son acciones globales sobre la zapata (mano derecha).` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| CARGAS | E9 | `=IF(inp_convert_p="Si",ABS(C9),C9)` | `=inp_sign_p*C9` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| CARGAS | E19 | `Las cargas verticales se transforman con ABS(P) si se activa convP.` | `P positivo en compresión según SIGNO_COMPRESION_P. Mx/My son acciones globales sobre la zapata (mano derecha).` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| CARGAS | E24 | `=IF(inp_convert_p="Si",ABS(C24),C24)` | `=inp_sign_p*C24` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| CARGAS | G9 | `=IF(C9<0,"Advertencia: carga vertical negativa; revisar convencion SAP2000","")` | `=IF(E9<=0,"LEVANTAMIENTO / TRACCIÓN: P interno <= 0","")` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| CARGAS | G24 | `=IF(C24<0,"Advertencia: carga vertical negativa; revisar convencion SAP2000","")` | `=IF(E24<=0,"LEVANTAMIENTO / TRACCIÓN: P interno <= 0","")` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| GEOMETRIA | A14 | `(vacía)` | `Control de entradas` | Dimensiones positivas; columna contenida; barras, capas y grilla válidas. |
| GEOMETRIA | B4 | `=inp_bx*inp_by` | `=IF(geo_input_state="OK",inp_bx*inp_by,"")` | No dividir ni diseñar con geometría inválida. |
| GEOMETRIA | B5 | `=inp_bx*inp_by*inp_h` | `=IF(geo_input_state="OK",inp_bx*inp_by*inp_h,"")` | No dividir ni diseñar con geometría inválida. |
| GEOMETRIA | B6 | `=IF(inp_peso_zapata="Si",B5*inp_gamma_c,0)` | `=IF(geo_input_state="OK",IF(inp_peso_zapata="Si",B5*inp_gamma_c,0),"")` | No dividir ni diseñar con geometría inválida. |
| GEOMETRIA | B7 | `=IF(inp_peso_suelo="Si",inp_bx*inp_by*inp_hs*inp_gamma_s,0)` | `=IF(geo_input_state="OK",IF(inp_peso_suelo="Si",inp_bx*inp_by*inp_hs*inp_gamma_s,0),"")` | No dividir ni diseñar con geometría inválida. |
| GEOMETRIA | B8 | `=B6+B7` | `=IF(geo_input_state="OK",B6+B7,"")` | No dividir ni diseñar con geometría inválida. |
| GEOMETRIA | B9 | `=inp_bx*inp_by^3/12` | `=IF(geo_input_state="OK",inp_bx*inp_by^3/12,"")` | No dividir ni diseñar con geometría inválida. |
| GEOMETRIA | B10 | `=inp_by*inp_bx^3/12` | `=IF(geo_input_state="OK",inp_by*inp_bx^3/12,"")` | No dividir ni diseñar con geometría inválida. |
| GEOMETRIA | B11 | `=MIN(3*inp_h*100,inp_sep_max_usuario)` | `=IF(geo_input_state="OK",MIN(3*inp_h*100,inp_sep_max_usuario),"")` | No dividir ni diseñar con geometría inválida. |
| GEOMETRIA | B12 | `=IF(AND(ABS(inp_xc)+inp_cx/2<=inp_bx/2,ABS(inp_yc)+inp_cy/2<=inp_by/2),"CUMPLE","NO CUMPLE")` | `=IF(geo_input_state="OK","CUMPLE","NO CUMPLE")` | Control geométrico explícito. |
| GEOMETRIA | B13 | `=MIN(inp_bx/2-(ABS(inp_xc)+inp_cx/2),inp_by/2-(ABS(inp_yc)+inp_cy/2))` | `=IF(geo_input_state="OK",MIN(inp_bx/2-(ABS(inp_xc)+inp_cx/2),inp_by/2-(ABS(inp_yc)+inp_cy/2)),"")` | No dividir ni diseñar con geometría inválida. |
| GEOMETRIA | B14 | `(vacía)` | `=IF(AND(COUNT(inp_bx,inp_by,inp_h,inp_cx,inp_cy,inp_xc,inp_yc,inp_rec_inf,inp_rec_sup,inp_fc,inp_fy,inp_n_div_x,inp_n_div_y)=13,MIN(inp_bx,inp_by,inp_h,inp_cx,inp_cy,inp_fc,inp_fy)>0,inp_rec_inf>=0,inp_rec_sup>=0,inp_n_div_x>=4,inp_n_div_x<=50,inp_n_div_y>=4,inp_n_div_y<=50,MOD(inp_n_div_x,1)=0,MOD(inp_n_div_y,1)=0,ABS(inp_xc)+inp_cx/2<=inp_bx/2,ABS(inp_yc)+inp_cy/2<=inp_by/2,OR(inp_sign_p=1,inp_sign_p=-1),OR(inp_order_inf="X inferior / Y superior",inp_order_inf="Y inferior / X superior"),OR(inp_order_sup="X exterior / Y interior",inp_order_sup="Y exterior / X interior"),OR(inp_col_type="INTERIOR",inp_col_type="BORDE",inp_col_type="ESQUINA"),COUNTIF(bar_codes,inp_bar_inf_x)=1,COUNTIF(bar_codes,inp_bar_inf_y)=1,COUNTIF(bar_codes,inp_bar_sup_x)=1,COUNTIF(bar_codes,inp_bar_sup_y)=1),"OK","DATOS / GEOMETRÍA INVÁLIDOS")` | Dimensiones positivas; columna contenida; barras, capas y grilla válidas. |
| GEOMETRIA | C14 | `(vacía)` | `-` | Dimensiones positivas; columna contenida; barras, capas y grilla válidas. |
| GEOMETRIA | C18:C2618 | `=IF(OR(A18>inp_n_div_x,B18>inp_n_div_y),"",-inp_bx/2+A18*inp_bx/inp_n_div_x)` | `=IF(geo_input_state="OK",IF(OR(A18>inp_n_div_x,B18>inp_n_div_y),"",-inp_bx/2+A18*inp_bx/inp_n_div_x),"")` | Grilla conservada; proteger entradas inválidas. Fórmula mostrada en la primera fila; referencias relativas avanzan por fila, salvo ramas iniciales explícitas. |
| GEOMETRIA | D13 | `Si es menor que d revisar` | `Perímetro interior debe revisar proximidad a bordes libres.` | No confundir perímetro cerrado con sección mínima cerca de un borde. |
| GEOMETRIA | D14 | `(vacía)` | `Dimensiones positivas; columna contenida; barras, capas y grilla válidas.` | Dimensiones positivas; columna contenida; barras, capas y grilla válidas. |
| GEOMETRIA | F17 | `q_serv_corr` | `q_serv sin truncar` | No usar MAX(0,q). |
| GEOMETRIA | F18:F2618 | `=IF(E18="","",MAX(0,E18))` | `=IF(E18="","",E18)` | Conservar el signo de presión bruta de servicio; eliminar truncamiento. Fórmula mostrada en la primera fila; referencias relativas avanzan por fila, salvo ramas iniciales explícitas. |
| GEOMETRIA | H17 | `q_u_corr` | `q_u sin truncar` | No usar MAX(0,q). |
| GEOMETRIA | H18:H2618 | `=IF(G18="","",MAX(0,G18))` | `=IF(G18="","",G18)` | Conservar el signo de presión bruta última; eliminar truncamiento. Fórmula mostrada en la primera fila; referencias relativas avanzan por fila, salvo ramas iniciales explícitas. |
| GEOMETRIA | K18:K2618 | `=IF(OR(E18<0,G18<0),"Presion negativa","")` | `=IF(geo_input_state="OK",IF(OR(E18<0,G18<0),"Presion negativa",""),"")` | Grilla conservada; proteger entradas inválidas. Fórmula mostrada en la primera fila; referencias relativas avanzan por fila, salvo ramas iniciales explícitas. |
| RESULTANTE | A12 | `=IF(OR(srv_raw_p<0,ult_raw_p<0),"Las cargas verticales tienen signo negativo; verificar convencion SAP2000.","")` | `=IF(OR(srv_p<=0,ult_p<=0),"LEVANTAMIENTO / TRACCIÓN: se conserva el signo físico de P.","")` | Convención interna P positivo en compresión: P_interno=SIGNO_COMPRESION_P*P_ingreso; se conserva levantamiento real. |
| RESULTANTE | C6 | `=geo_w_zapata` | `=IF(geo_input_state="OK",geo_w_zapata*inp_fwz_u,"")` | Factor de peso propio explícito del estado último. |
| RESULTANTE | D6 | `=geo_w_suelo` | `=IF(geo_input_state="OK",geo_w_suelo*inp_fws_u,"")` | Factor de relleno explícito del estado último. |
| RESULTANTE | E5:E6 | `=B5+C5+D5` | `=IF(geo_input_state="OK",B5+C5+D5,"")` | Reacción bruta con pesos del mismo estado. |
| RESULTANTE | F4 | `Mx total` | `Primer momento q en Y` | No rotular como momento externo; es la resultante del campo de presiones. |
| RESULTANTE | F5 | `=srv_mx+srv_p*inp_yc` | `=-srv_mx+srv_p*inp_yc` | Primer momento de presión en Y = P*yc-Mx para acciones globales de mano derecha; equilibrio ΣMx. |
| RESULTANTE | F6 | `=ult_mx+ult_p*inp_yc` | `=-ult_mx+ult_p*inp_yc` | Primer momento de presión en Y = P*yc-Mx para acciones globales de mano derecha; equilibrio ΣMx. |
| RESULTANTE | G4 | `My total` | `Primer momento q en X` | Convención global de equilibrio. |
| RESULTANTE | H5:H6 | `=IF(E5<>0,G5/E5,"")` | `=IF(AND(geo_input_state="OK",E5>0),IF(E5<>0,G5/E5,""),"")` | Excentricidad no aplicable con resultante no compresiva. |
| RESULTANTE | I5:I6 | `=IF(E5<>0,F5/E5,"")` | `=IF(AND(geo_input_state="OK",E5>0),IF(E5<>0,F5/E5,""),"")` | Excentricidad no aplicable con resultante no compresiva. |
| RESULTANTE | J5:J6 | `=IF(ABS(H5)<=inp_bx/6,"CUMPLE","NO CUMPLE")` | `=IF(AND(geo_input_state="OK",E5>0),IF(ABS(H5)<=inp_bx/6,"CUMPLE","NO CUMPLE"),"")` | Excentricidad no aplicable con resultante no compresiva. |
| RESULTANTE | K5:K6 | `=IF(ABS(I5)<=inp_by/6,"CUMPLE","NO CUMPLE")` | `=IF(AND(geo_input_state="OK",E5>0),IF(ABS(I5)<=inp_by/6,"CUMPLE","NO CUMPLE"),"")` | Excentricidad no aplicable con resultante no compresiva. |
| RESULTANTE | L5:L6 | `=H5` | `=IF(AND(geo_input_state="OK",E5>0),H5,"")` | Excentricidad no aplicable con resultante no compresiva. |
| RESULTANTE | M5:M6 | `=I5` | `=IF(AND(geo_input_state="OK",E5>0),I5,"")` | Excentricidad no aplicable con resultante no compresiva. |
| RESULTANTE | N5:N6 | `=IF(AND(J5="CUMPLE",K5="CUMPLE"),"CUMPLE","FUERA DEL NUCLEO")` | `=IF(geo_input_state<>"OK",geo_input_state,IF(E5<=0,"RESULTANTE NO COMPRESIVA",IF(ABS(H5)/(inp_bx/6)+ABS(I5)/(inp_by/6)<=1,"CUMPLE","FUERA DEL NUCLEO")))` | El núcleo central biaxial es un rombo; comprobar suma de excentricidades normalizadas, no límites independientes. |
| PRESIONES_SERVICIO | A14 | `Verificacion qmin >= 0` | `Estado de contacto` | Estado explícito de contacto. |
| PRESIONES_SERVICIO | D5:D8 | `=res_srv_p_tot/geo_area+B5*6*res_srv_my_tot/(inp_by*inp_bx^2)+C5*6*res_srv_mx_tot/(inp_bx*inp_by^2)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+B5*6*res_srv_my_tot/(inp_by*inp_bx^2)+C5*6*res_srv_mx_tot/(inp_bx*inp_by^2),"")` | Presión lineal bruta sin truncar; signos de primeros momentos corregidos en RESULTANTE. |
| PRESIONES_SERVICIO | D10 | `=MAX(D5:D8)` | `=IF(geo_input_state="OK",MAX(D5:D8),"")` | Conservar qmin negativo como diagnóstico. |
| PRESIONES_SERVICIO | D11 | `=MIN(D5:D8)` | `=IF(geo_input_state="OK",MIN(D5:D8),"")` | Conservar qmin negativo como diagnóstico. |
| PRESIONES_SERVICIO | D13 | `=IF(D10<=D12,"CUMPLE","NO CUMPLE")` | `=IF(D14<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS DE CONTACTO PARCIAL",IF(D10<=D12,"CUMPLE","NO CUMPLE"))` | No declarar cumple portante con contacto no resuelto. |
| PRESIONES_SERVICIO | D14 | `=IF(D11>=0,"CUMPLE","NO CUMPLE")` | `=IF(geo_input_state<>"OK",geo_input_state,IF(res_srv_p_tot<=0,"RESULTANTE NO COMPRESIVA",IF(D11<0,"PÉRDIDA PARCIAL DE CONTACTO","CONTACTO COMPLETO")))` | Bloquear distribución lineal si qmin<0. |
| PRESIONES_SERVICIO | D15 | `=IF(D11<0,"Existe levantamiento parcial del suelo. Se requiere aumentar dimensiones o analizar area efectiva comprimida.","")` | `=IF(D14<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS DE CONTACTO PARCIAL","")` | Advertencia requerida. |
| PRESIONES_ULTIMAS | A13 | `Verificacion qmin,u >= 0` | `Estado de contacto` | Estado explícito de contacto. |
| PRESIONES_ULTIMAS | A17 | `(vacía)` | `Estado para diseño estructural` | Bloqueo físico del método de presión neta. |
| PRESIONES_ULTIMAS | A19 | `(vacía)` | `Pu columna` | Carga de superestructura; excluye pesos de zapata y relleno. |
| PRESIONES_ULTIMAS | A20 | `(vacía)` | `q neta media` | Método neto: qu bruto menos pesos uniformes del mismo estado. |
| PRESIONES_ULTIMAS | A21 | `(vacía)` | `Gradiente q neta en X` | (Pu*xc+My)/Iy |
| PRESIONES_ULTIMAS | A22 | `(vacía)` | `Gradiente q neta en Y` | (Pu*yc-Mx)/Ix |
| PRESIONES_ULTIMAS | A23 | `(vacía)` | `Peso uniforme último` | Se resta de qu bruto; no se vuelve a incluir en Vu neto. |
| PRESIONES_ULTIMAS | D5:D8 | `=res_u_p_tot/geo_area+B5*6*res_u_my_tot/(inp_by*inp_bx^2)+C5*6*res_u_mx_tot/(inp_bx*inp_by^2)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+B5*6*res_u_my_tot/(inp_by*inp_bx^2)+C5*6*res_u_mx_tot/(inp_bx*inp_by^2),"")` | Presión lineal bruta sin truncar; signos de primeros momentos corregidos en RESULTANTE. |
| PRESIONES_ULTIMAS | D10 | `=MAX(D5:D8)` | `=IF(geo_input_state="OK",MAX(D5:D8),"")` | Conservar qmin negativo como diagnóstico. |
| PRESIONES_ULTIMAS | D11 | `=MIN(D5:D8)` | `=IF(geo_input_state="OK",MIN(D5:D8),"")` | Conservar qmin negativo como diagnóstico. |
| PRESIONES_ULTIMAS | D13 | `=IF(D11>=0,"CUMPLE","ADVERTENCIA: LEVANTAMIENTO")` | `=IF(geo_input_state<>"OK",geo_input_state,IF(res_u_p_tot<=0,"RESULTANTE NO COMPRESIVA",IF(D11<0,"PÉRDIDA PARCIAL DE CONTACTO","CONTACTO COMPLETO")))` | Bloquear distribución lineal si qmin<0. |
| PRESIONES_ULTIMAS | D14 | `=IF(D11<0,"Existe levantamiento en estado ultimo; revisar area comprimida y estabilidad.","")` | `=IF(D13<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS DE CONTACTO PARCIAL","")` | Advertencia requerida. |
| PRESIONES_ULTIMAS | D17 | `(vacía)` | `=IF(geo_input_state<>"OK",geo_input_state,IF(OR(COUNT(ult_p,ult_mx,ult_my)<3,COUNT(srv_p,srv_mx,srv_my)<3,COUNT(punz_d_x,punz_d_y)<2,inp_phi_p<>0.85,inp_phi_v<>0.85),"REVISAR DATOS / PHI E.060",IF(MIN(punz_d_x,punz_d_y)<=0,"PERALTE EFECTIVO NO POSITIVO",IF(ult_p<=0,"LEVANTAMIENTO / TRACCIÓN: NO DISEÑAR",IF(D13<>"CONTACTO COMPLETO","REQUIERE ANÁLISIS DE CONTACTO PARCIAL","OK")))))` | No diseñar con presión sin equilibrio ni con tracción de columna; phi cortante/punzonamiento = 0.85. |
| PRESIONES_ULTIMAS | D19 | `(vacía)` | `=ult_p` | Carga de superestructura; excluye pesos de zapata y relleno. |
| PRESIONES_ULTIMAS | D20 | `(vacía)` | `=IF(struct_state="OK",ult_p/geo_area,"")` | Método neto: qu bruto menos pesos uniformes del mismo estado. |
| PRESIONES_ULTIMAS | D21 | `(vacía)` | `=IF(struct_state="OK",res_u_my_tot/geo_iy,"")` | (Pu*xc+My)/Iy |
| PRESIONES_ULTIMAS | D22 | `(vacía)` | `=IF(struct_state="OK",res_u_mx_tot/geo_ix,"")` | (Pu*yc-Mx)/Ix |
| PRESIONES_ULTIMAS | D23 | `(vacía)` | `=IF(struct_state="OK",(RESULTANTE!C6+RESULTANTE!D6)/geo_area,"")` | Se resta de qu bruto; no se vuelve a incluir en Vu neto. |
| PRESIONES_ULTIMAS | F19 | `(vacía)` | `tonf` | Carga de superestructura; excluye pesos de zapata y relleno. |
| PRESIONES_ULTIMAS | F20 | `(vacía)` | `tonf/m2` | Método neto: qu bruto menos pesos uniformes del mismo estado. |
| PRESIONES_ULTIMAS | F21 | `(vacía)` | `tonf/m3` | (Pu*xc+My)/Iy |
| PRESIONES_ULTIMAS | F22 | `(vacía)` | `tonf/m3` | (Pu*yc-Mx)/Ix |
| PRESIONES_ULTIMAS | F23 | `(vacía)` | `tonf/m2` | Se resta de qu bruto; no se vuelve a incluir en Vu neto. |
| PRESIONES_ULTIMAS | H19 | `(vacía)` | `Carga de superestructura; excluye pesos de zapata y relleno.` | Carga de superestructura; excluye pesos de zapata y relleno. |
| PRESIONES_ULTIMAS | H20 | `(vacía)` | `Método neto: qu bruto menos pesos uniformes del mismo estado.` | Método neto: qu bruto menos pesos uniformes del mismo estado. |
| PRESIONES_ULTIMAS | H21 | `(vacía)` | `(Pu*xc+My)/Iy` | (Pu*xc+My)/Iy |
| PRESIONES_ULTIMAS | H22 | `(vacía)` | `(Pu*yc-Mx)/Ix` | (Pu*yc-Mx)/Ix |
| PRESIONES_ULTIMAS | H23 | `(vacía)` | `Se resta de qu bruto; no se vuelve a incluir en Vu neto.` | Se resta de qu bruto; no se vuelve a incluir en Vu neto. |
| DIAGRAMAS_X | A68 | `(vacía)` | `EXTREMOS EXACTOS (V=0 Y LÍMITES)` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A69 | `(vacía)` | `Coordenada` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A70 | `(vacía)` | `Borde izquierdo` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A71 | `(vacía)` | `Cara izquierda` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A72 | `(vacía)` | `Columna antes` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A73 | `(vacía)` | `Columna después` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A74 | `(vacía)` | `Cara derecha` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A75 | `(vacía)` | `Borde derecho` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A76 | `(vacía)` | `Raíz izquierda 1` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A77 | `(vacía)` | `Raíz izquierda 2` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A78 | `(vacía)` | `Raíz derecha 1` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | A79 | `(vacía)` | `Raíz derecha 2` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_X | B4 | `=MAX(J14:J64)` | `=IF(struct_state="OK",IF(MAX(D70:D79)>MAX(0.00000001,0.0000000001*ABS(ult_p*inp_bx)),MAX(D70:D79),0),"")` | Envolvente positiva exacta; normalizar únicamente ruido numérico menor que tolerancia absoluta/relativa, sin cambiar diagrama ni cierre. |
| DIAGRAMAS_X | B5 | `=ABS(MIN(J14:J64))` | `=IF(struct_state="OK",IF(-MIN(D70:D79)>MAX(0.00000001,0.0000000001*ABS(ult_p*inp_bx)),-MIN(D70:D79),0),"")` | Magnitud negativa; evitar acero superior ficticio por residuos de redondeo próximos a cero. No se fuerza el cierre del diagrama. |
| DIAGRAMAS_X | B6 | `=MAX(ABS(MIN(I14:I64)),ABS(MAX(I14:I64)))` | `=IF(struct_state="OK",MAX(ABS(MIN(I14:I64)),ABS(MAX(I14:I64))),"")` | Demanda de cortante en diagrama. |
| DIAGRAMAS_X | B7 | `=IFERROR(INDEX($J$14:$J$64,MATCH(inp_xc-inp_cx/2,$B$14:$B$64,1)),0)` | `=IF(struct_state="OK",$J$7*((inp_xc-inp_cx/2)+inp_bx/2)^2/2+$J$8*((inp_xc-inp_cx/2)+inp_bx/2)^3/6-ult_p*MAX(0,(inp_xc-inp_cx/2)-inp_xc),"")` | Momento exacto en cara de columna según 15.4.1/2; sin INDEX/MATCH aproximado. |
| DIAGRAMAS_X | B8 | `=IFERROR(INDEX($J$14:$J$64,MATCH(inp_xc+inp_cx/2,$B$14:$B$64,1)),0)` | `=IF(struct_state="OK",$J$7*((inp_xc+inp_cx/2)+inp_bx/2)^2/2+$J$8*((inp_xc+inp_cx/2)+inp_bx/2)^3/6-ult_p*MAX(0,(inp_xc+inp_cx/2)-inp_xc)+ $J$9,"")` | Momento exacto en cara opuesta de columna. |
| DIAGRAMAS_X | B9 | `=MAX(B4,B5)/inp_by` | `=IF(struct_state="OK",MAX(B4,B5)/inp_by,"")` | Envolvente por metro coherente con diagramas corregidos. |
| DIAGRAMAS_X | B14:B64 | `=-inp_bx/2+A14*inp_bx/inp_n_div_x` | `=IF(AND(struct_state="OK",A14<=inp_n_div_x),IF(A14<=$J$10,-inp_bx/2+A14*(inp_xc+inp_bx/2)/$J$10,IF(A14=$J$10+1,inp_xc,inp_xc+(A14-$J$10-1)*(inp_bx/2-inp_xc)/(inp_n_div_x-$J$10-1))),"")` | Grilla con dos coordenadas idénticas antes/después de columna para dibujar saltos de P y M; extremo libre alcanzado para nx/ny editables. |
| DIAGRAMAS_X | B70 | `(vacía)` | `=IF(struct_state="OK",-inp_bx/2,"")` | Coordenada de sección crítica/extremo. |
| DIAGRAMAS_X | B71 | `(vacía)` | `=IF(struct_state="OK",inp_xc-inp_cx/2,"")` | Coordenada de sección crítica/extremo. |
| DIAGRAMAS_X | B72:B73 | `(vacía)` | `=IF(struct_state="OK",inp_xc,"")` | Coordenada de sección crítica/extremo. |
| DIAGRAMAS_X | B74 | `(vacía)` | `=IF(struct_state="OK",inp_xc+inp_cx/2,"")` | Coordenada de sección crítica/extremo. |
| DIAGRAMAS_X | B75 | `(vacía)` | `=IF(struct_state="OK",inp_bx/2,"")` | Coordenada de sección crítica/extremo. |
| DIAGRAMAS_X | B76:B77 | `(vacía)` | `=IF(C76="","",IF(AND(C76-inp_bx/2>=-inp_bx/2,C76-inp_bx/2<=inp_xc),C76-inp_bx/2,""))` | Aceptar raíz solo dentro de su tramo; ninguna sustitución optimista por cero. |
| DIAGRAMAS_X | B78:B79 | `(vacía)` | `=IF(C78="","",IF(AND(C78-inp_bx/2>=inp_xc,C78-inp_bx/2<=inp_bx/2),C78-inp_bx/2,""))` | Aceptar raíz solo dentro de su tramo; ninguna sustitución optimista por cero. |
| DIAGRAMAS_X | C14:C64 | `=res_u_p_tot/geo_area+res_u_my_tot/geo_iy*B14` | `=IF(AND(struct_state="OK",A14<=inp_n_div_x),net_q0+net_gx*B14+gross_weight_u,"")` | Presión bruta integrada en dirección transversal; pesos uniformes coherentes. |
| DIAGRAMAS_X | C76 | `(vacía)` | `=IF(struct_state="OK",IF(ABS($J$8)<0.000000000001,IF(ABS($J$7)>0.000000000001,0/$J$7,""),IF($J$7^2+2*$J$8*0>=0,(-$J$7+(1)*SQRT($J$7^2+2*$J$8*0))/$J$8,"")),"")` | Raíz analítica de V(t)=a*t+b*t²/2-PH; discriminar tramo y radicando. |
| DIAGRAMAS_X | C77 | `(vacía)` | `=IF(struct_state="OK",IF(ABS($J$8)<0.000000000001,IF(ABS($J$7)>0.000000000001,0/$J$7,""),IF($J$7^2+2*$J$8*0>=0,(-$J$7+(-1)*SQRT($J$7^2+2*$J$8*0))/$J$8,"")),"")` | Raíz analítica de V(t)=a*t+b*t²/2-PH; discriminar tramo y radicando. |
| DIAGRAMAS_X | C78 | `(vacía)` | `=IF(struct_state="OK",IF(ABS($J$8)<0.000000000001,IF(ABS($J$7)>0.000000000001,ult_p/$J$7,""),IF($J$7^2+2*$J$8*ult_p>=0,(-$J$7+(1)*SQRT($J$7^2+2*$J$8*ult_p))/$J$8,"")),"")` | Raíz analítica de V(t)=a*t+b*t²/2-PH; discriminar tramo y radicando. |
| DIAGRAMAS_X | C79 | `(vacía)` | `=IF(struct_state="OK",IF(ABS($J$8)<0.000000000001,IF(ABS($J$7)>0.000000000001,ult_p/$J$7,""),IF($J$7^2+2*$J$8*ult_p>=0,(-$J$7+(-1)*SQRT($J$7^2+2*$J$8*ult_p))/$J$8,"")),"")` | Raíz analítica de V(t)=a*t+b*t²/2-PH; discriminar tramo y radicando. |
| DIAGRAMAS_X | D13 | `q_u corr` | `q_u sin truncar` | Presión bruta sin MAX(0,q). |
| DIAGRAMAS_X | D14:D64 | `=MAX(0,C14)` | `=C14` | Sin truncamiento de presiones. |
| DIAGRAMAS_X | D70:D72 | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B70)),$J$7*(B70+inp_bx/2)^2/2+$J$8*(B70+inp_bx/2)^3/6-ult_p*MAX(0,B70-inp_xc),"")` | Momento exacto en extremo/raíz. |
| DIAGRAMAS_X | D73:D75 | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B73)),$J$7*(B73+inp_bx/2)^2/2+$J$8*(B73+inp_bx/2)^3/6-ult_p*MAX(0,B73-inp_xc)+ $J$9,"")` | Momento exacto en extremo/raíz. |
| DIAGRAMAS_X | D76:D77 | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B76)),$J$7*(B76+inp_bx/2)^2/2+$J$8*(B76+inp_bx/2)^3/6-ult_p*MAX(0,B76-inp_xc),"")` | Momento exacto en extremo/raíz. |
| DIAGRAMAS_X | D78:D79 | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B78)),$J$7*(B78+inp_bx/2)^2/2+$J$8*(B78+inp_bx/2)^3/6-ult_p*MAX(0,B78-inp_xc)+ $J$9,"")` | Momento exacto en extremo/raíz. |
| DIAGRAMAS_X | E14:E64 | `=inp_by*D14` | `=IF(AND(struct_state="OK",A14<=inp_n_div_x),inp_by*D14,"")` | Reacción bruta por unidad de longitud. |
| DIAGRAMAS_X | F14:F64 | `=geo_w_total/inp_bx` | `=IF(AND(struct_state="OK",A14<=inp_n_div_x),inp_by*gross_weight_u,"")` | Mismos pesos del estado último; cancelan exactamente al obtener presión neta. |
| DIAGRAMAS_X | G4 | `(vacía)` | `ERROR_FUERZAS_X` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_X | G5 | `(vacía)` | `ERROR_MOMENTOS_X` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_X | G6 | `(vacía)` | `Equilibrio X` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_X | G7 | `(vacía)` | `a: w neta borde izquierdo` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_X | G8 | `(vacía)` | `b: pendiente w neta` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_X | G9 | `(vacía)` | `Momento concentrado` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_X | G10 | `(vacía)` | `Divisiones hasta columna` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_X | G11 | `(vacía)` | `Caso actual` | Identificar las acciones del diagrama. |
| DIAGRAMAS_X | G14:G64 | `=E14-F14` | `=IF(AND(struct_state="OK",A14<=inp_n_div_x),E14-F14,"")` | w neta estructural. |
| DIAGRAMAS_X | H13 | `P_col tramo` | `P concentrada` | Acción concentrada de columna. |
| DIAGRAMAS_X | H14 | `=0` | `=IF(AND(struct_state="OK",A14<=inp_n_div_x),IF(A14=$J$10+1,ult_p,0),"")` | P aplicada una sola vez en centro de columna. |
| DIAGRAMAS_X | H15:H64 | `=ult_p*MAX(0,MIN(B15,inp_xc+inp_cx/2)-MAX(B14,inp_xc-inp_cx/2))/inp_cx` | `=IF(AND(struct_state="OK",A15<=inp_n_div_x),IF(A15=$J$10+1,ult_p,0),"")` | P aplicada una sola vez en centro de columna. |
| DIAGRAMAS_X | I14 | `=0` | `=IF(AND(struct_state="OK",A14<=inp_n_div_x),$J$7*(B14+inp_bx/2)+$J$8*(B14+inp_bx/2)^2/2-IF(A14>$J$10,ult_p,0),"")` | V exacto: integral w - P H; salto antes/después de columna. |
| DIAGRAMAS_X | I15:I64 | `=I14+((G14+G15)/2)*(B15-B14)-H15` | `=IF(AND(struct_state="OK",A15<=inp_n_div_x),$J$7*(B15+inp_bx/2)+$J$8*(B15+inp_bx/2)^2/2-IF(A15>$J$10,ult_p,0),"")` | V exacto: integral w - P H; salto antes/después de columna. |
| DIAGRAMAS_X | J4 | `(vacía)` | `=IF(struct_state="OK",INDEX(I14:I64,inp_n_div_x+1),"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_X | J5 | `(vacía)` | `=IF(struct_state="OK",INDEX(J14:J64,inp_n_div_x+1),"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_X | J6 | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(AND(ABS(J4)<=MAX(0.000001,0.001*ABS(ult_p)),ABS(J5)<=MAX(0.000001,0.001*MAX(ABS(ult_my),ABS(ult_p*inp_bx)))),"OK","ERROR"))` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_X | J7 | `(vacía)` | `=IF(struct_state="OK",inp_by*(net_q0-net_gx*inp_bx/2),"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_X | J8 | `(vacía)` | `=IF(struct_state="OK",inp_by*net_gx,"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_X | J9 | `(vacía)` | `=IF(struct_state="OK",ult_my,"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_X | J10 | `(vacía)` | `=IF(struct_state="OK",MAX(1,MIN(inp_n_div_x-2,ROUND(inp_n_div_x*(inp_xc+inp_bx/2)/inp_bx,0))),"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_X | J11 | `(vacía)` | `=inp_case` | Caso/combination actual. |
| DIAGRAMAS_X | J14 | `=0` | `=IF(AND(struct_state="OK",A14<=inp_n_div_x),$J$7*(B14+inp_bx/2)^2/2+$J$8*(B14+inp_bx/2)^3/6-ult_p*MAX(0,B14-inp_xc)+IF(A14>$J$10,$J$9,0),"")` | M exacto: integral V + salto del momento de columna; no se cierra artificialmente el último punto. |
| DIAGRAMAS_X | J15:J64 | `=J14+((I14+I15)/2)*(B15-B14)` | `=IF(AND(struct_state="OK",A15<=inp_n_div_x),$J$7*(B15+inp_bx/2)^2/2+$J$8*(B15+inp_bx/2)^3/6-ult_p*MAX(0,B15-inp_xc)+IF(A15>$J$10,$J$9,0),"")` | M exacto: integral V + salto del momento de columna; no se cierra artificialmente el último punto. |
| DIAGRAMAS_X | K4 | `(vacía)` | `tonf` | Unidades del control. |
| DIAGRAMAS_X | K5 | `(vacía)` | `tonf*m` | Unidades del control. |
| DIAGRAMAS_X | K7 | `(vacía)` | `tonf/m` | Unidades del control. |
| DIAGRAMAS_X | K8 | `(vacía)` | `tonf/m2` | Unidades del control. |
| DIAGRAMAS_X | K9 | `(vacía)` | `tonf*m` | Unidades del control. |
| DIAGRAMAS_X | K10 | `(vacía)` | `-` | Unidades del control. |
| DIAGRAMAS_X | K14:K64 | `=IF(AND(B14>=inp_xc-inp_cx/2,B14<=inp_xc+inp_cx/2),"Si","No")` | `=IF(AND(struct_state="OK",A14<=inp_n_div_x),IF(AND(B14>=inp_xc-inp_cx/2,B14<=inp_xc+inp_cx/2),"Si","No"),"")` | Zona de columna conservada. |
| DIAGRAMAS_X | L14:L64 | `=IF(D14=0,"Presion corregida por levantamiento","")` | `=IF(struct_state<>"OK",struct_state,IF(A14=$J$10+1,"SALTO P Y M",""))` | Advertencias mecánicas sin ocultar errores. |
| DIAGRAMAS_Y | A68 | `(vacía)` | `EXTREMOS EXACTOS (V=0 Y LÍMITES)` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A69 | `(vacía)` | `Coordenada` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A70 | `(vacía)` | `Borde izquierdo` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A71 | `(vacía)` | `Cara izquierda` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A72 | `(vacía)` | `Columna antes` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A73 | `(vacía)` | `Columna después` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A74 | `(vacía)` | `Cara derecha` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A75 | `(vacía)` | `Borde derecho` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A76 | `(vacía)` | `Raíz izquierda 1` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A77 | `(vacía)` | `Raíz izquierda 2` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A78 | `(vacía)` | `Raíz derecha 1` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | A79 | `(vacía)` | `Raíz derecha 2` | Cálculo de envolvente exacta independiente de la grilla gráfica. |
| DIAGRAMAS_Y | B4 | `=MAX(J14:J64)` | `=IF(struct_state="OK",IF(MAX(D70:D79)>MAX(0.00000001,0.0000000001*ABS(ult_p*inp_by)),MAX(D70:D79),0),"")` | Envolvente positiva exacta; normalizar únicamente ruido numérico menor que tolerancia absoluta/relativa, sin cambiar diagrama ni cierre. |
| DIAGRAMAS_Y | B5 | `=ABS(MIN(J14:J64))` | `=IF(struct_state="OK",IF(-MIN(D70:D79)>MAX(0.00000001,0.0000000001*ABS(ult_p*inp_by)),-MIN(D70:D79),0),"")` | Magnitud negativa; evitar acero superior ficticio por residuos de redondeo próximos a cero. No se fuerza el cierre del diagrama. |
| DIAGRAMAS_Y | B6 | `=MAX(ABS(MIN(I14:I64)),ABS(MAX(I14:I64)))` | `=IF(struct_state="OK",MAX(ABS(MIN(I14:I64)),ABS(MAX(I14:I64))),"")` | Demanda de cortante en diagrama. |
| DIAGRAMAS_Y | B7 | `=IFERROR(INDEX($J$14:$J$64,MATCH(inp_yc-inp_cy/2,$B$14:$B$64,1)),0)` | `=IF(struct_state="OK",$J$7*((inp_yc-inp_cy/2)+inp_by/2)^2/2+$J$8*((inp_yc-inp_cy/2)+inp_by/2)^3/6-ult_p*MAX(0,(inp_yc-inp_cy/2)-inp_yc),"")` | Momento exacto en cara de columna según 15.4.1/2; sin INDEX/MATCH aproximado. |
| DIAGRAMAS_Y | B8 | `=IFERROR(INDEX($J$14:$J$64,MATCH(inp_yc+inp_cy/2,$B$14:$B$64,1)),0)` | `=IF(struct_state="OK",$J$7*((inp_yc+inp_cy/2)+inp_by/2)^2/2+$J$8*((inp_yc+inp_cy/2)+inp_by/2)^3/6-ult_p*MAX(0,(inp_yc+inp_cy/2)-inp_yc)+ $J$9,"")` | Momento exacto en cara opuesta de columna. |
| DIAGRAMAS_Y | B9 | `=MAX(B4,B5)/inp_bx` | `=IF(struct_state="OK",MAX(B4,B5)/inp_bx,"")` | Envolvente por metro coherente con diagramas corregidos. |
| DIAGRAMAS_Y | B14:B64 | `=-inp_by/2+A14*inp_by/inp_n_div_y` | `=IF(AND(struct_state="OK",A14<=inp_n_div_y),IF(A14<=$J$10,-inp_by/2+A14*(inp_yc+inp_by/2)/$J$10,IF(A14=$J$10+1,inp_yc,inp_yc+(A14-$J$10-1)*(inp_by/2-inp_yc)/(inp_n_div_y-$J$10-1))),"")` | Grilla con dos coordenadas idénticas antes/después de columna para dibujar saltos de P y M; extremo libre alcanzado para nx/ny editables. |
| DIAGRAMAS_Y | B70 | `(vacía)` | `=IF(struct_state="OK",-inp_by/2,"")` | Coordenada de sección crítica/extremo. |
| DIAGRAMAS_Y | B71 | `(vacía)` | `=IF(struct_state="OK",inp_yc-inp_cy/2,"")` | Coordenada de sección crítica/extremo. |
| DIAGRAMAS_Y | B72:B73 | `(vacía)` | `=IF(struct_state="OK",inp_yc,"")` | Coordenada de sección crítica/extremo. |
| DIAGRAMAS_Y | B74 | `(vacía)` | `=IF(struct_state="OK",inp_yc+inp_cy/2,"")` | Coordenada de sección crítica/extremo. |
| DIAGRAMAS_Y | B75 | `(vacía)` | `=IF(struct_state="OK",inp_by/2,"")` | Coordenada de sección crítica/extremo. |
| DIAGRAMAS_Y | B76:B77 | `(vacía)` | `=IF(C76="","",IF(AND(C76-inp_by/2>=-inp_by/2,C76-inp_by/2<=inp_yc),C76-inp_by/2,""))` | Aceptar raíz solo dentro de su tramo; ninguna sustitución optimista por cero. |
| DIAGRAMAS_Y | B78:B79 | `(vacía)` | `=IF(C78="","",IF(AND(C78-inp_by/2>=inp_yc,C78-inp_by/2<=inp_by/2),C78-inp_by/2,""))` | Aceptar raíz solo dentro de su tramo; ninguna sustitución optimista por cero. |
| DIAGRAMAS_Y | C14:C64 | `=res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*B14` | `=IF(AND(struct_state="OK",A14<=inp_n_div_y),net_q0+net_gy*B14+gross_weight_u,"")` | Presión bruta integrada en dirección transversal; pesos uniformes coherentes. |
| DIAGRAMAS_Y | C76 | `(vacía)` | `=IF(struct_state="OK",IF(ABS($J$8)<0.000000000001,IF(ABS($J$7)>0.000000000001,0/$J$7,""),IF($J$7^2+2*$J$8*0>=0,(-$J$7+(1)*SQRT($J$7^2+2*$J$8*0))/$J$8,"")),"")` | Raíz analítica de V(t)=a*t+b*t²/2-PH; discriminar tramo y radicando. |
| DIAGRAMAS_Y | C77 | `(vacía)` | `=IF(struct_state="OK",IF(ABS($J$8)<0.000000000001,IF(ABS($J$7)>0.000000000001,0/$J$7,""),IF($J$7^2+2*$J$8*0>=0,(-$J$7+(-1)*SQRT($J$7^2+2*$J$8*0))/$J$8,"")),"")` | Raíz analítica de V(t)=a*t+b*t²/2-PH; discriminar tramo y radicando. |
| DIAGRAMAS_Y | C78 | `(vacía)` | `=IF(struct_state="OK",IF(ABS($J$8)<0.000000000001,IF(ABS($J$7)>0.000000000001,ult_p/$J$7,""),IF($J$7^2+2*$J$8*ult_p>=0,(-$J$7+(1)*SQRT($J$7^2+2*$J$8*ult_p))/$J$8,"")),"")` | Raíz analítica de V(t)=a*t+b*t²/2-PH; discriminar tramo y radicando. |
| DIAGRAMAS_Y | C79 | `(vacía)` | `=IF(struct_state="OK",IF(ABS($J$8)<0.000000000001,IF(ABS($J$7)>0.000000000001,ult_p/$J$7,""),IF($J$7^2+2*$J$8*ult_p>=0,(-$J$7+(-1)*SQRT($J$7^2+2*$J$8*ult_p))/$J$8,"")),"")` | Raíz analítica de V(t)=a*t+b*t²/2-PH; discriminar tramo y radicando. |
| DIAGRAMAS_Y | D13 | `q_u corr` | `q_u sin truncar` | Presión bruta sin MAX(0,q). |
| DIAGRAMAS_Y | D14:D64 | `=MAX(0,C14)` | `=C14` | Sin truncamiento de presiones. |
| DIAGRAMAS_Y | D70:D72 | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B70)),$J$7*(B70+inp_by/2)^2/2+$J$8*(B70+inp_by/2)^3/6-ult_p*MAX(0,B70-inp_yc),"")` | Momento exacto en extremo/raíz. |
| DIAGRAMAS_Y | D73:D75 | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B73)),$J$7*(B73+inp_by/2)^2/2+$J$8*(B73+inp_by/2)^3/6-ult_p*MAX(0,B73-inp_yc)+ $J$9,"")` | Momento exacto en extremo/raíz. |
| DIAGRAMAS_Y | D76:D77 | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B76)),$J$7*(B76+inp_by/2)^2/2+$J$8*(B76+inp_by/2)^3/6-ult_p*MAX(0,B76-inp_yc),"")` | Momento exacto en extremo/raíz. |
| DIAGRAMAS_Y | D78:D79 | `(vacía)` | `=IF(AND(struct_state="OK",ISNUMBER(B78)),$J$7*(B78+inp_by/2)^2/2+$J$8*(B78+inp_by/2)^3/6-ult_p*MAX(0,B78-inp_yc)+ $J$9,"")` | Momento exacto en extremo/raíz. |
| DIAGRAMAS_Y | E14:E64 | `=inp_bx*D14` | `=IF(AND(struct_state="OK",A14<=inp_n_div_y),inp_bx*D14,"")` | Reacción bruta por unidad de longitud. |
| DIAGRAMAS_Y | F14:F64 | `=geo_w_total/inp_by` | `=IF(AND(struct_state="OK",A14<=inp_n_div_y),inp_bx*gross_weight_u,"")` | Mismos pesos del estado último; cancelan exactamente al obtener presión neta. |
| DIAGRAMAS_Y | G4 | `(vacía)` | `ERROR_FUERZAS_Y` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_Y | G5 | `(vacía)` | `ERROR_MOMENTOS_Y` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_Y | G6 | `(vacía)` | `Equilibrio Y` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_Y | G7 | `(vacía)` | `a: w neta borde izquierdo` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_Y | G8 | `(vacía)` | `b: pendiente w neta` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_Y | G9 | `(vacía)` | `Momento concentrado` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_Y | G10 | `(vacía)` | `Divisiones hasta columna` | Control visible de equilibrio y parámetros de integración exacta. |
| DIAGRAMAS_Y | G11 | `(vacía)` | `Caso actual` | Identificar las acciones del diagrama. |
| DIAGRAMAS_Y | G14:G64 | `=E14-F14` | `=IF(AND(struct_state="OK",A14<=inp_n_div_y),E14-F14,"")` | w neta estructural. |
| DIAGRAMAS_Y | H13 | `P_col tramo` | `P concentrada` | Acción concentrada de columna. |
| DIAGRAMAS_Y | H14 | `=0` | `=IF(AND(struct_state="OK",A14<=inp_n_div_y),IF(A14=$J$10+1,ult_p,0),"")` | P aplicada una sola vez en centro de columna. |
| DIAGRAMAS_Y | H15:H64 | `=ult_p*MAX(0,MIN(B15,inp_yc+inp_cy/2)-MAX(B14,inp_yc-inp_cy/2))/inp_cy` | `=IF(AND(struct_state="OK",A15<=inp_n_div_y),IF(A15=$J$10+1,ult_p,0),"")` | P aplicada una sola vez en centro de columna. |
| DIAGRAMAS_Y | I14 | `=0` | `=IF(AND(struct_state="OK",A14<=inp_n_div_y),$J$7*(B14+inp_by/2)+$J$8*(B14+inp_by/2)^2/2-IF(A14>$J$10,ult_p,0),"")` | V exacto: integral w - P H; salto antes/después de columna. |
| DIAGRAMAS_Y | I15:I64 | `=I14+((G14+G15)/2)*(B15-B14)-H15` | `=IF(AND(struct_state="OK",A15<=inp_n_div_y),$J$7*(B15+inp_by/2)+$J$8*(B15+inp_by/2)^2/2-IF(A15>$J$10,ult_p,0),"")` | V exacto: integral w - P H; salto antes/después de columna. |
| DIAGRAMAS_Y | J4 | `(vacía)` | `=IF(struct_state="OK",INDEX(I14:I64,inp_n_div_y+1),"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_Y | J5 | `(vacía)` | `=IF(struct_state="OK",INDEX(J14:J64,inp_n_div_y+1),"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_Y | J6 | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(AND(ABS(J4)<=MAX(0.000001,0.001*ABS(ult_p)),ABS(J5)<=MAX(0.000001,0.001*MAX(ABS((-ult_mx)),ABS(ult_p*inp_by)))),"OK","ERROR"))` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_Y | J7 | `(vacía)` | `=IF(struct_state="OK",inp_bx*(net_q0-net_gy*inp_by/2),"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_Y | J8 | `(vacía)` | `=IF(struct_state="OK",inp_bx*net_gy,"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_Y | J9 | `(vacía)` | `=IF(struct_state="OK",(-ult_mx),"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_Y | J10 | `(vacía)` | `=IF(struct_state="OK",MAX(1,MIN(inp_n_div_y-2,ROUND(inp_n_div_y*(inp_yc+inp_by/2)/inp_by,0))),"")` | Integración analítica; no se impone cero al extremo. |
| DIAGRAMAS_Y | J11 | `(vacía)` | `=inp_case` | Caso/combination actual. |
| DIAGRAMAS_Y | J14 | `=0` | `=IF(AND(struct_state="OK",A14<=inp_n_div_y),$J$7*(B14+inp_by/2)^2/2+$J$8*(B14+inp_by/2)^3/6-ult_p*MAX(0,B14-inp_yc)+IF(A14>$J$10,$J$9,0),"")` | M exacto: integral V + salto del momento de columna; no se cierra artificialmente el último punto. |
| DIAGRAMAS_Y | J15:J64 | `=J14+((I14+I15)/2)*(B15-B14)` | `=IF(AND(struct_state="OK",A15<=inp_n_div_y),$J$7*(B15+inp_by/2)^2/2+$J$8*(B15+inp_by/2)^3/6-ult_p*MAX(0,B15-inp_yc)+IF(A15>$J$10,$J$9,0),"")` | M exacto: integral V + salto del momento de columna; no se cierra artificialmente el último punto. |
| DIAGRAMAS_Y | K4 | `(vacía)` | `tonf` | Unidades del control. |
| DIAGRAMAS_Y | K5 | `(vacía)` | `tonf*m` | Unidades del control. |
| DIAGRAMAS_Y | K7 | `(vacía)` | `tonf/m` | Unidades del control. |
| DIAGRAMAS_Y | K8 | `(vacía)` | `tonf/m2` | Unidades del control. |
| DIAGRAMAS_Y | K9 | `(vacía)` | `tonf*m` | Unidades del control. |
| DIAGRAMAS_Y | K10 | `(vacía)` | `-` | Unidades del control. |
| DIAGRAMAS_Y | K14:K64 | `=IF(AND(B14>=inp_yc-inp_cy/2,B14<=inp_yc+inp_cy/2),"Si","No")` | `=IF(AND(struct_state="OK",A14<=inp_n_div_y),IF(AND(B14>=inp_yc-inp_cy/2,B14<=inp_yc+inp_cy/2),"Si","No"),"")` | Zona de columna conservada. |
| DIAGRAMAS_Y | L14:L64 | `=IF(D14=0,"Presion corregida por levantamiento","")` | `=IF(struct_state<>"OK",struct_state,IF(A14=$J$10+1,"SALTO P Y M",""))` | Advertencias mecánicas sin ocultar errores. |
| PUNZONAMIENTO | A20 | `(vacía)` | `β columna` | Lado largo / lado corto de columna. |
| PUNZONAMIENTO | A21 | `(vacía)` | `αs` | Parametrizado; BORDE/ESQUINA no usan perímetro interior. |
| PUNZONAMIENTO | A22 | `(vacía)` | `Factor conversión MPa a kgf/cm²` | 1/sqrt(0.0980665); 1 kgf/cm²=0.0980665 MPa. |
| PUNZONAMIENTO | A23 | `(vacía)` | `Vc1` | E.060 ecuación 11-33. |
| PUNZONAMIENTO | A24 | `(vacía)` | `Vc2` | E.060 ecuación 11-34. |
| PUNZONAMIENTO | A25 | `(vacía)` | `Vc3` | E.060 ecuación 11-35. |
| PUNZONAMIENTO | A26 | `(vacía)` | `Ecuación gobernante` | La menor resistencia nominal. |
| PUNZONAMIENTO | A27 | `(vacía)` | `φ` | E.060: 0.85. |
| PUNZONAMIENTO | A28 | `(vacía)` | `Estado de punzonamiento` | Control de contacto, peraltes y perímetro. |
| PUNZONAMIENTO | A29 | `(vacía)` | `Pu columna` | Carga vertical neta de superestructura. |
| PUNZONAMIENTO | A30 | `(vacía)` | `Reacción ascendente interior` | Integración exacta del campo lineal neto. |
| PUNZONAMIENTO | A31 | `(vacía)` | `b crítico X` | cx+d. |
| PUNZONAMIENTO | A32 | `(vacía)` | `b crítico Y` | cy+d. |
| PUNZONAMIENTO | A33 | `(vacía)` | `Ac = bo d` | Área resistente vertical del perímetro. |
| PUNZONAMIENTO | A34 | `(vacía)` | `Jcx` | Fig. 11.12.6: propiedad de sección crítica para Mx. |
| PUNZONAMIENTO | A35 | `(vacía)` | `Jcy` | Fig. 11.12.6: propiedad de sección crítica para My. |
| PUNZONAMIENTO | A36 | `(vacía)` | `γfx` | E.060 13.5.3.1; b1=dimensión en Y para Mx. |
| PUNZONAMIENTO | A37 | `(vacía)` | `γfy` | E.060 13.5.3.1; b1=dimensión en X para My. |
| PUNZONAMIENTO | A38 | `(vacía)` | `vu_max (absoluto)` | Máxima magnitud entre las cuatro esquinas; considera ambos momentos. |
| PUNZONAMIENTO | A39 | `(vacía)` | `vu_min (con signo)` | Control de inversión local del esfuerzo cortante. |
| PUNZONAMIENTO | A40 | `(vacía)` | `φ vn` | φ Vc/(bo*d). |
| PUNZONAMIENTO | A41 | `(vacía)` | `γvx` | Fracción de Mx por excentricidad de cortante. |
| PUNZONAMIENTO | A42 | `(vacía)` | `γvy` | Fracción de My por excentricidad de cortante. |
| PUNZONAMIENTO | A43 | `(vacía)` | `Mx entrada aplicada` | Acción global mano derecha sobre zapata. |
| PUNZONAMIENTO | A44 | `(vacía)` | `My entrada aplicada` | Acción global mano derecha sobre zapata. |
| PUNZONAMIENTO | A45 | `(vacía)` | `Mx transferido en perímetro` | Momento de columna + momento de reacción neta interior respecto a columna. |
| PUNZONAMIENTO | A46 | `(vacía)` | `My transferido en perímetro` | Momento de columna - primer momento neto interior en X. |
| PUNZONAMIENTO | A47 | `(vacía)` | `γfx Mx por flexión` | Detallar refuerzo local dentro de ancho efectivo E.060 13.5.3.1/3. |
| PUNZONAMIENTO | A48 | `(vacía)` | `γfy My por flexión` | Sin incremento opcional de γf permitido en 13.5.3.2. |
| PUNZONAMIENTO | A49 | `(vacía)` | `vu esquina +X,+Y` | vu=Vu/Ac-γvx Mx*y/Jcx+γvy My*x/Jcy. |
| PUNZONAMIENTO | A50 | `(vacía)` | `vu esquina +X,-Y` | Ambos momentos simultáneos. |
| PUNZONAMIENTO | A51 | `(vacía)` | `vu esquina -X,+Y` | Ambos momentos simultáneos. |
| PUNZONAMIENTO | A52 | `(vacía)` | `vu esquina -X,-Y` | Ambos momentos simultáneos. |
| PUNZONAMIENTO | A53 | `(vacía)` | `Caso / combinación actual` | Acciones actualmente ingresadas en CARGAS. |
| PUNZONAMIENTO | A54 | `(vacía)` | `Método de presión` | Pu y qu netos: sin doble cómputo de pesos de zapata/relleno. |
| PUNZONAMIENTO | A55 | `(vacía)` | `Ancho efectivo flexión por Mx` | Franja en X para momento Mx; E.060 13.5.3.1. |
| PUNZONAMIENTO | A56 | `(vacía)` | `Ancho efectivo flexión por My` | Franja en Y para momento My; E.060 13.5.3.1. |
| PUNZONAMIENTO | A57 | `(vacía)` | `Detalle local de transferencia` | El acero global por metro no acredita por sí solo el detalle local de conexión. |
| PUNZONAMIENTO | A58 | `(vacía)` | `vu_max (con signo)` | Se conserva también el máximo algebraico. |
| PUNZONAMIENTO | B6 | `=INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0))` | `=IF(geo_input_state="OK",INDEX(bar_diam_cm,MATCH(inp_bar_inf_x,bar_codes,0)),"")` | Diámetro real comercial; validar selección antes de INDEX/MATCH. |
| PUNZONAMIENTO | B7 | `=INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0))` | `=IF(geo_input_state="OK",INDEX(bar_diam_cm,MATCH(inp_bar_inf_y,bar_codes,0)),"")` | Diámetro real comercial; validar selección antes de INDEX/MATCH. |
| PUNZONAMIENTO | B8 | `=inp_h*100-inp_rec_inf-B6/2` | `=IF(geo_input_state="OK",inp_h*100-inp_rec_inf-IF(inp_order_inf="X inferior / Y superior",B6/2,B7+B6/2),"")` | dx según ubicación real de dos parrillas ortogonales superpuestas. |
| PUNZONAMIENTO | B9 | `=inp_h*100-inp_rec_inf-B7/2` | `=IF(geo_input_state="OK",inp_h*100-inp_rec_inf-IF(inp_order_inf="Y inferior / X superior",B7/2,B6+B7/2),"")` | dy según ubicación real de dos parrillas ortogonales superpuestas. |
| PUNZONAMIENTO | B10 | `=MIN(B8,B9)` | `=IF(geo_input_state="OK",(B8+B9)/2,"")` | d bidireccional = promedio dx/dy (centroide de capas ortogonales); nunca adoptar d máximo. |
| PUNZONAMIENTO | B11 | `=2*(B4+B10)+2*(B5+B10)` | `=IF(geo_input_state="OK",IF(AND(geo_input_state="OK",inp_col_type="INTERIOR",MIN(B8:B9)>0,geo_min_edge_dist>=MAX(inp_cx,inp_cy)/2+B10/100),2*(B4+B10)+2*(B5+B10),""),"")` | Perímetro completo a d/2 solo para interior con borde libre suficientemente alejado. Control conservador de perímetro abierto alternativo; IF externo evita evaluar peraltes vacíos en AND. |
| PUNZONAMIENTO | B12 | `=(inp_cx+B10/100)*(inp_cy+B10/100)` | `=IF(ISNUMBER(B11),(inp_cx+B10/100)*(inp_cy+B10/100),"")` | Área interior del perímetro completo en m². |
| PUNZONAMIENTO | B13 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*inp_yc+res_u_my_tot/geo_iy*inp_xc)` | `=IF(AND(struct_state="OK",ISNUMBER(B11)),net_q0+net_gx*inp_xc+net_gy*inp_yc,"")` | Presión estructural neta media sobre área rectangular simétrica en torno a columna. |
| PUNZONAMIENTO | B14 | `=MAX(0,ult_p-B13*B12)` | `=IF(B28="OK",ult_p-B13*B12,"")` | Vu neto = Pu - reacción neta interior, sin sumar/restar otra vez pesos propios. |
| PUNZONAMIENTO | B15 | `=0.53*SQRT(inp_fc)*B11*B10/1000` | `=IF(ISNUMBER(B11),MIN(B23:B25),"")` | Capacidad nominal mínima entre las tres expresiones E.060 11.12.2.1. |
| PUNZONAMIENTO | B16 | `=inp_phi_p*B15` | `=IF(ISNUMBER(B15),inp_phi_p*B15,"")` | phi punzonamiento=0.85; mantener visible. |
| PUNZONAMIENTO | B17 | `=IF(B16>0,B14/B16,999)` | `=IF(B28="OK",B38/B40,"")` | D/C por máximo esfuerzo debido a Vu, Mx y My simultáneos. |
| PUNZONAMIENTO | B18 | `=IF(B17<=1,"CUMPLE","NO CUMPLE")` | `=IF(B28<>"OK",B28,IF(B17<=1,"CUMPLE","NO CUMPLE"))` | No producir CUMPLE cuando el perímetro o el contacto no están resueltos. |
| PUNZONAMIENTO | B19 | `=IF(geo_min_edge_dist<B10/100,"La distancia de la columna al borde es menor que d; revisar cortante y punzonamiento.","")` | `=IF(inp_col_type<>"INTERIOR","BORDE/ESQUINA: REQUIERE GEOMETRÍA DE PERÍMETRO ABIERTO",IF(NOT(ISNUMBER(B11)),"BORDE LIBRE PRÓXIMO: REVISAR PERÍMETRO MÍNIMO",""))` | Control explícito del alcance del perímetro. |
| PUNZONAMIENTO | B20 | `(vacía)` | `=IF(geo_input_state="OK",MAX(B4,B5)/MIN(B4,B5),"")` | Lado largo / lado corto de columna. |
| PUNZONAMIENTO | B21 | `(vacía)` | `=IF(inp_col_type="INTERIOR",40,IF(inp_col_type="BORDE",30,IF(inp_col_type="ESQUINA",20,"")))` | Parametrizado; BORDE/ESQUINA no usan perímetro interior. |
| PUNZONAMIENTO | B22 | `(vacía)` | `3.193299567810587` | 1/sqrt(0.0980665); 1 kgf/cm²=0.0980665 MPa. |
| PUNZONAMIENTO | B23 | `(vacía)` | `=IF(ISNUMBER(B11),0.17*$B$22*(1+2/B20)*SQRT(inp_fc)*B11*B10/1000,"")` | E.060 ecuación 11-33. |
| PUNZONAMIENTO | B24 | `(vacía)` | `=IF(ISNUMBER(B11),0.083*$B$22*(B21*B10/B11+2)*SQRT(inp_fc)*B11*B10/1000,"")` | E.060 ecuación 11-34. |
| PUNZONAMIENTO | B25 | `(vacía)` | `=IF(ISNUMBER(B11),0.33*$B$22*SQRT(inp_fc)*B11*B10/1000,"")` | E.060 ecuación 11-35. |
| PUNZONAMIENTO | B26 | `(vacía)` | `=IF(ISNUMBER(B15),INDEX({"Vc1 (11-33)","Vc2 (11-34)","Vc3 (11-35)"},1,MATCH(B15,B23:B25,0)),"")` | La menor resistencia nominal. |
| PUNZONAMIENTO | B27 | `(vacía)` | `=inp_phi_p` | E.060: 0.85. |
| PUNZONAMIENTO | B28 | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(NOT(ISNUMBER(B11)),"REQUIERE GEOMETRÍA DE PERÍMETRO CRÍTICO","OK"))` | Control de contacto, peraltes y perímetro. |
| PUNZONAMIENTO | B29 | `(vacía)` | `=ult_p` | Carga vertical neta de superestructura. |
| PUNZONAMIENTO | B30 | `(vacía)` | `=IF(B28="OK",B13*B12,"")` | Integración exacta del campo lineal neto. |
| PUNZONAMIENTO | B31 | `(vacía)` | `=IF(ISNUMBER(B11),B4+B10,"")` | cx+d. |
| PUNZONAMIENTO | B32 | `(vacía)` | `=IF(ISNUMBER(B11),B5+B10,"")` | cy+d. |
| PUNZONAMIENTO | B33 | `(vacía)` | `=IF(ISNUMBER(B11),B11*B10,"")` | Área resistente vertical del perímetro. |
| PUNZONAMIENTO | B34 | `(vacía)` | `=IF(ISNUMBER(B11),B10*B32^3/6+B32*B10^3/6+B10*B31*B32^2/2,"")` | Fig. 11.12.6: propiedad de sección crítica para Mx. |
| PUNZONAMIENTO | B35 | `(vacía)` | `=IF(ISNUMBER(B11),B10*B31^3/6+B31*B10^3/6+B10*B32*B31^2/2,"")` | Fig. 11.12.6: propiedad de sección crítica para My. |
| PUNZONAMIENTO | B36 | `(vacía)` | `=IF(ISNUMBER(B11),1/(1+(2/3)*SQRT(B32/B31)),"")` | E.060 13.5.3.1; b1=dimensión en Y para Mx. |
| PUNZONAMIENTO | B37 | `(vacía)` | `=IF(ISNUMBER(B11),1/(1+(2/3)*SQRT(B31/B32)),"")` | E.060 13.5.3.1; b1=dimensión en X para My. |
| PUNZONAMIENTO | B38 | `(vacía)` | `=IF(B28="OK",MAX(MAX(B49:B52),-MIN(B49:B52)),"")` | Máxima magnitud entre las cuatro esquinas; considera ambos momentos. |
| PUNZONAMIENTO | B39 | `(vacía)` | `=IF(B28="OK",MIN(B49:B52),"")` | Control de inversión local del esfuerzo cortante. |
| PUNZONAMIENTO | B40 | `(vacía)` | `=IF(ISNUMBER(B16),B16*1000/B33,"")` | φ Vc/(bo*d). |
| PUNZONAMIENTO | B41 | `(vacía)` | `=IF(ISNUMBER(B11),1-B36,"")` | Fracción de Mx por excentricidad de cortante. |
| PUNZONAMIENTO | B42 | `(vacía)` | `=IF(ISNUMBER(B11),1-B37,"")` | Fracción de My por excentricidad de cortante. |
| PUNZONAMIENTO | B43 | `(vacía)` | `=ult_mx` | Acción global mano derecha sobre zapata. |
| PUNZONAMIENTO | B44 | `(vacía)` | `=ult_my` | Acción global mano derecha sobre zapata. |
| PUNZONAMIENTO | B45 | `(vacía)` | `=IF(B28="OK",ult_mx+net_gy*B12*(B32/100)^2/12,"")` | Momento de columna + momento de reacción neta interior respecto a columna. |
| PUNZONAMIENTO | B46 | `(vacía)` | `=IF(B28="OK",ult_my-net_gx*B12*(B31/100)^2/12,"")` | Momento de columna - primer momento neto interior en X. |
| PUNZONAMIENTO | B47 | `(vacía)` | `=IF(B28="OK",B36*B45,"")` | Detallar refuerzo local dentro de ancho efectivo E.060 13.5.3.1/3. |
| PUNZONAMIENTO | B48 | `(vacía)` | `=IF(B28="OK",B37*B46,"")` | Sin incremento opcional de γf permitido en 13.5.3.2. |
| PUNZONAMIENTO | B49 | `(vacía)` | `=IF(B28="OK",B14*1000/B33-B41*B45*100000*(B32/2)/B34+B42*B46*100000*(B31/2)/B35,"")` | vu=Vu/Ac-γvx Mx*y/Jcx+γvy My*x/Jcy. |
| PUNZONAMIENTO | B50 | `(vacía)` | `=IF(B28="OK",B14*1000/B33+B41*B45*100000*(B32/2)/B34+B42*B46*100000*(B31/2)/B35,"")` | Ambos momentos simultáneos. |
| PUNZONAMIENTO | B51 | `(vacía)` | `=IF(B28="OK",B14*1000/B33-B41*B45*100000*(B32/2)/B34-B42*B46*100000*(B31/2)/B35,"")` | Ambos momentos simultáneos. |
| PUNZONAMIENTO | B52 | `(vacía)` | `=IF(B28="OK",B14*1000/B33+B41*B45*100000*(B32/2)/B34-B42*B46*100000*(B31/2)/B35,"")` | Ambos momentos simultáneos. |
| PUNZONAMIENTO | B53 | `(vacía)` | `=inp_case` | Acciones actualmente ingresadas en CARGAS. |
| PUNZONAMIENTO | B54 | `(vacía)` | `NETO` | Pu y qu netos: sin doble cómputo de pesos de zapata/relleno. |
| PUNZONAMIENTO | B55 | `(vacía)` | `=IF(B28="OK",MIN(inp_bx,inp_cx+3*inp_h),"")` | Franja en X para momento Mx; E.060 13.5.3.1. |
| PUNZONAMIENTO | B56 | `(vacía)` | `=IF(B28="OK",MIN(inp_by,inp_cy+3*inp_h),"")` | Franja en Y para momento My; E.060 13.5.3.1. |
| PUNZONAMIENTO | B57 | `(vacía)` | `=IF(B28<>"OK",B28,IF(MAX(ABS(B47),ABS(B48))>0.000001,"ADVERTENCIA: VERIFICAR REFUERZO LOCAL γf Mu (13.5.3.3)","SIN MOMENTO TRANSFERIDO"))` | El acero global por metro no acredita por sí solo el detalle local de conexión. |
| PUNZONAMIENTO | B58 | `(vacía)` | `=IF(B28="OK",MAX(B49:B52),"")` | Se conserva también el máximo algebraico. |
| PUNZONAMIENTO | C18:C19 | `-` | `(vacía)` | Espacio de advertencia combinado; el resultado y la justificación se presentan en otras filas. |
| PUNZONAMIENTO | C20 | `(vacía)` | `-` | Lado largo / lado corto de columna. |
| PUNZONAMIENTO | C21 | `(vacía)` | `-` | Parametrizado; BORDE/ESQUINA no usan perímetro interior. |
| PUNZONAMIENTO | C22 | `(vacía)` | `-` | 1/sqrt(0.0980665); 1 kgf/cm²=0.0980665 MPa. |
| PUNZONAMIENTO | C23 | `(vacía)` | `tonf` | E.060 ecuación 11-33. |
| PUNZONAMIENTO | C24 | `(vacía)` | `tonf` | E.060 ecuación 11-34. |
| PUNZONAMIENTO | C25 | `(vacía)` | `tonf` | E.060 ecuación 11-35. |
| PUNZONAMIENTO | C26 | `(vacía)` | `-` | La menor resistencia nominal. |
| PUNZONAMIENTO | C27 | `(vacía)` | `-` | E.060: 0.85. |
| PUNZONAMIENTO | C29 | `(vacía)` | `tonf` | Carga vertical neta de superestructura. |
| PUNZONAMIENTO | C30 | `(vacía)` | `tonf` | Integración exacta del campo lineal neto. |
| PUNZONAMIENTO | C31 | `(vacía)` | `cm` | cx+d. |
| PUNZONAMIENTO | C32 | `(vacía)` | `cm` | cy+d. |
| PUNZONAMIENTO | C33 | `(vacía)` | `cm2` | Área resistente vertical del perímetro. |
| PUNZONAMIENTO | C34 | `(vacía)` | `cm4` | Fig. 11.12.6: propiedad de sección crítica para Mx. |
| PUNZONAMIENTO | C35 | `(vacía)` | `cm4` | Fig. 11.12.6: propiedad de sección crítica para My. |
| PUNZONAMIENTO | C36 | `(vacía)` | `-` | E.060 13.5.3.1; b1=dimensión en Y para Mx. |
| PUNZONAMIENTO | C37 | `(vacía)` | `-` | E.060 13.5.3.1; b1=dimensión en X para My. |
| PUNZONAMIENTO | C38 | `(vacía)` | `kgf/cm2` | Máxima magnitud entre las cuatro esquinas; considera ambos momentos. |
| PUNZONAMIENTO | C39 | `(vacía)` | `kgf/cm2` | Control de inversión local del esfuerzo cortante. |
| PUNZONAMIENTO | C40 | `(vacía)` | `kgf/cm2` | φ Vc/(bo*d). |
| PUNZONAMIENTO | C41 | `(vacía)` | `-` | Fracción de Mx por excentricidad de cortante. |
| PUNZONAMIENTO | C42 | `(vacía)` | `-` | Fracción de My por excentricidad de cortante. |
| PUNZONAMIENTO | C43:C44 | `(vacía)` | `tonf*m` | Acción global mano derecha sobre zapata. |
| PUNZONAMIENTO | C45 | `(vacía)` | `tonf*m` | Momento de columna + momento de reacción neta interior respecto a columna. |
| PUNZONAMIENTO | C46 | `(vacía)` | `tonf*m` | Momento de columna - primer momento neto interior en X. |
| PUNZONAMIENTO | C47 | `(vacía)` | `tonf*m` | Detallar refuerzo local dentro de ancho efectivo E.060 13.5.3.1/3. |
| PUNZONAMIENTO | C48 | `(vacía)` | `tonf*m` | Sin incremento opcional de γf permitido en 13.5.3.2. |
| PUNZONAMIENTO | C49 | `(vacía)` | `kgf/cm2` | vu=Vu/Ac-γvx Mx*y/Jcx+γvy My*x/Jcy. |
| PUNZONAMIENTO | C50:C52 | `(vacía)` | `kgf/cm2` | Ambos momentos simultáneos. |
| PUNZONAMIENTO | C53 | `(vacía)` | `-` | Acciones actualmente ingresadas en CARGAS. |
| PUNZONAMIENTO | C54 | `(vacía)` | `-` | Pu y qu netos: sin doble cómputo de pesos de zapata/relleno. |
| PUNZONAMIENTO | C55 | `(vacía)` | `m` | Franja en X para momento Mx; E.060 13.5.3.1. |
| PUNZONAMIENTO | C56 | `(vacía)` | `m` | Franja en Y para momento My; E.060 13.5.3.1. |
| PUNZONAMIENTO | C58 | `(vacía)` | `kgf/cm2` | Se conserva también el máximo algebraico. |
| PUNZONAMIENTO | D8 | `h - rinf - db/2` | `X: h-rec-dbX/2 o h-rec-dbY-dbX/2` | Ubicación física de X. |
| PUNZONAMIENTO | D9 | `h - rinf - db/2` | `Y: h-rec-dbY/2 o h-rec-dbX-dbY/2` | Ubicación física de Y. |
| PUNZONAMIENTO | D10 | `Usar minimo` | `Promedio (dx+dy)/2 para dos direcciones.` | Criterio explícito de peralte bidireccional. |
| PUNZONAMIENTO | D13 | `En centro de columna` | `qu neta promedio interior, sin truncar.` | Metodología neta. |
| PUNZONAMIENTO | D14 | `Vu = Pu - q*Acrit` | `Vu = Pu - qu_neta*Acrit.` | Metodología neta coherente. |
| PUNZONAMIENTO | D15 | `0.53*sqrt(fc)*bo*d` | `MIN(Vc1,Vc2,Vc3), E.060.` | Capacidad de punzonamiento corregida. |
| PUNZONAMIENTO | D17 | `Demanda / capacidad` | `vu_max absoluto / (phi*vn).` | Demanda biaxial, no solo Vu/(phi Vc). |
| PUNZONAMIENTO | D18 | `Punzonamiento` | `(vacía)` | Espacio de advertencia combinado; el resultado y la justificación se presentan en otras filas. |
| PUNZONAMIENTO | D19 | `Geometria` | `(vacía)` | Espacio de advertencia combinado; el resultado y la justificación se presentan en otras filas. |
| PUNZONAMIENTO | D20 | `(vacía)` | `Lado largo / lado corto de columna.` | Lado largo / lado corto de columna. |
| PUNZONAMIENTO | D21 | `(vacía)` | `Parametrizado; BORDE/ESQUINA no usan perímetro interior.` | Parametrizado; BORDE/ESQUINA no usan perímetro interior. |
| PUNZONAMIENTO | D22 | `(vacía)` | `1/sqrt(0.0980665); 1 kgf/cm²=0.0980665 MPa.` | 1/sqrt(0.0980665); 1 kgf/cm²=0.0980665 MPa. |
| PUNZONAMIENTO | D23 | `(vacía)` | `E.060 ecuación 11-33.` | E.060 ecuación 11-33. |
| PUNZONAMIENTO | D24 | `(vacía)` | `E.060 ecuación 11-34.` | E.060 ecuación 11-34. |
| PUNZONAMIENTO | D25 | `(vacía)` | `E.060 ecuación 11-35.` | E.060 ecuación 11-35. |
| PUNZONAMIENTO | D26 | `(vacía)` | `La menor resistencia nominal.` | La menor resistencia nominal. |
| PUNZONAMIENTO | D27 | `(vacía)` | `E.060: 0.85.` | E.060: 0.85. |
| PUNZONAMIENTO | D29 | `(vacía)` | `Carga vertical neta de superestructura.` | Carga vertical neta de superestructura. |
| PUNZONAMIENTO | D30 | `(vacía)` | `Integración exacta del campo lineal neto.` | Integración exacta del campo lineal neto. |
| PUNZONAMIENTO | D31 | `(vacía)` | `cx+d.` | cx+d. |
| PUNZONAMIENTO | D32 | `(vacía)` | `cy+d.` | cy+d. |
| PUNZONAMIENTO | D33 | `(vacía)` | `Área resistente vertical del perímetro.` | Área resistente vertical del perímetro. |
| PUNZONAMIENTO | D34 | `(vacía)` | `Fig. 11.12.6: propiedad de sección crítica para Mx.` | Fig. 11.12.6: propiedad de sección crítica para Mx. |
| PUNZONAMIENTO | D35 | `(vacía)` | `Fig. 11.12.6: propiedad de sección crítica para My.` | Fig. 11.12.6: propiedad de sección crítica para My. |
| PUNZONAMIENTO | D36 | `(vacía)` | `E.060 13.5.3.1; b1=dimensión en Y para Mx.` | E.060 13.5.3.1; b1=dimensión en Y para Mx. |
| PUNZONAMIENTO | D37 | `(vacía)` | `E.060 13.5.3.1; b1=dimensión en X para My.` | E.060 13.5.3.1; b1=dimensión en X para My. |
| PUNZONAMIENTO | D38 | `(vacía)` | `Máxima magnitud entre las cuatro esquinas; considera ambos momentos.` | Máxima magnitud entre las cuatro esquinas; considera ambos momentos. |
| PUNZONAMIENTO | D39 | `(vacía)` | `Control de inversión local del esfuerzo cortante.` | Control de inversión local del esfuerzo cortante. |
| PUNZONAMIENTO | D40 | `(vacía)` | `φ Vc/(bo*d).` | φ Vc/(bo*d). |
| PUNZONAMIENTO | D41 | `(vacía)` | `Fracción de Mx por excentricidad de cortante.` | Fracción de Mx por excentricidad de cortante. |
| PUNZONAMIENTO | D42 | `(vacía)` | `Fracción de My por excentricidad de cortante.` | Fracción de My por excentricidad de cortante. |
| PUNZONAMIENTO | D43:D44 | `(vacía)` | `Acción global mano derecha sobre zapata.` | Acción global mano derecha sobre zapata. |
| PUNZONAMIENTO | D45 | `(vacía)` | `Momento de columna + momento de reacción neta interior respecto a columna.` | Momento de columna + momento de reacción neta interior respecto a columna. |
| PUNZONAMIENTO | D46 | `(vacía)` | `Momento de columna - primer momento neto interior en X.` | Momento de columna - primer momento neto interior en X. |
| PUNZONAMIENTO | D47 | `(vacía)` | `Detallar refuerzo local dentro de ancho efectivo E.060 13.5.3.1/3.` | Detallar refuerzo local dentro de ancho efectivo E.060 13.5.3.1/3. |
| PUNZONAMIENTO | D48 | `(vacía)` | `Sin incremento opcional de γf permitido en 13.5.3.2.` | Sin incremento opcional de γf permitido en 13.5.3.2. |
| PUNZONAMIENTO | D49 | `(vacía)` | `vu=Vu/Ac-γvx Mx*y/Jcx+γvy My*x/Jcy.` | vu=Vu/Ac-γvx Mx*y/Jcx+γvy My*x/Jcy. |
| PUNZONAMIENTO | D50:D52 | `(vacía)` | `Ambos momentos simultáneos.` | Ambos momentos simultáneos. |
| PUNZONAMIENTO | D53 | `(vacía)` | `Acciones actualmente ingresadas en CARGAS.` | Acciones actualmente ingresadas en CARGAS. |
| PUNZONAMIENTO | D54 | `(vacía)` | `Pu y qu netos: sin doble cómputo de pesos de zapata/relleno.` | Pu y qu netos: sin doble cómputo de pesos de zapata/relleno. |
| PUNZONAMIENTO | D55 | `(vacía)` | `Franja en X para momento Mx; E.060 13.5.3.1.` | Franja en X para momento Mx; E.060 13.5.3.1. |
| PUNZONAMIENTO | D56 | `(vacía)` | `Franja en Y para momento My; E.060 13.5.3.1.` | Franja en Y para momento My; E.060 13.5.3.1. |
| PUNZONAMIENTO | D58 | `(vacía)` | `Se conserva también el máximo algebraico.` | Se conserva también el máximo algebraico. |
| CORTANTE_UNIDIRECCIONAL | A15 | `(vacía)` | `Vu_X` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | A16 | `(vacía)` | `φVc_X` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | A17 | `(vacía)` | `D/C_X` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | A18 | `(vacía)` | `Resultado X` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | A20 | `(vacía)` | `Vu_Y` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | A21 | `(vacía)` | `φVc_Y` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | A22 | `(vacía)` | `D/C_Y` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | A23 | `(vacía)` | `Resultado Y` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | B5 | `=(inp_xc-inp_cx/2)+inp_bx/2` | `=IF(struct_state="OK",(inp_xc-inp_cx/2)+inp_bx/2,"")` | Longitud libre fuera de cara de columna. |
| CORTANTE_UNIDIRECCIONAL | B6 | `=inp_bx/2-(inp_xc+inp_cx/2)` | `=IF(struct_state="OK",inp_bx/2-(inp_xc+inp_cx/2),"")` | Longitud libre fuera de cara de columna. |
| CORTANTE_UNIDIRECCIONAL | B7 | `=(inp_yc-inp_cy/2)+inp_by/2` | `=IF(struct_state="OK",(inp_yc-inp_cy/2)+inp_by/2,"")` | Longitud libre fuera de cara de columna. |
| CORTANTE_UNIDIRECCIONAL | B8 | `=inp_by/2-(inp_yc+inp_cy/2)` | `=IF(struct_state="OK",inp_by/2-(inp_yc+inp_cy/2),"")` | Longitud libre fuera de cara de columna. |
| CORTANTE_UNIDIRECCIONAL | B11 | `=MAX(F5:F8)` | `=IF(struct_state="OK",MAX(F5:F8),"")` | Resultados de cortante bloqueados sin contacto completo. |
| CORTANTE_UNIDIRECCIONAL | B12 | `=MAX(H5:H8)` | `=IF(struct_state="OK",MAX(H5:H8),"")` | Resultados de cortante bloqueados sin contacto completo. |
| CORTANTE_UNIDIRECCIONAL | B13 | `=IF(B12<=1,"CUMPLE","NO CUMPLE")` | `=IF(struct_state<>"OK",struct_state,IF(B12<=1,"CUMPLE","NO CUMPLE"))` | Estado global consistente con ambos ejes. |
| CORTANTE_UNIDIRECCIONAL | B15 | `(vacía)` | `=IF(struct_state="OK",MAX(F5:F6),"")` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | B16 | `(vacía)` | `=IF(struct_state="OK",G5,"")` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | B17 | `(vacía)` | `=IF(struct_state="OK",MAX(H5:H6),"")` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | B18 | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(B17<=1,"CUMPLE","NO CUMPLE"))` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | B20 | `(vacía)` | `=IF(struct_state="OK",MAX(F7:F8),"")` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | B21 | `(vacía)` | `=IF(struct_state="OK",G7,"")` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | B22 | `(vacía)` | `=IF(struct_state="OK",MAX(H7:H8),"")` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | B23 | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(B22<=1,"CUMPLE","NO CUMPLE"))` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | C5:C6 | `=MAX(0,B5-punz_d_cm/100)` | `=IF(struct_state="OK",MAX(0,B5-punz_d_x/100),"")` | Sección crítica a d propio de dirección desde cara; MAX solo delimita longitud geométrica. |
| CORTANTE_UNIDIRECCIONAL | C7:C8 | `=MAX(0,B7-punz_d_cm/100)` | `=IF(struct_state="OK",MAX(0,B7-punz_d_y/100),"")` | Sección crítica a d propio de dirección desde cara; MAX solo delimita longitud geométrica. |
| CORTANTE_UNIDIRECCIONAL | C15:C16 | `(vacía)` | `tonf/m` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | C17:C18 | `(vacía)` | `-` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | C20:C21 | `(vacía)` | `tonf/m` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | C22:C23 | `(vacía)` | `-` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | D5 | `=(q_u_mx_py+q_u_mx_my)/2` | `=IF(struct_state="OK",net_q0+net_gx*(-inp_bx/2+C5/2)+gross_weight_u,"")` | Presión bruta media exacta del segmento crítico; no presión extrema del borde. |
| CORTANTE_UNIDIRECCIONAL | D6 | `=(q_u_px_py+q_u_px_my)/2` | `=IF(struct_state="OK",net_q0+net_gx*(inp_bx/2-C6/2)+gross_weight_u,"")` | Presión bruta media exacta del segmento crítico; no presión extrema del borde. |
| CORTANTE_UNIDIRECCIONAL | D7 | `=(q_u_px_my+q_u_mx_my)/2` | `=IF(struct_state="OK",net_q0+net_gy*(-inp_by/2+C7/2)+gross_weight_u,"")` | Presión bruta media exacta del segmento crítico; no presión extrema del borde. |
| CORTANTE_UNIDIRECCIONAL | D8 | `=(q_u_px_py+q_u_mx_py)/2` | `=IF(struct_state="OK",net_q0+net_gy*(inp_by/2-C8/2)+gross_weight_u,"")` | Presión bruta media exacta del segmento crítico; no presión extrema del borde. |
| CORTANTE_UNIDIRECCIONAL | D15:D18 | `(vacía)` | `Resultados independientes por dirección, con d propio.` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | D20:D23 | `(vacía)` | `Resultados independientes por dirección, con d propio.` | Resultados independientes por dirección, con d propio. |
| CORTANTE_UNIDIRECCIONAL | E5 | `=MAX(0,D5-geo_w_total/geo_area)` | `=IF(struct_state="OK",net_q0+net_gx*(-inp_bx/2+C5/2),"")` | Presión neta media; sin truncar. |
| CORTANTE_UNIDIRECCIONAL | E6 | `=MAX(0,D6-geo_w_total/geo_area)` | `=IF(struct_state="OK",net_q0+net_gx*(inp_bx/2-C6/2),"")` | Presión neta media; sin truncar. |
| CORTANTE_UNIDIRECCIONAL | E7 | `=MAX(0,D7-geo_w_total/geo_area)` | `=IF(struct_state="OK",net_q0+net_gy*(-inp_by/2+C7/2),"")` | Presión neta media; sin truncar. |
| CORTANTE_UNIDIRECCIONAL | E8 | `=MAX(0,D8-geo_w_total/geo_area)` | `=IF(struct_state="OK",net_q0+net_gy*(inp_by/2-C8/2),"")` | Presión neta media; sin truncar. |
| CORTANTE_UNIDIRECCIONAL | F5:F8 | `=E5*C5` | `=IF(struct_state="OK",ABS(E5*C5),"")` | Vu por metro = integral exacta q neta; ABS de demanda cortante, nunca de P. |
| CORTANTE_UNIDIRECCIONAL | G5:G6 | `=inp_phi_v*0.53*SQRT(inp_fc)*100*punz_d_cm/1000` | `=IF(struct_state="OK",inp_phi_v*0.17*PUNZONAMIENTO!$B$22*SQRT(inp_fc)*100*punz_d_x/1000,"")` | Cortante como viga E.060 11.3.1.1 en kgf/cm², b=100cm; conversión rigurosa de 0.17 MPa. |
| CORTANTE_UNIDIRECCIONAL | G7:G8 | `=inp_phi_v*0.53*SQRT(inp_fc)*100*punz_d_cm/1000` | `=IF(struct_state="OK",inp_phi_v*0.17*PUNZONAMIENTO!$B$22*SQRT(inp_fc)*100*punz_d_y/1000,"")` | Cortante como viga E.060 11.3.1.1 en kgf/cm², b=100cm; conversión rigurosa de 0.17 MPa. |
| CORTANTE_UNIDIRECCIONAL | H5:H8 | `=IF(G5>0,F5/G5,999)` | `=IF(struct_state="OK",F5/G5,"")` | D/C individual por sección y dirección. |
| FLEXION_ACERO | A14 | `(vacía)` | `Momento negativo X` | Signo negativo explícito; acero superior requerido si <0. |
| FLEXION_ACERO | A15 | `(vacía)` | `Momento negativo Y` | Signo negativo explícito; acero superior requerido si <0. |
| FLEXION_ACERO | A16 | `(vacía)` | `Advertencia acero superior` | Envolvente actual exacta. |
| FLEXION_ACERO | A17 | `(vacía)` | `Transferencia local γf Mu` | Verificar concentración/anclaje en franjas de E.060 13.5.3.1/3. |
| FLEXION_ACERO | B14 | `(vacía)` | `=IF(struct_state="OK",-diagx_m_neg/inp_by,"")` | Signo negativo explícito; acero superior requerido si <0. |
| FLEXION_ACERO | B15 | `(vacía)` | `=IF(struct_state="OK",-diagy_m_neg/inp_bx,"")` | Signo negativo explícito; acero superior requerido si <0. |
| FLEXION_ACERO | B16 | `(vacía)` | `=IF(struct_state<>"OK",struct_state,IF(MAX(D7:D8)>0.000001,"REQUIERE ACERO SUPERIOR POR INVERSIÓN DE MOMENTO","SIN DEMANDA NEGATIVA GLOBAL"))` | Envolvente actual exacta. |
| FLEXION_ACERO | B17 | `(vacía)` | `=PUNZONAMIENTO!B57` | Verificar concentración/anclaje en franjas de E.060 13.5.3.1/3. |
| FLEXION_ACERO | C14:C15 | `(vacía)` | `tonf*m/m` | Signo negativo explícito; acero superior requerido si <0. |
| FLEXION_ACERO | C16 | `(vacía)` | `-` | Envolvente actual exacta. |
| FLEXION_ACERO | C17 | `(vacía)` | `-` | Verificar concentración/anclaje en franjas de E.060 13.5.3.1/3. |
| FLEXION_ACERO | D5 | `=diagx_m_pos/inp_by` | `=IF(struct_state="OK",diagx_m_pos/inp_by,"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | D6 | `=diagy_m_pos/inp_bx` | `=IF(struct_state="OK",diagy_m_pos/inp_bx,"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | D7 | `=diagx_m_neg/inp_by` | `=IF(struct_state="OK",diagx_m_neg/inp_by,"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | D8 | `=diagy_m_neg/inp_bx` | `=IF(struct_state="OK",diagy_m_neg/inp_bx,"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | D14:D15 | `(vacía)` | `Signo negativo explícito; acero superior requerido si <0.` | Signo negativo explícito; acero superior requerido si <0. |
| FLEXION_ACERO | D16 | `(vacía)` | `Envolvente actual exacta.` | Envolvente actual exacta. |
| FLEXION_ACERO | D17 | `(vacía)` | `Verificar concentración/anclaje en franjas de E.060 13.5.3.1/3.` | Verificar concentración/anclaje en franjas de E.060 13.5.3.1/3. |
| FLEXION_ACERO | E5 | `=punz_d_x` | `=IF(struct_state="OK",punz_d_x,"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | E6 | `=punz_d_y` | `=IF(struct_state="OK",punz_d_y,"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | E7 | `=inp_h*100-inp_rec_sup-INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))/2` | `=IF(struct_state="OK",inp_h*100-inp_rec_sup-IF(inp_order_sup="X exterior / Y interior",INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))/2,INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))+INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))/2),"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | E8 | `=inp_h*100-inp_rec_sup-INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))/2` | `=IF(struct_state="OK",inp_h*100-inp_rec_sup-IF(inp_order_sup="Y exterior / X interior",INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))/2,INDEX(bar_diam_cm,MATCH(inp_bar_sup_x,bar_codes,0))+INDEX(bar_diam_cm,MATCH(inp_bar_sup_y,bar_codes,0))/2),"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | F5:F8 | `=IF(D5<=0,0,IF((inp_fy*E5)^2-4*(inp_fy^2/(2*0.85*inp_fc*100))*(D5*100000/inp_phi_f)<0,999,(inp_fy*E5-SQRT((inp_fy*E5)^2-4*(inp_fy^2/(2*0.85*inp_fc*100))*(D5*100000/inp_phi_f)))/(2*(inp_fy^2/(2*0.85*inp_fc*100)))))` | `=IF(struct_state="OK",IF(D5<=0,0,IF((inp_fy*E5)^2-4*(inp_fy^2/(2*0.85*inp_fc*100))*(D5*100000/inp_phi_f)<0,999,(inp_fy*E5-SQRT((inp_fy*E5)^2-4*(inp_fy^2/(2*0.85*inp_fc*100))*(D5*100000/inp_phi_f)))/(2*(inp_fy^2/(2*0.85*inp_fc*100))))),"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | G5:G8 | `=IF(OR(B5="Inferior",D5>0),inp_rho_min*100*inp_h*100,0)` | `=IF(struct_state="OK",IF(OR(B5="Inferior",D5>0),inp_rho_min*100*inp_h*100,0),"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | H5:H8 | `=IF(F5=999,999,MAX(F5,G5))` | `=IF(struct_state="OK",IF(F5=999,999,MAX(F5,G5)),"")` | Preservar fórmula clásica de acero; corregir peralte por capa y bloquear demanda sin contacto completo. |
| FLEXION_ACERO | H12 | `=acero_dc_max` | `=IF(struct_state="OK",acero_dc_max,"")` | Resultado global de acero; propagar bloqueo físico. |
| FLEXION_ACERO | I5:I8 | `=IF(F5=999,"REVISAR SECCION","VER DETALLADO")` | `=IF(struct_state<>"OK",struct_state,IF(E5<=0,"PERALTE NO POSITIVO",IF(F5=999,"REVISAR SECCION","VER DETALLADO")))` | No declarar resultado favorable sin cálculo aplicable. |
| ACERO_DETALLADO | B11 | `=MAX(IF(H5>0,D5/H5,0),IF(H6>0,D6/H6,0),IF(H7>0,D7/H7,0),IF(H8>0,D8/H8,0))` | `=IF(struct_state="OK",MAX(IF(H5>0,D5/H5,0),IF(H6>0,D6/H6,0),IF(H7>0,D7/H7,0),IF(H8>0,D8/H8,0)),"")` | D/C de acero sin ocultar bloqueo. |
| ACERO_DETALLADO | B12 | `=IF(COUNTIF(J5:J8,"NO CUMPLE")=0,"CUMPLE","NO CUMPLE")` | `=IF(struct_state<>"OK",struct_state,IF(COUNTIF(J5:J8,"NO CUMPLE")=0,"CUMPLE","NO CUMPLE"))` | No considerar textos de bloqueo como ausencia de NO CUMPLE. |
| ACERO_DETALLADO | C5:C8 | `=INDEX(bar_area_cm2,MATCH(B5,bar_codes,0))` | `=IF(COUNTIF(bar_codes,B5)=1,INDEX(bar_area_cm2,MATCH(B5,bar_codes,0)),"")` | Si el código de barra no existe, mostrar entrada no válida sin generar #N/A. |
| ACERO_DETALLADO | D5 | `=flex_as_req_inf_x` | `=IF(struct_state="OK",flex_as_req_inf_x,"")` | Acero requerido/colocado conserva entradas; estados dependientes del contacto no calculables se muestran bloqueados. |
| ACERO_DETALLADO | D6 | `=flex_as_req_inf_y` | `=IF(struct_state="OK",flex_as_req_inf_y,"")` | Acero requerido/colocado conserva entradas; estados dependientes del contacto no calculables se muestran bloqueados. |
| ACERO_DETALLADO | D7 | `=flex_as_req_sup_x` | `=IF(struct_state="OK",flex_as_req_sup_x,"")` | Acero requerido/colocado conserva entradas; estados dependientes del contacto no calculables se muestran bloqueados. |
| ACERO_DETALLADO | D8 | `=flex_as_req_sup_y` | `=IF(struct_state="OK",flex_as_req_sup_y,"")` | Acero requerido/colocado conserva entradas; estados dependientes del contacto no calculables se muestran bloqueados. |
| ACERO_DETALLADO | E5:E8 | `=IF(D5<=0,"No requerido",C5*100/D5)` | `=IF(struct_state="OK",IF(D5<=0,"No requerido",C5*100/D5),"")` | Acero requerido/colocado conserva entradas; estados dependientes del contacto no calculables se muestran bloqueados. |
| ACERO_DETALLADO | H5:H8 | `=IF(D5<=0,0,C5*100/F5)` | `=IF(struct_state="OK",IF(D5<=0,0,C5*100/F5),"")` | Acero requerido/colocado conserva entradas; estados dependientes del contacto no calculables se muestran bloqueados. |
| ACERO_DETALLADO | I5:I8 | `=IF(D5<=0,1,H5/D5)` | `=IF(struct_state="OK",IF(D5<=0,1,H5/D5),"")` | Acero requerido/colocado conserva entradas; estados dependientes del contacto no calculables se muestran bloqueados. |
| ACERO_DETALLADO | J5:J8 | `=IF(D5<=0,"CUMPLE",IF(AND(H5>=D5,F5<=G5),"CUMPLE","NO CUMPLE"))` | `=IF(struct_state<>"OK",struct_state,IF(D5<=0,"CUMPLE",IF(AND(H5>=D5,F5<=G5),"CUMPLE","NO CUMPLE")))` | No convertir falta de cálculo en CUMPLE. |
| GRAFICOS | A4 | `=-inp_bx/2` | `=IF(geo_input_state="OK",-inp_bx/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | A5:A6 | `=inp_bx/2` | `=IF(geo_input_state="OK",inp_bx/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | A7:A8 | `=-inp_bx/2` | `=IF(geo_input_state="OK",-inp_bx/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | A26 | `=-inp_bx/2` | `=IF(geo_input_state="OK",-inp_bx/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | A27 | `=inp_bx/2` | `=IF(geo_input_state="OK",inp_bx/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | A132 | `=inp_bar_inf_x&" @ "&inp_sep_inf_x&" cm en X"` | `=IF(geo_input_state="OK",inp_bar_inf_x&" @ "&inp_sep_inf_x&" cm en X","")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | A133 | `=inp_bar_inf_y&" @ "&inp_sep_inf_y&" cm en Y"` | `=IF(geo_input_state="OK",inp_bar_inf_y&" @ "&inp_sep_inf_y&" cm en Y","")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B4:B5 | `=-inp_by/2` | `=IF(geo_input_state="OK",-inp_by/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B6:B7 | `=inp_by/2` | `=IF(geo_input_state="OK",inp_by/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B8 | `=-inp_by/2` | `=IF(geo_input_state="OK",-inp_by/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B12 | `=q_srv_px_py` | `=IF(geo_input_state="OK",q_srv_px_py,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B13 | `=q_srv_px_my` | `=IF(geo_input_state="OK",q_srv_px_my,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B14 | `=q_srv_mx_py` | `=IF(geo_input_state="OK",q_srv_mx_py,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B15 | `=q_srv_mx_my` | `=IF(geo_input_state="OK",q_srv_mx_my,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B19 | `=flex_as_req_inf_x` | `=IF(struct_state="OK",flex_as_req_inf_x,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B20 | `=flex_as_req_inf_y` | `=IF(struct_state="OK",flex_as_req_inf_y,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B21 | `=flex_as_req_sup_x` | `=IF(struct_state="OK",flex_as_req_sup_x,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B22 | `=flex_as_req_sup_y` | `=IF(struct_state="OK",flex_as_req_sup_y,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | B26:B27 | `=-inp_by/2-MAX(inp_bx,inp_by)*0.08` | `=IF(geo_input_state="OK",-inp_by/2-MAX(inp_bx,inp_by)*0.08,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | C4 | `=inp_xc-inp_cx/2` | `=IF(geo_input_state="OK",inp_xc-inp_cx/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | C5:C6 | `=inp_xc+inp_cx/2` | `=IF(geo_input_state="OK",inp_xc+inp_cx/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | C7:C8 | `=inp_xc-inp_cx/2` | `=IF(geo_input_state="OK",inp_xc-inp_cx/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | C9 | `=inp_xc` | `=IF(geo_input_state="OK",inp_xc,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | C12:C15 | `=inp_qadm` | `=IF(geo_input_state="OK",inp_qadm,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | C19 | `=steel_as_inf_x` | `=IF(struct_state="OK",steel_as_inf_x,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | C20 | `=steel_as_inf_y` | `=IF(struct_state="OK",steel_as_inf_y,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | C21 | `=steel_as_sup_x` | `=IF(struct_state="OK",steel_as_sup_x,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | C22 | `=steel_as_sup_y` | `=IF(struct_state="OK",steel_as_sup_y,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | C26:C27 | `=-inp_bx/2-MAX(inp_bx,inp_by)*0.08` | `=IF(geo_input_state="OK",-inp_bx/2-MAX(inp_bx,inp_by)*0.08,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D4:D5 | `=inp_yc-inp_cy/2` | `=IF(geo_input_state="OK",inp_yc-inp_cy/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D6:D7 | `=inp_yc+inp_cy/2` | `=IF(geo_input_state="OK",inp_yc+inp_cy/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D8 | `=inp_yc-inp_cy/2` | `=IF(geo_input_state="OK",inp_yc-inp_cy/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D9 | `=inp_yc` | `=IF(geo_input_state="OK",inp_yc,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D12 | `=q_u_px_py` | `=IF(geo_input_state="OK",q_u_px_py,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D13 | `=q_u_px_my` | `=IF(geo_input_state="OK",q_u_px_my,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D14 | `=q_u_mx_py` | `=IF(geo_input_state="OK",q_u_mx_py,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D15 | `=q_u_mx_my` | `=IF(geo_input_state="OK",q_u_mx_my,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D26 | `=-inp_by/2` | `=IF(geo_input_state="OK",-inp_by/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D27 | `=inp_by/2` | `=IF(geo_input_state="OK",inp_by/2,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D132 | `=IF(flex_as_req_sup_x>0,inp_bar_sup_x&" @ "&inp_sep_sup_x&" cm en X","No requerido por momento negativo X")` | `=IF(struct_state="OK",IF(flex_as_req_sup_x>0,inp_bar_sup_x&" @ "&inp_sep_sup_x&" cm en X","No requerido por momento negativo X"),"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | D133 | `=IF(flex_as_req_sup_y>0,inp_bar_sup_y&" @ "&inp_sep_sup_y&" cm en Y","No requerido por momento negativo Y")` | `=IF(struct_state="OK",IF(flex_as_req_sup_y>0,inp_bar_sup_y&" @ "&inp_sep_sup_y&" cm en Y","No requerido por momento negativo Y"),"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | E4 | `=res_srv_ex` | `=IF(geo_input_state="OK",res_srv_ex,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | F4 | `=res_srv_ey` | `=IF(geo_input_state="OK",res_srv_ey,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | G4 | `=res_u_ex` | `=IF(geo_input_state="OK",res_u_ex,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | H4 | `=res_u_ey` | `=IF(geo_input_state="OK",res_u_ey,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J3 | `Mapa presion servicio (tonf/m2)` | `PRESIONES SERVICIO SIN TRUNCAR` | Mapa de presión lineal conserva valores negativos y advierte contacto parcial. |
| GRAFICOS | J5 | `=-0.5*inp_by` | `=IF(geo_input_state="OK",-0.5*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J6 | `=-0.4*inp_by` | `=IF(geo_input_state="OK",-0.4*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J7 | `=-0.3*inp_by` | `=IF(geo_input_state="OK",-0.3*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J8 | `=-0.2*inp_by` | `=IF(geo_input_state="OK",-0.2*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J9 | `=-0.0999999999999999*inp_by` | `=IF(geo_input_state="OK",-0.0999999999999999*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J10 | `=0*inp_by` | `=IF(geo_input_state="OK",0*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J11 | `=0.0999999999999999*inp_by` | `=IF(geo_input_state="OK",0.0999999999999999*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J12 | `=0.199999999999999*inp_by` | `=IF(geo_input_state="OK",0.199999999999999*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J13 | `=0.3*inp_by` | `=IF(geo_input_state="OK",0.3*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J14 | `=0.4*inp_by` | `=IF(geo_input_state="OK",0.4*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J15 | `=0.5*inp_by` | `=IF(geo_input_state="OK",0.5*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J19 | `Mapa presion ultima (tonf/m2)` | `PRESIONES ÚLTIMAS SIN TRUNCAR` | Mapa de presión lineal conserva valores negativos y advierte contacto parcial. |
| GRAFICOS | J21 | `=-0.5*inp_by` | `=IF(geo_input_state="OK",-0.5*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J22 | `=-0.4*inp_by` | `=IF(geo_input_state="OK",-0.4*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J23 | `=-0.3*inp_by` | `=IF(geo_input_state="OK",-0.3*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J24 | `=-0.2*inp_by` | `=IF(geo_input_state="OK",-0.2*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J25 | `=-0.0999999999999999*inp_by` | `=IF(geo_input_state="OK",-0.0999999999999999*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J26 | `=0*inp_by` | `=IF(geo_input_state="OK",0*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J27 | `=0.0999999999999999*inp_by` | `=IF(geo_input_state="OK",0.0999999999999999*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J28 | `=0.199999999999999*inp_by` | `=IF(geo_input_state="OK",0.199999999999999*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J29 | `=0.3*inp_by` | `=IF(geo_input_state="OK",0.3*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J30 | `=0.4*inp_by` | `=IF(geo_input_state="OK",0.4*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | J31 | `=0.5*inp_by` | `=IF(geo_input_state="OK",0.5*inp_by,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | K4 | `=-0.5*inp_bx` | `=IF(geo_input_state="OK",-0.5*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | K5:K15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*K$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*K$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | K20 | `=-0.5*inp_bx` | `=IF(geo_input_state="OK",-0.5*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | K21:K31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*K$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*K$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | L4 | `=-0.4*inp_bx` | `=IF(geo_input_state="OK",-0.4*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | L5:L15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*L$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*L$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | L20 | `=-0.4*inp_bx` | `=IF(geo_input_state="OK",-0.4*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | L21:L31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*L$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*L$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | M4 | `=-0.3*inp_bx` | `=IF(geo_input_state="OK",-0.3*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | M5:M15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*M$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*M$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | M20 | `=-0.3*inp_bx` | `=IF(geo_input_state="OK",-0.3*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | M21:M31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*M$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*M$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | N4 | `=-0.2*inp_bx` | `=IF(geo_input_state="OK",-0.2*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | N5:N15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*N$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*N$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | N20 | `=-0.2*inp_bx` | `=IF(geo_input_state="OK",-0.2*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | N21:N31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*N$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*N$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | O4 | `=-0.0999999999999999*inp_bx` | `=IF(geo_input_state="OK",-0.0999999999999999*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | O5:O15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*O$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*O$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | O20 | `=-0.0999999999999999*inp_bx` | `=IF(geo_input_state="OK",-0.0999999999999999*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | O21:O31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*O$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*O$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | P4 | `=0*inp_bx` | `=IF(geo_input_state="OK",0*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | P5:P15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*P$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*P$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | P20 | `=0*inp_bx` | `=IF(geo_input_state="OK",0*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | P21:P31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*P$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*P$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | Q4 | `=0.0999999999999999*inp_bx` | `=IF(geo_input_state="OK",0.0999999999999999*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | Q5:Q15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*Q$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*Q$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | Q20 | `=0.0999999999999999*inp_bx` | `=IF(geo_input_state="OK",0.0999999999999999*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | Q21:Q31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*Q$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*Q$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | R4 | `=0.199999999999999*inp_bx` | `=IF(geo_input_state="OK",0.199999999999999*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | R5:R15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*R$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*R$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | R20 | `=0.199999999999999*inp_bx` | `=IF(geo_input_state="OK",0.199999999999999*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | R21:R31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*R$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*R$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | S4 | `=0.3*inp_bx` | `=IF(geo_input_state="OK",0.3*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | S5:S15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*S$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*S$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | S20 | `=0.3*inp_bx` | `=IF(geo_input_state="OK",0.3*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | S21:S31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*S$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*S$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | T4 | `=0.4*inp_bx` | `=IF(geo_input_state="OK",0.4*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | T5:T15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*T$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*T$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | T20 | `=0.4*inp_bx` | `=IF(geo_input_state="OK",0.4*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | T21:T31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*T$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*T$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | U4 | `=0.5*inp_bx` | `=IF(geo_input_state="OK",0.5*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | U5:U15 | `=MAX(0,res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*U$4)` | `=IF(geo_input_state="OK",res_srv_p_tot/geo_area+res_srv_mx_tot/geo_ix*$J5+res_srv_my_tot/geo_iy*U$4,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | U20 | `=0.5*inp_bx` | `=IF(geo_input_state="OK",0.5*inp_bx,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| GRAFICOS | U21:U31 | `=MAX(0,res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*U$20)` | `=IF(geo_input_state="OK",res_u_p_tot/geo_area+res_u_mx_tot/geo_ix*$J21+res_u_my_tot/geo_iy*U$20,"")` | Preservar tablas/gráficos existentes y propagar estado de entradas; sin aplanar fórmulas. |
| RESUMEN | A38 | `Las cargas verticales tienen signo negativo; verificar convencion de SAP2000.` | `Carga de columna en levantamiento / tracción real.` | Convención de signo conserva física. |
| RESUMEN | A41 | `(vacía)` | `RESULTADOS TÉCNICOS FASE 1` | Ampliación mínima del resumen original. |
| RESUMEN | A42 | `(vacía)` | `Caso actual` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A43 | `(vacía)` | `dx` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A44 | `(vacía)` | `Contacto servicio` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A45 | `(vacía)` | `Vc1` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A46 | `(vacía)` | `Vc3` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A47 | `(vacía)` | `Ecuación gobernante` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A48 | `(vacía)` | `vu_max absoluto` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A49 | `(vacía)` | `D/C punzonamiento` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A50 | `(vacía)` | `D/C cortante X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A51 | `(vacía)` | `D/C cortante Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A52 | `(vacía)` | `M positivo X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A53 | `(vacía)` | `As requerido inf X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A54 | `(vacía)` | `As requerido sup X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A55 | `(vacía)` | `M positivo Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A56 | `(vacía)` | `As requerido inf Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A57 | `(vacía)` | `As requerido sup Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A58 | `(vacía)` | `ERROR_FUERZAS_X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A59 | `(vacía)` | `ERROR_FUERZAS_Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A60 | `(vacía)` | `Equilibrio X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A61 | `(vacía)` | `γfx Mx` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A62 | `(vacía)` | `Detalle local` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A63 | `(vacía)` | `Vu neto` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | A64 | `(vacía)` | `Área interior` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B23 | `=IF(AND(q_srv_max<=inp_qadm,q_srv_min>=0,punz_result="CUMPLE",cort_result="CUMPLE",acero_result="CUMPLE",acero_sep_result="CUMPLE",geo_col_inside_status="CUMPLE",res_srv_nucleo="CUMPLE"),"CUMPLE","NO CUMPLE")` | `=IF(OR(PRESIONES_SERVICIO!D14<>"CONTACTO COMPLETO",struct_state<>"OK"),"REQUIERE REVISIÓN DE CONTACTO / DATOS",IF(punz_state<>"OK",punz_state,IF(AND(q_srv_max<=inp_qadm,punz_result="CUMPLE",cort_result="CUMPLE",acero_result="CUMPLE",acero_sep_result="CUMPLE",geo_col_inside_status="CUMPLE",eq_x="OK",eq_y="OK"),IF(PUNZONAMIENTO!B57="SIN MOMENTO TRANSFERIDO","CUMPLE","ADVERTENCIA: VERIFICAR REFUERZO LOCAL γf Mu"),"NO CUMPLE")))` | Conservar NO CUMPLE real; no certificar conexión local sin detalle γfMu y equilibrio. |
| RESUMEN | B38 | `=IF(OR(srv_raw_p<0,ult_raw_p<0),"ACTIVA","")` | `=IF(OR(srv_p<=0,ult_p<=0),"ACTIVA","")` | Detectar signo interno, no signo crudo del programa. |
| RESUMEN | B42 | `(vacía)` | `=inp_case` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B43 | `(vacía)` | `=punz_d_x` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B44 | `(vacía)` | `=PRESIONES_SERVICIO!D14` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B45 | `(vacía)` | `=punz_vc1` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B46 | `(vacía)` | `=punz_vc3` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B47 | `(vacía)` | `=PUNZONAMIENTO!B26` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B48 | `(vacía)` | `=punz_vumax` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B49 | `(vacía)` | `=punz_dc` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B50 | `(vacía)` | `=CORTANTE_UNIDIRECCIONAL!B17` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B51 | `(vacía)` | `=CORTANTE_UNIDIRECCIONAL!B22` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B52 | `(vacía)` | `=flex_mu_inf_x` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B53 | `(vacía)` | `=flex_as_req_inf_x` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B54 | `(vacía)` | `=flex_as_req_sup_x` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B55 | `(vacía)` | `=flex_mu_inf_y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B56 | `(vacía)` | `=flex_as_req_inf_y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B57 | `(vacía)` | `=flex_as_req_sup_y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B58 | `(vacía)` | `=DIAGRAMAS_X!J4` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B59 | `(vacía)` | `=DIAGRAMAS_Y!J4` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B60 | `(vacía)` | `=eq_x` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B61 | `(vacía)` | `=PUNZONAMIENTO!B47` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B62 | `(vacía)` | `=PUNZONAMIENTO!B57` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B63 | `(vacía)` | `=punz_vu` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | B64 | `(vacía)` | `=PUNZONAMIENTO!B12` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C42 | `(vacía)` | `-` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C43 | `(vacía)` | `cm` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C45:C46 | `(vacía)` | `tonf` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C47 | `(vacía)` | `-` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C48 | `(vacía)` | `kgf/cm2` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C52 | `(vacía)` | `tonf*m/m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C53:C54 | `(vacía)` | `cm2/m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C55 | `(vacía)` | `tonf*m/m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C56:C57 | `(vacía)` | `cm2/m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C58:C59 | `(vacía)` | `tonf` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C60 | `(vacía)` | `-` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C61 | `(vacía)` | `tonf*m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C63 | `(vacía)` | `tonf` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | C64 | `(vacía)` | `m2` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | D23 | `Debe cumplir servicio, concreto armado, acero, geometria y nucleo central.` | `Requiere contacto, resistencia, acero, geometría, equilibrio y detalle local de transferencia.` | Estados pendientes visibles. |
| RESUMEN | D60 | `(vacía)` | `=eq_x` | Estados de control enlazados. |
| RESUMEN | E42 | `(vacía)` | `Tipo columna` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E43 | `(vacía)` | `dy` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E44 | `(vacía)` | `Contacto último` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E45 | `(vacía)` | `Vc2` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E46 | `(vacía)` | `Vc gobernante` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E47 | `(vacía)` | `φ Vc` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E48 | `(vacía)` | `φ vn` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E49 | `(vacía)` | `Punzonamiento` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E50 | `(vacía)` | `Cortante X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E51 | `(vacía)` | `Cortante Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E52 | `(vacía)` | `M negativo X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E53 | `(vacía)` | `As colocado inf X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E54 | `(vacía)` | `As colocado sup X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E55 | `(vacía)` | `M negativo Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E56 | `(vacía)` | `As colocado inf Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E57 | `(vacía)` | `As colocado sup Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E58 | `(vacía)` | `ERROR_MOMENTOS_X` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E59 | `(vacía)` | `ERROR_MOMENTOS_Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E60 | `(vacía)` | `Equilibrio Y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E61 | `(vacía)` | `γfy My` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E62 | `(vacía)` | `Acero superior` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E63 | `(vacía)` | `qu neta interior` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | E64 | `(vacía)` | `Reacción interior` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F42 | `(vacía)` | `=inp_col_type` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F43 | `(vacía)` | `=punz_d_y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F44 | `(vacía)` | `=PRESIONES_ULTIMAS!D13` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F45 | `(vacía)` | `=punz_vc2` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F46 | `(vacía)` | `=PUNZONAMIENTO!B15` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F47 | `(vacía)` | `=punz_phi_vc` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F48 | `(vacía)` | `=punz_phi_vn` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F49 | `(vacía)` | `=punz_result` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F50 | `(vacía)` | `=CORTANTE_UNIDIRECCIONAL!B18` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F51 | `(vacía)` | `=CORTANTE_UNIDIRECCIONAL!B23` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F52 | `(vacía)` | `=FLEXION_ACERO!B14` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F53 | `(vacía)` | `=steel_as_inf_x` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F54 | `(vacía)` | `=steel_as_sup_x` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F55 | `(vacía)` | `=FLEXION_ACERO!B15` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F56 | `(vacía)` | `=steel_as_inf_y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F57 | `(vacía)` | `=steel_as_sup_y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F58 | `(vacía)` | `=DIAGRAMAS_X!J5` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F59 | `(vacía)` | `=DIAGRAMAS_Y!J5` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F60 | `(vacía)` | `=eq_y` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F61 | `(vacía)` | `=PUNZONAMIENTO!B48` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F62 | `(vacía)` | `=FLEXION_ACERO!B16` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F63 | `(vacía)` | `=PUNZONAMIENTO!B13` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | F64 | `(vacía)` | `=PUNZONAMIENTO!B30` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G42 | `(vacía)` | `-` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G43 | `(vacía)` | `cm` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G45:G47 | `(vacía)` | `tonf` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G48 | `(vacía)` | `kgf/cm2` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G52 | `(vacía)` | `tonf*m/m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G53:G54 | `(vacía)` | `cm2/m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G55 | `(vacía)` | `tonf*m/m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G56:G57 | `(vacía)` | `cm2/m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G58:G59 | `(vacía)` | `tonf*m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G60 | `(vacía)` | `-` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G61 | `(vacía)` | `tonf*m` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G63 | `(vacía)` | `tonf/m2` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | G64 | `(vacía)` | `tonf` | Resumen enlazado con resultados Fase 1. |
| RESUMEN | H60 | `(vacía)` | `=eq_y` | Estado equilibrio Y. |

### Nombres nuevos y validaciones

| Nombre | Destino |
|---|---|
| eq_x | `DIAGRAMAS_X!$J$6` |
| eq_y | `DIAGRAMAS_Y!$J$6` |
| geo_input_state | `GEOMETRIA!$B$14` |
| gross_weight_u | `PRESIONES_ULTIMAS!$D$23` |
| inp_case | `INGRESO_DATOS!$C$67` |
| inp_col_type | `INGRESO_DATOS!$C$66` |
| inp_fws_u | `INGRESO_DATOS!$C$70` |
| inp_fwz_u | `INGRESO_DATOS!$C$69` |
| inp_order_inf | `INGRESO_DATOS!$C$65` |
| inp_order_sup | `INGRESO_DATOS!$C$68` |
| inp_sign_p | `INGRESO_DATOS!$C$50` |
| net_gx | `PRESIONES_ULTIMAS!$D$21` |
| net_gy | `PRESIONES_ULTIMAS!$D$22` |
| net_q0 | `PRESIONES_ULTIMAS!$D$20` |
| punz_phi_vn | `PUNZONAMIENTO!$B$40` |
| punz_state | `PUNZONAMIENTO!$B$28` |
| punz_vc1 | `PUNZONAMIENTO!$B$23` |
| punz_vc2 | `PUNZONAMIENTO!$B$24` |
| punz_vc3 | `PUNZONAMIENTO!$B$25` |
| punz_vumax | `PUNZONAMIENTO!$B$38` |
| struct_state | `PRESIONES_ULTIMAS!$D$17` |

- Validación `INGRESO_DATOS!C50`: lista `1,-1`. C50 reemplaza la lista Si/No antigua; las demás son nuevas. Se mantienen las otras validaciones.

- Validación `INGRESO_DATOS!C65`: lista `X inferior / Y superior,Y inferior / X superior`. C50 reemplaza la lista Si/No antigua; las demás son nuevas. Se mantienen las otras validaciones.

- Validación `INGRESO_DATOS!C66`: lista `INTERIOR,BORDE,ESQUINA`. C50 reemplaza la lista Si/No antigua; las demás son nuevas. Se mantienen las otras validaciones.

- Validación `INGRESO_DATOS!C68`: lista `X exterior / Y interior,Y exterior / X interior`. C50 reemplaza la lista Si/No antigua; las demás son nuevas. Se mantienen las otras validaciones.

### Extensiones de formato y estados

No se cambió el estilo general ni se eliminó ninguna regla original. Se copiaron formatos de filas adyacentes a los bloques nuevos INGRESO_DATOS!A64:H70, PUNZONAMIENTO!A20:F58, PRESIONES_ULTIMAS!A17:H23, CORTANTE_UNIDIRECCIONAL!A15:H23, FLEXION_ACERO!A14:I17 y RESUMEN!A41:H64; se formatearon G4:L11 y A68:D79 de ambos diagramas. Las alturas locales y wrap evitan recorte. Reglas nuevas exactas: CUMPLE/OK/CONTACTO COMPLETO verde; NO CUMPLE/ERROR rojo; ADVERTENCIA/REQUIERE/PÉRDIDA/TRACCIÓN/INVÁLIDO/PERALTE/REVISAR amarillo. Se verificaron colores DisplayFormat tras cambiar las entradas.

Rangos combinados añadidos: `INGRESO_DATOS!A64:H64`, `DIAGRAMAS_X!G4:I4`, `DIAGRAMAS_X!G5:I5`, `DIAGRAMAS_X!G6:I6`, `DIAGRAMAS_X!G7:I7`, `DIAGRAMAS_X!G8:I8`, `DIAGRAMAS_X!G9:I9`, `DIAGRAMAS_X!G10:I10`, `DIAGRAMAS_X!G11:I11`, `DIAGRAMAS_Y!G4:I4`, `DIAGRAMAS_Y!G5:I5`, `DIAGRAMAS_Y!G6:I6`, `DIAGRAMAS_Y!G7:I7`, `DIAGRAMAS_Y!G8:I8`, `DIAGRAMAS_Y!G9:I9`, `DIAGRAMAS_Y!G10:I10`, `DIAGRAMAS_Y!G11:I11`, `RESUMEN!A41:H41`, `PUNZONAMIENTO!B18:F18`, `PUNZONAMIENTO!B19:F19`, `PUNZONAMIENTO!B28:F28`, `PUNZONAMIENTO!B57:F57`, `RESUMEN!B44:D44`, `RESUMEN!F44:H44`, `RESUMEN!B49:D49`, `RESUMEN!F49:H49`, `RESUMEN!B50:D50`, `RESUMEN!F50:H50`, `RESUMEN!B51:D51`, `RESUMEN!F51:H51`, `RESUMEN!B62:D62`, `RESUMEN!F62:H62`, `DIAGRAMAS_X!J6:L6`, `DIAGRAMAS_X!J11:L11`, `DIAGRAMAS_Y!J6:L6`, `DIAGRAMAS_Y!J11:L11`, `INGRESO_DATOS!A65:B65`, `INGRESO_DATOS!E65:H65`, `INGRESO_DATOS!A66:B66`, `INGRESO_DATOS!E66:H66`, `INGRESO_DATOS!A67:B67`, `INGRESO_DATOS!E67:H67`, `INGRESO_DATOS!A68:B68`, `INGRESO_DATOS!E68:H68`, `INGRESO_DATOS!A69:B69`, `INGRESO_DATOS!E69:H69`, `INGRESO_DATOS!A70:B70`, `INGRESO_DATOS!E70:H70`. Ningún rango combinado original desapareció.

### Límite del commit

Solo se incorporan el libro corregido y este Markdown. El original se conserva sin modificación. Archivos de prueba, PDFs, PNGs, fuente normativa y scripts de auditoría permanecen locales fuera del commit. Mensaje del commit: `Corrección técnica Fase 1 - zapata aislada E060`. El hash completo y confirmación del push se entregan en la respuesta final (no se intenta incluir el hash autorreferencial en este archivo).
