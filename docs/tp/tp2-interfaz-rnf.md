---
title: TP2 — Interfaz de Usuario y Requerimientos No Funcionales
nav_order: 2
---

# Ingeniería del Software - 2026 - TP 2

## Interfaz de Usuario y Requerimientos No Funcionales

---

## 1. Objetivos de aprendizaje

Al finalizar este trabajo práctico, el grupo deberá ser capaz de:

- Reconocer los atributos de calidad de un sistema de software y determinar cuáles resultan más influyentes o de mayor impacto para el proyecto que están desarrollando, y seleccionar los cinco más críticos.
- Redactar escenarios de atributo de calidad completos, con estímulo, fuente del estímulo, artefacto, entorno, respuesta y medida de la respuesta.
- Priorizar escenarios que ocurran en condiciones degradadas o significativas para el tipo de sistema modelado, por sobre escenarios de comportamiento normal.
- Elaborar perfiles de usuario a partir de los actores identificados en el TP1 y utilizarlos como base para el diseño de la interfaz, aplicando los principios del diseño centrado en el usuario.
- Aplicar las diez heurísticas de usabilidad de Nielsen sobre interfaces de usuario concretas.
- Utilizar inteligencia artificial como herramienta de apoyo para la elaboración y la evaluación crítica de artefactos de requerimientos y de diseño, ejerciendo en todo momento el criterio propio del equipo por sobre la respuesta literal de la IA.
- Documentar el proceso de iteración con IA de forma trazable: qué se pidió, qué se obtuvo, qué se aceptó, qué se rechazó y por qué.

---

## 2. Modalidad de trabajo

Este TP es continuación directa del proyecto que cada grupo viene desarrollando desde el TP1. No se cambia de proyecto ni de alcance definido: se profundiza sobre él.

El trabajo se organiza en dos partes independientes entre sí en cuanto a contenido, pero ambas obligatorias:

- Parte A: Escenarios de atributo de calidad.
- Parte B: Interfaz de usuario mediante generación y evaluación crítica asistida por IA.

Ambas partes deben quedar documentadas en el repositorio del grupo, respetando la estructura de carpetas indicada en la sección 5 de esta guía.

---

## 3. Parte A: Escenarios de atributo de calidad

### 3.1 Consigna

El grupo elige cinco atributos de calidad para su proyecto: los que considere más críticos, es decir, los que más le exigen a la solución que está desarrollando. Los atributos pueden tomarse de la norma ISO/IEC 25010:2023, cuya taxonomía se ofrece como referencia en el Anexo A, o de cualquier otra taxonomía de calidad. En ese caso, el grupo indica cuál utilizó y qué significa el atributo elegido.

Para cada uno de los cinco atributos:

- Define entre uno y tres escenarios de atributo de calidad.
- Si el atributo proviene de la norma ISO/IEC 25010:2023, cada escenario indica la subcaracterística que pone a prueba. Con dos escenarios en una misma característica, el grupo puede elegir ambos para la misma subcaracterística o uno para cada una de dos subcaracterísticas distintas. Con tres escenarios rige el mismo criterio.
- Los escenarios deben priorizar el impacto potencial sobre decisiones de diseño del sistema, por sobre la cantidad.
- Los escenarios deben ubicarse mayoritariamente en entornos degradados o en condiciones que resulten significativas para el tipo de sistema que el grupo está modelando, y no en el camino normal de uso, es decir, aquel en el que el sistema se comporta simplemente como se espera que lo haga.

Un entorno degradado o condición significativa es aquel en el que el sistema opera bajo una circunstancia adversa, límite o excepcional para ese atributo. Por ejemplo, para seguridad, un escenario en camino normal sería un usuario que inicia sesión correctamente; un escenario en entorno degradado sería un intento de acceso mediante múltiples solicitudes de login simultáneas desde distintas direcciones IP, simulando un ataque automatizado.

### 3.2 Estructura del escenario

Cada escenario de atributo de calidad debe identificar el atributo al que corresponde (y su subcaracterística, si proviene de ISO/IEC 25010:2023), y documentarse con los siguientes seis componentes:

