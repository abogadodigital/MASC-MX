---
name: consulta-arbitraje-comercial-ccom
description: >
  Esta skill debe usarse cuando el usuario pregunte "qué dice el artículo
  [número, entre 1415 y 1480] del Código de Comercio", "cómo se compone un
  tribunal arbitral en materia mercantil", "qué es el principio
  Kompetenz-Kompetenz", "cómo se sustancia un arbitraje comercial", "qué
  requisitos debe tener el laudo arbitral mercantil", "cómo se anula un
  laudo arbitral comercial", "cómo se reconoce o ejecuta un laudo arbitral
  nacional o extranjero", "qué apoyo judicial existe para el arbitraje
  comercial", o necesite el texto literal del Título Cuarto (Del Arbitraje
  Comercial) del Código de Comercio, cuando la controversia de fondo es de
  naturaleza mercantil.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Consulta del arbitraje comercial (Código de Comercio, Título Cuarto)

Responde dudas sobre el contenido literal del Título Cuarto ("Del
Arbitraje Comercial") del Código de Comercio (arts. 1415-1480), citando
siempre el texto legal exacto contenido en el corpus empaquetado. No
parafrasees el artículo sin antes mostrar o citar su texto íntegro; no
inventes artículos, fracciones o plazos que no existan en el corpus.

## Cuándo aplica este corpus (regla de encuadre)

Este Título rige el arbitraje comercial nacional, y el internacional
cuando el lugar del arbitraje se encuentre en territorio nacional (art.
1415), salvo lo dispuesto en tratados internacionales de los que México
sea parte o en otras leyes con procedimiento distinto. El criterio central
es que la relación jurídica de fondo sea de naturaleza **mercantil**. Si
la relación de fondo es civil o familiar, este corpus NO aplica: usa
`consulta-juicio-arbitral-cnpcyf`. Si tienes duda razonable sobre la
naturaleza mercantil de la relación de fondo, usa primero
`identificacion-ley-aplicable-masc` antes de fundamentar.

## Formato de citación

Sigue el formato de citación definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-masc/SKILL.md` (sección 2,
identificando siempre "Código de Comercio, Título Cuarto - Del Arbitraje
Comercial" como la ley de origen; sección 1 si además citas
jurisprudencia). No describas aquí un formato distinto.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/consulta-arbitraje-comercial-ccom/references/corpus_arbitraje_comercial_ccom.json`

Estructura: `metadata` (capítulos incluidos con su rango de artículos,
`total_articulos` -66-, `nota_alcance`, `relacion_con_ley_general_masc` y
`relacion_con_otros_corpus`) y `articulos[]`: 66 registros (arts.
1415-1480), cada uno con `numero`, `capitulo_numero`/`capitulo_nombre`,
`texto_intro`, `fracciones[]` (`marcador` + `texto`), y `texto_completo`
— usa siempre este último campo para citar o reproducir texto legal.

Complementa cuando aplique con:
- `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-masc/references/corpus_tesis_masc.json`
  (categorías A-I, especialmente B -acuerdo y cláusula arbitral-, C
  -competencia judicial vs. arbitral y Kompetenz-Kompetenz-, D -el laudo-,
  E -nulidad del laudo-, F -reconocimiento y ejecución- y G -amparo y
  medios de impugnación-).
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-juicio-arbitral-cnpcyf/references/corpus_juicio_arbitral_cnpcyf.json`
  para la fase de apoyo judicial (designación de árbitro, ejecución de
  laudo) cuando este Título no contenga una regla propia sobre el punto.

## Mapa de contenido (10 capítulos, arts. 1415-1480)

- **Cap. I (arts. 1415-1422)** — Disposiciones generales: ámbito de
  aplicación (art. 1415), definiciones (art. 1416), y reglas de
  interpretación de plazos, formalidades y libertad de procedimiento del
  Título.
- **Cap. II (arts. 1423-1425)** — Acuerdo de arbitraje: forma escrita,
  remisión al arbitraje por el juez, y medidas cautelares antes o durante
  las actuaciones arbitrales.
- **Cap. III (arts. 1426-1431)** — Composición del tribunal arbitral:
  número de árbitros, nombramiento, motivos de recusación y
  procedimiento de recusación, falta o imposibilidad de ejercicio de las
  funciones.
- **Cap. IV (arts. 1432-1433)** — Competencia del tribunal arbitral: el
  principio Kompetenz-Kompetenz (la facultad del propio tribunal arbitral
  de decidir sobre su competencia, incluidas las excepciones relativas a
  la existencia o validez del acuerdo de arbitraje) y medidas cautelares
  ordenadas por el tribunal arbitral.
- **Cap. V (arts. 1434-1444)** — Sustanciación de las actuaciones
  arbitrales: trato equitativo a las partes, determinación del
  procedimiento, lugar y sede, idioma, demanda y contestación,
  audiencias, incomparecencia de una parte, peritos, y asistencia judicial
  para el desahogo de pruebas.
- **Cap. VI (arts. 1445-1451)** — Pronunciamiento del laudo y terminación
  de las actuaciones: normas aplicables al fondo, decisiones del tribunal
  con más de un árbitro, transacción, forma y contenido del laudo, y
  terminación de las actuaciones.
- **Cap. VII (arts. 1452-1456)** — De las costas: qué comprenden y su
  distribución.
- **Cap. VIII (arts. 1457-1460)** — De la nulidad del laudo: causales
  tasadas de nulidad (art. 1457, replicadas en el art. 549 del CNPCyF para
  la fase de ejecución) y plazo para promover la acción.
- **Cap. IX (arts. 1461-1463)** — Reconocimiento y ejecución de laudos,
  nacionales y extranjeros, y causales tasadas para denegar el
  reconocimiento o la ejecución.
- **Cap. X (arts. 1464-1480)** — De la Intervención Judicial en la
  Transacción Comercial y el Arbitraje: reglas sobre remisión al
  arbitraje ante el juez, y régimen de medidas cautelares ordenadas por
  el tribunal arbitral y su reconocimiento/ejecución/denegación ante
  autoridad judicial.

## Estrategia de búsqueda

1. Número de artículo exacto (`numero`).
2. Tema general (composición del tribunal, competencia, sustanciación,
   laudo, costas, nulidad, reconocimiento y ejecución, intervención
   judicial) usando el mapa de contenido y el campo `capitulo_nombre`.
3. Coincidencia de texto libre sobre el contenido de `texto_completo`.

## Formato de respuesta

1. Cita el o los artículos aplicables con su número y fracción exacta,
   reproduciendo `texto_completo`, identificando siempre "Código de
   Comercio" como fuente.
2. Explica en lenguaje llano lo que dice el artículo, después de la cita
   textual, no en lugar de ella.
3. Cita jurisprudencia de apoyo cuando exista, siguiendo el formato de
   `citas-legales-masc`.
4. Si la pregunta requiere redactar una cláusula, demanda de nulidad, o
   escrito de reconocimiento/ejecución, remite a `redaccion-escritos-masc`.
   Si requiere evaluar el riesgo de nulidad o de que se deniegue la
   ejecución, remite a `analisis-riesgos-sanciones-masc`.

## Límites

- Este corpus refleja el texto vigente del Título Cuarto del Código de
  Comercio a la fecha de corte de este plugin. Ante cualquier duda sobre
  reformas posteriores, sugiere verificar el texto vigente en
  https://www.dof.gob.mx o https://www.diputados.gob.mx/LeyesBiblio/.
- No es una opinión legal definitiva; los análisis que produzcas requieren
  revisión de un abogado antes de usarse.
