---
title: TP4 — Diseño Detallado, Implementación y Testing Unitario
nav_order: 4
---

# Ingeniería del Software - 2026 - TP 4

## Diseño Detallado, Implementación y Testing Unitario

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

## 2. Modalidad de trabajo

Este TP es continuación directa del proyecto desarrollado en el TP1, el TP2 y el TP3. No se cambia de proyecto ni de alcance.

### 2.1 Alcance

El grupo elige **una historia de usuario** (HU) de su proyecto y hace con ella el trabajo completo: análisis, diseño, implementación y pruebas. Es preferible una HU trabajada de punta a punta que varias a medias.

**Qué significa "completo".** Para esa HU el grupo entrega: la ficha con su relación con el TP3, el análisis tridimensional, el diagrama de robustez, los diagramas de secuencia (uno por camino), el modelo de clases, la justificación del diseño, el código con una interfaz gráfica mínima, los casos de prueba con sus pruebas automatizadas, el reporte de cobertura y la trazabilidad.

**Cómo elegir la HU.** La HU tiene que sostener el análisis de las tres dimensiones (funcionalidad, estructura y calidad). Para eso debe cumplir estas condiciones, que se comprueban con lo que el grupo ya entregó en los TP anteriores:

| Condición | Cómo se comprueba |
|---|---|
| Está asociada a **al menos un escenario de calidad** (`EC-xx`) | Figura en la tabla de trazabilidad del TP3 con un escenario |
| **Atraviesa la estructura** elegida | Su recorrido sobre las vistas del TP3 pasa por varios componentes de la arquitectura |
| Hay una **decisión de arquitectura** que la afecta | Un `DA-xx` cita sus componentes |

Una HU que solo da de alta un registro con campos simples, sin reglas ni rechazos, deja poco para diseñar. Si la HU elegida es muy extensa, se trabaja uno de sus slices (por ejemplo, el flujo principal con su rechazo más importante). El grupo escribe en el documento **por qué eligió esa HU**: además de cumplir las condiciones, debe explicar qué tiene de relevante para el proyecto, para que la elección no sea solo un ajuste a la consigna.

Se parte de la HU y de sus criterios de aceptación (Given-When-Then) escritos en el TP1.

### 2.2 Qué se implementa y qué se simula

| Se implementa | Se simula o se deja afuera |
|---|---|
| Clases de dominio (entidades) | Base de datos real: la persistencia se reemplaza por una implementación en memoria, detrás de una interfaz |
| Controladores | Servicios externos (correo, colas, pagos): se reemplazan por una implementación simulada, detrás de una interfaz |
| Interfaces (repositorios y puertos hacia el exterior) | Autenticación real y despliegue |
| Una **interfaz gráfica mínima** que permita ejecutar y mostrar el flujo de la HU | Estilos y pulido visual: no se evalúan |

La interfaz gráfica es parte de lo que se entrega porque en la defensa el grupo debe **mostrar el sistema funcionando** (sección 9). Puede ser web (por ejemplo, con Flask o Streamlit) o de escritorio (por ejemplo, con Tkinter). Como referencia se pueden tomar las pantallas del TP2. Su única función es recibir los datos del usuario, llamar al controlador y mostrar la respuesta; la lógica no va en ella (ver sección 4.3).

### 2.3 Lenguaje y herramientas

La implementación y las pruebas se hacen en el **lenguaje que el grupo elija** (en general, el mismo del proyecto o el que mejor conozca el equipo), con el framework de pruebas de ese lenguaje. En clase se usa pytest como ejemplo de herramienta; JUnit, Jest, xUnit u otros sirven igual. En este TP se evalúa el diseño y su verificación, no la tecnología. Los ejemplos de esta guía están en Python solo para mostrar el nivel de detalle.

Los diagramas se escriben en Mermaid dentro de archivos Markdown, igual que en el TP3.

### 2.4 Organización del trabajo

El trabajo se organiza en tres partes que se retroalimentan, todas obligatorias:

- Parte A: Diseño detallado de la HU.
- Parte B: Implementación.
- Parte C: Pruebas unitarias.

| Fecha | Actividad en clase |
|---|---|
| 02/11 | Inicio. Diseño dirigido por HU: análisis tridimensional, diagrama de robustez, diagrama de secuencia (Parte A) |
| 10/11 | Primera implementación de clases e interfaces. Diseño de casos de prueba. Pruebas de software, técnicas, TDD y pytest (Partes B y C) |
| 16/11 | Cierre. Implementación de las pruebas, ejecución y reporte de cobertura |
| 17/11 | Instancia 4: presentación del diseño detallado, la implementación y las pruebas |

Recomendación: el trabajo se realiza en una rama del repositorio y se integra mediante Pull Request con revisión cruzada del grupo, según el instructivo de Git y GitHub.

---

## 3. Parte A: Diseño detallado de cada historia de usuario

### 3.1 Visión general

El diseño detallado se hace **una historia de usuario por vez**, en cinco pasos. Cada paso produce un resultado que el siguiente transforma:

```mermaid
flowchart LR
    P1["1. Seleccionar<br/>la funcionalidad"] --> P2["2. Análisis<br/>tridimensional"]
    P2 --> P3["3. Robustez<br/>quién es quién"]
    P3 --> P4["4. Secuencia<br/>quién hace qué"]
    P4 --> P5["5. Modelo<br/>de clases"]
    P5 -.->|"si algo falta,<br/>se corrige el paso anterior"| P4
```

| Paso | Pregunta que responde | Resultado |
|---|---|---|
| 1. Seleccionar la funcionalidad | ¿Qué HU se diseña y qué dice su criterio de aceptación? | HU elegida, con su relación con el TP3 |
| 2. Análisis tridimensional | ¿Qué hace, con qué se hace y qué propiedades debe cumplir? | Tabla de las tres dimensiones |
| 3. Diagrama de robustez | ¿Qué elementos intervienen y de qué tipo son? | Diagrama de robustez |
| 4. Diagrama de secuencia | ¿En qué orden colaboran y quién tiene cada responsabilidad? | Diagrama de secuencia |
| 5. Modelo de clases | ¿Qué clases, atributos, operaciones y relaciones hacen falta? | Diagrama de clases |

Los pasos 3, 4 y 5 se hacen en ese orden porque cada diagrama se deriva del anterior: **lo que no aparece en el diagrama de secuencia no aparece en el de clases**, y lo que no aparece en el de robustez no se invoca en el de secuencia. Si al dibujar un diagrama el grupo descubre que falta algo, vuelve al anterior y lo corrige.

### 3.2 Paso 1 — Seleccionar la funcionalidad

El grupo elige la HU y copia en el documento su enunciado y sus criterios de aceptación (Given-When-Then), tal como quedaron en el TP1. Indica además:

- De qué caso de uso o slice proviene.
- Qué escenario de calidad (`EC-xx`) la condiciona, qué táctica lo resuelve y qué decisión de arquitectura (`DA-xx`) la respalda.
- Qué estilo y patrones del TP3 rigen en el contenedor donde se ejecuta.
- Qué componentes de la vista de componentes del TP3 atraviesa, en qué capa está cada uno y cuál de ellos es el principal (por ejemplo, "Servicio de análisis" del contenedor API).
- Qué **entidades del modelo de dominio** del TP1 intervienen en la HU (ver más abajo).
- Por qué la eligió, según la sección 2.1.

Estos datos se reúnen en una **tabla de coherencia**, que es el primer producto de la HU y la base de los pasos siguientes:

