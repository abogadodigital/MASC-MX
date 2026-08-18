---
name: consulta-juicio-arbitral-cnpcyf
description: >
  Esta skill debe usarse cuando el usuario pregunte "qué dice el artículo
  [número, 386 a 390 o 533 a 549] del Código Nacional de Procedimientos
  Civiles y Familiares", "cómo pido al juez que designe árbitro si no se
  nombró en el contrato", "qué negocios no pueden someterse a arbitraje en
  materia civil o familiar", "cómo se ejecuta un laudo arbitral civil ante
  el juez", "qué causales existen para negar la ejecución de un laudo",
  "puedo arbitrar mi divorcio o la guarda y custodia de mis hijos", o
  necesite el texto literal de la Sección Tercera del Libro Tercero
  (Preparación del Juicio Arbitral) o del Título Tercero (Del Juicio
  Arbitral) del Código Nacional de Procedimientos Civiles y Familiares,
  cuando la controversia de fondo es de naturaleza civil o familiar, o
  cuando se requiere apoyo judicial para cualquier arbitraje.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Consulta del juicio arbitral civil y familiar (CNPCyF)

Responde dudas sobre el contenido literal de la Sección Tercera del Libro
Tercero ("De la Preparación del Juicio Arbitral", arts. 386-390) y el
Título Tercero ("Del Juicio Arbitral", arts. 533-549) del Código Nacional
de Procedimientos Civiles y Familiares (CNPCyF), citando siempre el texto
legal exacto contenido en el corpus empaquetado. No parafrasees el
artículo sin antes mostrar o citar su texto íntegro; no inventes
artículos, fracciones o causales que no existan en el corpus.

## Cuándo aplica este corpus (regla de encuadre)

Este corpus regula dos supuestos: (1) la designación judicial de árbitro
cuando existe cláusula de arbitraje y no se ha nombrado árbitro, éste se
rehusó, falleció o no hay sustituto (arts. 386-390), aplicable con
independencia de si la materia de fondo es mercantil o civil/familiar,
salvo que el Código de Comercio contenga regla especial; y (2) el juicio
arbitral en materia **civil o familiar** propiamente dicho (arts.
533-549). Si la relación de fondo es mercantil y el punto ya está resuelto
por el Código de Comercio, usa `consulta-arbitraje-comercial-ccom` en su
lugar. Recuerda que el art. 1 de la LGMASC hace a este Código supletorio
de la LGMASC en todo lo no previsto por ella. Si tienes duda sobre cuál de
las tres leyes aplica, usa primero `identificacion-ley-aplicable-masc`.

## Formato de citación

Sigue el formato de citación definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-masc/SKILL.md` (sección 2,
identificando siempre "CNPCyF" como la ley de origen; sección 1 si además
citas jurisprudencia). No describas aquí un formato distinto.

## Fuente de datos

`${CLAUDE_PLUGIN_ROOT}/skills/consulta-juicio-arbitral-cnpcyf/references/corpus_juicio_arbitral_cnpcyf.json`

Estructura: `metadata` (`secciones_incluidas` con su rango de artículos,
`total_articulos` -22-, `nota_alcance`,
`relacion_con_ley_general_masc_y_ccom` y `relacion_con_otros_corpus`) y
`articulos[]`: 22 registros (arts. 386-390 y 533-549), cada uno con
`numero`, `titulo_nombre`, `capitulo_nombre`, `seccion_nombre` (cuando
aplica), `texto_intro`, `fracciones[]` (`marcador` + `texto`), y
`texto_completo` — usa siempre este último campo para citar o reproducir
texto legal.

## Mapa de contenido

- **Sección Tercera, Preparación del Juicio Arbitral (arts. 386-390)** —
  procedimiento ante el juez para designar árbitro cuando hay cláusula
  pero no hay árbitro nombrado, cuando el árbitro nombrado renuncia o
  fallece sin sustituto, requisitos del escrito y de la audiencia en la
  que se elige árbitro de común acuerdo o lo designa la autoridad.
- **Título Tercero, Cap. I, Disposiciones Generales (arts. 533-545)** —
  derecho de las partes de someterse a juicio arbitral (art. 533), forma
  y momento del acuerdo de arbitraje (art. 534-536), quiénes pueden
  comprometer en árbitros (personas tutoras, albaceas, síndicos de
  concursos civiles — arts. 537-539), **negocios que NO pueden someterse
  a arbitraje (art. 540)**: alimentos, régimen de convivencia, guarda y
  custodia y demás derechos de niñas, niños y adolescentes; divorcios
  (salvo separación de bienes y liquidación/disolución de la sociedad
  conyugal); nulidad de matrimonio; estado civil de las personas (con las
  excepciones del Código Civil o Familiar aplicable); y los demás que la
  ley prohíba expresamente; conflicto de interés e imparcialidad del
  árbitro (art. 541), trato igualitario y libertad procedimental (art.
  542), la excepción de remisión al arbitraje y litispendencia (art. 543),
  normas aplicables al fondo (art. 544), y condena en costas (art. 545).
- **Título Tercero, Cap. II, De la Ejecución de Laudos (arts. 546-549)** —
  presentación del laudo para su ejecución (art. 546), competencia
  judicial (art. 547), auxilio de la jurisdicción al tribunal arbitral
  (art. 548), y las **causales tasadas del art. 549** para negar la
  ejecución (incapacidad de una parte o invalidez del acuerdo; falta de
  notificación debida o imposibilidad de hacer valer sus derechos; laudo
  sobre controversia no prevista en el acuerdo o que excede sus términos;
  composición del tribunal o procedimiento no ajustados al acuerdo; laudo
  no obligatorio, anulado o suspendido) — nota: contra el laudo arbitral
  no procede recurso alguno; solo la ejecución admite estas
  impugnaciones.

## Estrategia de búsqueda

1. Número de artículo exacto (`numero`).
2. Tema general (designación de árbitro, negocios excluidos del
   arbitraje, remisión al arbitraje, ejecución de laudo, causales de
   denegación) usando el mapa de contenido y el campo
   `titulo_nombre`/`capitulo_nombre`/`seccion_nombre`.
3. Coincidencia de texto libre sobre el contenido de `texto_completo`.

## Formato de respuesta

1. Cita el o los artículos aplicables con su número y fracción exacta,
   reproduciendo `texto_completo`, identificando siempre "CNPCyF" como
   fuente.
2. Explica en lenguaje llano lo que dice el artículo, después de la cita
   textual, no en lugar de ella.
3. Cita jurisprudencia de apoyo cuando exista (categorías C, E, F, J y K
   del corpus de tesis son especialmente relevantes aquí), siguiendo el
   formato de `citas-legales-masc`.
4. Si la pregunta requiere redactar el escrito de designación de árbitro,
   la demanda de nulidad o el escrito de ejecución, remite a
   `redaccion-escritos-masc`. Si requiere evaluar el riesgo de que se
   deniegue la ejecución, remite a `analisis-riesgos-sanciones-masc`.

## Límites

- Este corpus refleja el texto vigente de estas secciones del CNPCyF a la
  fecha de corte de este plugin. Ante cualquier duda sobre reformas
  posteriores, sugiere verificar el texto vigente en
  https://www.dof.gob.mx o https://www.diputados.gob.mx/LeyesBiblio/.
- No es una opinión legal definitiva; los análisis que produzcas requieren
  revisión de un abogado antes de usarse, particularmente en materia
  familiar por la sensibilidad de las exclusiones del art. 540.
