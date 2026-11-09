---
title: TP4 — Diseño Detallado, Implementación y Testing Unitario
nav_order: 4
---

# Ingeniería del Software - 2026 - TP 4

## Diseño Detallado, Implementación y Testing Unitario — Consigna

> **Cómo se organiza este TP.** Este documento es la **consigna**: qué hay que hacer, qué hay que entregar y cómo se verifica cada entrega. Los conceptos, las reglas y las explicaciones están en la [Guía de referencia del TP4](tp4-guia-de-referencia.md), y un caso resuelto de punta a punta está en el [Ejemplo resuelto del TP4](ejemplo-resuelto-tp4.md). En cada paso, el recuadro **Para profundizar** indica qué parte de esos documentos conviene leer. La forma de trabajar es con los tres a mano: la consigna dice *qué* hacer, la referencia explica *cómo y por qué*, y el ejemplo muestra *cómo se ve*.

---

## 1. Objetivos de aprendizaje

Al finalizar este trabajo práctico, el grupo deberá ser capaz de:

- Pasar de la arquitectura (TP3) al diseño detallado, tomando una historia de usuario (HU) como unidad de trabajo.
- Analizar la HU elegida en sus tres dimensiones: **funcionalidad** (qué hace), **estructura** (qué elementos la componen) y **calidad** (qué propiedades debe cumplir).
- Construir, para esa HU, un diagrama de **robustez**, diagramas de **secuencia** (uno por camino) y un **modelo de clases**, de modo que cada uno se derive del anterior.
- Aplicar los criterios GRASP (asignación de responsabilidades) para justificar qué clase hace cada cosa y cómo se relacionan las clases.
- Implementar las clases e interfaces diseñadas en el lenguaje elegido por el grupo, con una interfaz gráfica mínima que permita mostrar el flujo de la HU funcionando.
- Diseñar casos de prueba de caja negra y de caja blanca a partir de los criterios de aceptación y del código, y automatizarlos con un framework de pruebas (por ejemplo, pytest).
- Medir la cobertura de las pruebas e interpretar el reporte.
- Mantener la trazabilidad entre HU, componente del modelo C4, diagramas de diseño, clases, código y pruebas.
- Utilizar inteligencia artificial (IA) como apoyo para diseñar, programar y probar, ejerciendo el criterio propio del equipo y documentando el proceso.

---

## 2. Organización del trabajo

Este TP es continuación directa del proyecto desarrollado en el TP1, el TP2 y el TP3. No se cambia de proyecto ni de alcance.

El grupo elige **una historia de usuario** de su proyecto y hace con ella el trabajo completo: análisis, diseño, implementación y pruebas. Es preferible una HU trabajada de punta a punta que varias a medias.

El trabajo se organiza en tres partes que se retroalimentan, todas obligatorias:

- **Parte A:** diseño detallado de la HU.
- **Parte B:** implementación.
- **Parte C:** pruebas unitarias.

| Fecha | Actividad en clase |
|---|---|
| 02/11 | Inicio. Diseño dirigido por HU: análisis tridimensional, diagrama de robustez, diagrama de secuencia (Parte A) |
| 10/11 | Primera implementación de clases e interfaces. Diseño de casos de prueba. Pruebas de software, técnicas y pytest (Partes B y C) |
| 16/11 | Cierre. Implementación de las pruebas, ejecución y reporte de cobertura |
| 23/11 | No hay práctica |
| 24/11 | Instancia 4: presentación del diseño detallado, la implementación y las pruebas |

**Lenguaje y herramientas.** La implementación y las pruebas se hacen en el **lenguaje que el grupo elija** (en general, el mismo del proyecto o el que mejor conozca el equipo), con el framework de pruebas de ese lenguaje. En clase se usa pytest como ejemplo de herramienta; JUnit, Jest, xUnit u otros sirven igual. En este TP se evalúa el diseño y su verificación, no la tecnología. Los diagramas se escriben en Mermaid dentro de archivos Markdown, igual que en el TP3.

**Trabajo en el repositorio.** Se recomienda trabajar en una rama del repositorio e integrar mediante Pull Request con revisión cruzada del grupo, según el instructivo de Git y GitHub.

---

