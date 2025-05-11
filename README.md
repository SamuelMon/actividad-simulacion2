# Actividad de seguimiento - Simulación 2

| Integrante                | correo                     | usuario github |
| ------------------------- | -------------------------- | -------------- | --- |
| Sofia Vanegas Cordoba     | sofia.vanegasc@udea.edu.co | Sofito-code    |
| Samuel David Montoya Cano | samuel.montoya@udea.edu.co | SamuelMon      | .   |

## Instrucciones

Antes de empezar a realizar esta actividad haga un **fork** de este repositorio y sobre este trabaje en la solución de las preguntas planteadas en la actividad de simulación. Las respuestas deben ser respondidas en español o si lo prefiere en ingles en el lugar señalado para ello (La palabra **answer** muestra donde).

## Homework (Simulation)

This program, [mlfq.py](mlfq.py), allows you to see how the MLFQ scheduler presented in this chapter behaves. See the [README](https://github.com/remzi-arpacidusseau/ostep-homework/blob/master/cpu-sched-mlfq/README.md) for details.

### Questions

1. Run a few randomly-generated problems with just two jobs and two queues; compute the MLFQ execution trace for each. Make your life easier by limiting the length of each job and turning off I/Os.

<details> <summary>Answer</summary> Se ejecutaron varios experimentos con 2 trabajos y 2 colas, sin operaciones de E/S (opción -M 0 para desactivarlas). Se observaron las trazas de ejecución para verificar el comportamiento de MLFQ bajo estas condiciones. Los resultados muestran cómo los trabajos cambian de prioridad al agotar su quantum y cómo el scheduler da preferencia al trabajo en la cola de mayor prioridad. </details> <br>
2. How would you run the scheduler to reproduce each of the examples in the chapter?

<details> <summary>Answer</summary> Para reproducir ejemplos del capítulo, se deben configurar manualmente las colas (-Q), los allotments (-A) y las características de los trabajos (-l). Por ejemplo, -Q 5,10 define una cola de alta prioridad con quantum 5 y otra con quantum 10. Con -l, se especifican los trabajos (tiempo de llegada, duración y frecuencia de E/S). </details> <br>
3. How would you configure the scheduler parameters to behave just like a round-robin scheduler?

<details> <summary>Answer</summary> Para simular un Round Robin, se usa solo una cola (-n 1) con un quantum fijo (-q). Sin allotments ni reglas de degradación, todos los trabajos se ejecutan de manera cíclica, recibiendo turnos iguales de CPU. </details> <br>
4. Craft a workload with two jobs and scheduler parameters so that one job takes advantage of the older Rules 4a and 4b (turned on with the -S flag) to game the scheduler and obtain 99% of the CPU over a particular time interval.

<details> <summary>Answer</summary> Se diseñó un escenario con dos trabajos. Uno de ellos (JOB 1) emite E/S con frecuencia (ioFreq=3), y con la opción -S, se mantiene en la misma cola de alta prioridad. El otro trabajo (JOB 0) es largo y sin E/S. Esto permite que JOB 1 acapare hasta el 99% del CPU durante ciertos intervalos. </details> <br>
5. Given a system with a quantum length of 10 ms in its highest queue, how often would you have to boost jobs back to the highest priority level (with the -B flag) in order to guarantee that a single longrunning (and potentially-starving) job gets at least 5% of the CPU?

<details> <summary>Answer</summary> Probando con boosts cada 100 ms (-B 100), el trabajo largo obtiene CPU con suficiente frecuencia para lograr al menos el 5% del uso total. Sin boosts, este trabajo sería postergado indefinidamente por los trabajos interactivos. </details> <br>
6. One question that arises in scheduling is which end of a queue to add a job that just finished I/O; the -I flag changes this behavior for this scheduling simulator. Play around with some workloads and see if you can see the effect of this flag.

<details> <summary>Answer</summary> Al jugar con la opción -I, se observa que cambiar el punto de reinserción de un trabajo tras E/S (al principio o al final de la cola) afecta significativamente la latencia de respuesta de trabajos interactivos. Insertarlos al principio favorece tiempos de respuesta rápidos. </details> <br>

## Conclusions

Se observó cómo la planificación MLFQ permite dar prioridad a procesos interactivos y degradar la prioridad de trabajos CPU-intensivos. El uso de flags como `-S`, `-I` y `-B` permite modelar diferentes políticas del planificador. Entender y manipular estos parámetros ayuda a simular comportamientos reales de un sistema operativo y cómo se pueden mitigar o provocar fenómenos como el _starvation_.

### Criterios de evaluación

- [x] Despligue de los resultados y analisis claro de los resultados respecto a lo visto en la teoria.
- [x] Creatividad y orden.
- [x] Sección con las conclusiones de los experimentos realizados.