- Estímulo: la condición que dispara el escenario.
- Fuente del estímulo: quién o qué genera esa condición.
- Artefacto: qué parte del sistema es estimulada.
- Entorno: bajo qué condiciones ocurre, normal o degradada.
- Respuesta: qué debería hacer el sistema ante el estímulo.
- Medida de la respuesta: cómo se verifica o cuantifica que la respuesta fue adecuada.

### 3.3 Justificación de la selección y de la criticidad

El grupo explica por qué eligió esos cinco atributos y no otros: qué le exige cada uno a la solución que está desarrollando y por qué resulta más crítico que los atributos que quedaron afuera. Para cada escenario, explica además por qué es crítico o significativo para el sistema que está modelando.

Si además el grupo puede fundamentar qué impacto tendría el escenario sobre la arquitectura del sistema, por ejemplo sobre su estructura o sobre las decisiones de diseño que condiciona, puede incluirlo. Esta fundamentación es opcional en esta instancia. Los escenarios quedan como insumo para las decisiones de arquitectura del proyecto.

### 3.4 Dónde documentarlo

Se recomienda documentar los escenarios de atributo de calidad junto al SRS, dado que son en esencia requerimientos no funcionales que nacen del mismo proceso de elicitación que las historias de usuario. En la práctica, por su relación con las decisiones que condicionan, también pueden ubicarse como activo de arquitectura. Lo importante es que el grupo elija una ubicación, la mantenga, y deje clara la trazabilidad hacia el SRS. Ver sección 5 para la ruta recomendada dentro del repositorio.

---

## 4. Parte B: Interfaz de usuario asistida por IA

### 4.1 Punto de partida

Se maquetan únicamente las interfaces correspondientes a las historias de usuario desarrolladas en el TP1, en el marco de los casos de uso 2.0. Si alguna de esas historias no requiere interfaz, se indica y no se maqueta. No se agregan historias nuevas ni pantallas que no estén respaldadas por una historia del TP1.

Todo el análisis de esta parte se realiza exclusivamente con la información ya producida en el TP1: los actores, los casos de uso, las historias de usuario y el SRS. No se incorpora información nueva de usuarios en esta instancia.

### 4.2 Diseño centrado en el usuario

Antes de solicitar cualquier maquetado, el grupo debe comprender para quién está diseñando. Para cada actor principal identificado en el TP1, el grupo elabora:

- **Perfil de usuario:** quién es, qué objetivo persigue con el sistema, en qué contexto lo utiliza (lugar, dispositivo, urgencia), qué nivel de conocimiento técnico tiene y qué limitaciones o frustraciones pueden condicionar su uso.
- **Escenario de uso:** una narración breve de cómo ese usuario completa una tarea concreta, tomada de una de sus historias de usuario del TP1.
- **Flujo de navegación:** las pantallas por las que ese usuario pasa para completar la tarea. Este flujo define qué pantallas se maquetan.

Los perfiles deben apoyarse en lo que el TP1 ya establece sobre cada actor. Si el grupo utiliza IA para asistir en su redacción, debe proporcionarle los documentos del TP1 como fuente y verificar que el resultado no incorpore atributos inventados ni estereotipados. Todo lo que el perfil afirme del usuario debe poder rastrearse a algo del TP1 o quedar declarado explícitamente como supuesto del grupo.

### 4.3 Primer ciclo: generación del maquetado

El grupo define previamente, antes de recurrir a la IA, los criterios que va a utilizar para pedir la generación de cada pantalla: tipo de sistema, lenguaje o framework a utilizar, el perfil de usuario y el escenario de uso correspondientes, y cualquier otro criterio que consideren relevante para su proyecto.

Con esos criterios definidos, el grupo solicita a la IA la generación del maquetado en HTML de la interfaz correspondiente a cada pantalla del flujo de navegación.

### 4.4 Segundo ciclo: evaluación crítica