## 3. Elección de la HU

La HU tiene que sostener el análisis de las tres dimensiones (funcionalidad, estructura y calidad). Para eso debe cumplir estas condiciones, que se comprueban con lo que el grupo ya entregó en los TP anteriores:

| Condición | Cómo se comprueba |
|---|---|
| Está asociada a **al menos un escenario de calidad** (`EC-xx`) | Figura en la tabla de trazabilidad del TP3 con un escenario |
| **Atraviesa la estructura** elegida | Su recorrido sobre las vistas del TP3 pasa por varios componentes de la arquitectura |
| Hay una **decisión de arquitectura** (`DA-xx`) que la afecta | Un `DA-xx` cita sus componentes |

Una HU que solo da de alta un registro con campos simples, sin reglas ni rechazos, deja poco para diseñar. Si la HU elegida es muy extensa, se trabaja uno de sus slices (por ejemplo, el flujo principal con su rechazo más importante). El grupo escribe en el documento **por qué eligió esa HU**: además de cumplir las condiciones, debe explicar qué tiene de relevante para el proyecto, para que la elección no sea solo un ajuste a la consigna.

Se parte de la HU y de sus criterios de aceptación (Given-When-Then) escritos en el TP1.

---

## 4. Parte A: Diseño detallado de la HU

El diseño se hace en seis pasos: los cinco de diseño y una verificación final de coherencia. Cada paso produce un resultado que el siguiente transforma. Los pasos 3, 4 y 5 se hacen en ese orden porque cada diagrama se deriva del anterior: si al dibujar uno el grupo descubre que falta algo, vuelve al anterior y lo corrige.

| Paso | Qué se entrega | Para profundizar |
|---|---|---|
| 1. Ficha de la HU | Tabla de coherencia y tabla de entidades del dominio | Referencia: «Paso 1» · Ejemplo: «Paso 1» |
| 2. Análisis tridimensional | Tabla de las tres dimensiones | Referencia: «Paso 2» · Ejemplo: «Paso 2» |
| 3. Diagrama de robustez | Diagrama y reglas de negocio ubicadas | Referencia: «Paso 3» · Ejemplo: «Paso 3» |
| 4. Diagramas de secuencia | Un diagrama por camino y asignación de responsabilidades | Referencia: «Paso 4» · Ejemplo: «Paso 4» |
| 5. Modelo de clases | Diagrama de clases y justificación del diseño | Referencia: «Paso 5» y «Justificación del diseño» · Ejemplo: «Paso 5» |
| 6. Coherencia y trazabilidad | Verificación contra el TP3 y el TP1, y tabla de trazabilidad | Referencia: «Coherencia con la arquitectura y trazabilidad» · Ejemplo: «Trazabilidad y pruebas» |

### Paso 1 — Ficha de la HU

**Qué se entrega**

- El enunciado y los criterios de aceptación (Given-When-Then) de la HU, tal como quedaron en el TP1.
- Una **tabla de coherencia** con las filas funcionalidad, estructura, calidad, dominio y verificación. Debe indicar: de qué caso de uso o slice proviene la HU; qué escenario de calidad (`EC-xx`) la condiciona, qué táctica lo resuelve y qué decisión de arquitectura (`DA-xx`) la respalda; qué estilo y patrones del TP3 rigen en el contenedor; qué componentes de la vista de componentes atraviesa, en qué capa está cada uno y cuál es el principal; y cómo se comprueba la medida del escenario.
- Una **tabla de entidades del modelo de dominio** del TP1: una fila por cada entidad considerada, con si interviene en la HU, qué usa la HU de ella y si la crea, la consulta o la modifica. Se explica también por qué las demás entidades no intervienen. Si la HU necesita un concepto, un atributo o una relación que el modelo no tiene, se agrega al modelo del TP1 y se documenta el cambio.

**Cómo se sabe que está bien:** todos los campos de la tabla de coherencia tienen valor, y cada entidad del modelo de dominio figura como interviniente o no, con su motivo.

### Paso 2 — Análisis tridimensional

**Qué se entrega:** una tabla con las tres dimensiones separadas, con una fila por cada criterio de aceptación y por cada escenario de calidad que alcanza a la HU.

