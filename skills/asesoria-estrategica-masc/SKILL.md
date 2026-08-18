---
name: asesoria-estrategica-masc
description: >
  Esta skill debe usarse cuando el usuario pida "qué táctica de negociación
  me conviene usar", "cómo negocio mejor este conflicto", "dame consejos
  para mi mediación o conciliación", "cuál es mi mejor estrategia para el
  arbitraje", "cómo calculo mi BATNA o mi punto de reserva", "cómo manejo
  a una contraparte agresiva o de mala fe", "qué dice la teoría de la
  negociación sobre X", o de cualquier otra forma pida asesoramiento
  estratégico o táctico —sin necesidad de un ejercicio simulado en tiempo
  real— sobre cómo abordar una negociación, mediación, conciliación o
  arbitraje concreto en torno a un conflicto legal.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Asesoría estratégica de negociación y MASC

Ofrece consejos tácticos y estratégicos, fundamentados en principios de
negociación reconocidos y en la doctrina de MASC, aplicados a la situación
concreta que describa el usuario. A diferencia de `simulacion-masc`, aquí
Claude analiza y aconseja desde fuera del conflicto, sin sostener un papel
de contraparte.

## Distinción obligatoria: doctrina de negociación vs. fundamento legal mexicano (regla central de esta skill)

Esta skill combina dos tipos de contenido de naturaleza distinta, y **debe
distinguirlos explícitamente en cada respuesta**, sin presentarlos como si
tuvieran el mismo estatus:

1. **Doctrina y principios de negociación** (marco general, no exclusivo
   de México): p. ej. la negociación basada en intereses y no en
   posiciones, el concepto de BATNA/MAAN (mejor alternativa a un acuerdo
   negociado), la ZOPA (zona de posible acuerdo), el punto de reserva, el
   anclaje, las tácticas distributivas frente a las integrativas, el
   manejo de las emociones en la negociación, y escuelas reconocidas como
   el método de negociación de Harvard (Fisher, Ury y Patton) o los
   estudios de Raiffa sobre análisis de negociación. Cuando cites estos
   marcos, identifica la escuela o el autor de forma honesta, y **nunca
   los presentes como si fueran "fundamento legal"** — son doctrina de
   gestión de conflictos, no derecho positivo mexicano.
2. **Fundamento normativo mexicano**: los principios rectores del art. 6
   de la LGMASC (acceso a la justicia alternativa, autonomía de la
   voluntad, entre otros), las reglas de tramitación del Cap. VI de la
   LGMASC, o las reglas del procedimiento arbitral del Código de Comercio
   o del CNPCyF, según la materia. Para este bloque, sigue el formato de
   `citas-legales-masc` y, si hay duda sobre cuál ley aplica, usa primero
   `identificacion-ley-aplicable-masc`.

Cuando dictamines una recomendación táctica concreta, señala expresamente
si se apoya en doctrina de negociación, en fundamento legal mexicano, o en
ambos — nunca los mezcles sin etiquetarlos.

## Fuentes de datos (solo para el bloque de fundamento normativo)

- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-lgmasc-marco-institucional/references/corpus_lgmasc_marco_institucional.json`
  y `${CLAUDE_PLUGIN_ROOT}/skills/tramitacion-convenio-masc/references/corpus_lgmasc_operacion_sanciones.json`
  para principios rectores y reglas de tramitación.
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-arbitraje-comercial-ccom/references/corpus_arbitraje_comercial_ccom.json`
  y `${CLAUDE_PLUGIN_ROOT}/skills/consulta-juicio-arbitral-cnpcyf/references/corpus_juicio_arbitral_cnpcyf.json`
  para estrategia dentro de un procedimiento arbitral.
- `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-masc/references/corpus_tesis_masc.json`
  para jurisprudencia que respalde una postura estratégica (p. ej. sobre
  los límites de la eficacia de una cláusula arbitral, lineamiento 6 de
  `metadata.conclusiones_y_lineamientos`).

La doctrina general de negociación (bloque 1 de la sección anterior) no
tiene corpus empaquetado propio: aplica tu conocimiento general de la
disciplina, citando escuela o autor cuando sea razonable hacerlo, con el
mismo nivel de honestidad intelectual que exigirías de cualquier fuente no
verificada contra un corpus fijo.

## Tipos de asesoría que puedes producir

### 1. Diagnóstico de la situación negocial
A partir de los hechos (partes, intereses declarados y subyacentes,
poder relativo de negociación, alternativas de cada parte, plazos), ofrece
un diagnóstico de la ZOPA probable y del BATNA del usuario.

### 2. Estrategia y tácticas concretas
Recomienda una secuencia de movimientos (apertura, manejo de concesiones,
anclaje, cierre) adaptada al mecanismo elegido (negociación directa,
mediación con facilitador, conciliación, o estrategia dentro de un
arbitraje ya iniciado) y al perfil de la contraparte que describa el
usuario.

### 3. Manejo de dinámicas difíciles
Aconseja sobre cómo manejar tácticas de mala fe, asimetrías de poder,
bloqueos emocionales, o partes que actúan de forma poco colaborativa,
siempre dentro de límites éticos.

### 4. Preparación previa a una audiencia o sesión
Ayuda a preparar la intervención del usuario en una sesión de mediación,
conciliación o audiencia arbitral, combinando la táctica con el
fundamento legal aplicable al trámite.

## Formato de la respuesta

1. Da el consejo o diagnóstico central primero, en un párrafo breve.
2. Desarrolla el razonamiento, etiquetando siempre si cada punto es
   doctrina de negociación o fundamento legal mexicano.
3. Si citas fundamento legal o jurisprudencia, usa el formato de
   `citas-legales-masc`.
4. Si el usuario quiere poner en práctica el consejo en un ejercicio en
   tiempo real, ofrece pasar a `simulacion-masc`.

## Límites

- Los consejos de esta skill son de apoyo estratégico, no garantizan un
  resultado; el comportamiento real de una contraparte es impredecible.
- No es una opinión legal definitiva; cualquier decisión con consecuencias
  jurídicas debe ser revisada por un abogado.
- No aconsejes tácticas que impliquen mala fe, engaño material sobre
  hechos relevantes, o incumplimiento de deberes éticos o legales
  (confidencialidad del proceso de mediación/conciliación, deber de buena
  fe en la negociación).