El grupo toma el HTML generado y se lo entrega a la IA en una nueva interacción, indicándole que asuma el rol de especialista en interfaz de usuario. Se le solicita que evalúe la pantalla heurística por heurística, según las diez heurísticas de usabilidad de Nielsen, teniendo en cuenta el perfil de usuario y el escenario de uso definidos, y no un usuario genérico. Para cada heurística debe señalar si se cumple, si se cumple parcialmente o si se incumple, y por qué.

Esta evaluación debe quedar documentada como un artefacto por pantalla.

### 4.5 Revisión crítica del grupo

El grupo debe revisar cada hallazgo devuelto por la IA en el paso anterior y, para cada uno, decidir si lo acepta o lo rechaza, documentando el motivo de esa decisión. Esta revisión es el núcleo pedagógico de la actividad: la IA identifica posibles problemas, pero el criterio sobre su validez y aplicabilidad al usuario y al proyecto concretos es responsabilidad exclusiva del grupo.

### 4.6 Ciclos adicionales

Si producto de la revisión crítica el grupo decide ajustar la interfaz, puede volver a interactuar con la IA tantas veces como sea necesario, hasta arribar a una versión de la interfaz que consideren razonablemente usable. Cada ciclo adicional debe quedar igualmente documentado.

### 4.7 Qué debe quedar documentado como mínimo

Para cada pantalla trabajada, el documento de evaluación heurística debe incluir, como mínimo:

- El prompt utilizado para solicitar la generación del HTML y la respuesta obtenida de la IA.
- El prompt utilizado para solicitar la evaluación heurística y la respuesta completa de la IA, con sus hallazgos.
- La justificación del grupo para cada hallazgo aceptado o rechazado.
- El registro de los ciclos adicionales de ajuste, si los hubo, con el mismo nivel de detalle.

Además, el grupo documenta por separado los perfiles de usuario, los escenarios de uso y los flujos de navegación definidos en la sección 4.2.

---

## 5. Estructura de entregables en el repositorio

Dentro de la estructura de repositorio ya definida para el proyecto, este TP incorpora las siguientes rutas:

Escenarios de atributo de calidad:

- docs/requirements/quality-scenarios/ — ubicación recomendada (ver sección 3.4). Un documento Markdown por atributo de calidad, o un documento único que agrupe los cinco atributos, a criterio del grupo, siempre que la trazabilidad quede clara.

Interfaz de usuario:

- docs/ui/user-profiles/ — un documento Markdown por perfil de usuario, con su escenario de uso y su flujo de navegación (sección 4.2).
- docs/ui/mockups/ — los archivos HTML generados en el primer ciclo, uno por pantalla, con nombres de archivo que permitan identificar a qué historia de usuario corresponden.
- docs/ui/heuristic-review/ — un documento Markdown por pantalla, conteniendo la totalidad de lo indicado en la sección 4.7: prompts, respuestas de la IA, justificación del grupo, y ciclos adicionales si los hubo.

Se espera que los nombres de archivo dentro de cada carpeta permitan identificar de forma directa a qué historia de usuario o caso de uso corresponde cada artefacto.

---

## 6. Uso de IA

El uso de inteligencia artificial está permitido y forma parte de la consigna en ambas partes del TP. En la Parte A puede asistir en la identificación de atributos y en la redacción y el refinamiento de escenarios. En la Parte B es parte explícita de los ciclos de generación y de evaluación.

En ambas partes el grupo documenta con transparencia cada interacción: qué solicitó, qué obtuvo, qué aceptó, modificó o descartó, y por qué. En ningún caso adopta una recomendación o un resultado de la IA sin ejercer su propio criterio. El detalle mínimo de la Parte B está en la sección 4.7. En la Parte A, el registro se guarda junto a los escenarios.

---

## 7. Checklist de entregables

