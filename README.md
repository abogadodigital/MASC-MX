# MASC MX

Plugin de Claude especializado en mecanismos alternativos de solución de
controversias (MASC) y arbitraje en México. Empaqueta cinco corpus de
datos —tres leyes distintas y su jurisprudencia— junto con trece skills
funcionales para identificar cuál ley aplica a cada caso, consultar el
texto normativo, tramitar y redactar convenios y escritos, evaluar
riesgos de sanción y de nulidad de laudo, buscar jurisprudencia, entrenar
habilidades de negociación y MASC (asesoría estratégica y simulación de
escenarios), generar material docente y un formato de citación unificado
para todo el plugin.

Las skills se activan automáticamente cuando la solicitud del usuario
coincide con su propósito; no requieren invocación explícita.

## Por qué tres leyes, no una

A diferencia de un plugin construido sobre un solo ordenamiento, MASC MX
empaqueta **tres leyes distintas** porque así está organizada la materia
en México: la Ley General de Mecanismos Alternativos de Solución de
Controversias (LGMASC) regula el marco institucional y los MASC no
adjudicativos (negociación, mediación, conciliación); el arbitraje
mercantil se rige por el Código de Comercio; y el arbitraje civil o
familiar, así como la designación judicial de árbitro y la ejecución de
laudos, por el Código Nacional de Procedimientos Civiles y Familiares
(CNPCyF). El propio artículo 4, fracción V, de la LGMASC remite el
arbitraje a estas otras dos leyes. Por eso este plugin incluye una skill
dedicada, `identificacion-ley-aplicable-masc`, cuyo único propósito es
evitar que se crucen fundamentos de leyes distintas — un riesgo real
cuando conviven tres ordenamientos en una misma materia.

## Corpus incluidos

| Archivo | Contenido | Artículos/Registros |
|---|---|---|
| `corpus_lgmasc_marco_institucional.json` | LGMASC, Cap. I-V: naturaleza y objeto, competencia, personas facilitadoras y su certificación, registros y Plataforma Nacional, y las partes | 60 artículos |
| `corpus_lgmasc_operacion_sanciones.json` | LGMASC, Cap. VI-IX: tramitación de los MASC, el convenio, Centros de MASC en el ámbito administrativo, y régimen de responsabilidades y sanciones | 84 artículos |
| `corpus_arbitraje_comercial_ccom.json` | Código de Comercio, Título Cuarto (Del Arbitraje Comercial): acuerdo de arbitraje, tribunal arbitral, sustanciación, laudo, costas, nulidad, reconocimiento y ejecución | 66 artículos (1415-1480) |
| `corpus_juicio_arbitral_cnpcyf.json` | CNPCyF: preparación del juicio arbitral (Sección Tercera) y juicio arbitral civil/familiar, incluida la ejecución de laudos (Título Tercero) | 22 artículos (386-390 y 533-549) |
| `corpus_tesis_masc.json` | Tesis y jurisprudencia de la SCJN y tribunales federales sobre arbitraje y MASC, 13 categorías temáticas (A-M) | 78 criterios |