| Dimensión | Qué se completa | Ejemplo (biblioteca) |
|---|---|---|
| Funcionalidad | HU, caso de uso o slice, y caminos de los criterios | `HU-03` Prestar un ejemplar; camino principal y rechazos (socio no habilitado, ejemplar no disponible) |
| Estructura | Componentes que atraviesa, capas, estilo y patrones | «Controladores», «Servicio de préstamos» y «Acceso a datos» del contenedor API; patrón de capas |
| Calidad | `EC-xx`, táctica y `DA-xx` | `EC-02` préstamos simultáneos del mismo ejemplar; operación atómica y transacción en el acceso a datos (`DA-02`) |
| Dominio | Entidades del modelo del TP1 que intervienen y qué usa la HU de cada una | `Socio`, `Ejemplar` y `Prestamo`; no intervienen `Libro`, `Autor` ni `Multa` |
| Verificación | Cómo se comprueba la medida del escenario | Prueba con pedidos simultáneos del mismo ejemplar |

**Entidades del modelo de dominio que intervienen en la HU.** Este punto es central: el diseño detallado no reemplaza el modelado de dominio, sino que parte de los datos, las reglas y los conceptos del negocio que el grupo ya identificó en el TP1 y decide quién hace qué con ellos. Para la HU elegida, el grupo identifica qué entidades del diagrama de dominio **"pegan" con ella**, es decir, cuáles aparecen en sus criterios de aceptación o hacen falta para cumplirlos. Se sugiere este procedimiento:

1. Marcar los sustantivos del enunciado y de los criterios Given-When-Then.
2. Buscar cada uno en el diagrama de dominio del TP1 e identificar qué entidad le corresponde.
3. Para cada entidad que interviene, anotar qué usa la HU de ella (atributos, reglas, relaciones con otras entidades que intervienen) y si la HU la crea, la consulta o la modifica.
4. Revisar las entidades del modelo que no intervienen y explicar por qué: porque la HU no las usa, o porque alcanza con un dato que expone otra entidad.
5. Si la HU necesita un concepto, un atributo o una relación que el modelo no tiene, se agrega al modelo de dominio del TP1 y se documenta el cambio.

El resultado es una tabla, con una fila por cada entidad del modelo que se haya considerado:

| Entidad del modelo (TP1) | ¿Interviene? | Qué usa la HU de ella | La HU la... |
|---|---|---|---|
| `Socio` | Sí | Si está activo, sus multas pendientes y sus préstamos vigentes | Consulta y modifica |
| `Libro` | No | No interviene en la lógica del préstamo | — |

Las entidades de esta tabla son las que se llevan al diagrama de robustez (sección 3.4). El Anexo A muestra la tabla completa de un ejemplo.

### 3.3 Paso 2 — Análisis tridimensional

El diseño de una funcionalidad se mira desde tres dimensiones. Cada una aporta información distinta y ninguna reemplaza a las otras:

| Dimensión | Pregunta | Fuente | Ejemplo |
|---|---|---|---|
| Funcionalidad | ¿Qué debe hacer el sistema para el usuario? | Criterios de aceptación de la HU | "Si el socio tiene multas, rechazar el préstamo e informar el motivo" |
| Estructura | ¿Qué elementos (pantallas, lógica, datos, sistemas externos) hacen falta? | Componente C4 y modelo de dominio | Una pantalla, un controlador, las entidades `Socio` y `Ejemplar`, un repositorio |
| Calidad | ¿Qué propiedades debe cumplir esta funcionalidad? | Escenarios `EC-xx` del TP2 y decisiones del TP3 | "Dos préstamos simultáneos del mismo ejemplar: solo uno se concreta" (`EC-02`) |

El resultado es una tabla con una fila por cada criterio de aceptación y por cada escenario de calidad que la alcanza. La dimensión de calidad es la que conecta este TP con el anterior: **las propiedades de calidad que el TP3 resolvió a nivel de estructura global ahora se resuelven en operaciones concretas** (por ejemplo, una operación que verifica y descuenta en un solo paso para que no haya inconsistencias). Una HU sin ninguna propiedad de calidad asociada es válida, pero el grupo debe poder explicar por qué.

### 3.4 Paso 3 — Diagrama de robustez

El diagrama de robustez es un puente entre lo que pide la HU y el diseño de clases. Clasifica cada elemento que interviene en tres tipos:

| Tipo | Qué representa | Ejemplos |
|---|---|---|
| **Boundary** (frontera) | Lo que conecta el sistema con un actor o con otro sistema: pantallas, interfaces hacia servicios externos | Pantalla de préstamo; conexión con un servicio de avisos por correo |
| **Controller** (controlador) | Coordina la ejecución de la funcionalidad: decide qué se hace y en qué orden | Controlador de préstamos; repositorios |
| **Entity** (entidad) | Un concepto del dominio, con sus datos y reglas | Socio; ejemplar; préstamo |

**De dónde salen las entidades.** Las entidades del diagrama de robustez no se inventan: son las que el grupo identificó en el paso 1 como entidades del modelo de dominio que intervienen en la HU. Si al dibujar el diagrama aparece una entidad que no está en esa tabla, hay dos salidas: se corrige el diagrama o se agrega la entidad al modelo de dominio y se documenta.

**Reglas de conexión:**

| Desde | Hacia | ¿Permitido? | Por qué |
|---|---|---|---|
| Actor | Boundary | Sí | El actor solo interactúa a través de interfaces |
| Boundary | Controller | Sí | La frontera delega la lógica en el controlador |
| Controller | Entity | Sí | El controlador manipula los datos del dominio |
| Controller | Controller | Sí | Los controladores se coordinan entre sí |
| Boundary | Entity | **No** | Rompe la separación de capas |
| Actor | Entity o Controller | **No** | El actor no accede directamente a los datos ni a la lógica |

Cuando aparece una conexión no permitida, es señal de una responsabilidad mal ubicada o de que falta un elemento intermedio (casi siempre, un controlador). Un controlador puede apoyarse en otros controladores (en el ejemplo, los repositorios) y en fronteras hacia sistemas externos (por ejemplo, un servicio de avisos por correo). Lo que no se admite es que acceda a un sistema externo sin pasar por una frontera.

**La decisión clave: dónde vive cada regla.** Cada regla del negocio que aparece en los criterios de la HU (por ejemplo, "un socio con multas no puede retirar un libro") tiene que vivir en algún lugar, y la robustez es el momento de decidirlo. Hay tres candidatos:

| Opción | Dónde se valida | Problema |
|---|---|---|
| A | En la pantalla (boundary) | Es una frontera que decide: si mañana hay otra pantalla o una API, la regla se duplica o se pierde |
| B | En el controlador | Funciona, pero con muchas reglas el controlador engorda y se vuelve obeso |
| C | En la entidad | La entidad sabe qué es estar en condiciones y no se puede saltear: cualquier camino que llegue a ella pasa por la regla |

La opción C suele ser la mejor por tres razones: la entidad tiene la información necesaria (criterio Experto), la regla no se puede saltear y no pueden existir estados inválidos. La pantalla puede avisar antes, lo que mejora la usabilidad, pero no reemplaza la regla del dominio: **la pantalla ayuda, el dominio garantiza**. El grupo indica en el documento, para cada regla de su HU, dónde vive y por qué.

