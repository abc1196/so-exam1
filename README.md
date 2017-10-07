### Examen 1
**Universidad ICESI**  
**Curso:** Sistemas Operativos  
**Docente:** Daniel Barragán C.  
**Tema:** Comandos de Linux, Virtualización  
**Correo:** daniel.barragan at correo.icesi.edu.co
**Nombre:** Alejandro Bueno Cardona
**Código:** A00335472

### Objetivos
* Conocer y emplear comandos de Linux para la realización de tareas administrativas
* Virtualizar un sistema operativo
* Conocer y emplear capacidades de CentOS7 para la vitualización

### Prerrequisitos
* Virtualbox o WMWare
* Máquina virtual con sistema operativo CentOS7

### Descripción
El primer parcial del curso sistemas operativos trata sobre el manejo de los comandos de Linux, virtualización y el uso de las características de CentOS7

### Actividades
1. Incluir nombre, código (5%)
2. Ortografía y redacción cuando sea necesario (5%)
3. Resuelva los siguienes retos de la página https://cmdchallenge.com y presente la solución a cada uno de ellos a través de un ejemplo práctico en CentOS7. Presente capturas de pantalla relevantes como evidencias de lo realizado (20%)
  * sum_all_numbers
  * replace_spaces_in_filenames
  * reverse_readme
  * remove_duplicated_lines
  * disp_table
4. Realice un script que cumpla las condiciones que se describen a continuación. Presente capturas de pantalla relevantes como evidencias del funcionamiento (30%)
  * El usuario gutenberg debe existir en el sistema operativo
  * El script se debe ejecutar cada 5 minutos, consulte el manual de crontab
  * EL script debe descargar un libro del proyecto https://www.gutenberg.org/ en el directorio /home/gutenberg/mybooks
  * Si ya existe un libro en el directorio mybooks, debe ser reemplazado  
5. Describa el funcionamiento del código fuente rickroll.c del repositorio de github https://github.com/jvns/kernel-module-fun. Muestre el funcionamiento al compilar el código y cargarlo como un módulo del kernel a través de un video que deberá cargar en Youtube e incluir el enlace en el informe (30%). Se recomienda emplear el sistema operativo Ubuntu con interfaz gráfica para esta prueba.
6. El informe debe ser entregado en formato pdf a través del moodle y el informe en formato README.md debe ser subido a un repositorio de github. El repositorio de github debe ser un fork de https://github.com/ICESI-Training/so-exam1 y para la entrega deberá hacer un Pull Request (PR) respetando la estructura definida. El código fuente y la url de github deben incluirse en el informe (10%)  

### Solución

#### Retos CMD Challenge

**1. sum_all_numbers**
Para el primer reto se creó un script para ejecutar la tarea. El script inicia declarando la variable suma igual a cero. Luego, un loop (while) se encarga de leer cada línea del archivo. Este valor es agregado a la variable suma, que es mostrada, al final del bucle, mediante el comando echo.

    #!/bin/bash
    suma=0;
    while read number;
    do ((suma+=number));
    done  sum-me.txt
    echo $suma;

| CMD | CentOs7 |
| --- | --- |
| ![][1] | ![][2] |

**2. replace_spaces_in_filenames**
Para el primer reto se creó un script para ejecutar la tarea. El script inicia declarando la variable suma igual a cero. Luego, un loop (while) se encarga de leer cada línea del archivo. Este valor es agregado a la variable suma, que es mostrada, al final del bucle, mediante el comando echo.

    ls | sed 's/ /\./g'

| CMD | CentOs7 |
| --- | --- |
| ![][3] ![][4]| ![][5] ![][6] |

**3. reverse_readme**
El tercer reto no tuvo mayor dificultad. El comando cat, utilizado para ver el contenido de los archivos, tiene su inverso: tac, que permite mostrar el contenido de un archivo en sentido contrario, es decir, la primera línea se imprime de última y la última línea de primera.

    tac README

| CMD | CentOs7 |
| --- | --- |
| ![][7] | ![][8] ![][9] |

