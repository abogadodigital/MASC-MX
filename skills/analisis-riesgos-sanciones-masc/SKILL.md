---
name: analisis-riesgos-sanciones-masc
description: >
  Esta skill debe usarse cuando el usuario pregunte "qué sanción tiene una
  persona facilitadora que [conducta]", "qué causas de inhabilitación
  existen para facilitadores públicos", "qué le puede pasar a un Centro de
  MASC que incumple sus obligaciones", "qué dice el artículo [número,
  entre 139 y 144] de la LGMASC", "en qué casos se anula un laudo
  arbitral", "qué riesgo tiene mi laudo de ser anulado o de que no se
  ejecute", "qué causales existen para negar el reconocimiento o la
  ejecución de un laudo", o proporcione los hechos de una conducta de una
  persona facilitadora, persona abogada colaborativa, Centro de MASC o de
  un procedimiento arbitral concreto, y pregunte por el riesgo de sanción
  administrativa (régimen de la LGMASC) o por el riesgo de nulidad o de
  denegación de reconocimiento/ejecución de un laudo (Código de Comercio o
  CNPCyF, según la materia).
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Análisis de riesgos, sanciones y nulidad en materia de MASC y arbitraje

Detecta, a partir de los hechos que proporcione el usuario, dos tipos de
riesgo que este plugin trata de forma diferenciada porque provienen de
leyes distintas: (1) el riesgo de **responsabilidad y sanción** de una
persona facilitadora, persona abogada colaborativa o Centro de MASC
conforme a la LGMASC; y (2) el riesgo de que un **laudo arbitral** sea
anulado, o de que se deniegue su reconocimiento o ejecución, conforme al
Código de Comercio (arbitraje mercantil) o al CNPCyF (arbitraje civil o
familiar). Identifica siempre con cuál de los dos estás tratando antes de
fundamentar — no son intercambiables. Si tienes duda, usa primero
`identificacion-ley-aplicable-masc`.

## Fuentes de datos

- `${CLAUDE_PLUGIN_ROOT}/skills/tramitacion-convenio-masc/references/corpus_lgmasc_operacion_sanciones.json`
  — Cap. IX de la LGMASC (Régimen de Responsabilidades y Sanciones, arts.
  139-144): causas de responsabilidad de personas facilitadoras, personas
  abogadas colaborativas y Centros, y causas de inhabilitación (art. 144).
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-arbitraje-comercial-ccom/references/corpus_arbitraje_comercial_ccom.json`
  — Cap. VIII (De la Nulidad del Laudo, arts. 1457-1460) y Cap. IX
  (Reconocimiento y Ejecución de Laudos, arts. 1461-1463) para arbitraje
  mercantil.
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-juicio-arbitral-cnpcyf/references/corpus_juicio_arbitral_cnpcyf.json`
  — art. 549 (causales tasadas para negar la ejecución del laudo) para
  arbitraje civil o familiar.
- `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-masc/references/corpus_tesis_masc.json`
  — categoría E (nulidad del laudo, 10 criterios, la más numerosa del
  corpus), categoría F (reconocimiento y ejecución) y categoría G (amparo
  y medios de impugnación).

## Formato de citación

Sigue el formato de citación (artículos y jurisprudencia, identificando
siempre de cuál de las tres leyes proviene cada cita) definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-masc/SKILL.md`.

## Marco de análisis: dos vías, expresamente distintas

### 1. Responsabilidad y sanción de facilitadores, abogados colaborativos y Centros (LGMASC, Cap. IX, arts. 139-144)

1. Identifica si la conducta encuadra en alguna de las causas de
   responsabilidad previstas en el capítulo — verifica el texto exacto en
   el corpus antes de afirmar la fracción aplicable.
2. Identifica si la conducta alcanza el umbral de las causas de
   inhabilitación del art. 144, que son de mayor gravedad que una simple
   causa de responsabilidad.
3. Precisa la autoridad competente para conocer del procedimiento
   sancionador según el capítulo de competencia (remite a
   `consulta-lgmasc-marco-institucional` para el fundamento de competencia
   si hace falta).

### 2. Nulidad, reconocimiento y ejecución del laudo arbitral (Código de Comercio o CNPCyF)

1. Determina primero si la materia de fondo del arbitraje es mercantil
   (Código de Comercio) o civil/familiar (CNPCyF) — usa
   `identificacion-ley-aplicable-masc` si hay duda.
2. Si es mercantil: aplica las causales tasadas del art. 1457 (nulidad) y
   arts. 1461-1463 (denegación de reconocimiento o ejecución) del Código
   de Comercio.
3. Si es civil o familiar: aplica las causales tasadas del art. 549 del
   CNPCyF para la ejecución (el CNPCyF no contempla un recurso contra el
   laudo en sí, solo contra su ejecución).
4. Ambos regímenes son de **numerus clausus** (lista cerrada de causales):
   no inventes causales adicionales ni las generalices; cita siempre la
   fracción o inciso exacto.
5. Señala el plazo aplicable para promover la acción, cuando el corpus lo
   contenga, y adviértele al usuario que lo verifique si no está en el
   corpus.

## Formato de la respuesta

1. Presenta primero, en un párrafo breve, cuál de las dos vías aplica
   (responsabilidad/sanción de la LGMASC, o nulidad/ejecución del laudo) y
   por qué, remitiendo si hace falta a `identificacion-ley-aplicable-masc`.
2. Desarrolla el fundamento artículo por artículo, citando siempre
   `texto_completo` del corpus correspondiente e identificando la ley de
   origen.
3. Cita la jurisprudencia aplicable con su rubro y contenido, siguiendo el
   formato de `citas-legales-masc` — la categoría E del corpus de tesis
   (10 criterios) es la más relevante para nulidad de laudo.
4. Si el riesgo detectado deriva de un defecto en la tramitación de un
   MASC no adjudicativo, remite a `tramitacion-convenio-masc` para la
   corrección. Si se requiere redactar la demanda de nulidad o el escrito
   de oposición a la ejecución, remite a `redaccion-escritos-masc`.

## Límites

- Este es un análisis preliminar de trabajo, no una opinión legal
  definitiva. La calificación de una causal de nulidad o de denegación de
  ejecución depende de elementos probatorios que solo una autoridad puede
  valorar; no la presentes como una certeza.
- No mezcles el régimen sancionador de la LGMASC con las causales de
  nulidad del laudo arbitral: son consecuencias jurídicas de naturaleza y
  ley distintas, aunque ambas puedan surgir del mismo expediente.
- Recomienda siempre la revisión de un abogado especializado antes de
  tomar decisiones o iniciar cualquier acción.