**Coherencia con la estructura.** Cada elemento del diagrama debe poder asignarse a uno de los componentes de la ficha (tabla de coherencia, sección 3.2) y a su capa. Un elemento que no pertenece a ningún componente es una alerta: o el elemento sobra, o falta un componente en la arquitectura. Las conexiones deben respetar las restricciones del estilo y de los patrones que rigen el contenedor (por ejemplo, en una arquitectura en capas, ninguna capa depende de las superiores ni se saltea una capa).

**Notación.** Mermaid no tiene un tipo de diagrama de robustez; se dibuja con `flowchart` y una leyenda, como se hizo con el diagrama de flujo de datos del TP1. Se sugiere usar la forma redondeada para boundary, el círculo para controller y el rectángulo con barras para entity, y colores distintos para que se distingan. Los nombres se escriben con el tipo entre comillas angulares (`«boundary»`). El Anexo A muestra un ejemplo.

**Cómo se construye, en seis pasos.**

1. Leer la HU y detectar las acciones y los actores.
2. Boundaries: todo lo que habla con los actores o con otros sistemas.
3. Entities: los sustantivos del dominio (los de la tabla del paso 1).
4. Controllers: los verbos que requieren lógica.
5. Conectar los elementos según las reglas de conexión.
6. Revisar que nada quede fuera de su lugar.

Si lleva más de 10 minutos, se está sobrediseñando.

**Errores típicos.**

| Error | Qué pasa |
|---|---|
| Boundaries que deciden | Si la pantalla empieza a validar reglas o a buscar datos, la arquitectura desaparece |
| Controllers obesos | Si el controlador hace todo, concentra la lógica y se vuelve imposible de mantener |
| Entities que procesan | Las entidades pueden verificar su propia integridad, pero no coordinar operaciones |
| Entidades anémicas | Si las entidades no tienen comportamiento propio, el dominio se vacía y todo queda en el controlador |

### 3.5 Paso 4 — Diagrama de secuencia

El diagrama de secuencia muestra, en orden, qué mensajes se envían los elementos del diagrama de robustez para cumplir el criterio de aceptación. Es donde se **asignan las responsabilidades**: cada mensaje es una operación que algún objeto debe tener.

Reglas:

- Los participantes son los elementos del diagrama de robustez (más el actor). No se agregan elementos nuevos sin volver a robustez.
- Se dibuja una secuencia por **camino** que piden los criterios de aceptación: una para el flujo principal y otra para los rechazos (por ejemplo, el rechazo porque el socio tiene multas). Todas usan los mismos participantes de la robustez. Con `alt` u `opt` se muestran las variantes pequeñas dentro de un mismo camino.
- Los mensajes son llamadas con nombre y parámetros reales (`tomar()`, `motivo_de_rechazo()`), no frases ("verifica si está libre").
- Cada mensaje entre elementos de **componentes distintos** debe existir en el catálogo de relaciones de la vista de componentes del TP3. Si no existe, hay dos salidas: se corrige el diseño o se actualiza el TP3, porque la arquitectura estaba incompleta. En ese caso se documenta el cambio.
- La **táctica** del escenario de calidad de la ficha debe verse en el diagrama como una operación o un mensaje concreto (por ejemplo, una transacción, una verificación previa o una llamada a la auditoría).

**Cómo se lee el diagrama.**

| Elemento | Qué significa |
|---|---|
| Participante | Un objeto o actor; aparece arriba, en su caja |
| Línea de vida | La vertical punteada: la existencia del participante durante la operación |
| Mensaje | Flecha sólida: una llamada a una operación, que espera respuesta |
| Retorno | Flecha punteada: un valor o una confirmación |
| Tiempo | Corre de arriba hacia abajo: lo de arriba ocurre antes |
| Fragmento | Un recuadro con una condición: `alt` (camino alternativo), `opt` (paso opcional) o `loop` (paso que se repite) |

Regla práctica: cada diagrama entra en una pantalla. Si tiene 50 mensajes, no se está modelando una historia sino un sprint. Además, ninguna frontera decide, y cada mensaje tiene un responsable.

**Cómo decidir qué objeto hace cada cosa.** Se aplican los criterios GRASP (patrones generales para asignar responsabilidades). Los cinco que se usan en este TP:

| Criterio | La pregunta | Regla | Ejemplo |
|---|---|---|---|
| Experto en información | ¿Quién tiene la información? | La responsabilidad se asigna a la clase que tiene los datos necesarios | `Socio` decide si puede retirar, porque conoce sus multas y sus préstamos vigentes |
| Creador | ¿Quién crea la instancia? | Crea un objeto quien lo contiene, lo usa de forma directa o tiene los datos para iniciarlo | El controlador crea el `Prestamo`, porque tiene el socio y el ejemplar elegidos |
| Controlador | ¿Quién orquesta el pedido que llega de la interfaz? | Un objeto recibe y coordina el evento del sistema, sin hacer él mismo el trabajo del dominio | `ControladorPrestamos` coordina; no decide si el socio puede retirar ni guarda |
| Bajo acoplamiento | ¿Cómo evito que un objeto conozca detalles ajenos? | Se prefiere la asignación que genera menos dependencias entre clases | La pantalla conoce solo al controlador |
| Alta cohesión | ¿Cada clase hace una sola cosa bien? | Cada clase concentra responsabilidades relacionadas entre sí | Los repositorios solo guardan y recuperan |

**Cuando un dato pertenece a otro módulo o sistema.** Si para cumplir la HU hace falta un dato que no es de nuestro módulo (por ejemplo, saber si un docente está asignado a una materia, algo que sabe otro módulo), no hay una entidad propia que lo represente. Se modela como una **frontera hacia ese módulo**: una interfaz que el controlador usa para preguntar, sin saber cómo el otro módulo guarda sus datos. Así se mantiene el bajo acoplamiento entre módulos.

**Checklist para validar la secuencia.**

- ¿Cada mensaje tiene un responsable lógico?
- ¿Hay pasos implícitos que no están modelados?
- ¿La frontera evita tomar decisiones?
- ¿El controlador coordina sin ahogarse?
- ¿Las entidades mantienen la coherencia del dominio?
- ¿El flujo es claro de principio a fin, y hay un camino de error?

### 3.6 Paso 5 — Modelo de clases

El diagrama de clases no se inventa: se descubre a partir de la secuencia. El método es casi mecánico:

1. Cada participante de la secuencia pasa a ser una clase o una interfaz.
2. Cada mensaje que recibe pasa a ser una operación de esa clase.
3. La información que necesita para cumplir su tarea son sus atributos.
4. Las líneas del modelo (dependencias y asociaciones) surgen de la colaboración entre las clases.

**Lo que no aparece en la secuencia no aparece en el modelo de clases, y al revés: si aparece en el modelo, tiene que tener respaldo en el comportamiento.**

Reglas:

- Cada clase incluye los atributos y las operaciones que el diagrama de secuencia usa, con sus tipos. No se agregan operaciones "por si acaso".
- Los repositorios y las conexiones hacia sistemas externos se modelan como **interfaces**; la clase concreta (en memoria, simulada) aparece aparte y las implementa. Esto permite reemplazar la persistencia real sin tocar el controlador.
- Las relaciones indican su tipo: asociación, dependencia (`..>`), realización de interfaz (`..|>`), herencia y composición. Se indica la multiplicidad cuando importa.
- Las clases de dominio conservan los nombres y las relaciones del modelo de dominio del TP1. Si el diseño necesita cambiar algo (un nombre, una relación o una clase nueva), el cambio se documenta y el modelo del TP1 se actualiza.
- El diagrama de clases es **uno solo** y reúne lo que aparece en todas las secuencias de la HU (éxito y rechazos).