**4. remove_duplicated_lines**
En el cuarto reto se buscó e implementó el comando awk. El parámetro ‘!duplicate[$0]++’ le indica al comando que líneas imprimir. $0 contiene toda la línea. Si el contenido del índice del arreglo, en este caso duplicate, no ha sido establecido, entonces el índice duplicate se incremente y la línea se imprime.

    awk '!duplicate[$0]++' faces.txt

| CMD | CentOs7 |
| --- | --- |
| ![][10] ![][11] | ![][12] |

**5. disp_table**
En el quinto reto se implementó uno de los comandos vistos en clase de nuevo: sed. En este caso, se muestra el contenido del archivo table.csv. Posteriormente, se utilizó el comando sed reemplazar las comas (“\,”) con espacios (“/ /”). Por último, el comando column permite ordenar la información del archivo en formato de columnas. El parámetro -t tabula simple a cada una.

    cat table.csv | sed 's/\,/ /g' | column -t

| CMD | CentOs7 |
| --- | --- |
| ![][13] | ![][14] |

#### Script Gutenberg-Crontab

En el momento que se realizó el parcial, Gutenberg contaba con 66588 libros en su página. Cada uno se obtiene mediante el enlace  https://www,gutenberg.org/files/numID/numID.txt. Sin embargo, a partir del numID=40, los libros presentan variaciones en su identificador. Por esto, el script presenta, de manera aleatoria, los primeros 40 libros, es decir, el conjunto de libros con numID entre 1 y 40. El script que realiza la descarga del libro en el directorio /home/Gutenberg/mybooks es el siguiente:

![][15]

El script asigna dos variables: numID, con el identificador aleatorio mencionado anteriormente; hora, con la hora actual en formato HH:MM. Luego, se crea el URL, se elimina el libro anterior (comando rm) y, finalmente, se descarga el libro con el comando wget, cuyo parámetro -O almacena la descarga en el directorio /home/Gutenberg/mybooks y en el archivo fiveMinuteBook$numID-$hora.txt.

Por otro lado, para ejecutar el script cada 5 minutos, se utilizó crontab, que es un archivo de texto, donde se guarda una lista de comandos para ser ejecutados. A continuación, se puede ver el formato para los comandos de crontab:

![][16]
* Tomada de http://www.desarrollolibre.net/blog/tema/106/linux/ejecutar-script-automaticamente-con-cron-en-linux#.WdhTJ2jWxEY

Cambiando el primero parámetro de minutos a */5 y dejando en * los demás, crontab procede a ejecutar el script cada 5 minutos.

![][17]

En el momento en que se guardó el archivo crontab, llegó notificación al usuario root con la siguiente información:

![][18]

En la anterior imagen, se evidenció que el script se ejecuta y almacena el nuevo archivo: fiveMinuteBook-21:30.txt. Este archivo tiene numID=3 y fue descargado a las 21:30 (hora de la VM).

Pasados 5 minutos, llegó notificación al usuario root con la nueva descarga:

![][19]

![][20]

Ahora, se guardó el archivo con numID=20 a las 21:35 (hora de la VM).

Para terminar, se comprobó la existencia del archivo en el usuario y directorio requerido:

![][21]




### Referencias
* https://cmdchallenge.com  
* https://www.gutenberg.org  
* https://github.com/jvns/kernel-module-fun/blob/master/rickroll.c
* https://www.youtube.com/watch?v=efEZZZf_nTc
* http://www.desarrollolibre.net/blog/tema/106/linux/ejecutar-script-automaticamente-con-cron-en-linux#.WdhTJ2jWxEY

[1]: images/reto1CMD.png
[2]: images/reto1CO.png
[3]: images/reto2CMDI.png
[4]: images/reto2CMDII.png
[5]: images/reto2COI.png
[6]: images/reto2COII.png
[7]: images/reto3CMD.png
[8]: images/reto3COI.png
[9]: images/reto3COII.png
[10]: images/reto4CMDI.png
[11]: images/reto4CMDII.png
[12]: images/reto4CO.png
[13]: images/reto5CMD.png
[14]: images/reto5CO.png
[15]: images/sgc1.png
[16]: images/sgc2.png
[17]: images/sgc3.png
[18]: images/sgc4.png
[19]: images/sgc5.png
[20]: images/sgc6.png
[21]: images/sgc7.png