- [ ] Cinco atributos de calidad seleccionados y justificados, con la taxonomía utilizada indicada.
- [ ] Uno a tres escenarios por atributo, con la subcaracterística indicada en cada uno cuando el atributo proviene de ISO/IEC 25010:2023.
- [ ] Escenarios priorizados por impacto potencial y mayoritariamente en entornos degradados o condiciones significativas para el sistema.
- [ ] Cada escenario con sus seis componentes completos: estímulo, fuente, artefacto, entorno, respuesta y medida de la respuesta.
- [ ] Justificación de criticidad de cada escenario, sin referencia a decisiones arquitectónicas.
- [ ] Perfil de usuario, escenario de uso y flujo de navegación para cada actor principal, elaborados a partir de la información del TP1.
- [ ] Maquetado HTML generado para cada pantalla correspondiente a las historias de usuario del TP1 que requieren interfaz.
- [ ] Documento de evaluación heurística por pantalla, con prompts, respuestas de la IA, justificación del grupo y ciclos adicionales documentados.
- [ ] Registro del uso de IA en ambas partes, según la sección 6.
- [ ] Todo el material ubicado en las rutas indicadas en la sección 5.

---

## 8. Instancia de defensa

En la instancia de defensa de este TP se podrá solicitar al grupo que:

- Justifique oralmente por qué priorizó determinados atributos de calidad por sobre otros.
- Explique la diferencia entre un escenario en camino normal y uno en entorno degradado, con un ejemplo propio de su proyecto.
- Explique cómo el perfil de usuario condicionó las decisiones de diseño de al menos una pantalla.
- Muestre al menos un caso en el que hayan rechazado un hallazgo de la evaluación heurística de la IA, y argumente por qué.
- Describa cómo llegaron de la primera versión del maquetado a la versión final, si hubo ciclos adicionales de ajuste.

---

## 9. Checklist final

- [ ] Repositorio actualizado con commits que reflejen el avance de este TP.
- [ ] Estructura de carpetas respetada según la sección 5.
- [ ] Documentación en Markdown, sin herramientas externas al repositorio.
- [ ] Grupo en condiciones de defender oralmente cada decisión tomada.

---

## Anexo A. Taxonomía de referencia de atributos de calidad (ISO/IEC 25010:2023)

### Versión utilizada

Este anexo se ofrece como referencia y vocabulario común. El grupo puede elegir sus cinco atributos de esta taxonomía o de cualquier otra.

Este TP utiliza el modelo de calidad del producto de la norma **ISO/IEC 25010:2023**, *Systems and software engineering — Systems and software Quality Requirements and Evaluation (SQuaRE) — Product quality model* (segunda edición, noviembre de 2023). Esta edición reemplaza a ISO/IEC 25010:2011.

Buena parte del material académico y comercial todavía usa los nombres de la edición 2011. Las diferencias principales son:

- **Usabilidad** pasó a llamarse **Capacidad de interacción**.
- **Portabilidad** pasó a llamarse **Flexibilidad**.
- **Seguridad física (Safety)** se agregó como característica nueva. No se incluye en el listado de este anexo.
- Se agregaron las subcaracterísticas *inclusividad*, *autodescriptividad*, *resistencia* y *escalabilidad*.
- *Estética de la interfaz* y *madurez* se reemplazaron por *compromiso del usuario* y *ausencia de fallos*.
- *Accesibilidad* se dividió en *inclusividad* y *asistencia al usuario*.

El modelo de calidad en uso, que en la edición 2011 estaba en la misma norma, se trasladó a ISO/IEC 25019:2023. Este anexo se limita al modelo de calidad del producto y lista ocho de sus nueve características: no incluye *Seguridad física (Safety)*. No debe confundirse con *Seguridad de la información (Security)*, que sí está listada. Las definiciones de este anexo están redactadas en lenguaje de la cátedra a modo de vocabulario de trabajo. El texto normativo es el de la norma.

### Las ocho características

**1. Adecuación funcional (Functional suitability).** El sistema ofrece las funciones que las personas necesitan, y las ofrece bien.

- *Completitud funcional:* las funciones cubren todas las tareas y objetivos previstos.
- *Corrección funcional:* las funciones producen resultados correctos y con la precisión necesaria.
- *Pertinencia funcional:* las funciones ayudan a cumplir las tareas sin pasos innecesarios.

