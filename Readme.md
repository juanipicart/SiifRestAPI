# Pruebas JMX - JMeter

**Version del JMeter**:  JMeter 5.0 (Requires Java 8 or 9.) :+1:


Guia referencia para .md [GitHub help](https://help.github.com/articles/basic-writing-and-formatting-syntax/).

*Sobre el despliegue*

Cuando se menciona que se realizarán pruebas de rendimiento, performance y balanceo. Consideramos necesario se elabore una sección específica que considere al menos:
Que se probará
Por ejemplo se desarrollará un script que ingrese al sistema, ingrese a la pantalla de ingreso de bienes, acceda a la bandeja de entrada y apruebe la transacción.

*[Respuesta]* Se realizarán pruebas con JMeter donde se realizarán llamadas al Rest API expuesta para consumo de la capa de Presentación. Se correrá un  test que realizará una cierta cantidad de ingresos de usuario por segundo y una cierta  de llamadas para obtener 10 tareas de aprobación, donde se iterará por cada tarea llamando al API de aprobación de bien con el id de la tarea, entre cada iteración agregaremos un determinado retraso que se podrá configurar en los test entre una aprobación y otra.

Se presentarán los resultados de la ejecución de este test con distinta configuración se muestra un ejemplo de la configuración, se variará la configuración hasta ver que el sistema falla por falta de memoria.


| Ingreso de Bienes por Segundo | Obtener 10 tareas pendientes por segundo | Retraso entre una aprobación y otra en milisegundos  |
| ----------------------------- | ---------------------------------------- | ---------------------------------------------------- | 
| 10  | 1 | 100  |
| 50  | 5  | 20  |
| 100  | 10  | 10  |
| 200  | 20  | 5  |

## Configuración de hilos ##


**Primero Ciclo:**
 Grupo de hilos 1 
 
| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 1  | 1 | 1  |


Grupos de hilos 2

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 100  | 10 | 6  |

Grupos de hilos 3

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 2  | 5 | 6  |

**Segundo Ciclo:**

Grupo de hilos 1

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 1  | 1 | 1  |

Grupos de hilos 2

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 500  | 10 | 6  |

Grupos de hilos 3

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 5  | 10 | 12  |

**Tercer Ciclo:**

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 1  | 1 | 1  |

Grupos de hilos 2

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 1000  | 20 | 12  |

Grupos de hilos 3

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 10  | 20 | 24  |


**Cuarto Ciclo:**

Grupo de hilos 1

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 1  | 1 | 1  |

Grupos de hilos 2

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 2000  | 40 | 24  |

Grupos de hilos 3

| Number of Threads | Ramp-up | Loop  |
| ----------------- | ------- | ----- | 
| 20  | 40 | 48 |

<br />
<br />

**Que se medirá**
Por ejemplo se medirá el tiempo de respuesta del botón aprobación.<br />
*[Respuesta]* Se medirán los tiempos de respuestas de las llamadas al Rest API que se hicieron con JMeter, y mientras la aplicación está siendo estresada con JMeter, navegaremos desde un navegador utilizando Selenium  para inspeccionar los tiempos de respuesta de ingresar un bien y aprobarlo.



**Cómo se probará**
Por ejemplo se someterá a pruebas de carga en un esquema de 1 nodo en cada capa hasta llegar un nivel de degradación predefinido, se duplica los nodos verificando que el nivel de degradación se aumenta.<br />
*[Respuesta]* Se probará como se mencionó en el punto a), con 1 nodo por componente de la arquitectura y luego con 2 nodos por componente.



**Que se presentará**
Por ejemplo: consumo de CPU, consumo de memoria, IO, memory leak, gráficos de tiempo de respuesta, hits por segundo, throughputs, excepciones por segundo.<br />
*[Respuesta]* Consumo de CPU y memoria por componente, y un gráfico con los tiempos de respuesta de las llamadas al Rest API, tabla con los tiempos de respuesta de los botones de alta de bien y de aprobación para las distintas configuraciones de carga y diferente configuración de despliegue (1 o 2 nodos).
<br />

    
![alt text](../SiifRestAPI/img/donut.png)

