Ej1: Explique la programación estructurada:

La programación estructurada es una metodología a seguir que lo que trata de lograr es que no haya diferencias estructurales entre un programa estático y uno dinámico. Es decir, un programa estático se ejecuta "por una linea a la vez y en orden de texto", el objetivo es que un programa dinámico se comporte lo más similar a eso.

Respuesta de GPT: La programación estructurada es una disciplina que construye programas solo con secuencia, selección e iteración (bloques con una entrada/una salida), sin goto, de modo que la estructura del código refleje el flujo de ejecución. Esto mejora legibilidad, verificación y testeo.

Ej2: Describa el proceso de codificación: Desarrollo dirigido por test.

El TDD (Test Driven Development) es un proceso de codificación que hace invierte la en cierto modo la estructura del proceso incremental clásico. En primer lugar se necesita tener las especificaciones del trabajo, una vez las tengamos creamos test que prueben esas especificaciones. Luego de tener los test, escribimos código para que puedan pasar esos test, posteriormente se corren los scripts de tests. Si hubo errores volvemos a modificar el código, si no los hubo nos preguntamos si hace falta refactorizarlo. Si hace falta que lo refactoricemos entonces volvemos a la sección de escribir código, si no hace falta nos preguntamos si cumple con las especificaciones. Si cumple entonces terminamos, si no cumple volvemos a escribir tests.

Respuesta de GPT: En TDD se avanza en ciclos Red–Green–Refactor: (1) escribir un test que falle para el próximo comportamiento, (2) escribir el mínimo código para pasarlo, y (3) refactorizar sin romper la suite. Se repite test por test hasta completar la historia. Los tests guían el diseño y funcionan como oráculo de regresión.

Cuadro de TDD a modo de código:

void TDD(){
    Specification of the module;
    Write/add test for some functionality;
    Add code to pass test;
    Run test;
    if (errors){
        Fix;
        goto RunTest;
    }
    if (Code requires improvements){
        Improve code;
        goto Run test;
    }
    if (!All specs are coevered){
        goto Write/add test for some functionality;
    }
    Exit
}

Ej3: Describa exhaustivamente el modelo COCOMO.

COCOMO (Constructive Cost Model) es una estimación del costo de producción de sw, normalmente calculado en persona/mes. Inicialmente se debe estimar el tamaño del proyecto, usualmente en KLOC, luego se establece si es un proyecto orgánico, semirígido o rígido. Orgánico es un proyecto pequeño que no requiere gran organización, rígido son proyectos grandes que requieren mucha preparación y análisis, y semirígido es un termino medio entre los dos. La estimación se calcula con la formula a * tamaño^b con a y b constantes establecidas por el tipo de proyecto. Luego el resultado se corrige por un factor de corrección que es productoria de 1 a 15 de fk. Donde fk son distintos factores como RELY (confianza en el proyecto) o TIME (capacidad del CPU).

Respuesta de GPT:

# COCOMO (Constructive Cost Model) — versión “examen”

## Idea central (frasecita)

Modelo empírico que **estima esfuerzo** de desarrollo en **persona-mes (PM)** a partir del **tamaño** (KLOC) y **ajustes por factores de costo**; de ahí se deriva **calendario** y **plan por fases**.

## Supuestos y pasos

1. **Insumo inicial: tamaño** del software (**KLOC**) → puede obtenerse por históricos o convertir desde **Function Points**.

2. **Modo del proyecto:**

   * **Orgánico**: pequeño/estable, equipo con experiencia y requisitos conocidos.
   * **Semi-rígido**: mediano, mezcla de experiencia y restricciones.
   * **Rígido**: grande/estricto, alta criticidad y fuertes restricciones HW/SW/estándares.

3. **Estimador inicial (A):** esfuerzo base
   [
   E_0 ;=; a\cdot(\text{KLOC})^{,b}
   ]
   con ((a,b)) según el modo (valores típicos usados en la cátedra):

   * **Orgánico:** (a=3.2,; b=1.05)
   * **Semi-rígido:** (a=3.0,; b=1.12)
   * **Rígido:** (a=2.8,; b=1.20)