**2. Eficiencia de desempeño (Performance efficiency).** Qué tan bien responde el sistema en relación con los recursos que consume.

- *Comportamiento temporal:* tiempos de respuesta, de procesamiento y tasas de rendimiento.
- *Utilización de recursos:* cantidad y tipo de recursos que usa (CPU, memoria, almacenamiento, red).
- *Capacidad:* límites máximos que soporta (usuarios simultáneos, volumen de datos, transacciones).

**3. Compatibilidad (Compatibility).** El sistema convive e intercambia información con otros sistemas.

- *Coexistencia:* funciona junto a otros sistemas en el mismo entorno sin afectarlos ni ser afectado.
- *Interoperabilidad:* intercambia información con otros sistemas y la usa correctamente.

**4. Capacidad de interacción (Interaction capability).** Qué tan bien las personas pueden usar el sistema para lograr sus objetivos. Antes llamada *usabilidad*.

- *Reconocibilidad de la adecuación:* el usuario reconoce si el sistema le sirve para su necesidad.
- *Capacidad de aprendizaje:* el usuario aprende a usarlo con esfuerzo razonable.
- *Operabilidad:* el sistema es fácil de operar y controlar.
- *Protección frente a errores del usuario:* el sistema previene, detecta y ayuda a corregir los errores del usuario.
- *Compromiso del usuario:* la interacción es motivadora y mantiene el interés.
- *Inclusividad:* el sistema puede ser usado por personas con distintas capacidades, contextos y características.
- *Asistencia al usuario:* el sistema ofrece ayuda para completar las tareas cuando el usuario la necesita.
- *Autodescriptividad:* el sistema explica por sí mismo qué hace, qué está pasando y qué se espera del usuario.

**5. Fiabilidad (Reliability).** El sistema funciona de manera consistente y sostenida a lo largo del tiempo.

- *Ausencia de fallos:* en operación normal, el sistema falla poco.
- *Disponibilidad:* el sistema está operativo y accesible cuando se lo necesita.
- *Tolerancia a fallos:* sigue funcionando, quizá degradado, ante fallos de hardware o software.
- *Capacidad de recuperación:* se recupera de una falla, restablece el servicio y restaura los datos afectados.

**6. Seguridad de la información (Security).** El sistema protege la información y los recursos frente a accesos y usos indebidos.

- *Confidencialidad:* los datos son accesibles solo para quienes están autorizados.
- *Integridad:* se impide la modificación no autorizada de datos y del sistema.
- *No repudio:* se puede demostrar que una acción o evento ocurrió, sin que pueda negarse.
- *Responsabilidad (accountability):* las acciones de cada entidad pueden rastrearse hasta ella.
- *Autenticidad:* se puede comprobar que un sujeto o recurso es quien dice ser.
- *Resistencia:* el sistema sigue operando y protege su función durante un ataque, y se recupera después.

**7. Mantenibilidad (Maintainability).** Qué tan fácil es mejorar, corregir o adaptar el sistema.

- *Modularidad:* los componentes están separados de modo que cambiar uno afecta poco a los demás.
- *Reusabilidad:* los componentes pueden usarse en otros sistemas o contextos.
- *Analizabilidad:* se puede evaluar el impacto de un cambio y diagnosticar fallas o causas.
- *Modificabilidad:* se puede modificar sin introducir defectos ni degradar la calidad.
- *Capacidad de prueba (testability):* se pueden definir criterios de prueba y ejecutarlas de forma efectiva.

**8. Flexibilidad (Flexibility).** Qué tan bien el sistema se adapta a cambios de contexto, entorno o necesidad. Antes llamada *portabilidad*.

- *Adaptabilidad:* se adapta a otros entornos o contextos de uso sin cambios mayores.
- *Escalabilidad:* crece o decrece su capacidad ante variaciones de carga o necesidad.
- *Instalabilidad:* se instala, desinstala y actualiza con facilidad en el entorno previsto.
- *Reemplazabilidad:* puede sustituir a otro sistema para el mismo propósito o ser sustituido.
