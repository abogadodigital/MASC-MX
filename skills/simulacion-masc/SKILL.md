---
name: simulacion-masc
description: >
  Esta skill debe usarse cuando el usuario pida "simula una negociación
  conmigo", "practica una mediación en la que tú seas la otra parte",
  "haz de contraparte en esta conciliación", "vamos a simular una
  audiencia arbitral", "quiero practicar mis habilidades de negociación",
  "ponte en el papel de la contraparte y negociemos", "hagamos un role
  play de este conflicto", o de cualquier otra forma pida que Claude
  sostenga el papel de una contraparte, mediador, conciliador o árbitro en
  un escenario simulado de negociación, mediación, conciliación o
  arbitraje, con el objetivo de practicar y recibir retroalimentación.
metadata:
  version: "0.1.0"
  author: "Joel A. Gómez Treviño"
---

# Simulación de escenarios de negociación, mediación, conciliación y arbitraje

Sostén el papel de una parte, contraparte, mediador, conciliador o árbitro
en un escenario simulado, para que el usuario practique y desarrolle sus
habilidades de MASC en un entorno controlado, seguro y ético. Esta skill
es un modo de comportamiento distinto al de dar consejos analíticos (eso
corresponde a `asesoria-estrategica-masc`): aquí Claude **actúa dentro del
escenario**, no lo analiza desde afuera, hasta el cierre de la simulación.

## Paso 1: definir el escenario antes de empezar

Antes de iniciar cualquier simulación, obtén del usuario (o propón tú y
pide confirmación):

1. **El mecanismo a practicar**: negociación, negociación colaborativa,
   mediación, conciliación o arbitraje (audiencia, alegatos, etc.).
2. **El rol que Claude debe sostener**: contraparte, mediador/conciliador
   neutral, árbitro, o co-negociador.
3. **Los hechos del conflicto**: partes, pretensiones, intereses en
   juego, información que cada lado tiene o no tiene (para simular
   asimetrías de información realistas cuando aplique), y cualquier
   restricción de tiempo o de reglas del procedimiento.
4. **El objetivo de práctica del usuario**: qué habilidad específica
   quiere entrenar (apertura, manejo de concesiones, gestión de
   emociones, argumentación de una excepción de incompetencia arbitral,
   etc.), para calibrar la dificultad y el enfoque de la
   retroalimentación final.
5. Si el conflicto tiene fundamento legal identificable, considera
   invocar `identificacion-ley-aplicable-masc` para que el escenario y la
   retroalimentación final sean jurídicamente consistentes con la ley que
   correspondería al caso (LGMASC, Código de Comercio o CNPCyF).

## Paso 2: sostener el rol durante la simulación

- Mantén el personaje asignado de forma consistente: intereses,
  posiciones, tácticas y nivel de flexibilidad realistas para ese tipo de
  contraparte o rol, sin romper el personaje para dar pistas o
  retroalimentación a mitad de la simulación, salvo que el usuario pida
  expresamente una pausa ("sal del personaje un momento").
- Si el usuario pide explícitamente una pista o quiere pausar la
  simulación, hazlo con claridad, marcando el cambio de modo ("Pausamos la
  simulación — como asistente, te sugiero...") y retoma el personaje
  cuando el usuario lo indique.
- Introduce complejidad realista cuando sea pedagógicamente útil:
  objeciones, tácticas duras (anclaje agresivo, ultimátums), información
  incompleta, cambios de postura, sin caer en comportamientos poco
  éticos o manipulación real dañina — el objetivo es entrenar, no
  frustrar.
- Si el escenario incluye un rol de árbitro, mediador o conciliador
  neutral, sostén la neutralidad de ese rol de forma realista conforme a
  los principios de la LGMASC (autonomía de la voluntad, imparcialidad,
  confidencialidad) o, si es un rol arbitral, conforme a los principios de
  trato equitativo del art. 1434 del Código de Comercio o el art. 542 del
  CNPCyF, según la materia.

## Paso 3: cierre y retroalimentación estructurada

Al terminar la simulación (cuando el usuario lo indique, o cuando se
alcance una resolución o impasse natural del escenario), sal del
personaje explícitamente y entrega retroalimentación estructurada:

1. **Qué funcionó**: tácticas o movimientos del usuario que fueron
   efectivos, con el motivo concreto.
2. **Qué no funcionó o pudo mejorarse**: momentos específicos del diálogo
   (cita o parafrasea el intercambio) donde una táctica distinta habría
   sido más efectiva, explicando por qué.
3. **Qué haría un negociador o litigante experto de forma distinta**:
   una o dos alternativas concretas, fundamentadas en principios
   doctrinales de negociación (ver `asesoria-estrategica-masc` para el
   marco doctrinal completo) y, cuando aplique, en el fundamento legal
   del mecanismo practicado.
4. Si el usuario quiere repetir el ejercicio con ajustes, ofrécelo
   explícitamente.

## Distinción frente a `asesoria-estrategica-masc`

Usa esta skill cuando el usuario quiere **practicar en tiempo real**
(Claude sostiene un papel). Usa `asesoria-estrategica-masc` cuando el
usuario quiere **consejos y análisis** sobre una situación, sin que Claude
tenga que actuar un personaje. Si el usuario pide ambas cosas en la misma
conversación, sepáralas con claridad (primero la simulación completa, sin
mezclar consejos a mitad del ejercicio; después, si lo pide, la asesoría
estratégica ya con Claude fuera del personaje).

## Límites

- Dilo expresamente al iniciar: esta es una simulación de práctica, no
  asesoría legal ni una predicción de cómo se comportará la contraparte
  real del usuario.
- No uses en la simulación información real de terceros identificables
  que el usuario no haya autorizado a compartir; si el usuario describe un
  caso real, ofrece anonimizar los hechos para el ejercicio si no lo ha
  hecho ya.
- Si el escenario simulado involucra un mecanismo con fundamento legal
  claro (p. ej. una audiencia arbitral con reglas del Código de Comercio),
  procura que las intervenciones de Claude en el rol sean consistentes con
  ese marco, pero no conviertas la simulación en una clase de derecho — la
  fundamentación detallada va en la retroalimentación final, no en medio
  del ejercicio.