Para validar el modelo, se lo recorre como si se fuera el usuario y como si se fuera el sistema: ¿cada clase cumple un rol claro?, ¿cada método tiene una razón de existir?, ¿alguna clase conoce detalles técnicos que no le corresponden?

### 3.7 Justificación del diseño

Terminado el modelo de clases, el grupo justifica su diseño en el documento: para las clases principales, indica qué responsabilidad tiene cada una y con qué criterio GRASP se la asignó (la tabla de asignación de la sección 3.5 sirve de base), y explica las decisiones de diseño que tomó (por ejemplo, por qué hay una interfaz en ese lugar o por qué una regla vive en una entidad y no en el controlador).

La justificación tiene que ser honesta: más clases e interfaces tienen un costo (más indirección), y el grupo debe poder explicar cuándo ese costo vale la pena y cuándo no. Una clase de tres líneas con una sola implementación posible no necesita una interfaz solo porque el diagrama quede más prolijo.

**Patrones de diseño (opcional).** Si el diseño usa un patrón de los vistos en clase (por ejemplo, Strategy para variantes de cálculo, Factory para crear según un tipo, Repository para el acceso a datos), el grupo lo nombra, indica el problema que resuelve y señala dónde está en el diagrama de clases. No se pide usar patrones por obligación: un patrón que no resuelve un problema concreto del diseño empeora la nota, no la mejora.

### 3.8 Coherencia con la arquitectura y trazabilidad

**Coherencia.** Antes de cerrar la Parte A, el grupo verifica en una tabla que las tres dimensiones de la tabla de coherencia (sección 3.2) quedaron reflejadas en el diseño:

| Verificación | ¿Se cumple? | Evidencia |
|---|---|---|
| Cada participante de las secuencias pertenece a un componente de la ficha | | Tabla participante → componente |
| Cada mensaje entre componentes está en el catálogo de relaciones del TP3 | | Secuencia y catálogo |
| El diseño respeta las restricciones del estilo y de los patrones del contenedor | | Tabla de restricciones del TP3 |
| La táctica del escenario de calidad aparece como operación o mensaje | | Secuencia |
| Cada entidad del diagrama de robustez está en el modelo de dominio del TP1 (o se agregó a él) | | Tabla de entidades del paso 1 |
| Cada entidad que interviene según el paso 1 aparece en el diseño, o se explica por qué no | | Diagramas de robustez y de clases |
| La medida del escenario tiene una prueba que la verifica | | Caso de prueba |

Las diferencias que aparezcan entre el diseño y el TP3, o entre el diseño y el modelo de dominio del TP1, no son un error del grupo: el diseño se precisa al bajar de nivel. Lo importante es que cada diferencia quede documentada y que el documento anterior se actualice.

**Autoevaluación de los artefactos.** Antes de entregar, el grupo revisa cada artefacto con este criterio:

| Artefacto | Criterio |
|---|---|
| Análisis tridimensional | Las tres dimensiones están separadas y hay al menos un atributo de calidad que condiciona una decisión |
| Robustez | Cada elemento está en su categoría y no hay ninguna flecha prohibida |
| Secuencia | Entra en una pantalla, tiene un camino de error, ninguna frontera decide y cada mensaje tiene un responsable |
| Clases | Todo lo del modelo aparece en la secuencia y viceversa, y las entidades no son anémicas |

**Trazabilidad.** El grupo agrega a la tabla de trazabilidad del TP3 las columnas de diseño, de modo que la HU se pueda seguir hasta el código y la prueba que la verifica:

| HU | Componente C4 (TP3) | Clases | Archivo | Pruebas |
|---|---|---|---|---|
| `HU-03` | Servicio de préstamos; Acceso a datos | `ControladorPrestamos`, `Socio`, `Ejemplar`, `Prestamo` | `src/aplicacion/controlador_prestamos.py` | `test_presta_el_ejemplar_y_fija_la_fecha_de_devolucion`, `test_rechaza_si_el_ejemplar_ya_esta_prestado` |

Todo criterio de aceptación de la HU elegida debe llegar al menos a una prueba, y toda clase del diagrama debe aparecer en algún diagrama de secuencia.

---

## 4. Parte B: Implementación

### 4.1 Estructura del proyecto

Se sugiere organizar el código en capas que reflejen las reglas del diagrama de robustez, de modo que la estructura de carpetas haga visible el diseño:

```text
src/
├── dominio/            # entidades: Socio, Ejemplar, Prestamo
├── aplicacion/         # controladores e interfaces (puertos)
├── infraestructura/    # implementaciones en memoria y simuladas
└── interfaz/           # interfaz gráfica mínima (boundary)
tests/
```

### 4.2 Reglas de implementación

1. **El código sigue al diseño.** Los nombres de clases y operaciones coinciden con los del diagrama de clases. Si al programar el grupo descubre que el diseño estaba mal, corrige primero el diagrama y después el código: al final, ambos deben decir lo mismo.
2. **Dependencias en un solo sentido.** La interfaz gráfica depende de los controladores; los controladores, del dominio y de las interfaces; las implementaciones de infraestructura implementan esas interfaces. El dominio no importa nada de las demás capas.
3. **Los colaboradores se reciben, no se crean.** El controlador recibe sus repositorios y sus conexiones hacia servicios externos por el constructor (inyección de dependencias). Quién arma los objetos concretos es un único lugar, el punto de arranque del programa.
4. **Las reglas del dominio viven en las entidades.** Si el controlador tiene un `if` que verifica una regla del negocio, probablemente esa regla pertenece a una entidad.
5. **Sin base de datos ni servicios reales.** La persistencia es una clase en memoria (un diccionario o una lista) que implementa la interfaz del repositorio. Los servicios externos son clases simuladas que registran qué se les pidió.
6. **Se declaran los tipos** en las firmas de las operaciones públicas, en la medida en que el lenguaje lo permita, para que el código sea legible y coincida con el diagrama.

### 4.3 Interfaz gráfica mínima

La interfaz gráfica es una frontera (*boundary*) del diagrama de robustez y respeta sus reglas:

- Solo conoce a los controladores. No importa entidades ni repositorios.
- No contiene reglas de negocio: no calcula, no valida reglas del dominio ni decide.
- Muestra lo que el controlador responde, incluidos los rechazos (por ejemplo, el motivo por el que se rechazó un préstamo).

Alcance mínimo: una pantalla o formulario que permita ingresar los datos, ejecutar la operación y ver el resultado. Las pruebas unitarias de la Parte C **no** pasan por la interfaz gráfica: se prueban los controladores y las entidades directamente.

### 4.4 Cómo se ejecuta

El repositorio incluye en su `README.md` las instrucciones para instalar las dependencias (un archivo `requirements.txt`) y para ejecutar tanto la interfaz como las pruebas, con comandos que funcionen en una máquina limpia. Esto es lo que se usa en la defensa.

---

## 5. Parte C: Pruebas unitarias

### 5.1 Qué es probar software y qué se prueba en este TP

**Probar** es ejecutar el software con datos elegidos para comparar lo que hace con lo que debería hacer, con el objetivo de encontrar defectos. Una prueba no demuestra que el software es correcto: solo puede mostrar que, para esos datos, se comporta como se espera o que falla. Tres términos que conviene distinguir:

| Término | Qué es |
|---|---|
| Caso de prueba | Una combinación de datos de entrada, estado inicial y resultado esperado |
| Oráculo | Lo que permite saber cuál es el resultado esperado (en este TP, los criterios de aceptación y las reglas del dominio) |
| Defecto | Un error en el código que puede producir una falla cuando se ejecuta en ciertas condiciones |

Las pruebas se organizan en **niveles**, según qué parte del sistema se ejercita:

| Nivel | Qué verifica | En este TP |
|---|---|---|
| Unitario | Una unidad pequeña (una operación de una entidad, un método de un controlador) de forma aislada | **Es el nivel de este TP** |
| De integración | Que varias unidades funcionen bien juntas (por ejemplo, el controlador con la base real) | No se hace: la persistencia y los servicios son simulados |
| De sistema y de aceptación | El sistema completo desde el punto de vista del usuario | Se muestra en la demostración con la interfaz gráfica, pero no se automatiza |

Se prueban las clases de dominio y los controladores. Los colaboradores del controlador (repositorios, servicios externos) son las implementaciones en memoria o simuladas de la sección 4.2: gracias a que el controlador depende de interfaces, la prueba no necesita base de datos ni servicios reales. Estas implementaciones simuladas se llaman **dobles de prueba**: reemplazan a un colaborador real para controlar la prueba (por ejemplo, un repositorio en memoria que devuelve lo que se necesita, o un servicio simulado que registra qué se le pidió).

### 5.2 Diseño de casos de prueba

Los casos de prueba se diseñan **antes** de escribirlos y se registran en una tabla, con dos técnicas complementarias.

**Caja negra.** Se diseñan mirando solo la especificación, sin leer el código. La fuente son los criterios de aceptación de la HU. Para cada criterio se escribe al menos un caso. Tres técnicas ayudan a elegir los datos:

| Técnica | Idea | Ejemplo (préstamo de un libro) |
|---|---|---|
| Partición en clases de equivalencia | Se divide cada entrada en grupos de valores que el sistema trata igual, y se prueba un valor de cada grupo | Socios: activo sin multas, con multas, inactivo. Basta un socio de cada clase |
| Valores límite | Los errores aparecen en los bordes de los rangos: se prueba justo en el borde, uno por debajo y uno por encima | Límite de 3 préstamos: socios con 2 préstamos (puede), 3 (no puede) y 4 |
| Tabla de decisión | Cuando varias condiciones se combinan, se arma una tabla con las combinaciones y el resultado de cada una | Activo, sin multas y por debajo del límite: acepta. Si falla cualquiera de las tres, rechaza con su motivo |

**Caja blanca.** Se diseñan mirando el código. El objetivo es que las pruebas recorran lo que el código puede hacer. Hay tres niveles de exigencia:

| Cobertura | Qué pide | Qué descubre |
|---|---|---|
| De sentencias | Que cada línea se ejecute al menos una vez | Código que nunca se ejecuta |
| De decisiones (ramas) | Que cada `if` se pruebe con resultado verdadero y con resultado falso | Ramas que nadie probó |
| De caminos | Que se recorran las combinaciones de decisiones | Interacciones entre decisiones; es muy costosa y se aplica solo a lo crítico |

Este análisis puede mostrar casos que los criterios de aceptación no contemplan.

| ID | Técnica | Origen | Dado (entrada y estado) | Resultado esperado |
|---|---|---|---|---|
| `CP-01` | Caja negra | `HU-03`, criterio 1 | Socio activo sin multas y con 0 préstamos; ejemplar libre | Aceptado, fecha de devolución 14 días después, ejemplar no disponible, un préstamo guardado |
| `CP-02` | Caja negra | `HU-03`, criterio 2 | Socio con una multa pendiente | Rechazado e informa las multas; el ejemplar sigue disponible y no se guarda nada |
| `CP-04` | Caja negra, límite | `HU-03`, criterio 2 | Socio con 2 préstamos vigentes (uno menos que el límite) | Aceptado |
| `CP-06` | Caja blanca | `Ejemplar.tomar`, rama de rechazo | 20 pedidos simultáneos del mismo ejemplar libre | Solo uno lo toma; los demás son rechazados (`EC-02`) |

### 5.3 Estructura de una prueba

Cada prueba sigue la estructura de los criterios de aceptación del TP1: se prepara el estado inicial (*Given*), se ejecuta la operación (*When*) y se verifica el resultado (*Then*). El nombre de la prueba dice qué comportamiento verifica, no qué método llama. El ejemplo está en Python con pytest:

```python
def test_rechaza_al_socio_con_multas_y_el_ejemplar_sigue_disponible():
    controlador, ejemplar, prestamos = armar(Socio("s1", multas=1))   # Given
    r = controlador.prestar("s1", "e1")                               # When
    assert not r.aceptado and "multas" in r.motivo                    # Then
    assert ejemplar.disponible and prestamos.guardados == []
```

Reglas: una prueba verifica un solo comportamiento; no depende de otra ni del orden de ejecución; no usa la interfaz gráfica, la red ni el reloj del sistema sin controlarlo.

### 5.4 Desarrollo guiado por pruebas (TDD)

El grupo puede escribir las pruebas antes que el código, con el ciclo del TDD: escribir una prueba que falla, escribir el código mínimo para que pase y mejorar la estructura sin romper las pruebas. No es obligatorio aplicarlo en todo el TP, pero se sugiere probarlo en al menos una operación y comentar en el documento qué se observó.

### 5.5 Ejecución y cobertura

Se ejecutan las pruebas con el framework elegido y se genera el reporte de cobertura con la herramienta correspondiente de ese lenguaje. Por ejemplo, en Python con pytest y el complemento `pytest-cov`:

```bash
pip install pytest pytest-cov
pytest --cov=src --cov-report=term-missing
```

La **cobertura** indica qué porcentaje del código se ejecutó durante las pruebas (según la herramienta, de líneas o de ramas). Los reportes suelen listar, además, lo que no se ejecutó (en el ejemplo, con `term-missing`). Se entrega el reporte y un breve análisis:

- Qué líneas o ramas no quedaron cubiertas y por qué (código de la interfaz gráfica, código que no se pudo probar, falta de tiempo).
- Qué pruebas adicionales se escribieron al ver el reporte.
- Si hubo pruebas que pasan pero verifican poco.

Una cobertura alta no prueba que el código sea correcto: dice qué se ejecutó, no qué se verificó. Se sugiere apuntar a una cobertura de alrededor del 80 % sobre dominio y controladores, y se valora más un reporte analizado que un porcentaje alto sin análisis. La interfaz gráfica se puede excluir del cálculo, indicándolo.

### 5.6 Complejidad ciclomática

**A definir.** La forma en que se usa en la entrega se presenta en la clase del 10/11. Hasta entonces no se pide nada sobre este tema. Lo que sigue es material de apoyo.

**Qué mide.** La complejidad ciclomática de una operación es la cantidad de caminos independientes que tiene el código. Se calcula como la cantidad de decisiones (`if`, ciclos, condiciones combinadas con "y" u "o", casos de un `switch` y manejadores de excepciones) más uno. Sirve para dos cosas:

- **Estimar el esfuerzo de prueba:** es la cantidad mínima de casos de prueba necesaria para cubrir todas las ramas de la operación.
- **Detectar código difícil de entender y de mantener:** como referencia habitual, se considera que una operación con más de 10 conviene dividirla.

