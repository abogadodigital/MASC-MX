---
name: tramitacion-convenio-masc
description: >
  Esta skill debe usarse cuando el usuario pida ayuda para "tramitar una
  mediación o conciliación", "cómo inicio un procedimiento de negociación
  colaborativa", "qué requisitos debe tener el convenio de mediación o
  conciliación", "redacta el convenio resultante de mi mediación", "cómo
  opera un Centro de MASC en el ámbito administrativo", "qué efectos
  jurídicos tiene el convenio, tiene fuerza de cosa juzgada", "cuánto dura
  el procedimiento de mediación o conciliación", "qué pasa si una parte no
  comparece al MASC", "qué dice el artículo [número, entre 61 y 138] de la
  LGMASC", "hay ODR en México", "qué es la Solución de Controversias en
  Línea", "puedo tramitar una mediación o conciliación en línea o por
  medios electrónicos", "qué obligaciones tienen las plataformas o
  administradoras de Sistemas en Línea", o de cualquier otra forma
  necesite diseñar, tramitar o documentar un procedimiento de negociación,
  negociación colaborativa, mediación o conciliación conforme a la LGMASC,
  incluyendo la redacción del convenio resultante y el régimen especial de
  Solución de Controversias en Línea (arts. 86-93).
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Tramitación de MASC no adjudicativos y redacción del convenio (LGMASC, Cap. VI-VIII)

Ayuda al usuario a **tramitar** —no solo a entender— un procedimiento de
negociación, negociación colaborativa, mediación o conciliación conforme a
la LGMASC, y a redactar el convenio que documenta su resultado. Esta skill
combina consulta literal, análisis aplicado a los hechos del usuario y
redacción de instrumentos, porque en la práctica estas tareas casi siempre
se piden juntas.

## Cuándo aplica esta skill (regla de encuadre)

Esta skill cubre exclusivamente los MASC **no adjudicativos** (negociación,
negociación colaborativa, mediación, conciliación) y su marco operativo
bajo la LGMASC (tramitación, convenio, Centros de MASC en el ámbito
administrativo). Si el usuario necesita tramitar o redactar algo
relacionado con un **arbitraje** (acuerdo arbitral, demanda arbitral,
laudo), esta skill NO es la fuente: usa `redaccion-escritos-masc` con el
corpus de `consulta-arbitraje-comercial-ccom` o
`consulta-juicio-arbitral-cnpcyf` según la materia. Si tienes duda, usa
primero `identificacion-ley-aplicable-masc`.

## Formato de citación

Sigue el formato de citación (artículos de la LGMASC y jurisprudencia,
identificando siempre "LGMASC" como fuente) definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-masc/SKILL.md`. No describas
aquí un formato distinto.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/tramitacion-convenio-masc/references/corpus_lgmasc_operacion_sanciones.json`

Estructura: `metadata` (capítulos incluidos con su rango de artículos,
`total_articulos` -84-, `nota_alcance`, `relacion_con_otros_corpus`) y
`articulos[]`: 84 registros (arts. 61-144, Cap. VI-IX), cada uno con
`numero`, `capitulo_numero`/`capitulo_nombre`, `texto_intro`,
`fracciones[]`, y `texto_completo`. Esta skill usa principalmente los
Cap. VI (arts. 61-93), VII (arts. 94-114) y VIII (arts. 115-138); el Cap.
IX (arts. 139-144, sanciones) es el dominio de
`analisis-riesgos-sanciones-masc`, aunque ambas skills leen el mismo
archivo de corpus.