Los cuatro corpus normativos reflejan el texto vigente de cada ley a la
fecha de corte de este plugin; el corpus jurisprudencial refleja una
investigación con fecha de corte propia (ver `metadata.fecha_investigacion`
dentro de `corpus_tesis_masc.json`). Antes de invocar cualquier
disposición o criterio en un escrito, verificar vigencia en las fuentes
oficiales (https://www.dof.gob.mx,
https://www.diputados.gob.mx/LeyesBiblio/, https://sjf2.scjn.gob.mx).

## Skills incluidas

1. **identificacion-ley-aplicable-masc** — determina cuál de las tres
   leyes (LGMASC, Código de Comercio o CNPCyF) rige los hechos del
   usuario, evitando que el plugin cruce fundamentos de leyes distintas.
   Consúltala primero cuando el encuadre normativo no sea evidente.
2. **consulta-lgmasc-marco-institucional** — texto literal del marco
   institucional de la LGMASC (Cap. I-V).
3. **consulta-arbitraje-comercial-ccom** — texto literal del arbitraje
   comercial (Código de Comercio, Título Cuarto).
4. **consulta-juicio-arbitral-cnpcyf** — texto literal del juicio arbitral
   civil y familiar (CNPCyF).
5. **tramitacion-convenio-masc** — tramitación práctica de negociación,
   mediación y conciliación, y redacción del convenio resultante (LGMASC,
   Cap. VI-VIII).
6. **analisis-riesgos-sanciones-masc** — riesgo de sanción de personas
   facilitadoras y Centros de MASC (LGMASC, Cap. IX), y riesgo de nulidad
   o de denegación de reconocimiento/ejecución de un laudo arbitral
   (Código de Comercio o CNPCyF, según la materia).
7. **redaccion-escritos-masc** — cláusulas arbitrales, demandas de
   nulidad, escritos de designación de árbitro, escritos de
   reconocimiento/ejecución de laudo, y convenios de mediación o
   conciliación.
8. **busqueda-criterios-masc** — localiza y cita los 78 criterios de la
   SCJN y tribunales federales por categoría, artículo o palabra clave.
9. **simulacion-masc** — Claude sostiene el papel de contraparte,
   mediador, conciliador o árbitro en un escenario simulado, para
   practicar habilidades de MASC con retroalimentación estructurada al
   final.
10. **asesoria-estrategica-masc** — consejos tácticos de negociación y
    MASC, distinguiendo siempre entre doctrina general de negociación
    (Harvard, BATNA/MAAN, ZOPA, etc.) y fundamento legal mexicano.
11. **material-docente-masc** — genera resúmenes temáticos, casos
    prácticos, reactivos de examen, flashcards y cuadros comparativos
    para la enseñanza de arbitraje y MASC.
12. **actualizar-corpus-masc** *(opcional, mantenimiento)* — busca tesis
    y reformas posteriores a las fechas de corte, apoyándose en
    herramientas de búsqueda jurídica oficial disponibles en el entorno;
    degrada de forma controlada si no está disponible ninguna.
13. **citas-legales-masc** — define el formato único y obligatorio de
    citación de tesis, jurisprudencia y artículos de las tres leyes que
    usan las demás skills de este plugin, evitando que cada una describa
    su propio formato de forma inconsistente, e identificando siempre de
    cuál de las tres leyes proviene cada cita.

## Instalación

Instala este plugin en Claude Code, Claude Cowork o cualquier entorno
compatible con el estándar de plugins de Claude, apuntando al directorio
de este repositorio, al archivo `.plugin` empaquetado, o al
`.claude-plugin/marketplace.json` incluido.

## Limitaciones

- Los corpus normativos y jurisprudenciales son documentos de trabajo
  generados a partir de una investigación puntual; no sustituyen la
  consulta directa a las fuentes oficiales, particularmente ante reformas
  o criterios posteriores a las fechas de corte indicadas arriba.
- Ninguna skill de este plugin constituye asesoría legal definitiva. Todo
  borrador, dictamen, escrito, convenio o análisis producido requiere
  revisión de un abogado antes de usarse con consecuencias legales.
- La skill `actualizar-corpus-masc` tiene un nivel de verificación
  distinto al resto del plugin, porque no opera contra un corpus
  empaquetado fijo, sino contra búsqueda en vivo cuando el entorno lo
  permite.
- La doctrina general de negociación que usa `asesoria-estrategica-masc`
  no proviene de un corpus verificado (a diferencia del resto del
  plugin); se distingue expresamente del fundamento legal mexicano en
  cada respuesta.

## Autoría

**Joel A. Gómez Treviño**

## Licencia

CC BY-NC-SA 4.0 (con condiciones adicionales de uso no comercial) — ver `LICENSE.md`.