| Operación del ejemplo | Decisiones | Complejidad | Casos mínimos |
|---|---|---|---|
| `Socio.motivo_de_rechazo` | 3 (inactivo, con multas, en el límite) | 4 | 4: los tres rechazos y el caso habilitado |
| `ControladorPrestamos.prestar` | 2 (socio rechazado, ejemplar no tomado) | 3 | 3: las dos ramas de rechazo y el éxito |
| `Ejemplar.tomar` | 1 (no disponible) | 2 | 2 |

**Relación con los diagramas.** Cada `alt` o `opt` de un diagrama de secuencia es una decisión en el código. Por eso el diagrama permite estimar la complejidad de un controlador antes de escribirlo, y un controlador con muchas ramas es una señal de que está haciendo trabajo que le corresponde al dominio (controlador obeso).

Existen herramientas que la calculan automáticamente para la mayoría de los lenguajes (por ejemplo, `radon` en Python).

### 5.7 IA en las pruebas

La IA puede proponer casos de prueba y generar pruebas. El grupo debe verificar que las pruebas generadas verifiquen comportamiento real (una prueba que siempre pasa no sirve), que no repitan el código que prueban, y que los casos propuestos cubran los límites y los datos inválidos. Una buena práctica es dar a la IA el criterio de aceptación y pedirle casos de prueba **antes** de mostrarle el código.

---

## 6. Entregable

Todo el resultado se organiza dentro del repositorio del grupo:

- `docs/design/diseno-detallado.md` — documento de diseño detallado, con las secciones del Anexo B.
- `src/` — código fuente organizado según la sección 4.1.
- `tests/` — pruebas unitarias.
- `docs/design/cobertura.md` — reporte de cobertura y su análisis (puede ir como una sección del documento de diseño).
- `README.md` — instrucciones para instalar, ejecutar la interfaz y ejecutar las pruebas.
- `docs/uso-ia.md` — registro del uso de IA, según la sección 7.

---

## 7. Uso de IA

El uso de inteligencia artificial está permitido y forma parte de la consigna. Puede asistir en el diseño (proponer clases, detectar responsabilidades mal asignadas), en la programación y en la generación de pruebas.

La IA suele proponer diseños con más clases, más interfaces y más patrones de los que el problema necesita, y código que funciona pero no respeta el diseño del grupo. Por eso el grupo documenta cada interacción: qué solicitó, qué obtuvo, qué aceptó, modificó o descartó, y por qué. En particular debe verificar que los diagramas generados cumplan las reglas de las secciones 3.4 a 3.6, que el código coincida con el diagrama de clases, y que las pruebas verifiquen comportamiento real. El registro se guarda en `docs/uso-ia.md`.

---

## 8. Checklist de entregables

- [ ] HU seleccionada, con su enunciado, criterios de aceptación y justificación de la elección.
- [ ] Tabla de coherencia (funcionalidad, estructura, calidad y verificación): `EC-xx`, táctica, `DA-xx`, componentes y capas que atraviesa, estilo y patrones.
- [ ] Entidades del modelo de dominio del TP1 que intervienen en la HU, con lo que usa la HU de cada una y, si hizo falta, el cambio al modelo.
- [ ] Análisis tridimensional de la HU.
- [ ] Diagrama de robustez de la HU, que cumple las reglas de la sección 3.4.
- [ ] Un diagrama de secuencia por camino (éxito y rechazos), con las responsabilidades justificadas con GRASP.
- [ ] Un diagrama de clases derivado de los diagramas de secuencia.
- [ ] Justificación del diseño (criterios GRASP y, si los hay, patrones de diseño usados).
- [ ] Verificación de coherencia con la arquitectura (sección 3.8) y, si corresponde, actualización del TP3.
- [ ] Tabla de trazabilidad HU → componente C4 → clases → archivo → pruebas.
- [ ] Código en `src/`, coherente con el diagrama de clases, con persistencia en memoria y servicios simulados detrás de interfaces.
- [ ] Interfaz gráfica mínima que permite ejecutar la HU.
- [ ] Tabla de casos de prueba (caja negra y caja blanca), con su origen.
- [ ] Pruebas automatizadas en `tests/`, ejecutables con el framework elegido (por ejemplo, pytest).
- [ ] Reporte de cobertura y su análisis.
- [ ] `README.md` con las instrucciones para instalar y ejecutar.
- [ ] Registro del uso de IA, según la sección 7.

---

## 9. Instancia de defensa

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

## 10. Checklist final

- [ ] Repositorio actualizado con commits que reflejen el avance de este TP.
- [ ] Los nombres del código coinciden con los del diagrama de clases.
- [ ] El proyecto se instala y se ejecuta siguiendo solo el `README.md`.
- [ ] Las pruebas pasan todas al ejecutarlas desde cero.
- [ ] Diagramas en Mermaid dentro de archivos Markdown.
- [ ] Siglas aclaradas la primera vez que se usan.
- [ ] Grupo en condiciones de defender oralmente cada decisión tomada y de mostrar el sistema andando.

---

## Anexo A. Ejemplo de diseño de una HU (préstamo de un libro)

Se usa un sistema ficticio y cotidiano: una **biblioteca barrial**. No continúa el ejemplo de los TP anteriores; se supone un TP3 mínimo para mostrar cómo se conectan los pasos. Es un ejemplo de formato y de nivel de detalle, no un modelo a copiar: el diseño de cada grupo debe responder a su propio proyecto.

### A.1 Paso 1 — Selección

**HU-03 · Prestar un ejemplar a un socio** (deriva de `CU-02`, slice B). Como bibliotecario/a, quiero registrar el préstamo de un ejemplar a un socio, para controlar qué libros están afuera y cuándo deben volver.

Criterios de aceptación:

- Given un socio activo, sin multas y con menos de 3 préstamos vigentes, y un ejemplar disponible, When el bibliotecario/a confirma el préstamo, Then el sistema registra el préstamo, marca el ejemplar como no disponible y muestra la fecha de devolución (14 días después).
- Given un socio con multas pendientes, inactivo o con 3 préstamos vigentes, When el bibliotecario/a confirma el préstamo, Then el sistema lo rechaza e informa el motivo.
- Given un ejemplar que ya está prestado (incluso por otro bibliotecario/a al mismo tiempo), When el bibliotecario/a confirma el préstamo, Then el sistema lo rechaza e informa que el ejemplar no está disponible.

**Tabla de coherencia** (con el TP3 supuesto de este ejemplo: aplicación web, API y base de datos, con patrón de capas en la API):

| Dimensión | Contenido |
|---|---|
| Funcionalidad | `HU-03` Prestar un ejemplar; camino principal y dos rechazos (socio no habilitado, ejemplar no disponible) |
| Estructura | Contenedor API, componentes «Controladores», «Servicio de préstamos» y «Acceso a datos»; patrón de capas |
| Calidad | `EC-02` integridad: dos préstamos simultáneos del mismo ejemplar. Medida: 0 ejemplares con dos préstamos vigentes en 100 intentos simultáneos. Táctica: operación atómica y transacción en el acceso a datos (`DA-02`) |
| Dominio | Entidades del modelo del TP1 que intervienen: `Socio`, `Ejemplar` y `Prestamo` (ver abajo) |
| Verificación | Prueba con 20 pedidos simultáneos del mismo ejemplar: solo uno se concreta |

**Entidades del modelo de dominio que intervienen.** Este es el modelo de dominio supuesto del TP1; en verde, las entidades que "pegan" con la HU:

```mermaid
classDiagram
    class Socio
    class Multa
    class Libro
    class Autor
    class Ejemplar
    class Prestamo
    Socio "1" --> "0..*" Prestamo : realiza
    Socio "1" --> "0..*" Multa : tiene
    Libro "1" --> "1..*" Ejemplar : tiene copias
    Libro "*" --> "1..*" Autor : escrito por
    Ejemplar "1" --> "0..*" Prestamo : se presta en
    style Socio fill:#dcfce7,stroke:#15803d
    style Ejemplar fill:#dcfce7,stroke:#15803d
    style Prestamo fill:#dcfce7,stroke:#15803d
```

| Entidad del modelo (TP1) | ¿Interviene? | Qué usa la HU de ella | La HU la... |
|---|---|---|---|
| `Socio` | Sí | Si está activo, sus multas pendientes y sus préstamos vigentes (con eso decide si puede retirar) | Consulta y modifica (suma un préstamo) |
| `Ejemplar` | Sí | Si está disponible | Consulta y modifica (lo marca como prestado) |
| `Prestamo` | Sí | Fecha de préstamo y de devolución | Crea |
| `Multa` | No | La HU solo necesita saber si hay multas pendientes, dato que expone `Socio` | — |
| `Libro` | No | El préstamo es de un ejemplar concreto; el título no interviene en la lógica | — |
| `Autor` | No | No se usa | — |

En este ejemplo el modelo de dominio no necesitó cambios. Si la HU hubiera pedido, por ejemplo, conservar el historial de renovaciones de un préstamo, se agregaría esa entidad al modelo del TP1 y se anotaría el cambio.

### A.2 Paso 2 — Análisis tridimensional

| Dimensión | Elemento | Detalle |
|---|---|---|
| Funcionalidad | Criterio 1 | Si el socio puede retirar y el ejemplar está libre, registrar el préstamo y mostrar la fecha de devolución |
| Funcionalidad | Criterio 2 | Si el socio no puede retirar (inactivo, con multas o en el límite de préstamos), rechazar e informar el motivo |
| Funcionalidad | Criterio 3 | Si el ejemplar ya está prestado, rechazar e informar que no está disponible |
| Estructura | Frontera | Pantalla de préstamo |
| Estructura | Control | Un controlador de préstamos y los repositorios de socios, ejemplares y préstamos |
| Estructura | Dominio | `Socio` (sabe si puede retirar), `Ejemplar` (sabe si está disponible) y `Prestamo` (sabe cuándo vence) |
| Calidad | `EC-02` | Dos préstamos simultáneos del mismo ejemplar: solo uno se concreta |

### A.3 Paso 3 — Diagrama de robustez

Leyenda: borde punteado = actor; rectángulo redondeado azul = boundary; círculo naranja = controller; rectángulo con barras verde = entity.

```mermaid
flowchart LR
    bib["Bibliotecario/a<br/>(actor)"]
    ui(["«boundary»<br/>PantallaPrestamo"])
    cp(("«controller»<br/>ControladorPrestamos"))
    rs(("«controller»<br/>RepositorioSocios"))
    re(("«controller»<br/>RepositorioEjemplares"))
    rp(("«controller»<br/>RepositorioPrestamos"))
    so[["«entity»<br/>Socio"]]
    ej[["«entity»<br/>Ejemplar"]]
    pr[["«entity»<br/>Prestamo"]]
    bib --> ui
    ui --> cp
    cp --> rs
    cp --> re
    cp --> rp
    rs --> so
    re --> ej
    rp --> pr
    cp --> so
    cp --> ej
    cp --> pr
    classDef actor fill:#f3f4f6,stroke:#4b5563,color:#111827,stroke-dasharray: 4 3
    classDef boundary fill:#dbeafe,stroke:#1d4ed8,color:#0f172a
    classDef controller fill:#ffedd5,stroke:#c2410c,color:#0f172a
    classDef entity fill:#dcfce7,stroke:#15803d,color:#0f172a
    class bib actor
    class ui boundary
    class cp,rs,re,rp controller
    class so,ej,pr entity
```

Las tres entidades salen de la tabla del paso 1. Se verifican las reglas de la sección 3.4: el actor solo toca la pantalla, la pantalla solo toca al controlador, y ninguna entidad se accede desde una frontera. Cada elemento pertenece a un componente del TP3: la pantalla a la aplicación web, el controlador y las entidades a «Servicio de préstamos» y los repositorios a «Acceso a datos».

### A.4 Paso 4 — Diagramas de secuencia

Se dibujan dos secuencias con los mismos participantes: una para el camino de éxito y otra para los rechazos.

**Secuencia A: camino de éxito**

```mermaid
sequenceDiagram
    actor Bib as Bibliotecario/a
    participant UI as PantallaPrestamo
    participant CP as ControladorPrestamos
    participant RS as RepositorioSocios
    participant S as Socio
    participant RE as RepositorioEjemplares
    participant E as Ejemplar
    participant RP as RepositorioPrestamos
    Bib->>UI: confirma el préstamo
    UI->>CP: prestar(socio_id, ejemplar_id)
    CP->>RS: socio(socio_id)
    RS-->>CP: socio
    CP->>S: motivo_de_rechazo()
    S-->>CP: nada, puede retirar
    CP->>RE: ejemplar(ejemplar_id)
    RE-->>CP: ejemplar
    CP->>E: tomar()
    E-->>CP: tomado
    create participant P as Prestamo
    CP->>P: Prestamo(socio_id, ejemplar_id, hoy)
    CP->>S: registrar_prestamo()
    CP->>RP: guardar(prestamo)
    CP-->>UI: Respuesta(aceptado, fecha_devolucion)
    UI-->>Bib: muestra la fecha de devolución
```

**Secuencia B: caminos de rechazo**

```mermaid
sequenceDiagram
    actor Bib as Bibliotecario/a
    participant UI as PantallaPrestamo
    participant CP as ControladorPrestamos
    participant RS as RepositorioSocios
    participant S as Socio
    participant RE as RepositorioEjemplares
    participant E as Ejemplar
    Bib->>UI: confirma el préstamo
    UI->>CP: prestar(socio_id, ejemplar_id)
    CP->>RS: socio(socio_id)
    RS-->>CP: socio
    CP->>S: motivo_de_rechazo()
    alt el socio no puede retirar
        S-->>CP: motivo
        CP-->>UI: Respuesta(rechazado, motivo)
        UI-->>Bib: muestra el motivo
    else el socio puede retirar
        S-->>CP: nada
        CP->>RE: ejemplar(ejemplar_id)
        RE-->>CP: ejemplar
        CP->>E: tomar()
        alt el ejemplar ya estaba prestado
            E-->>CP: no tomado
            CP-->>UI: Respuesta(rechazado, no disponible)
            UI-->>Bib: informa que no está disponible
        end
    end
```

Asignación de responsabilidades:

| Responsabilidad | Quién | Criterio |
|---|---|---|
| Decidir si el socio puede retirar | `Socio` | Experto en información: conoce sus multas y sus préstamos vigentes |
| Verificar y marcar el ejemplar como prestado en un solo paso | `Ejemplar` | Experto en información; además resuelve `EC-02`, porque la operación es indivisible |
| Calcular la fecha de devolución | `Prestamo` | Experto en información: conoce su fecha de inicio y el plazo |
| Crear el préstamo | `ControladorPrestamos` | Creador: tiene el socio y el ejemplar elegidos |
| Coordinar el flujo | `ControladorPrestamos` | Controlador |
| Obtener y guardar | Repositorios | Alta cohesión y bajo acoplamiento: el controlador no sabe cómo se guarda |