**Cómo se sabe que está bien:** las tres dimensiones están separadas y hay al menos un atributo de calidad que condiciona una decisión.

### Paso 3 — Diagrama de robustez

**Qué se entrega**

- El diagrama de robustez de la HU, en Mermaid y con leyenda.
- Para cada regla de negocio de la HU, **dónde vive** (pantalla, controlador o entidad) y por qué.
- Una tabla que asigna cada elemento del diagrama a un componente del TP3 y a su capa.

**Cómo se sabe que está bien:** cada elemento está en su categoría, no hay ninguna flecha prohibida, las entidades salen de la tabla del Paso 1 y las reglas de negocio no viven en la pantalla.

### Paso 4 — Diagramas de secuencia

**Qué se entrega**

- **Un diagrama de secuencia por camino** que piden los criterios de aceptación: el flujo principal y los rechazos. Todos usan los participantes del diagrama de robustez.
- Una tabla de asignación de responsabilidades: qué objeto hace cada cosa y con qué criterio GRASP.

**Cómo se sabe que está bien:** cada diagrama entra en una pantalla, hay un camino de error, ninguna frontera decide y cada mensaje tiene un responsable. Cada mensaje entre componentes distintos existe en el catálogo de relaciones del TP3, y la táctica del escenario de calidad se ve como una operación o un mensaje concreto.

### Paso 5 — Modelo de clases

**Qué se entrega**

- Un **diagrama de clases** derivado de las secuencias, que reúne lo que aparece en todas ellas.
- La **justificación del diseño**: qué responsabilidad tiene cada clase principal y con qué criterio GRASP se la asignó, y las decisiones de diseño tomadas (por ejemplo, por qué hay una interfaz en un lugar o por qué una regla vive en una entidad). Si se usa un patrón de diseño, se nombra, se indica el problema que resuelve y dónde está en el diagrama. Los patrones son opcionales.

**Cómo se sabe que está bien:** todo lo del modelo aparece en las secuencias y viceversa, y las entidades no son anémicas.

### Paso 6 — Coherencia con la arquitectura y trazabilidad

**Qué se entrega**

- Una **tabla de verificación de coherencia**, completada con la evidencia de cada punto:

| Verificación | ¿Se cumple? | Evidencia |
|---|---|---|
| Cada participante de las secuencias pertenece a un componente de la ficha | | Tabla participante → componente |
| Cada mensaje entre componentes está en el catálogo de relaciones del TP3 | | Secuencia y catálogo |
| El diseño respeta las restricciones del estilo y de los patrones del contenedor | | Tabla de restricciones del TP3 |
| La táctica del escenario de calidad aparece como operación o mensaje | | Secuencia |
| Cada entidad del diagrama de robustez está en el modelo de dominio del TP1 (o se agregó a él) | | Tabla de entidades del Paso 1 |
| Cada entidad que interviene según el Paso 1 aparece en el diseño, o se explica por qué no | | Diagramas de robustez y de clases |
| La medida del escenario tiene una prueba que la verifica | | Caso de prueba |

- Las **actualizaciones** al TP3 y al modelo de dominio del TP1 que hayan surgido de la verificación, si las hubo.
- Una **tabla de trazabilidad** que agrega a la del TP3 las columnas de diseño: HU → componente C4 → clases → archivo → pruebas.

**Cómo se sabe que está bien:** todo criterio de aceptación de la HU llega al menos a una prueba, y toda clase del diagrama aparece en alguna secuencia.

---

## 5. Parte B: Implementación

**Qué se entrega:** el código de la HU, con una interfaz gráfica mínima que permita ejecutarla.

| Se implementa | Se simula o se deja afuera |
|---|---|
| Clases de dominio (entidades) | Servicios externos (correo, colas, pagos): se reemplazan por una implementación simulada, detrás de una interfaz |
| Controladores | Autenticación real y despliegue |
| Interfaces (repositorios y puertos hacia el exterior) | Estilos y pulido visual: no se evalúan |
| Una **interfaz gráfica mínima** que permita ejecutar y mostrar el flujo de la HU | |
| La **persistencia de los datos**, con la opción que elija el grupo (ver abajo) | |

