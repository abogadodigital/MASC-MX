---
name: identificacion-ley-aplicable-masc
description: >
  Esta skill debe usarse SIEMPRE como paso previo, antes de responder con
  fundamento normativo, cuando no sea inmediata y evidentemente claro cuál
  de las tres leyes empaquetadas en este plugin (Ley General de Mecanismos
  Alternativos de Solución de Controversias -LGMASC-, Código de Comercio
  -Título Cuarto, Del Arbitraje Comercial- o Código Nacional de
  Procedimientos Civiles y Familiares -CNPCyF, Sección Tercera y Título
  Tercero-) rige los hechos que describe el usuario. Actívala cuando el
  usuario pregunte "qué ley aplica a mi caso", "esto es arbitraje mercantil
  o civil", "puedo usar la LGMASC para esto o me voy al Código de
  Comercio", "cuál es la ley aplicable si mi conflicto es de [materia]",
  cuando describa hechos de un conflicto sin decir expresamente si es
  mercantil, civil, familiar o administrativo, o cuando otra skill de este
  plugin detecte que la pregunta del usuario podría encuadrar en más de una
  de las tres leyes. Esta skill es la que evita que el plugin cruce
  conceptos o cite el fundamento equivocado.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Identificación de la ley aplicable dentro de este plugin

Este plugin empaqueta **tres ordenamientos distintos**, no uno. A
diferencia de un plugin de una sola ley, aquí el primer paso de cualquier
análisis con fundamento normativo es identificar correctamente cuál (o
cuáles) de las tres leyes rige los hechos concretos del usuario, porque
mezclarlas produce fundamento incorrecto. Consulta esta skill al inicio de
cualquier análisis en el que la materia del conflicto, o el mecanismo MASC
concreto que el usuario menciona, no esté ya identificado sin ambigüedad.

## Las tres leyes y su ámbito de aplicación (regla de oro)

### 1. Ley General de Mecanismos Alternativos de Solución de Controversias (LGMASC)

**Aplica a:** negociación, negociación colaborativa, mediación y
conciliación — es decir, los MASC **no adjudicativos**, sin importar si la
materia subyacente es civil, familiar, mercantil o (en lo compatible)
administrativa — así como al régimen institucional transversal: personas
facilitadoras públicas y privadas y su certificación, Centros de MASC en
el ámbito administrativo, registros, la Plataforma Nacional, y el régimen
de responsabilidades y sanciones de quienes operan MASC.

