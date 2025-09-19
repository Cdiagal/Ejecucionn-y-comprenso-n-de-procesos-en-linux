# Ejecución y comprensión de procesos en linux.

## Bloque 1. Teoría 🎓

<details>

<summary>Clic para ver el contenido</summary>

### Ejercicio 1 - Define qué es un proceso y en qué se diferencia de un programa.

- **Proceso**: proceso se trata de un programa que entra en ejecución. Los procesos son una sucesión de instrucciones que pretenden llegar a un estado final o que persiguen realizar una tarea concreta.

- **Programa**: programa es un algoritmo que genera una secuencia de instrucciones con las que podemos realizar una tarea concreta. 


- **Diferencia**:
El programa es la secuencia de instrucciones escrita en un lenguaje de programación dado y un proceso es la instancia de ejecución de un programa.

[Referencia 1](https://www.profesionalreview.com/2019/09/23/proceso-informatico/)

[Referencia 2](https://lsi.vc.ehu.eus/pablogn/docencia/manuales/SO/TemasSOuJaen/DEFINICIONYCONTROLDEPROCESO/1y2Queesunproceso.EstadoyTransiciones.htm#:~:text=Un%20programa%20es%20una%20secuencia,%2C%20pila%20y%20datos%2C%20etc.)

---

### Ejercicio 2 - Explica qué es el kernel y su papel en la gestión de procesos.

El Kernel o núcleo, es una parte fundamental del sistema operativo que se encarga de conceder el acceso al hardware de forma segura para todo el software que lo solicita, el Kernel es una pequeña e invisible parte del sistema operativo, pero la más importante, ya que sin esta no podría funcionar.

El Kernel o núcleo de un sistema operativo sirve para administrar los recursos de hardware solicitados por los diferentes elementos de software y hacer de intermediario decidiendo a que y cuando se concede este acceso evitando así sobrecarga del sistema, recursos innecesarios y acceso a software malicioso al propio Kernel y llegar a poder controlar así todo el sistema. De este modo el Kernel sirve como elemento de seguridad teniendo que pasar por varias capas antes de poder tener acceso, además tiene que distribuir los recursos de manera eficiente y ordenada para que el Hardware trabaje junto al Software de la mejor manera posible.

[Referencia](https://www.geeknetic.es/Kernel/que-es-y-para-que-sirve)

---

### Ejercicio 3 - ¿Qué son PID y PPID? Explica con un ejemplo.

El `PID` es el número único que se le asigna a un proceso que lo identifica en el sistema cuando un programa es ejecutado.
Por otra parte, el `PPID` es el ID de proceso principal que indica qué proceso lo inició. En otras palabras, el `PPID` es el `PID` del proceso principal.

Por ejemplo, si el proceso1 con un con un `PID` de 101 inicia un proceso llamado proceso2, este recibirá un `PID` único, como 3240, pero el `PPID` de 101. Se trata de una relación padre-hijo. Un solo proceso padre puede generar varios procesos hijos, cada uno con un `PID` único, pero todos con el mismo `PPID`.

[Referencia](https://stackoverflow.com/questions/30493424/what-is-the-difference-between-a-process-pid-ppid-uid-euid-gid-and-egid#:~:text=The%20PPID%20is%20the%20PID,It's%20a%20parent%2Dchild%20relationship.)

---

### Ejercicio 4 - Describe qué es un cambio de contexto y por qué es costoso.

Un **cambio de contexto** consiste en la ejecución de una rutina perteneciente al núcleo del sistema operativo multitarea de una computadora, cuyo propósito es parar la ejecución de un hilo o proceso para dar paso a la ejecución de otro distinto.

En principio, una computadora que dispone de un único microprocesador solamente puede ejecutar un proceso al mismo tiempo. No es posible ejecutar otro proceso hasta que ha finalizado el anterior.

No obstante, es posible alternar el uso de la CPU entre varios procesos durante cortos periodos de tiempo. Esto se denomina ejecución concurrente o multiprogramación.

Además, durante la ejecución de un proceso existen muchos tiempos muertos donde no es necesario el uso de la CPU . Se trata de los momentos en los que el programa está esperando a que finalice una operación de entrada/salida, por ejemplo, una lectura desde el disco duro. Estos tiempos muertos podrían aprovecharse para ejecutar otro programa.

Se detalla en **cuatro** pasos ordenados:

1. Salvar el estado del programa que se estaba ejecutando.
2. Seleccionar otro programa para ejecutar.
3. Restaura el estado del programa seleccionado.
4. Ejecuta el programa seleccionado.


El motivo por el cual es costoso

[Referencia 1](https://es.wikipedia.org/wiki/Cambio_de_contexto)



---

### Ejercicio 5 - Explica qué es un PCB (Process Control Block) y qué información almacena.

El PCB (Process Control Block) o Bloque de Control de Proceso es una estructura de datos utilizada por los sistemas operativos para mantener y gestionar la información asociada a cada proceso que se encuentra en ejecución en el sistema.

Cada vez que se crea un proceso, el sistema operativo asigna un PCB en memoria para almacenar toda la información relevante sobre ese proceso. El PCB contiene detalles importantes como:

ID del proceso
Estado del proceso (suspendido, en espera,…)
Información de la CPU (contenido de los registros como el PC)
Información de memoria (espacio asignado)
Información de recursos (archivos abiertos, E/S,…)
Información de planificación (prioridad)

[Referencia](https://www.profesionalreview.com/2023/08/15/cpu-cambio-contexto/)

---

### Ejercicio 6 - Diferencia entre proceso padre y proceso hijo.

Un proceso iniciado por un programa o mandato es un proceso padre; un proceso hijo es el producto del proceso padre. Un proceso padre puede tener varios procesos hijo, pero un proceso hijo sólo puede tener un padre.

[Referencia](https://www.ibm.com/docs/es/aix/7.2.0?topic=processes-)

---

### Ejercicio 7 - Explica qué ocurre cuando un proceso queda huérfano en Linux.

Un proceso huérfano ocurre cuando un proceso padre finaliza antes que su proceso hijo, dejándolo ejecutándose sin su padre original. En sistemas Linux, los procesos hijos huérfanos son adoptados automáticamente por el proceso inito systemd(normalmente PID 1), lo que les permite continuar ejecutándose en segundo plano. En Windows, los procesos huérfanos también continúan ejecutándose, pero sin una relación padre-hijo, lo que dificulta la gestión y la limpieza de procesos. Aunque los procesos huérfanos no consumen recursos excesivos por naturaleza, su presencia involuntaria puede indicar fallos de diseño, fugas de recursos o una gestión ineficiente de los procesos dentro de las aplicaciones de software.

[Referencia](https://www.greptile.com/bug-wiki/memory-resource-management/orphaned-process)

---

### Ejercicio 8 - ¿Qué es un proceso zombie? Da un ejemplo de cómo puede ocurrir.

En sistemas operativos `Unix`, un proceso zombi o "defunct" (difunto) es un proceso que ha completado su ejecución pero aún tiene una entrada en la tabla de procesos,​ lo que permite al proceso que lo ha creado leer el estado de su salida.

[Referencia 1](https://es.wikipedia.org/wiki/Proceso_zombie)

[Referencia 2]()

---

### Ejercicio 9 - Diferencia entre concurrencia y paralelismo.

La concurrencia se enfoca más en el diseño del software, el paralelismo se relaciona con la ejecución de este.

Asimismo, es posible plantear una diferenciación en lo que respecta al proceder de concurrencia y paralelismo, ya que, por un lado, el paralelismo ejecuta múltiples tareas de forma simultánea, y por otra parte, la concurrencia computacional ejecuta y gestiona diversas tareas al mismo tiempo. Esto quiere decir que la concurrencia contribuye al procesamiento de varias tareas al tiempo y el paralelismo se encarga de dar resolución a una sola tarea de forma más eficiente.

[Referencia](https://keepcoding.io/blog/paralelismo-y-concurrencia-computacional/)

---

### Ejercicio 10 - Explica qué es un hilo (thread) y en qué se diferencia de un proceso.

Un hilo (thread) es la unidad más pequeña de procesamiento que puede ser ejecutada por un sistema operativo.  Dentro de un proceso, los hilos comparten el mismo espacio de memoria y otros recursos, como archivos abiertos o señales recibidas. Los hilos permiten que un proceso realice múltiples tareas simultáneamente o en paralelo.

[Referencia](https://www.mentorestech.com/resource-blog-content/process-vs-threads)

---
</details>

----




## Bloque 2. Práctica 🖥️
<details>

<summary>Clic para ver el contenido</summary>

### Ejercicio 11 - Usa echo $$ para mostrar el PID del proceso actual.



```bash
cdiagal@Carlos:~$ echo $$
227
```

### Ejercicio 12 - Usa echo $PPID para mostrar el PID del proceso padre.


```bash
cdiagal@Carlos:~$ echo $PPID
224
```

### Ejercicio 13 - Ejecuta pidof systemd y explica el resultado.



```bash
cdiagal@Carlos:~$ pidof systemd
405
```
pidof - comando que devuelve el identificador de proceso `(PID)` de un programa que está corriendo.

systemd - es el sistema de inicio y gestor de servicios que arranca primero en muchas distribuciones Linux modernas. Se encarga de inicializar el sistema y gestionar procesos.

405 - es el número de proceso `(PID)` asignado por el kernel a systemd.

Comprobación:

```bash
cdiagal@Carlos:~$ ps -p 405 -o pid,ppid,cmd
    PID    PPID CMD
    405       1 /usr/lib/systemd/systemd --user
```

### Ejercicio 14 - Abre un programa gráfico (ejemplo: gedit) y usa pidof para obtener sus PID.

En mi caso estoy con la WSL en windows por lo que haré la comprobación con `nano`

```bash
cdiagal@Carlos:~$ nano &
pidof nano
[1] 601
cdiagal@Carlos:~$ nano & pidof nano
[2] 603
603 601

[1]-  Stopped                 nano

[2]+  Stopped                 nano
cdiagal@Carlos:~$ nano & pidof nano
[3] 605
605 603 601
```

prueba hecha con el comando tres veces para aclarar que a cada proceso le da un `PID` y suspende los anteriores.

### Ejercicio 15 - Ejecuta ps -e y explica qué significan sus columnas.



```bash
    PID TTY          TIME CMD
      1 ?        00:00:01 systemd
      2 ?        00:00:00 init-systemd(Ub
      6 ?        00:00:00 init
     52 ?        00:00:00 systemd-journal
    101 ?        00:00:00 systemd-udevd
    111 ?        00:00:00 systemd-resolve
    112 ?        00:00:00 systemd-timesyn
    183 ?        00:00:00 cron
    184 ?        00:00:00 dbus-daemon
    200 ?        00:00:00 systemd-logind
    203 ?        00:00:00 wsl-pro-service
    219 hvc0     00:00:00 agetty
    222 ?        00:00:00 SessionLeader
    223 ?        00:00:00 rsyslogd
    224 ?        00:00:00 Relay(227)
    227 pts/0    00:00:00 bash
    228 tty1     00:00:00 agetty
    229 pts/1    00:00:00 login
    240 ?        00:00:00 unattended-upgr
    405 ?        00:00:00 systemd
    407 ?        00:00:00 (sd-pam)
    426 pts/1    00:00:00 bash
    601 pts/0    00:00:00 nano
    603 pts/0    00:00:00 nano
    605 pts/0    00:00:00 nano
    609 pts/0    00:00:00 ps
```
- **PID** - IDentificador único que se le asigna al proceso en el sistema.

- **TTY** - Teletype, es decir, Indica el terminal asociado al proceso (? no tiene ninguna terminal, pts/ es un pseudoterminal o sesiones abiertas dentro del shell y tty* es terminal física o consola virtual).

- **TIME** - El tiempo total de CPU que lleva consumiendo desde que arrancó el proceso.


### Ejercicio 16 -  Ejecuta ps -f y observa la relación entre procesos padre e hijo.



```bash
cdiagal@Carlos:~$ ps -f
UID          PID    PPID  C STIME TTY          TIME CMD
cdiagal      227     224  0 21:48 pts/0    00:00:00 -bash
cdiagal      601     227  0 22:45 pts/0    00:00:00 nano
cdiagal      603     227  0 22:45 pts/0    00:00:00 nano
cdiagal      605     227  0 22:45 pts/0    00:00:00 nano
cdiagal      647     227  0 23:03 pts/0    00:00:00 ps -f
```

### Ejercicio 17 - Usa ps -axf o pstree para mostrar el árbol de procesos y dibújalo



```bash
    PID TTY      STAT   TIME COMMAND
      1 ?        Ss     0:01 /sbin/init
      2 ?        Sl     0:00 /init
      6 ?        Sl     0:00  \_ plan9 --control-socket 7 --log-level 4 --server-fd 8 --pipe-fd 10 --log-truncate
    222 ?        Ss     0:00  \_ /init
    224 ?        S      0:00  |   \_ /init
    227 pts/0    Ss     0:00  |       \_ -bash
    601 pts/0    T      0:00  |           \_ nano
    603 pts/0    T      0:00  |           \_ nano
    605 pts/0    T      0:00  |           \_ nano
    648 pts/0    R+     0:00  |           \_ ps -axf
    229 pts/1    Ss     0:00  \_ /bin/login -f
    426 pts/1    S+     0:00      \_ -bash
     52 ?        S<s    0:00 /usr/lib/systemd/systemd-journald
    101 ?        Ss     0:00 /usr/lib/systemd/systemd-udevd
    111 ?        Ss     0:00 /usr/lib/systemd/systemd-resolved
    112 ?        Ssl    0:00 /usr/lib/systemd/systemd-timesyncd
    183 ?        Ss     0:00 /usr/sbin/cron -f -P
    184 ?        Ss     0:00 @dbus-daemon --system --address=systemd: --nofork --nopidfile --systemd-activation --syslog
    200 ?        Ss     0:00 /usr/lib/systemd/systemd-logind
    203 ?        Ssl    0:00 /usr/libexec/wsl-pro-service -vv
    219 hvc0     Ss+    0:00 /sbin/agetty -o -p -- \u --noclear --keep-baud - 115200,38400,9600 vt220
    223 ?        Ssl    0:00 /usr/sbin/rsyslogd -n -iNONE
    228 tty1     Ss+    0:00 /sbin/agetty -o -p -- \u --noclear - linux
    240 ?        Ssl    0:00 /usr/bin/python3 /usr/share/unattended-upgrades/unattended-upgrade-shutdown --wait-for-sign
    405 ?        Ss     0:00 /usr/lib/systemd/systemd --user
    407 ?        S      0:00  \_ (sd-pam)
```

### Ejercicio 18 - Ejecuta top o htop y localiza el proceso con mayor uso de CPU.



```bash
    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
    651 cdiagal   20   0    9272   5456   3344 R   0.3   0.0   0:00.11 top
      1 root      20   0   21692  12320   9328 S   0.0   0.1   0:01.14 systemd
      2 root      20   0    3060   1584   1584 S   0.0   0.0   0:00.01 init-systemd(Ub
      6 root      20   0    3076   1852   1760 S   0.0   0.0   0:00.00 init
     52 root      19  -1   66744  15000  14120 S   0.0   0.1   0:00.78 systemd-journal
    101 root      20   0   24872   6160   4928 S   0.0   0.0   0:00.53 systemd-udevd
    111 systemd+  20   0   21452  12144  10208 S   0.0   0.1   0:00.17 systemd-resolve
    112 systemd+  20   0   91020   7568   6688 S   0.0   0.0   0:00.31 systemd-timesyn
    183 root      20   0    4236   2464   2288 S   0.0   0.0   0:00.02 cron
    184 message+  20   0    9624   4576   4224 S   0.0   0.0   0:00.35 dbus-daemon
    200 root      20   0   17960   8272   7392 S   0.0   0.1   0:00.20 systemd-logind
    203 root      20   0 1756096  12144  10032 S   0.0   0.1   0:00.45 wsl-pro-service
    219 root      20   0    3160   1760   1760 S   0.0   0.0   0:00.01 agetty
    222 root      20   0    3064    880    880 S   0.0   0.0   0:00.00 SessionLeader
    223 syslog    20   0  222508   5456   4400 S   0.0   0.0   0:00.18 rsyslogd
    224 root      20   0    3080    880    880 S   0.0   0.0   0:00.05 Relay(227)
    227 cdiagal   20   0    6072   4928   3344 S   0.0   0.0   0:00.09 bash
    228 root      20   0    3116   1760   1760 S   0.0   0.0   0:00.01 agetty
    229 root      20   0    6820   4400   3696 S   0.0   0.0   0:00.01 login
    240 root      20   0  107012  21824  13024 S   0.0   0.1   0:00.16 unattended-upgr
    405 cdiagal   20   0   20288  11088   9152 S   0.0   0.1   0:00.13 systemd
    407 cdiagal   20   0   21144   3484   1760 S   0.0   0.0   0:00.00 (sd-pam)
    426 cdiagal   20   0    6072   4928   3344 S   0.0   0.0   0:00.01 bash
```
Por lo que se ve, el proceso que más CPU está consumiendo es el 651

### Ejercicio 19 - Ejecuta sleep 100 en segundo plano y busca su PID con ps.



```bash
cdiagal@Carlos:~$ sleep 100 &
[8] 666
```
```bash
cdiagal@Carlos:~$ ps
    PID TTY          TIME CMD
    227 pts/0    00:00:00 bash
    601 pts/0    00:00:00 nano
    603 pts/0    00:00:00 nano
    605 pts/0    00:00:00 nano
    651 pts/0    00:00:00 top
    664 pts/0    00:00:00 sleep
    665 pts/0    00:00:00 sleep
    666 pts/0    00:00:00 sleep
    671 pts/0    00:00:00 ps

```

En este caso lo hice tres veces por prueba y me identifica los tres `sleep`

### Ejercicio 20 - Finaliza un proceso con kill y comprueba con ps que ya no está.



```bash

```

</details>



-----



## Bloque 3. Práctica 🖥️
<details>

<summary>Clic para ver el contenido</summary>

### Ejercicio 21 - Identifica el PID del proceso init/systemd y explica su función.


```bash
cdiagal@Carlos:~$ ps -p 1 -o pid,cmd
    PID CMD
      1 /sbin/init
```

En este caso se solicita con `ps` el estado de los procesos
`-p` - solicita el proceso junto con el número que se solicita que en este caso es `1` porque en Linux el primer proceso den espacio de usuario es `init`.

### Ejercicio 22 - Explica qué ocurre con el PPID de un proceso hijo si su padre termina antes.


Cuando un proceso inicia un proceso hijo y muere antes que este, el proceso hijo pasa a ser un hijo de init inmediatamente.

### Ejercicio 23 - Ejecuta un programa que genere varios procesos hijos y observa sus PIDs con ps.


```bash

```

### Ejercicio 24 - Haz que un proceso quede en estado suspendido con Ctrl+Z y réanúdalo con fg.


```bash

```

### Ejercicio 25 - Lanza un proceso en segundo plano con & y obsérvalo con jobs.


```bash

```

### Ejercicio 26 - Explica la diferencia entre los estados de un proceso: Running, Sleeping, Zombie, Stopped.


```bash

```

### Ejercicio 27 - Usa ps -eo pid,ppid,stat,cmd para mostrar los estados de varios procesos.


```bash

```

### Ejercicio 28 - Ejecuta watch -n 1 ps -e y observa cómo cambian los procesos en tiempo real.


```bash

```

### Ejercicio 29 - Explica la diferencia entre ejecutar un proceso con & y con nohup.


```bash

```

### Ejercicio 30 - Usa ulimit -a para ver los límites de recursos de procesos en tu sistema.


```bash

```

</details>



-----