**Persistencia de los datos.** Queda a elección del grupo: puede ser una implementación en memoria (por ejemplo, un diccionario o una lista) o una base de datos real (por ejemplo, SQLite). En los dos casos la persistencia va detrás de la interfaz del repositorio, de modo que el controlador no cambia. Usar una base real no es un requisito: lo que se trabaja en este TP es el diseño y su verificación.

La interfaz gráfica es parte de lo que se entrega porque en la defensa el grupo debe **mostrar el sistema funcionando**. Puede ser web (por ejemplo, con Flask o Streamlit) o de escritorio (por ejemplo, con Tkinter). Como punto de partida se pueden tomar las pantallas del TP2. Alcance mínimo: una pantalla o formulario que permita ingresar los datos, ejecutar la operación y ver el resultado, incluidos los rechazos.

El `README.md` del repositorio incluye las instrucciones para instalar las dependencias y para ejecutar la interfaz y las pruebas, con comandos que funcionen en una máquina limpia. Si el grupo usa una base de datos real, indica también cómo crearla o inicializarla.

**Cómo se sabe que está bien:** los nombres de clases y operaciones del código coinciden con los del diagrama de clases; la interfaz solo conoce a los controladores y no contiene reglas de negocio; los servicios externos están simulados detrás de interfaces y la persistencia, sea en memoria o real, está detrás de la interfaz del repositorio; el proyecto se instala y se ejecuta siguiendo solo el `README.md`.

**Para profundizar:** Referencia: «Parte B — Implementación».

---

## 6. Parte C: Pruebas unitarias

**Qué se entrega**

- Una **tabla de casos de prueba**, con técnica (caja negra o caja blanca), origen (criterio de aceptación, escenario de calidad o parte del código), datos de entrada y estado, y resultado esperado.
- Las **pruebas automatizadas**, en `tests/`, ejecutables con el framework elegido.
- El **reporte de cobertura** y un breve análisis: qué no quedó cubierto y por qué, qué pruebas se agregaron al ver el reporte, y si hay pruebas que pasan pero verifican poco.
- La **complejidad ciclomática**: **a definir.** La forma en que se usa en la entrega se presenta en la clase del 10/11. Hasta entonces no se pide nada sobre este tema.

**Cómo se sabe que está bien:** cada criterio de aceptación de la HU tiene al menos un caso de prueba, la medida del escenario de calidad tiene una prueba que la verifica, las pruebas pasan todas al ejecutarlas desde cero, cada prueba verifica un solo comportamiento y no depende de otra, y no se prueba a través de la interfaz gráfica.

**Para profundizar:** Referencia: «Parte C — Pruebas unitarias».

---

## 7. Entregable

Todo el resultado se organiza dentro del repositorio del grupo:

- `docs/design/diseno-detallado.md`: documento de diseño detallado, con las secciones del Anexo de esta consigna.
- `src/`: código fuente.
- `tests/`: pruebas unitarias.
- `docs/design/cobertura.md`: reporte de cobertura y su análisis (puede ir como una sección del documento de diseño).
- `README.md`: instrucciones para instalar, ejecutar la interfaz y ejecutar las pruebas.
- `docs/uso-ia.md`: registro del uso de IA, según la sección siguiente.

---

## 8. Uso de IA

El uso de inteligencia artificial está permitido y forma parte de la consigna. Puede asistir en el diseño (proponer clases, detectar responsabilidades mal asignadas), en la programación y en la generación de pruebas.

La IA suele proponer diseños con más clases, más interfaces y más patrones de los que el problema necesita, y código que funciona pero no respeta el diseño del grupo. Por eso el grupo documenta cada interacción: qué solicitó, qué obtuvo, qué aceptó, modificó o descartó, y por qué. En particular debe verificar que los diagramas generados cumplan las reglas de la Referencia (Pasos 3 a 5), que el código coincida con el diagrama de clases, y que las pruebas verifiquen comportamiento real. El registro se guarda en `docs/uso-ia.md`.

---

## 9. Checklist de entrega

**Diseño (Parte A)**

