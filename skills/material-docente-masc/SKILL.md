---
name: material-docente-masc
description: >
  Esta skill debe usarse cuando el usuario pida "crear material de clase
  sobre arbitraje o MASC", "hazme un resumen temático para estudiantes",
  "genera reactivos de examen sobre la LGMASC o el arbitraje comercial",
  "arma un caso práctico para la clase de MASC", "prepara flashcards sobre
  Kompetenz-Kompetenz o nulidad del laudo", "diseña una actividad sobre
  mediación y conciliación", o de cualquier otra forma necesite material
  didáctico para un curso de derecho, taller o diplomado, con base en la
  LGMASC, el Código de Comercio, el CNPCyF y la doctrina jurisprudencial de
  arbitraje y MASC empaquetada con este plugin.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Material docente sobre arbitraje y MASC en México

Genera material didáctico (resúmenes temáticos, casos prácticos, reactivos
de examen, flashcards, cuadros comparativos) para la enseñanza de la
negociación, mediación, conciliación y arbitraje en México, con base
exclusivamente en el contenido empaquetado con este plugin: las tres leyes
(LGMASC, Código de Comercio Título Cuarto y CNPCyF) y los 78 criterios
jurisprudenciales.

## Formato de citación

Sigue el formato de citación (artículos, identificando siempre la ley de
origen, y jurisprudencia) definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-masc/SKILL.md`.

## Fuentes de datos

Usa según el tema solicitado:

- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-lgmasc-marco-institucional/references/corpus_lgmasc_marco_institucional.json`
- `${CLAUDE_PLUGIN_ROOT}/skills/tramitacion-convenio-masc/references/corpus_lgmasc_operacion_sanciones.json`
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-arbitraje-comercial-ccom/references/corpus_arbitraje_comercial_ccom.json`
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-juicio-arbitral-cnpcyf/references/corpus_juicio_arbitral_cnpcyf.json`
- `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-masc/references/corpus_tesis_masc.json`

## Ejes temáticos sugeridos

Organiza el material por ley (marco institucional y operación de la
LGMASC, arbitraje comercial del Código de Comercio, juicio arbitral civil
y familiar del CNPCyF) o por las 13 categorías del corpus de tesis (A-M).
Temas de mayor densidad jurisprudencial o práctica que suelen justificar
una sesión propia: fundamentos constitucionales del arbitraje a partir de
la reforma de 2008 (categoría A), el principio Kompetenz-Kompetenz
(categoría C), la nulidad del laudo (categoría E, la más numerosa con 10
criterios), el reconocimiento y ejecución de laudos nacionales y
extranjeros (categoría F), el contraste entre arbitraje mercantil (Código
de Comercio) y arbitraje civil/familiar (CNPCyF, incluidas las exclusiones
del art. 540), y el ejercicio de distinguir, ante un caso práctico, cuál
de las tres leyes es la aplicable (usa `identificacion-ley-aplicable-masc`
como insumo pedagógico para este ejercicio).

## Tipos de material que puedes producir

- **Resumen temático**: síntesis en lenguaje claro de un capítulo de
  alguna de las tres leyes o de una categoría de tesis, con citas
  textuales de los artículos y criterios más relevantes.
- **Caso práctico**: hechos hipotéticos (siempre ficticios, aclarándolo
  expresamente) que planteen un problema de encuadre normativo (qué ley
  aplica), de tramitación, de riesgo de nulidad, o de estrategia de MASC,
  con preguntas guía y, si se solicita, la solución razonada citando el
  fundamento aplicable.
- **Reactivos de examen**: opción múltiple, verdadero/falso o pregunta
  abierta, basados en el texto literal de los artículos o en el criterio
  jurídico de las tesis (nunca en interpretaciones no sustentadas en el
  corpus). Indica siempre la respuesta correcta y su fundamento.
- **Flashcards**: pares pregunta/respuesta breves para memorización de
  definiciones legales, plazos, causales tasadas de nulidad o de
  denegación de ejecución, y criterios de encuadre entre las tres leyes.
- **Cuadros comparativos**: p. ej. arbitraje mercantil (Código de
  Comercio) vs. arbitraje civil/familiar (CNPCyF); LGMASC vs. Código de
  Comercio vs. CNPCyF, según el mecanismo; nulidad del laudo vs.
  denegación de reconocimiento/ejecución.

Si el usuario pide construir un examen completo, un temario/syllabus, o la
revisión/calificación de evaluaciones ya elaboradas, considera usar en
conjunto las skills especializadas de docencia jurídica disponibles en el
entorno, aportando tú el contenido sustantivo de arbitraje y MASC que esas
skills necesiten.

## Reglas de contenido

- Toda afirmación normativa debe fundamentarse en el `texto_completo` del
  artículo correspondiente, identificando siempre de cuál de las tres
  leyes proviene; toda afirmación jurisprudencial, en el contenido de la
  tesis correspondiente, siguiendo el formato de `citas-legales-masc`.
- No inventes artículos, números de registro digital ni rubros de tesis
  que no existan en el corpus.
- Distingue siempre, en el material que generes, entre texto legal
  vigente, interpretación judicial de ese texto, y doctrina general de
  negociación (esta última sin corpus propio — ver
  `asesoria-estrategica-masc`).

## Límites

- El corpus jurisprudencial y normativo de este plugin refleja una fecha
  de corte determinada; adviértelo si el material se usará en cursos
  futuros, sugiriendo verificar reformas o criterios posteriores.
- Este material es de apoyo docente, no una opinión legal ni un sustituto
  de la lectura directa de las fuentes oficiales por parte del estudiante.
