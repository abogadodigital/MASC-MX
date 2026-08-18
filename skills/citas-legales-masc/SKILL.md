---
name: citas-legales-masc
description: >
  Esta skill define el formato obligatorio para citar tesis, jurisprudencia y
  artículos de la LGMASC, el Código de Comercio (Título Cuarto, Del Arbitraje
  Comercial) y el Código Nacional de Procedimientos Civiles y Familiares
  (Sección Tercera y Título Tercero) en cualquier respuesta de este plugin.
  Las demás skills de este plugin (identificacion-ley-aplicable-masc,
  consulta-lgmasc-marco-institucional, consulta-arbitraje-comercial-ccom,
  consulta-juicio-arbitral-cnpcyf, tramitacion-convenio-masc,
  analisis-riesgos-sanciones-masc, redaccion-escritos-masc,
  busqueda-criterios-masc, material-docente-masc) deben consultarla cada vez
  que citen un criterio jurisprudencial o un artículo de alguna de las tres
  leyes, en vez de describir su propio formato. También úsala cuando el
  usuario pregunte directamente "cómo citas la jurisprudencia", "cuál es el
  formato de citas de este plugin" o equivalente.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Formato de citación

Todas las demás skills de este plugin que citen jurisprudencia, tesis o
artículos de la LGMASC, el Código de Comercio o el Código Nacional de
Procedimientos Civiles y Familiares (CNPCyF) deben seguir exactamente las
reglas de este documento. Ninguna otra skill debe describir su propio
formato de citación en prosa ni inventar variantes: solo debe remitir aquí
(`${CLAUDE_PLUGIN_ROOT}/skills/citas-legales-masc/SKILL.md`).

## 1. Citación de jurisprudencia y tesis

### 1.1 Cuántos resultados dicta qué formato

- **1 a 4 criterios** → formato completo (sección 1.2). Es obligatorio
  siempre que la consulta arroje entre 1 y 4 resultados, sin excepción —
  nunca lo sustituyas por el formato abreviado solo porque el contenido
  del registro es extenso.
- **5 o más criterios** → formato abreviado (sección 1.3).

### 1.2 Formato completo (1 a 4 criterios)

Para cada criterio, en este orden, cada etiqueta en su propia línea, sin
fusionar dos etiquetas en un mismo renglón:

```
[TÍTULO COMPLETO DE LA TESIS O JURISPRUDENCIA, el `rubro` tal cual del corpus]
Autoridad emisora: [autoridad_emisora] (Ejemplo: Primera Sala de la Suprema Corte de Justicia de la Nación)
Tipo y época: [tipo_y_epoca] (Ejemplo: Tesis Aislada, Undécima Época)
Fecha: [fecha]
Registro digital: [registro_digital]
Enlace: [enlace] (Ejemplo: https://sjf2.scjn.gob.mx/detalle/tesis/2022901)
Resumen: [redacta un texto breve que resuma el criterio, apoyándote en el campo `resumen` del corpus]

- Contenido de la tesis -
Hechos: [copia los hechos en su totalidad, si el registro los tiene]
Criterio jurídico: [copia el criterio jurídico en su totalidad, si el registro lo tiene]
Justificación: [copia la justificación en su totalidad, si el registro la tiene]
```

Si el registro del corpus no tiene la estructura Hechos/Criterio
jurídico/Justificación sino un campo `texto_integro` (tesis de estructura
tradicional en bloque único, propia de la Novena Época y de precedentes
históricos), sustituye el bloque "- Contenido de la tesis -" por el
`texto_integro` completo, sin parafrasear ni resumir la regla legal
operativa.

No omitas ninguna etiqueta (Autoridad emisora, Tipo y época, Fecha,
Registro digital, Enlace, Resumen) aunque el dato parezca obvio por el
contexto. Nunca uses etiquetas distintas a las de esta plantilla.

### 1.3 Formato abreviado (5 o más criterios)