- [ ] HU seleccionada, con su enunciado, criterios de aceptación y justificación de la elección.
- [ ] Tabla de coherencia (funcionalidad, estructura, calidad, dominio y verificación).
- [ ] Tabla de entidades del modelo de dominio del TP1 que intervienen en la HU y, si hizo falta, el cambio al modelo.
- [ ] Análisis tridimensional de la HU.
- [ ] Diagrama de robustez, con la ubicación de cada regla de negocio.
- [ ] Un diagrama de secuencia por camino (éxito y rechazos), con las responsabilidades justificadas con GRASP.
- [ ] Un diagrama de clases derivado de los diagramas de secuencia.
- [ ] Justificación del diseño (criterios GRASP y, si los hay, patrones de diseño usados).
- [ ] Verificación de coherencia con la arquitectura y, si corresponde, actualización del TP3.
- [ ] Tabla de trazabilidad HU → componente C4 → clases → archivo → pruebas.

**Implementación (Parte B)**

- [ ] Código en `src/`, coherente con el diagrama de clases, con la persistencia elegida (en memoria o base de datos real) y los servicios externos simulados, detrás de interfaces.
- [ ] Interfaz gráfica mínima que permite ejecutar la HU.
- [ ] `README.md` con las instrucciones para instalar y ejecutar.

**Pruebas (Parte C)**

- [ ] Tabla de casos de prueba (caja negra y caja blanca), con su origen.
- [ ] Pruebas automatizadas en `tests/`, ejecutables con el framework elegido, que pasan todas al ejecutarlas desde cero.
- [ ] Reporte de cobertura y su análisis.

**General**

- [ ] Registro del uso de IA.
- [ ] Repositorio actualizado con commits que reflejen el avance de este TP.
- [ ] Diagramas en Mermaid dentro de archivos Markdown.
- [ ] Siglas aclaradas la primera vez que se usan.
- [ ] Grupo en condiciones de defender oralmente cada decisión tomada y de mostrar el sistema andando.

---

## 10. Instancia de defensa

La defensa incluye una **demostración del sistema funcionando**, a partir del repositorio, y preguntas sobre el diseño. Se podrá solicitar al grupo que:

- Ejecute la interfaz y recorra el criterio de aceptación de una HU, incluido un camino de rechazo.
- Muestre ese mismo recorrido en el diagrama de robustez, en el de secuencia y en el código del controlador.
- Explique por qué una responsabilidad está en una clase y no en otra, con el criterio GRASP que lo justifica.
- Cambie una implementación (por ejemplo, el repositorio en memoria por otro) y explique por qué el controlador no se modifica.
- Muestre en el modelo de dominio qué entidades intervienen en su HU y explique por qué las demás no.
- Muestre cómo su diseño respeta el estilo y los patrones del TP3, y qué cambió de la arquitectura al bajar al diseño detallado.
- Muestre la prueba que verifica un criterio de aceptación y la que verifica una propiedad de calidad del TP2 o del TP3.
- Explique qué líneas no quedaron cubiertas en el reporte de cobertura y por qué.
- Muestre un caso en que rechazó una sugerencia de la IA, y argumente por qué.

---

## Anexo. Estructura del documento de diseño detallado

| Sección | Qué contiene |
|---|---|
| 1. Introducción | Propósito, HU elegida, motivo de la elección y siglas usadas |
| 2. Relación con la arquitectura | Tabla de coherencia: `EC-xx`, táctica y `DA-xx`; componentes y capas que atraviesa; estilo y patrones; verificación de coherencia |
| 3. Diseño de la HU | Enunciado y criterios, entidades del modelo de dominio que intervienen, análisis tridimensional, diagrama de robustez, diagramas de secuencia (uno por camino) con la asignación de responsabilidades |
| 4. Modelo de clases | Un diagrama derivado de todas las secuencias |
| 5. Justificación del diseño | Asignación de responsabilidades (GRASP), decisiones de diseño y patrones de diseño usados, si los hay |
| 6. Implementación | Estructura del código, cómo se ejecuta y cómo se reemplazan la persistencia y los servicios externos |
| 7. Pruebas | Tabla de casos de prueba, resultados y análisis de cobertura |
| 8. Trazabilidad | HU → componente C4 → clases → archivo → pruebas |
| 9. Glosario y bibliografía | Siglas y términos, y referencias |