**No aplica** al procedimiento arbitral en sí mismo. El artículo 4,
fracción V, de la propia LGMASC define al arbitraje como uno de los MASC,
pero remite expresamente su regulación al Código de Comercio y al Código
Nacional de Procedimientos Civiles y Familiares ("con la participación de
una persona tercera llamada árbitro quien dicta un laudo conforme a las
normas establecidas en el Código de Comercio, el Código Nacional de
Procedimientos Civiles y Familiares, y los Tratados Internacionales de los
que el Estado mexicano sea parte, según proceda"). Si el usuario pregunta
por el procedimiento arbitral (nombramiento de árbitro, sustanciación,
laudo, nulidad, ejecución), la LGMASC solo es relevante para el marco
institucional (facilitadores, Centros, competencia), nunca para el
procedimiento arbitral sustantivo.

**Corpus:** `consulta-lgmasc-marco-institucional` (Cap. I-V: naturaleza,
competencia, facilitadores, registros, partes) y `tramitacion-convenio-masc`
/ `analisis-riesgos-sanciones-masc` (Cap. VI-IX: tramitación, convenio,
Centros, sanciones).

### 2. Código de Comercio, Título Cuarto (Del Arbitraje Comercial)

**Aplica a:** el procedimiento arbitral cuando la controversia es de
naturaleza **mercantil** (arbitraje comercial nacional, y el internacional
cuando el lugar del arbitraje esté en territorio nacional — art. 1415).
Es la ley especial que regula el acuerdo de arbitraje, la composición y
competencia del tribunal arbitral, la sustanciación, el laudo, las costas,
la nulidad del laudo, y el reconocimiento y ejecución de laudos.

**Criterio de activación:** la relación jurídica de fondo (el contrato o
la relación que originó el conflicto) debe ser mercantil — p. ej. un
contrato de compraventa mercantil, distribución, franquicia, sociedades,
títulos de crédito, etc. Si la relación de fondo es civil o familiar, no
uses este corpus: usa `consulta-juicio-arbitral-cnpcyf`.

**Corpus:** `consulta-arbitraje-comercial-ccom`.

### 3. Código Nacional de Procedimientos Civiles y Familiares (CNPCyF)

**Aplica a:** (a) la preparación del juicio arbitral ante autoridad
jurisdiccional cuando existe cláusula de arbitraje y no se ha nombrado
árbitro, éste se rehusó, falleció o no hay sustituto (arts. 386-390); y
(b) el juicio arbitral en materia **civil o familiar** propiamente dicho
(arts. 533-549), incluyendo qué negocios NO pueden someterse a arbitraje
(art. 540: alimentos, guarda y custodia, divorcios salvo excepciones
patrimoniales, nulidad de matrimonio, estado civil de las personas) y la
ejecución de laudos ante juez.

**Criterio de activación:** la relación jurídica de fondo es civil o
familiar (no mercantil), o el usuario necesita apoyo judicial para
designar árbitro o ejecutar un laudo cuando el Código de Comercio no
resuelve el punto. Recuerda además que el artículo 1 de la LGMASC dispone
que, en todo lo no previsto por esa ley, es supletorio el CNPCyF.

**Corpus:** `consulta-juicio-arbitral-cnpcyf`.

## Procedimiento de identificación

1. Pregunta o infiere, a partir de los hechos del usuario, dos datos
   mínimos: **(a) el mecanismo MASC concreto** (negociación, mediación,
   conciliación o arbitraje) y **(b) la naturaleza de la relación jurídica
   de fondo** (mercantil, civil, familiar u otra). Si el usuario no lo ha
   dicho, pregúntalo antes de fundamentar — no lo asumas.
2. Aplica la tabla de la sección anterior. Si el mecanismo es negociación,
   mediación o conciliación → LGMASC. Si es arbitraje y la relación de
   fondo es mercantil → Código de Comercio. Si es arbitraje y la relación
   de fondo es civil o familiar → CNPCyF. Si es arbitraje y hay apoyo
   judicial pendiente (designación de árbitro, ejecución) → revisa si el
   Código de Comercio ya lo resuelve; si no, aplica el CNPCyF como
   supletorio.
3. **Casos de concurrencia (dos o más leyes a la vez):** son legítimos y
   deben señalarse expresamente, no evitarse. Ejemplos típicos: (i) un
   arbitraje mercantil que además requiere el auxilio de un Centro de MASC
   certificado conforme a la LGMASC para su fase de facilitación previa a
   la cláusula arbitral; (ii) una mediación exitosa (LGMASC) cuyo convenio
   se pretende hacer valer ante un juez con fuerza de cosa juzgada,
   situación en la que puede ser relevante el CNPCyF; (iii) un arbitraje
   iniciado bajo el Código de Comercio en el que, ante un vacío, se acude
   supletoriamente al CNPCyF. En estos casos, identifica y cita cada
   fundamento por separado, dejando explícito qué resuelve cada ley.
4. Si después de aplicar los pasos 1-3 sigue existiendo duda razonable
   (p. ej. la naturaleza mercantil o civil de la relación de fondo no está
   clara), dilo expresamente al usuario, ofrece las dos lecturas posibles
   con su fundamento respectivo, y pide el dato que falta para resolver la
   ambigüedad — nunca elijas una ley al azar ni mezcles fundamento de dos
   leyes en una sola cita sin advertirlo.

## Tabla rápida de referencia

| Mecanismo | Materia de fondo | Ley aplicable | Skill de consulta |
|---|---|---|---|
| Negociación / negociación colaborativa / mediación / conciliación | Cualquiera | LGMASC | `consulta-lgmasc-marco-institucional`, `tramitacion-convenio-masc` |
| Arbitraje | Mercantil | Código de Comercio, Título Cuarto | `consulta-arbitraje-comercial-ccom` |
| Arbitraje | Civil o familiar | CNPCyF | `consulta-juicio-arbitral-cnpcyf` |
| Designación judicial de árbitro (cualquier materia, sin árbitro nombrado) | — | CNPCyF (arts. 386-390), salvo regla especial del Código de Comercio | `consulta-juicio-arbitral-cnpcyf` |
| Facilitadores, su certificación, Centros de MASC, sanciones a facilitadores | — | LGMASC | `consulta-lgmasc-marco-institucional`, `analisis-riesgos-sanciones-masc` |

## Uso por las demás skills de este plugin

Todas las demás skills de este plugin que requieran fundamento normativo
(`consulta-lgmasc-marco-institucional`, `consulta-arbitraje-comercial-ccom`,
`consulta-juicio-arbitral-cnpcyf`, `tramitacion-convenio-masc`,
`analisis-riesgos-sanciones-masc`, `redaccion-escritos-masc`,
`material-docente-masc`) deben aplicar el procedimiento de esta skill
cuando la ley aplicable a los hechos del usuario no sea evidente por sí
sola, en vez de asumir cuál de las tres leyes usar. No es necesario
invocar esta skill cuando el usuario ya identificó sin ambigüedad el
mecanismo y la materia (p. ej. "tengo una cláusula arbitral en un contrato
de compraventa mercantil" activa directamente el Código de Comercio).

## Límites

- Esta skill resuelve un problema de **encuadre normativo**, no sustituye
  el análisis de fondo (que corresponde a `tramitacion-convenio-masc`,
  `analisis-riesgos-sanciones-masc`, `redaccion-escritos-masc` o a las
  skills de consulta correspondientes).
- Ante hechos genuinamente mixtos o fronterizos (p. ej. la naturaleza
  mercantil o civil de un acto es discutible), no fuerces una respuesta
  única: expón el análisis de encuadre y sus consecuencias prácticas para
  cada hipótesis, y recomienda la revisión de un abogado para la
  calificación final.