Numera cada criterio por orden de aparición y usa las mismas etiquetas de
la sección 1.2, sin el bloque de "Contenido de la tesis":

```
[N]. [TÍTULO COMPLETO DE LA TESIS O JURISPRUDENCIA]
Autoridad emisora: [autoridad_emisora]
Tipo y época: [tipo_y_epoca]
Fecha: [fecha]
Registro digital: [registro_digital]
Enlace: [enlace]
Resumen: [el campo `resumen` del corpus, sin parafrasear]
```

No incluyas `hechos`/`criterio_juridico`/`justificacion`/`texto_integro` en
esta lista abreviada. Al final de la lista, pregunta al usuario si quiere
conocer el contenido completo de alguna tesis, pidiéndole que la identifique
**por orden de aparición** ("¿quieres que te muestre el contenido de la
primera, la segunda, la tercera...?"), no por número de registro digital.
Cuando el usuario responda, entrega ese criterio en el formato completo de
la sección 1.2.

### 1.4 Excepción expresa

Si el usuario pide explícitamente solo el título y el enlace (p. ej. "solo
dame los títulos y el link"), respeta esa instrucción y omite el resto de
las etiquetas, sin perder el título ni el enlace oficial.

## 2. Citación de artículos de la LGMASC, el Código de Comercio o el CNPCyF

Cada vez que cites un artículo de cualquiera de las tres leyes empaquetadas
en este plugin, usa este formato, identificando siempre la ley de origen:

```
Artículo [número] (LGMASC): [texto completo del artículo, incluyendo todos sus párrafos, fracciones e incisos]
Artículo [número] (Código de Comercio, Título Cuarto - Del Arbitraje Comercial): [texto completo]
Artículo [número] (CNPCyF): [texto completo]
```

Nunca cites solo el número de artículo sin su texto completo, ni
parafrasees el texto legal — reprodúcelo tal cual aparece en el campo
`texto_completo` del corpus normativo correspondiente
(`corpus_lgmasc_marco_institucional.json`,
`corpus_lgmasc_operacion_sanciones.json`,
`corpus_arbitraje_comercial_ccom.json` o
`corpus_juicio_arbitral_cnpcyf.json`, según el artículo).

## 3. Identificar siempre la ley de origen (regla propia de este plugin)

A diferencia de un plugin de una sola ley, este plugin empaqueta **tres
ordenamientos distintos** (LGMASC, Código de Comercio y CNPCyF). Cada vez
que cites un artículo, es obligatorio dejar explícito de cuál de las tres
proviene, tal como se muestra en los ejemplos de la sección 2 — nunca cites
"el artículo [número]" a secas cuando exista más de una ley en juego, para
no inducir al usuario a confundir el fundamento de una ley con el de otra.
Si tienes dudas sobre cuál de las tres leyes aplica al caso del usuario,
usa primero `identificacion-ley-aplicable-masc`.

## 4. Fuente de la cita: el corpus empaquetado

Cada criterio y cada artículo que cites proviene del corpus integrado con
este plugin, curado a partir de fuentes oficiales (DOF y SJF2). Al citar,
la fuente que reportas al usuario es siempre ese corpus y, en el caso de
jurisprudencia, el `enlace` oficial de verificación que trae cada registro
— esa es la referencia correcta y suficiente.

Todas las skills de este plugin que citan jurisprudencia o texto legal
trabajan contra este corpus ya integrado. La única excepción es
`actualizar-corpus-masc`, que puede apoyarse en conectores de búsqueda
jurídica disponibles en el entorno, pero solo cuando el usuario se lo pida
expresamente, y únicamente para proponer altas nuevas al corpus, no para
responder una consulta normal.

## 5. Regla general

Ninguna otra skill de este plugin debe reimplementar ni parafrasear estas
reglas: deben remitir a este documento para el formato exacto de citación,
tanto de jurisprudencia como de artículos de la LGMASC, el Código de
Comercio o el CNPCyF.