Complementa cuando aplique con:
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-lgmasc-marco-institucional/references/corpus_lgmasc_marco_institucional.json`
  para las definiciones legales del art. 5 y los principios rectores del
  art. 6 que sustentan el análisis de tramitación.
- `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-masc/references/corpus_tesis_masc.json`
  (categoría J: mediación y conciliación en materia civil y mercantil, y
  categoría K: la transacción).

## Mapa de contenido (Cap. VI-VIII, arts. 61-138)

- **Cap. VI, De la Tramitación (arts. 61-93)**: inicio del procedimiento,
  sesiones, confidencialidad, comparecencia de las partes y consecuencias
  de la incomparecencia, acciones preventivas durante el procedimiento,
  reglas de la comediación, y conclusión del procedimiento con o sin
  convenio.
  - **Sección "De la Solución de Controversias en Línea" / ODR (arts.
    86-93)**: régimen especial y autónomo para MASC tramitados por
    tecnologías de la información (arts. 86 y 89), con definiciones
    propias (art. 87), principios adicionales como el de pleno
    conocimiento (art. 88), reglas de inicio (art. 90), derechos
    reforzados de las partes (art. 91), obligaciones específicas de
    personas facilitadoras, administradoras y proveedoras de Sistemas en
    Línea (art. 92), y modalidades operativas: sesiones sincrónicas o
    asincrónicas, con o sin intervención de persona facilitadora (art.
    93). Complementa el principio general del art. 3 (mismo ordenamiento,
    corpus de `consulta-lgmasc-marco-institucional`), pero es este bloque
    de arts. 86-93, no el art. 3 por sí solo, el que desarrolla el
    régimen sustantivo de la Solución de Controversias en Línea. Cítalo
    expresamente cuando el usuario pregunte por ODR, MASC en línea o
    solución de controversias en línea, aunque no use esos términos
    exactos.
- **Cap. VII, Del Convenio (arts. 94-114)**: requisitos de validez del
  convenio, su contenido mínimo, efectos jurídicos (incluida su fuerza
  ejecutiva/cosa juzgada cuando la ley lo prevé), formalización ante
  persona facilitadora o Centro, y supuestos de nulidad o incumplimiento
  del convenio.
- **Cap. VIII, De los Centros de MASC en el ámbito administrativo (arts.
  115-138)**: constitución, registro y funcionamiento de los Centros,
  requisitos para operar, y su relación con las personas facilitadoras
  certificadas.

## Tipos de asistencia que puedes producir

### 1. Diagnóstico/ruta de tramitación
A partir de los hechos que describa el usuario (tipo de conflicto,
mecanismo elegido, si ya hay facilitador o Centro asignado, si hay partes
que se resisten a comparecer), traza la ruta procedimental aplicable
citando el artículo exacto de cada paso.

### 2. Redacción o revisión del convenio
Redacta o revisa el convenio resultante de una mediación o conciliación,
verificando que cumpla los requisitos del Cap. VII (identificación de las
partes, objeto, obligaciones asumidas, firma de la persona facilitadora
cuando corresponda, y las menciones necesarias para su fuerza ejecutiva).

### 3. Diseño del flujo ante un Centro de MASC
Diseña o explica el flujo institucional de un caso que se tramitará ante
un Centro de MASC en el ámbito administrativo, con base en el Cap. VIII.

## Formato de la respuesta

1. Si es un diagnóstico, presenta primero la ruta procedimental resumida
   en un párrafo breve.
2. Desarrolla el fundamento artículo por artículo, citando siempre
   `texto_completo`.
3. Si produces un documento (convenio, escrito de inicio), entrégalo
   completo y utilizable, no solo un esquema, salvo que el usuario pida
   explícitamente solo un esquema.
4. Cita jurisprudencia aplicable cuando exista, siguiendo el formato de
   `citas-legales-masc`.
5. Si el incumplimiento del procedimiento expone a una persona
   facilitadora, persona abogada colaborativa o Centro a una sanción,
   remite a `analisis-riesgos-sanciones-masc`. Si el usuario necesita
   practicar el procedimiento mismo (simulando a la contraparte), remite a
   `simulacion-masc`; si necesita consejos tácticos, remite a
   `asesoria-estrategica-masc`.

## Límites

- Todo lo que produzcas (convenio, ruta de tramitación, escrito) es un
  **borrador o insumo de trabajo para revisión de un abogado**, no un
  documento final listo para usarse sin supervisión. Dilo expresamente al
  entregarlo.
- No asumas hechos, plazos ni partes que el usuario no haya proporcionado;
  si la información es insuficiente, dilo y enumera qué falta.
- Advierte siempre sobre la necesidad de verificar la vigencia de las
  disposiciones citadas antes de usarlas con consecuencias legales.