4. **Factores de costo (B):** **15 multiplicadores** (f_k) (software, hardware, personal, proyecto). El **esfuerzo ajustado** es:
   [
   E ;=; E_0 \cdot \prod_{k=1}^{15} f_k
   ]
   **Ejemplos (y qué significan):**

   * **RELY** (*required reliability*): confiabilidad requerida del producto (↑ confiabilidad ⇒ ↑ esfuerzo).
   * **DATA**: tamaño de BD interna.
   * **CPLX**: complejidad del producto.
   * **TIME**: restricción de **tiempo de CPU**/performance (plazos de respuesta/throughput estrictos ⇒ ↑ esfuerzo).
   * **STOR**: restricción de memoria.
   * **VIRT/TURN**: entorno de ejecución y turnaround.
   * **ACAP/PCAP/AEXP/VEXP/LEXP**: capacidades/experiencia del equipo.
   * **MODP/TOOL**: modernidad del proceso/herramientas.
   * **SCED**: compresión de cronograma.

5. **Calendario (C):** duración en meses (M). Fórmulas de uso común:

   * **COCOMO (calendario):** ( M = 2.5 \cdot E^{0.38} )
   * (A veces también se muestra **IBM**: ( M = 4.1\cdot E^{0.36} ))
     **Tamaño de equipo** aproximado: ( N \approx \dfrac{E}{M} ).

6. **Distribución por fases (D):** repartir (E) en **diseño de producto / diseño detallado / codificación+TU / integración+test** con **porcentajes** que dependen del modo/tamaño (la tabla de la cátedra). Esto da **plan y cronograma** detallados.

---

## Qué corregir de tu texto

* **Definiciones de factores**:

  * **RELY** = **confiabilidad requerida** del **producto** (no “confianza en el proyecto”).
  * **TIME** = **restricción de tiempo de CPU / performance**, no “capacidad del CPU”.


Ej4: ¿Qué es y para qué sirve el oráculo de test? ¿Qué son y para qué sirven los criterios de selección de tests? ¿Cuál es la diferencia entre testing de caja blanca y el testing de caja negra?

El oráculo de test es una entidad que sabe cuál es el resultado esperado para una entrada dada. Sirve para poder comparar los programas que están siendo testeados y determinar si los test dieron algún fallo.
Los criterios de selección de test son una serie de pasos que nos permiten establecer una cantidad determinada de tests, para que haya una covertura significativa.
El testing de caja blanca testea todas las ramas del código, mientras que el testing de caja negra es totalmente funcional y no le interesa el código interno, sólo evalúa la entrada y la salida de una función.

Respuesta de GPT:

Oráculo: mecanismo que define el resultado esperado y decide pass/fail (especificación, golden master, propiedades, aserciones). Sirve para verificar automática y objetivamente cada test.

Criterios de selección: reglas para elegir una batería finita de tests eficaz y manejable (equivalencias, límites, pairwise; cobertura de sentencias/ramas/def-use). Sirven para maximizar detección de defectos con esfuerzo acotado.

Caja negra vs blanca: negra = desde requisitos (entradas/salidas, sin mirar código); blanca = desde la estructura interna (control/datos, metas de cobertura). Se complementan.

Ej5: Describa el proceso de inspección.

El proceso de inspección es tiene como objetivo detectar los defectos en los productos de trabajo mas no necesariamente corregirlos. Se siguen una serie de pasos, primero determinamos el poducto que vamos a revisar y se asignan los roles (moderador, autor, revisor,lector, escriba). Todos los participantes hacen previamente una revisión induvidual y luego preparan una reunion grupal. Se revisa el producto y se anotan todos los desperfectos. El autor luego es el encargado de arreglarlos y el moderador decide si aprobarlo o mandarlo a revisión nuevamente.


Respuesta de GPT:
Inspección: proceso estructurado de revisión por pares para detectar (no solucionar) defectos en artefactos (SRS, diseño, código, casos de test).
Roles: moderador (conduce), autor (aclara), revisores (detectan), lector (guía la lectura), escriba (registra).
Fases (ETVX):
Entry: paquete listo (artefacto, especificación, checklist, estándar) y equipo asignado.
Task: (1) preparación individual con checklist; (2) reunión guiada por el lector: se registran defectos sin debatir soluciones; (3) reporte con lista y métricas.
Verification: moderador verifica criterios de entrada (todos prepararon), control del tiempo y del foco (encontrar defectos).
Exit: se decide aceptar o reinspeccionar tras retrabajo del autor; el moderador cierra al comprobar correcciones.
Métricas: nº y severidad de defectos, tasa (defectos/hora), áreas problemáticas → mejora del proceso.

Ej6: ¿Qué es ETVX?


**ETVX** es un esquema para **definir y controlar procesos** de ingeniería de software. Ordena cada proceso en cuatro partes, haciendo explícitos **qué necesito para empezar, qué hago, cómo verifico lo hecho y cuándo puedo darlo por terminado**:

* **E — Entry (Entradas):** **precondiciones** e **insumos** requeridos (artefactos, roles asignados, herramientas, baseline).
* **T — Task (Tareas):** **pasos concretos** del proceso y **productos intermedios** que se generan.
* **V — Verification (Verificación):** **controles y criterios** para comprobar calidad/cumplimiento (revisiones, métricas, checklists).
* **X — eXit (Salida):** **entregables** y **criterios de salida** que habilitan pasar a la fase siguiente (go/no-go).

**Para qué sirve:** elimina ambigüedades, **estandariza** la ejecución, facilita **auditoría y medición**, mejora la **trazabilidad entre fases** y soporta la **mejora continua** del proceso.

**Mini-ejemplo (diseño de tests):**
E: SRS aprobada y criterios de aceptación.
T: clases de equivalencia, valores límite, especificar oráculos.
V: revisión por pares y cobertura mínima acordada.
X: casos de prueba versionados y datos listos para ejecución.

Ej7:
¿Qué es y para qué sirve la refactorización de código? Explique completamente los tipos más comunes y mencione al menos un ejemplo para cada uno de ellos.

Refactorización es la técnica de modificar internamente el código sin cambiar su comportamiento observable, para mejorar el diseño: legibilidad, cohesión, bajo acoplamiento, menor complejidad, y mayor facilidad de prueba y cambio.
Sirve para: reducir deuda técnica, bajar la complejidad ciclomatica, eliminar duplicación, hacer el código más mantenible y testable.
Cómo se hace bien: en pasos pequeños, con tests en verde (idealmente TDD): aplico un refactor → corro la suite → todo sigue pasando.

- Extract Method (extraer método)
- Rename (renombrar símbolo)
- Extract Variable / Introduce Explaining Variable (variable explicativa)
- Inline Method (inlinear método)
- Replace Temp with Query (reemplazar temporales por consultas)
- Introduce Parameter Object (objeto parámetro / data class)
- Replace Conditional with Polymorphism (condicional → polimorfismo)
- Decompose Conditional (descomponer condicional)
- Consolidate Duplicate Conditional Fragments (consolidar duplicados en condicionales)
- Move Method / Move Field (mover método/campo)
- Replace Magic Number with Symbolic Constant (constante simbólica)
- Encapsulate Field / Encapsulate Collection (encapsular campo/colección)
- Extract Class / Inline Class (extraer/inlinear clase)
- Pull Up / Push Down Method or Field (subir/bajar a super/subclase)
- Replace Loop with Pipeline (map/filter/reduce)
- Introduce Guard Clauses (cláusulas de guarda)

Ej8: Explique el testing de caja blanca de cobertura de ramificaciones. Dé un ejemplo en el que un error pueda ser encontrado por el criterio de cobertura de ramificaciones y no por el de cobertura de sentencia.

¡Respuesta de examen! 👇

# Cobertura de **ramificaciones** (caja blanca)

**Qué es:** criterio estructural que exige ejecutar **cada resultado** de **cada decisión** al menos una vez (todos los **verdaderos** y todos los **falsos** de cada `if`, cada rama de un `switch`, cada salida de un bucle, etc.).
**Para qué sirve:** detectar errores que aparecen sólo en **alguna** rama (p. ej., condiciones mal formuladas, ramas sin inicializar, `else` faltante, short-circuit no previsto).
**Relación con sentencias:** la cobertura de **ramas** suele **subsumir** (superar) a la cobertura de **sentencias** en código estructurado: podés tener 100% de **sentencias** sin haber ejercitado **todas** las decisiones en ambos sentidos.

---

# Ejemplo donde **ramas** encuentra un error y **sentencias** no

Código (C-like):

```c
int foo(int x) {
    int y;                 // (1)
    if (x >= 0)            // (2) decisión
        y = x;             // (3)
    // BUG: falta else -> y queda sin inicializar si x < 0
    return y;              // (4)
}
```

* **Con cobertura de sentencias**: un único caso `x = 5` ejecuta (1)–(4).
  Resultado: **100% sentencias** (todas las líneas ejecutadas al menos una vez) y **no** se detecta el bug.
* **Con cobertura de ramificaciones**: necesitás dos casos, uno con `x >= 0` y otro con `x < 0`.
  Con `x = -1` se toma la **rama falsa** del `if` y `y` se retorna **sin inicializar** → **falla** detectada.

> Moral: ejecutar “todas las líneas” no garantiza haber probado **ambos resultados** de cada decisión; la rama no recorrida puede esconder el defecto.

---

## Mini-checklist para contestar