### A.5 Paso 5 — Modelo de clases

```mermaid
classDiagram
    class PantallaPrestamo {
        +confirmar(socio_id, ejemplar_id)
        +mostrar(respuesta)
    }
    class ControladorPrestamos {
        -socios: RepositorioSocios
        -ejemplares: RepositorioEjemplares
        -prestamos: RepositorioPrestamos
        +prestar(socio_id, ejemplar_id) Respuesta
    }
    class RepositorioSocios {
        <<interface>>
        +socio(socio_id) Socio
    }
    class RepositorioEjemplares {
        <<interface>>
        +ejemplar(ejemplar_id) Ejemplar
    }
    class RepositorioPrestamos {
        <<interface>>
        +guardar(prestamo)
    }
    class RepositorioSociosEnMemoria
    class RepositorioEjemplaresEnMemoria
    class RepositorioPrestamosEnMemoria
    class Socio {
        -activo: bool
        -multas: int
        -prestamos_vigentes: int
        +motivo_de_rechazo() str
        +registrar_prestamo()
    }
    class Ejemplar {
        -disponible: bool
        +tomar() bool
    }
    class Prestamo {
        +socio_id
        +ejemplar_id
        +fecha_prestamo: date
        +fecha_devolucion() date
    }
    class Respuesta {
        +aceptado: bool
        +motivo: str
        +fecha_devolucion: date
    }
    PantallaPrestamo --> ControladorPrestamos
    ControladorPrestamos --> RepositorioSocios
    ControladorPrestamos --> RepositorioEjemplares
    ControladorPrestamos --> RepositorioPrestamos
    ControladorPrestamos ..> Socio : consulta
    ControladorPrestamos ..> Ejemplar : toma
    ControladorPrestamos ..> Prestamo : crea
    ControladorPrestamos ..> Respuesta : devuelve
    RepositorioSociosEnMemoria ..|> RepositorioSocios
    RepositorioEjemplaresEnMemoria ..|> RepositorioEjemplares
    RepositorioPrestamosEnMemoria ..|> RepositorioPrestamos
```

### A.6 Código (fragmento)

El ejemplo está en Python, pero nada del diseño depende del lenguaje: las clases, las interfaces y las pruebas se escriben igual en Java, JavaScript, C# u otro.

```python
# src/aplicacion/controlador_prestamos.py
class ControladorPrestamos:
    def __init__(self, socios, ejemplares, prestamos, hoy=date.today):
        self._socios = socios
        self._ejemplares = ejemplares
        self._prestamos = prestamos
        self._hoy = hoy

    def prestar(self, socio_id: str, ejemplar_id: str) -> Respuesta:
        socio = self._socios.socio(socio_id)
        motivo = socio.motivo_de_rechazo()
        if motivo:
            return Respuesta(False, motivo)
        ejemplar = self._ejemplares.ejemplar(ejemplar_id)
        if not ejemplar.tomar():
            return Respuesta(False, "el ejemplar no está disponible")
        prestamo = Prestamo(socio_id, ejemplar_id, self._hoy())
        socio.registrar_prestamo()
        self._prestamos.guardar(prestamo)
        return Respuesta(True, None, prestamo.fecha_devolucion)
```

```python
# src/dominio/ejemplar.py
class Ejemplar:
    def __init__(self, id: str, titulo: str):
        self.id, self.titulo = id, titulo
        self._disponible = True
        self._lock = Lock()

    def tomar(self) -> bool:
        with self._lock:                # verifica y marca en un solo paso (EC-02)
            if not self._disponible:
                return False
            self._disponible = False
            return True
```

### A.7 Trazabilidad y pruebas

| Criterio / escenario | Caso de prueba | Prueba |
|---|---|---|
| Criterio 1 | `CP-01` | `test_presta_el_ejemplar_y_fija_la_fecha_de_devolucion` |
| Criterio 2, multas | `CP-02` | `test_rechaza_al_socio_con_multas_y_el_ejemplar_sigue_disponible` |
| Criterio 2, límite | `CP-03` | `test_rechaza_al_socio_que_alcanzo_el_limite` |
| Criterio 2, borde | `CP-04` | `test_en_el_borde_con_dos_prestamos_todavia_puede_retirar` |
| Criterio 3 | `CP-05` | `test_rechaza_si_el_ejemplar_ya_esta_prestado` |
| `EC-02` | `CP-06` | `test_dos_prestamos_simultaneos_del_mismo_ejemplar_solo_concretan_uno` |

---

## Anexo B. Estructura del documento de diseño detallado

| Sección | Qué contiene |
|---|---|
| 1. Introducción | Propósito, HU elegida, motivo de la elección y siglas usadas |
| 2. Relación con la arquitectura | Tabla de coherencia: `EC-xx`, táctica y `DA-xx`; componentes y capas que atraviesa; estilo y patrones; verificación de coherencia (sección 3.8) |
| 3. Diseño de la HU | Enunciado y criterios, entidades del modelo de dominio que intervienen, análisis tridimensional, diagrama de robustez, diagramas de secuencia (uno por camino) con la asignación de responsabilidades |
| 4. Modelo de clases | Un diagrama derivado de todas las secuencias |
| 5. Justificación del diseño | Asignación de responsabilidades (GRASP), decisiones de diseño y patrones de diseño usados, si los hay |
| 6. Implementación | Estructura del código, cómo se ejecuta y cómo se reemplazan la persistencia y los servicios externos |
| 7. Pruebas | Tabla de casos de prueba, resultados y análisis de cobertura |
| 8. Trazabilidad | HU → componente C4 → clases → archivo → pruebas |
| 9. Glosario y bibliografía | Siglas y términos, y referencias |

---

## Anexo C. Siglas usadas

| Sigla | Significado |
|---|---|
| API | Interfaz de programación de aplicaciones: las operaciones que un programa ofrece a otros |
| C4 | Modelo de documentación de arquitectura en cuatro niveles: contexto, contenedores, componentes y código |
| CP | Caso de prueba |
| DA | Decisión de arquitectura |
| EC | Escenario de calidad |
| GoF | *Gang of Four*: los cuatro autores del libro clásico de patrones de diseño |
| GRASP | Patrones generales para asignar responsabilidades (*general responsibility assignment software patterns*) |
| GWT | Given-When-Then: formato de los criterios de aceptación |
| HU | Historia de usuario |
| IA | Inteligencia artificial |
| TDD | Desarrollo guiado por pruebas (*test-driven development*) |
| TP | Trabajo práctico |
| UML | Lenguaje unificado de modelado |

---

## Bibliografía

- Valotto, V. *Diseño tridimensional de software*. 2025. Incluye el material de clase aplicado a un caso real (carga de una pregunta de opción múltiple): análisis de funcionalidad, estructura y calidad; diagramas de robustez, de secuencia y de clases.
- Rosenberg, D. y Stephens, K. *Use Case Driven Object Modeling with UML: Theory and Practice*. Apress, 2007. Antecedente del diagrama de robustez.
- Larman, C. *Applying UML and Patterns: An Introduction to Object-Oriented Analysis and Design and Iterative Development*. Prentice Hall. Referencia para los criterios GRASP.
- Gamma, E., Helm, R., Johnson, R. y Vlissides, J. *Design Patterns: Elements of Reusable Object-Oriented Software*. Addison-Wesley.
- Documentación del framework de pruebas y de la herramienta de cobertura del lenguaje elegido (por ejemplo, pytest y pytest-cov).
