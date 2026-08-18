---
name: redaccion-escritos-masc
description: >
  Esta skill debe usarse cuando el usuario pida "redacta una cláusula
  compromisoria o de arbitraje", "redacta un acuerdo de arbitraje", "prepara
  la demanda de nulidad de un laudo arbitral", "redacta el escrito para
  pedir al juez que designe árbitro", "prepara el escrito de reconocimiento
  o ejecución de un laudo", "redacta el convenio de mediación o
  conciliación", "prepara un escrito ante un Centro de MASC", "redacta la
  oposición a la ejecución de un laudo", o necesite un borrador de escrito,
  cláusula o convenio relacionado con negociación, mediación, conciliación
  o arbitraje, con fundamento en la LGMASC, el Código de Comercio o el
  CNPCyF, según corresponda.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Redacción de escritos, cláusulas y convenios de MASC y arbitraje

Redacta borradores de trabajo (cláusulas arbitrales, acuerdos de
arbitraje, demandas de nulidad de laudo, escritos de designación judicial
de árbitro, escritos de reconocimiento/ejecución de laudo u oposición a
ella, convenios de mediación o conciliación, y escritos ante Centros de
MASC) con fundamento en la ley que corresponda según los hechos del
usuario.

## Paso obligatorio previo: identificar la ley aplicable

Antes de redactar, identifica con `identificacion-ley-aplicable-masc` cuál
de las tres leyes empaquetadas rige el escrito que se te pide, salvo que
ya sea evidente por los hechos (p. ej. "cláusula arbitral para un contrato
de compraventa mercantil" apunta claramente al Código de Comercio). Un
escrito mal fundamentado por citar la ley equivocada es un error grave en
este plugin — nunca mezcles fundamento de dos leyes sin advertirlo
expresamente.

## Formato de citación

Sigue el formato de citación (artículos y jurisprudencia, identificando
siempre de cuál de las tres leyes proviene cada cita) definido en
`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-masc/SKILL.md`.

## Fuentes de datos

Usa según el tipo de escrito solicitado:

- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-lgmasc-marco-institucional/references/corpus_lgmasc_marco_institucional.json`
  y `${CLAUDE_PLUGIN_ROOT}/skills/tramitacion-convenio-masc/references/corpus_lgmasc_operacion_sanciones.json`
  — para convenios de mediación/conciliación y escritos ante Centros de
  MASC.
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-arbitraje-comercial-ccom/references/corpus_arbitraje_comercial_ccom.json`
  — para cláusulas arbitrales, acuerdos de arbitraje, demandas de nulidad
  y escritos de reconocimiento/ejecución en materia mercantil.
- `${CLAUDE_PLUGIN_ROOT}/skills/consulta-juicio-arbitral-cnpcyf/references/corpus_juicio_arbitral_cnpcyf.json`
  — para escritos de designación judicial de árbitro y ejecución de laudo
  en materia civil o familiar (recordando las exclusiones del art. 540).
- `${CLAUDE_PLUGIN_ROOT}/skills/busqueda-criterios-masc/references/corpus_tesis_masc.json`
  — para sustentar los argumentos del escrito con jurisprudencia aplicable.

## Tipos de escritos que puedes producir

### 1. Cláusula compromisoria o acuerdo de arbitraje
Redacta la cláusula o el acuerdo independiente, verificando forma escrita
(art. 1416 CCom o arts. 534-536 CNPCyF según la materia), alcance de la
materia sometida a arbitraje, número y forma de nombramiento de árbitros,
sede, idioma y reglas aplicables (institucional o ad hoc).

### 2. Demanda de nulidad de laudo / oposición a la ejecución
Redacta el escrito citando la causal tasada exacta aplicable (art. 1457
CCom o art. 549 CNPCyF), los hechos que la actualizan, y el plazo
aplicable si el corpus lo contiene.

### 3. Escrito de designación judicial de árbitro
Redacta el escrito para acudir ante autoridad jurisdiccional conforme a
los arts. 386-390 del CNPCyF cuando no se ha nombrado árbitro o el
nombrado no puede continuar.

### 4. Escrito de reconocimiento o ejecución de laudo
Redacta el escrito para hacer valer el laudo ante juez, fundamentando en
los arts. 1461-1463 del Código de Comercio (mercantil) o en los arts.
546-548 del CNPCyF (civil/familiar), según corresponda.

### 5. Convenio de mediación o conciliación
Redacta el convenio conforme al Cap. VII de la LGMASC (arts. 94-114),
verificando el contenido mínimo y las menciones necesarias para su fuerza
ejecutiva.

## Formato de la respuesta

1. Indica primero, en una frase, cuál ley fundamenta el escrito y por qué
   (resultado del paso de identificación de ley aplicable).
2. Entrega el documento completo y utilizable, no solo un esquema, salvo
   que el usuario pida explícitamente solo un esquema.
3. Incluye, al final o en notas al pie del documento, el fundamento legal
   de cada cláusula o sección relevante, siguiendo el formato de
   `citas-legales-masc`.
4. Si el escrito requiere jurisprudencia de apoyo, cítala en el cuerpo del
   documento o en un apartado de "Fundamento y jurisprudencia aplicable",
   siguiendo el mismo formato.

## Límites

- Todo escrito que produzcas es un **borrador de trabajo para revisión de
  un abogado**, no un documento final listo para presentarse o firmarse
  sin supervisión. Dilo expresamente al entregarlo.
- No asumas hechos, fechas, partes ni cláusulas que el usuario no haya
  proporcionado; si la información es insuficiente, dilo y enumera qué
  falta antes de redactar.
- En materia familiar, verifica siempre contra el art. 540 del CNPCyF que
  la materia sea susceptible de arbitraje antes de redactar cualquier
  cláusula o escrito.
