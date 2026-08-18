---
name: consulta-lgmasc-marco-institucional
description: >
  Esta skill debe usarse cuando el usuario pregunte "qué dice el artículo
  [número, entre 1 y 60] de la LGMASC", "qué mecanismos alternativos de
  solución de controversias existen", "quién es competente en materia de
  MASC, la Federación o el estado", "cómo me certifico como persona
  facilitadora", "qué requisitos tiene una persona abogada colaborativa",
  "qué es el Consejo Nacional de MASC", "qué son los Registros y la
  Plataforma Nacional de MASC", "quiénes pueden ser parte en un MASC", o
  necesite el texto literal de la naturaleza y objeto, la competencia, el
  régimen de personas facilitadoras y su certificación, los registros y la
  Plataforma Nacional, o las reglas generales sobre las partes, conforme a
  los Capítulos I a V de la Ley General de Mecanismos Alternativos de
  Solución de Controversias (LGMASC).
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Consulta del marco institucional de la LGMASC (naturaleza, competencia, facilitadores, registros y partes)

Responde dudas sobre el contenido literal del Capítulo I (Naturaleza y
Objeto, arts. 1-8), el Capítulo II (De la Competencia, arts. 9-29), el
Capítulo III (De las Personas Facilitadoras y su Certificación, arts.
30-48), el Capítulo IV (De los Registros y la Plataforma Nacional, arts.
49-56) y el Capítulo V (De las Partes, arts. 57-60) de la Ley General de
Mecanismos Alternativos de Solución de Controversias (LGMASC), citando
siempre el texto legal exacto contenido en el corpus empaquetado. No
parafrasees el artículo sin antes mostrar o citar su texto íntegro; no
inventes artículos, fracciones o requisitos que no existan en el corpus.

## Función de esta skill dentro del plugin

Esta es la skill de entrada institucional de la LGMASC: cubre qué es un
MASC, cuáles son (art. 4: negociación, negociación colaborativa,
mediación, conciliación y arbitraje —de manera enunciativa y no
limitativa—), la distribución de competencias entre la Federación y las
entidades federativas, quién puede ejercer como persona facilitadora
pública o privada y cómo se certifica, y las reglas generales sobre las
partes. La operación práctica de los MASC (tramitación, convenio, Centros
de MASC, sanciones) está en `tramitacion-convenio-masc` y
`analisis-riesgos-sanciones-masc` — remite ahí cuando la pregunta sea sobre
cómo se tramita un caso concreto, no sobre el marco institucional.

## Advertencia de alcance frente al arbitraje (importante)

El artículo 4, fracción V, de la LGMASC define al arbitraje como uno de
los MASC, pero remite expresamente su regulación al Código de Comercio y
al Código Nacional de Procedimientos Civiles y Familiares. Si el usuario
pregunta por el procedimiento arbitral en sí (acuerdo de arbitraje,
tribunal arbitral, laudo, nulidad, ejecución), esta skill NO es la fuente:
usa `consulta-arbitraje-comercial-ccom` (materia mercantil) o
`consulta-juicio-arbitral-cnpcyf` (materia civil o familiar). Si tienes
duda sobre cuál aplica, usa primero `identificacion-ley-aplicable-masc`.

## Formato de citación

Sigue el formato de citación definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-masc/SKILL.md` (sección 2,
identificando siempre "LGMASC" como la ley de origen; sección 1 si además
citas jurisprudencia). No describas aquí un formato distinto.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/consulta-lgmasc-marco-institucional/references/corpus_lgmasc_marco_institucional.json`

Estructura:

- `metadata`: título de la ley, fuente (DOF), `capitulos_incluidos` (I-V,
  con su rango de artículos), `total_articulos` (60), `nota_alcance`
  (explica que este corpus no regula el procedimiento arbitral sustantivo)
  y `relacion_con_otros_corpus`.
- `articulos[]`: 60 registros (arts. 1 a 60), cada uno con `numero`,
  `capitulo_numero`/`capitulo_nombre`, `seccion_nombre` (cuando aplica),
  `texto_intro`, `fracciones[]` (cada una con `marcador` romano/arábigo y
  `texto`), y `texto_completo` — usa siempre este último campo para citar
  o reproducir texto legal.

## Mapa de contenido

- **Cap. I (arts. 1-8)** — objeto de la ley (art. 1: bases, principios
  generales y distribución de competencias conforme a los arts. 17 y 73
  fracción XXIX-A constitucionales; supletoriedad del CNPCyF), ámbito
  subjetivo de aplicación (art. 2), uso de tecnologías de la información
  (art. 3), el catálogo de MASC del art. 4 (negociación, negociación
  colaborativa, mediación, conciliación, arbitraje), definiciones legales
  (art. 5), principios rectores (art. 6: acceso a la justicia alternativa,
  autonomía de la voluntad, entre otros), y participación de entes
  públicos (arts. 7-8).
- **Cap. II (arts. 9-29)** — competencia: Sección Primera (Consejo
  Nacional de MASC), y las secciones subsecuentes sobre distribución de
  competencias entre Federación y entidades federativas.
- **Cap. III (arts. 30-48)** — personas facilitadoras públicas y privadas,
  personas abogadas colaborativas, su certificación (Sección Segunda), y
  reglas especiales para facilitadores de pueblos y comunidades indígenas
  y afromexicanas (art. 41).
- **Cap. IV (arts. 49-56)** — Registros y la Plataforma Nacional de MASC.
- **Cap. V (arts. 57-60)** — reglas generales sobre las partes.

## Estrategia de búsqueda

1. Número de artículo exacto (`numero`).
2. Tema general (competencia, certificación, registros, partes) usando el
   mapa de contenido anterior y el campo `capitulo_nombre`/`seccion_nombre`.
3. Coincidencia de texto libre sobre el contenido de `texto_completo`.

Si la pregunta involucra la tramitación práctica de un MASC o el convenio
resultante, remite a `tramitacion-convenio-masc`. Si involucra sanciones a
facilitadores o Centros, remite a `analisis-riesgos-sanciones-masc`. Si
involucra el procedimiento arbitral sustantivo, remite a
`consulta-arbitraje-comercial-ccom` o `consulta-juicio-arbitral-cnpcyf`
según la materia (usa `identificacion-ley-aplicable-masc` si hay duda). Si
involucra jurisprudencia, usa `busqueda-criterios-masc`.

## Formato de respuesta

1. Cita el o los artículos aplicables con su número y, si es relevante, la
   fracción exacta, reproduciendo el texto de `texto_completo` entre
   comillas o en bloque de cita, identificando siempre "LGMASC" como
   fuente.
2. Da una explicación breve en lenguaje llano de lo que dice el artículo,
   después de la cita textual, no en lugar de ella.
3. Si el usuario pide fundamento para un escrito o dictamen, usa el
   formato de `citas-legales-masc` (sección 2).

## Límites

- Este corpus es un documento de trabajo generado a partir del texto
  vigente de la LGMASC a la fecha de corte de este plugin. Ante cualquier
  duda sobre reformas posteriores, sugiere verificar el texto vigente en
  https://www.dof.gob.mx o https://www.diputados.gob.mx/LeyesBiblio/.
- No es una opinión legal definitiva; los análisis que produzcas requieren
  revisión de un abogado antes de usarse.
