# FuncionalIA

Sistema de aprendizaje adaptativo de **Alimentos Funcionales** (asignatura 1548, Grado en Ciencia y Tecnología de los Alimentos, EPS Orihuela, Universidad Miguel Hernández de Elche). Es una aplicación web de un solo fichero, construida a partir de la Guía Docente 2026-2027.

**Usar la app:** https://fborrasumh.github.io/funcionalia/

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.23822320.svg)](https://doi.org/10.5281/zenodo.23822320)

**Idiomas:** español (por defecto), inglés y portugués. Se eligen en el selector de la barra superior o con `?lang=en` / `?lang=pt` en la URL.

## Qué hace

- **Diagnóstico**: 12 preguntas, dos por unidad, que estiman el punto de partida en cada resultado de aprendizaje (RA). Admite «No lo sé».
- **Práctica adaptativa**:
  - Hay un modelo Elo por RA que tiene en cuenta el olvido: el dominio que no se practica se reduce a la mitad en 30 días.
  - Cada pregunta vuelve tras 1, 3, 7, 14 o 30 días según el estudiante la acierte (cajas de Leitner); si la falla, vuelve al día siguiente.
  - La siguiente pregunta se elige con reglas deterministas que el estudiante puede leer en pantalla: primero los fallos que toca repasar; después el RA con más peso × (1 − dominio); dentro de él, la pregunta con una probabilidad de acierto más cercana al 70 %, intercalando unidades.
  - Con los mismos eventos sale siempre la misma ruta, y hay una prueba automática que lo comprueba.
- **Simulacro de examen**:
  - Ofrece 20, 30 o 40 preguntas, repartidas según las horas que el cronograma da a cada unidad.
  - Puntúa con la regla de la guía (por cada 4 incorrectas se resta una correcta) en sus dos lecturas posibles: proporcional (−0,25 por fallo) y por bloques completos de 4 fallos.
  - Comprueba la nota mínima de 4 que exige la guía, desglosa el resultado por unidad, muestra el valor esperado de contestar al azar y permite revisar los fallos.
- **Problemas de las prácticas con solución calculada por el código**: recuento de viables (UFC/g), capacidad antioxidante en equivalentes de Trolox (DPPH/ABTS) y formulación de un yogur con fibra.
  - Cada problema trae datos nuevos y la app enseña la solución paso a paso.
  - Si el resultado es incorrecto, el código recalcula los errores típicos (no dividir por el volumen sembrado, olvidar la dilución o el paso de mL a L, no tener en cuenta la dilución del ingrediente…) y dice cuál coincide.
- **Declaraciones nutricionales y de salud**:
  - Aplica las condiciones del anexo del Reglamento (CE) 1924/2006 a la composición por 100 g o 100 ml, con la energía calculada con los factores del Reg. (UE) 1169/2011.
  - Incluye una selección de declaraciones de propiedades saludables con sus condiciones de uso (Reg. (UE) 432/2012, Reg. (CE) 983/2009 y Reg. (UE) 2015/2314) y el aviso sobre el término «probiótico».
- **Laboratorio de diseño** (RA 08 de diseño):
  - El estudiante describe su alimento funcional: proceso y protección del bioactivo, estabilidad, plan sensorial, sostenibilidad y subproductos, y evidencia y declaración.
  - El código comprueba que la cantidad cumple la declaración elegida, que cada apartado está desarrollado y que el plan es coherente (viables, protección del bioactivo, prueba sensorial concreta).
  - Con la clave de cada persona, la IA comenta cada criterio citando literalmente el texto del estudiante, y el código revisa la respuesta:
    - verifica cada cita;
    - degrada a «sin evidencia verificada» lo que la IA da por sólido sin una cita real;
    - marca las cifras que no están en el diseño y las normas que no reconoce;
    - retira cualquier nota o puntuación.
  - El diseño se exporta en Word.
- **Otra explicación (IA)**: después de un fallo, se puede pedir otra explicación. El código marca las cifras y normas que no aparecen en la pregunta ni en su explicación de referencia.
- **Mi progreso**: dominio por RA (con el texto literal de la guía y su reescritura medible), resultados por unidad e historial de simulacros. Permite hacer una copia de seguridad, restaurarla y exportar las respuestas de forma **anónima y voluntaria**.
- **Profesorado**:
  - Analítica de ítems a partir de los ficheros anónimos del alumnado: dificultad, discriminación punto-biserial, distractores que nadie elige y avisos.
  - Matriz de alineación RA × unidades y exportación del banco a Moodle XML (penalización −25 %), GIFT y CSV.
  - Un asistente de IA redacta borradores de preguntas, el código los valida (cuatro opciones distintas, explicación, sin «todas/ninguna de las anteriores», sin duplicados) y el profesorado decide cuáles añade.
- **Ejemplo sin clave** en los tres idiomas, con datos ficticios.

## Ciencia del aprendizaje en la que se apoya

- Práctica de recuperación: Roediger y Karpicke (2006), https://doi.org/10.1111/j.1467-9280.2006.01693.x
- Práctica espaciada: Cepeda et al. (2006), https://doi.org/10.1037/0033-2909.132.3.354
- Revisión de técnicas de estudio: Dunlosky et al. (2013), https://doi.org/10.1177/1529100612453266
- Intercalado de problemas: Rohrer y Taylor (2007), https://doi.org/10.1007/s11251-007-9015-8
- Modelo Elo en sistemas adaptativos: Pelánek (2016), https://doi.org/10.1016/j.compedu.2016.03.017

Las definiciones de probiótico, prebiótico y simbiótico siguen los consensos de la ISAPP (Hill et al., 2014; Gibson et al., 2017; Swanson et al., 2020). La taxonomía de *Lactobacillus* sigue a Zheng et al. (2020) y la digestión in vitro, el protocolo INFOGEST (Brodkorb et al., 2019). Todos los DOI se comprobaron al publicar esta versión.

## Cómo se usa la IA

La IA es opcional y funciona con la clave propia de cada persona (OpenAI, Google Gemini o Anthropic Claude). La clave se guarda solo en el navegador y no hace falta servidor. Sin clave funciona todo excepto los comentarios del laboratorio, la «otra explicación» y el asistente del profesorado.

## Privacidad

- Las respuestas, el progreso y los diseños se guardan solo en el navegador (IndexedDB).
- Solo sale texto hacia el proveedor de IA cuando la persona lo pide: el diseño o una pregunta ya contestada. Los correos, documentos de identidad y teléfonos se envían enmascarados, y antes del primer envío de cada sesión se muestra exactamente lo que sale.
- La exportación anónima contiene un seudónimo aleatorio y, por cada respuesta, el ítem, si fue correcta, la opción elegida, el tiempo y el día (sin hora). No incluye nombre ni texto libre.
- **Investigación**: la app genera los datos, pero no produce por sí sola evidencia publicable. Para publicar con esos datos hace falta la aprobación del comité de ética (Oficina de Evaluación de Proyectos de la UMH), consentimiento informado y cumplimiento del RGPD; lo ideal es además un diseño preregistrado con grupo de comparación.

## Límites

- El **banco inicial de 49 preguntas** lo redactó el equipo de la app a partir de la guía y de fuentes citadas, y **está pendiente de revisión por el profesorado**. Cada corrección aceptada saldrá en una versión nueva con DOI.
- La guía numera dos resultados como «08» y ninguno como «07». En la app se llaman *08 · diseño* y *08 · legal*.
- La guía no dice cuántas preguntas tiene el examen ni cómo se aplica exactamente la penalización. El simulacro calcula las dos interpretaciones.
- El verificador de declaraciones es una **herramienta de estudio con una selección de condiciones**: no sustituye la consulta del texto consolidado ni del Registro de la UE de declaraciones. No contempla las grasas trans, los polialcoholes ni el alcohol en el cálculo de energía.
- El dominio es una **estimación** para orientar la práctica, no una nota. La IA comenta, pero no califica.
- Esta versión se ha probado con una IA simulada en los tres proveedores, **no con una clave real**.

## Pruebas realizadas (v1.0.0)

- **Lógica pura en Node** (`tests/nucleo_test.js`):
  - integridad del banco en los tres idiomas;
  - ruta determinista;
  - olvido;
  - puntuación del simulacro con las dos lecturas de la regla;
  - 900 variantes de problemas con la solución aceptada y cada error típico diagnosticado;
  - reglas de declaraciones;
  - validación de ítems;
  - exportaciones.
- **Navegador** (`tests/smoke_test.py`, Playwright):
  - CSP;
  - flujos completos;
  - IA simulada que inventa una cita, pone una nota, cita una norma inexistente y añade una cifra (el código detecta todo);
  - descargas (Word abierto con python-docx, también sin CDN);
  - persistencia y funcionamiento sin red;
  - **axe-core sin infracciones WCAG 2.2 A/AA en 9 pantallas × 3 idiomas**;
  - navegación con teclado;
  - móvil sin desbordes;
  - primera pregunta en menos de 3 s con la CPU ralentizada ×4.

Sobre accesibilidad: el objetivo verificado es WCAG 2.2 AA. Además se cumplen algunos criterios AAA (sin límites de tiempo, botones grandes y ayuda contextual), pero no se afirma la conformidad AAA de toda la app.

## Adaptarla a otra asignatura o universidad

1. Copia `src/curriculum.js` y cambia la ficha, los RA (texto literal + reescritura medible), las unidades con sus horas y el banco de ítems.
2. Ajusta los problemas de `src/nucleo.js` (`PROBS`) si tu asignatura tiene otros cálculos.
3. Traduce los textos nuevos en `tools/gen_i18n.py` y ejecuta `python3 build.py`.
4. Pasa las pruebas (`node tests/nucleo_test.js` y `python3 tests/smoke_test.py`) y publica.

## Autoría

Fernando Borrás Rocher (Universidad Miguel Hernández de Elche) y María José Frutos Fernández (Universidad Miguel Hernández de Elche).

Construida a partir de la Guía Docente 2026-2027 de la asignatura 1548 Alimentos Funcionales (profesorado: Estefanía Valero Cases, responsable; María José Frutos Fernández; Raquel Lucas González).

Roles (CRediT):

- Fernando Borrás Rocher: conceptualización, software, metodología, validación.
- María José Frutos Fernández: recursos (asignatura y guía docente), conceptualización del dominio y validación de contenidos pendiente sobre el banco inicial.

Para sumarse como coautor (por ejemplo, otros docentes de la asignatura) hay que hacer una contribución con `Signed-off-by: Nombre <correo>` o abrir una issue desde la cuenta de GitHub propia, indicando el ORCID y la conformidad con la licencia. Cada incorporación sale como versión nueva en Zenodo.

ORCID: Fernando Borrás Rocher [0000-0002-5519-4573](https://orcid.org/0000-0002-5519-4573) · María José Frutos Fernández [0000-0003-0620-5050](https://orcid.org/0000-0003-0620-5050)

## Cómo citar

Borrás Rocher, F. y Frutos Fernández, M. J. (2026). *FuncionalIA* (v1.0.0) [Software]. DOI: [10.5281/zenodo.23822320](https://doi.org/10.5281/zenodo.23822320)

## Licencia

MIT. Véase [LICENSE](LICENSE). Es una licencia de software. Si en el futuro se publica por separado el banco de preguntas como contenido educativo, lo habitual sería CC BY 4.0, y CC0 o CC BY para los datos.