* Definí “ramas”: **cada resultado** de **cada decisión**.
* Decí el **objetivo**: cubrir **True/False** (o todas las salidas) para revelar errores lógicos.
* Contrastá con **sentencias**: puede pasar 100% sentencias y **no** cubrir una rama → riesgo.
* Dalo con un **ejemplo** como el de variable no inicializada / `else` faltante (o un `switch` con `default` incorrecto).


Ej9: Describa exhaustivamente la Administración de Riesgos.


# Administración de Riesgos — qué es y para qué sirve

**Qué es:** conjunto de actividades para **reducir la probabilidad** de fracaso del proyecto y **minimizar el impacto** si eventos inciertos ocurren. Un **riesgo** es “condición/evento incierto que puede causar la falla del proyecto”. **Objetivo:** bajar el impacto en **costos, calidad y tiempos** cuando los riesgos se materializan. 

---

# Proceso (fases y artefactos)

## 1) Planeamiento de la gestión de riesgos

Definís **cómo** vas a gestionar: fuentes, responsables, criterios de probabilidad/impacto, formato del **registro de riesgos**, y ritmo de revisión. (La cátedra lo presenta dentro de “Administración del riesgo: Evaluación + Control” y distingue actividades de **planeamiento** vs **ejecución/seguimiento**). 

## 2) Identificación

Listar **posibles riesgos** mediante checklists, lecciones aprendidas, *brainstorming* (“¿qué pasaría si…?”), etc. (se construye el **registro de riesgos** con descripción, causas, disparadores). 

> **9 factores frecuentes** (ejemplos que la cátedra remarca): **personal** no entrenado; **tiempos/costos irreales**; **componentes externas** incompatibles; **discrepancias** con requerimientos o **UI**; **arquitectura/desempeño** mal evaluados; **cambios continuos**; **software legado**; **tareas tercerizadas** demoradas. 

## 3) Análisis y priorización

Para cada riesgo, estimar **probabilidad** y **impacto**, y calcular el **RE (Risk Exposure)** = probabilidad × impacto (valor esperado de la pérdida). Priorizás y enfocás mitigación en los **RE más altos**. 

> **Matriz probabilidad–impacto**: clasificar **Bajo/Medio/Alto** en ambos e **identificar AA y AM/MA** para concentrar esfuerzos (técnica eficaz en proyectos chicos/medianos). 

## 4) Plan de respuesta (control de riesgos)

Estrategias:

* **Evitar**: cambiar el plan para eliminar el riesgo (p. ej., usar **hardware ya verificado** en lugar del nuevo). 
* **Mitigar**: **reducir probabilidad/impacto** con acciones planificadas (tienen **costo extra** y **cronograma**).  
* **Transferir/Aceptar**: si aplica (seguro, contrato; o aceptación con **planes de contingencia**).

**Ejemplos de mitigación (que pueden preguntarte):**

* *Demasiados cambios de requerimientos*: procedimiento formal de cambios, visibilizar impacto acumulado, negociar pagos por esfuerzo real. 
* *Desgaste del personal*: múltiples recursos en áreas clave, *team building*, rotación de tareas, *backup*, documentación, seguir proceso de cambios. 
* *Planificación irreal*: renegociar tiempos, paralelizar tareas, alistar recursos temprano, automatizar, renegociar camino crítico, pagos por esfuerzo real. 

> **Plan de mitigación**: lista de **pasos concretos**, costeados y **calendarizados**; **distintos** de las **acciones de contingencia** (que solo se ejecutan **si** el riesgo ocurre). **Revisión periódica**. 

## 5) Seguimiento y control

Durante la ejecución: **monitorear** disparadores, actualizar el **registro**, verificar que se ejecutan las **mitigaciones**, y decidir **retrabajos**. (La cátedra liga esto con el **seguimiento del proyecto**: medir tiempo, esfuerzo, defectos, tamaño, y tomar acciones correctivas).  

---

# Qué te pueden pedir “de memoria”

* **Definición de riesgo** y **objetivo** de la gestión. 
* **Fases**: identificación → análisis/priorización (RE) → plan de respuesta (evitar/mitigar/transferir/aceptar) → seguimiento. 
* **Matriz prob–impacto** y **RE** (fórmula).  
* **Ejemplos concretos** de mitigación (requisitos cambiantes, desgaste, tiempos irreales).   
* **Plan de mitigación** vs **contingencia** y **revisiones periódicas**. 

Con esto tenés una respuesta exhaustiva, alineada a las filminas de “Planeamiento”. ¿Querés que te deje una **plantilla de registro de riesgos** (ID, causa, disparador, prob, impacto, RE, estrategia, dueño, fecha de revisión)?

