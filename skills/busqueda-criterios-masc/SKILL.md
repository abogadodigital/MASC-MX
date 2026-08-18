---
name: busqueda-criterios-masc
description: >
  Esta skill debe usarse cuando el usuario pida "buscar tesis sobre
  arbitraje o MASC", "encuentra jurisprudencia sobre X" (fundamentos
  constitucionales, acuerdo o cláusula arbitral, Kompetenz-Kompetenz,
  nulidad del laudo, reconocimiento y ejecución, amparo contra el
  arbitraje, arbitraje médico, arbitraje de consumo o financiero,
  mediación y conciliación, la transacción, MASC en materia penal, etc.),
  "cita el criterio del registro [número]", "qué dice la tesis sobre el
  artículo [número] del Código de Comercio o de la LGMASC", o necesite
  localizar y citar correctamente uno o más de los 78 criterios de la
  SCJN y tribunales federales sobre arbitraje y MASC empaquetados con este
  plugin.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Búsqueda y cita de criterios sobre arbitraje y MASC

Localiza el criterio o los criterios relevantes dentro del corpus
empaquetado y devuélvelos en formato de citación legal mexicana correcto.
No busques en internet ni inventes criterios: esta skill trabaja
exclusivamente contra el archivo empaquetado.

## Formato de citación (obligatorio — ver skill dedicada)

El formato exacto de citación está definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-masc/SKILL.md`. Esta skill no
repite esas reglas: consúltalas ahí y aplícalas al pie de la letra cada
vez que entregues un criterio de este corpus.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-masc/references/corpus_tesis_masc.json`

Estructura: `metadata.categorias` (A-M con título y `total` de criterios),
`metadata.conclusiones_y_lineamientos` (10 lineamientos prácticos
transversales), `metadata.relacion_con_otros_corpus`, y `criterios[]`: 78
registros con `id`, `rubro`, `categoria_codigo`/`categoria_titulo`,
`autoridad_emisora`, `tipo_y_epoca`, `fecha`, `registro_digital`,
`enlace`, `resumen`, y `hechos`/`criterio_juridico`/`justificacion` (para
tesis con estructura moderna) o `texto_integro` (para tesis con estructura
tradicional de bloque único, propia de la Novena Época y de los
precedentes históricos). Nota: en varios criterios solo están presentes
`hechos` y `criterio_juridico` sin `justificacion`, u otros solo tienen
`texto_integro` — respeta la estructura del JSON tal cual está, sin
inventar contenido adicional.

## Mapa de categorías (A-M, 78 criterios)

- **A** — Fundamentos constitucionales y principios generales del
  arbitraje y los MASC (7): concepto de arbitraje, arbitraje voluntario,
  autonomía de la voluntad, constitucionalización a partir de la reforma
  de 2008 al art. 17 constitucional.
- **B** — El acuerdo, la cláusula y el compromiso arbitral (6).
- **C** — Competencia judicial vs. arbitral: remisión al arbitraje y el
  principio Kompetenz-Kompetenz (6).
- **D** — El laudo arbitral: emisión, contenido y tipos (4).
- **E** — Nulidad del laudo arbitral: causas y régimen procesal (10, la
  categoría más numerosa).
- **F** — Reconocimiento y ejecución del laudo arbitral, nacional y
  extranjero (8).
- **G** — Amparo y medios de impugnación frente al arbitraje (6).
- **H** — Arbitraje médico, CONAMED y comisiones estatales (5).
- **I** — Arbitraje y protección de consumidores y usuarios financieros,
  CONDUSEF y PROFECO (6).
- **J** — Mediación y conciliación como medios alternativos en materia
  civil y mercantil (4).
- **K** — La transacción como mecanismo alterno de solución de
  controversias (4).
- **L** — MASC en materia penal (6).
- **M** — Precedentes históricos, Quinta y Séptima Épocas (6).

## Estrategia de búsqueda

Empareja la solicitud del usuario, en este orden de precedencia:

1. `registro_digital` exacto, si se proporciona.
2. `categoria_codigo`/`categoria_titulo` si el usuario nombra un tema que
   corresponde a una de las 13 categorías anteriores.
3. Referencias a artículos de la LGMASC, el Código de Comercio o el CNPCyF
   mencionadas en el `resumen`, `hechos`, `criterio_juridico`,
   `justificacion` o `texto_integro` (p. ej. "artículo 1457 del Código de
   Comercio", "artículo 17 constitucional", "artículo 540 del CNPCyF").
4. Coincidencias de texto libre en `rubro` y `resumen`.

Lee `metadata.conclusiones_y_lineamientos` cuando el usuario haga una
pregunta sintética ("¿cuál es el criterio de mayor jerarquía sobre X?",
"¿cómo se relacionan estos criterios?", "dame un panorama general"): esa
sección sistematiza 10 lineamientos prácticos transversales (jerarquía de
las fuentes, la constitucionalización del arbitraje a partir de 2008, el
principio Kompetenz-Kompetenz como eje del sistema, el control judicial
limitado al procedimiento y no al fondo en materia de nulidad, la
evolución jurisprudencial documentada con criterios sustituidos o
abandonados, los límites a la eficacia de las cláusulas arbitrales y los
convenios de MASC, el arbitraje especializado médico y de consumo, el
MASC en materia penal como justicia restaurativa, la transacción como MASC
autónomo, y la vigencia y aplicación temporal de los criterios).

Al presentar el formato abreviado de 5 o más criterios, agrupa la lista
por `categoria_codigo` y presenta primero la fuente de mayor jerarquía
(Pleno y Salas de la SCJN > Plenos Regionales/de Circuito > Tribunales
Colegiados), conforme al primer lineamiento de
`metadata.conclusiones_y_lineamientos`.

## Cuando no hay coincidencias

Si ningún registro del corpus responde la consulta, dilo claramente y
sugiere al usuario realizar una búsqueda en vivo en el Semanario Judicial
de la Federación oficial (https://sjf2.scjn.gob.mx), o, si hay algún
conector de búsqueda jurisprudencial disponible en este entorno, ofrece
usarlo directamente sin dar por hecho de cuál se trata. Nunca fabriques un
registro digital ni un rubro.

## Advertencia de vigencia

Señala siempre, al entregar una cita para uso en un escrito, que el
corpus es un documento de trabajo con fecha de corte determinada (ver
`metadata.fecha_investigacion` del corpus) y que la vigencia debe
confirmarse en la fuente oficial antes de usarse, especialmente si el
criterio pudo haber sido sustituido o abandonado por jurisprudencia
posterior (el lineamiento 5 de `metadata.conclusiones_y_lineamientos`
documenta al menos dos casos de esto dentro del propio corpus).
