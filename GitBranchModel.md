# Git branch Model

> Este termino hace referencia a un modelo de trabajo que se sigue para realizar proyectos en Git.

> La configuración del repositorio que utilizamos y que funciona bien con este modelo de ramificación es la de un repositorio central de "verdad". Teniendo en cuenta que este repositorio solo se  considera el central (dado que Git es un DVCS, no existe un repositorio central a nivel técnico). Nos referiremos a este repositorio como origin, ya que este nombre es familiar para todos los usuarios de Git.

!["Imagen"](https://nvie.com/img/centr-decentr@2x.png)

> Cada desarrollador tira y empuja al origen. Pero además de las relaciones centralizadas push-pull, cada desarrollador también puede extraer cambios de otros pares para formar sub equipos. Por ejemplo, esto podría ser útil para trabajar junto con dos o más desarrolladores en una nueva característica importante, antes de adelantar originprematuramente el trabajo en progreso . En la figura anterior, hay subgrupos de Alice y Bob, Alice y David, y Clair y David.

> Técnicamente, esto no significa nada más que que Alice haya definido un control remoto Git, llamado bob, apuntando al repositorio de Bob, y viceversa.

## Ramas Principales 

> En esencia, el modelo de desarrollo está muy inspirado en los modelos existentes que existen. El repositorio central tiene dos ramas principales con una vida infinita:

* **master**

* **develop**

> La master sucursal en origin debería ser familiar para todos los usuarios de Git. Paralelo a la master rama, existe otra rama llamada develop.
>> Consideramos origin/master como la rama principal donde el código fuente de HEAD siempre refleja un estado listo para producción .

> Consideramos origin/develop como la rama principal donde el código fuente de HEAD siempre refleja un estado con los últimos cambios de desarrollo entregados para la próxima versión. Algunos llamarían a esto la "rama de integración". Aquí es donde se construyen las construcciones nocturnas automáticas.

> Cuando el código fuente en la rama develop  alcanza un punto estable y está listo para ser lanzado, todos los cambios deben fusionarse de master alguna manera y luego etiquetarse con un número de versión. Cómo se hace esto en detalle se discutirá más adelante.
>> Por lo tanto, cada vez que los cambios se fusionan nuevamente master, esta es una nueva versión de producción por definición . Tendemos a ser muy estrictos en esto, de modo que, en teoría, podríamos usar un script de enlace Git para construir y desplegar automáticamente nuestro software en nuestros servidores de producción cada vez que se realiza una confirmación master.

!["Imagen"](https://nvie.com/img/main-branches@2x.png)

### Ramas de apoyo

> Junto a las ramas principales master y develop, este modelo de desarrollo utiliza una variedad de ramas de soporte para ayudar al desarrollo paralelo entre los miembros del equipo, facilitar el seguimiento de las características, prepararse para lanzamientos de producción y ayudar a solucionar rápidamente los problemas de producción en vivo. A diferencia de las ramas principales, estas ramas siempre tienen un tiempo de vida limitado, ya que eventualmente se eliminarán.

> Los diferentes tipos de ramas que podemos usar son:

* **Ramas de características**

* **Liberar ramas**

* **Ramas de revisión**

> Cada una de estas ramas tiene un propósito específico y están sujetas a reglas estrictas sobre qué ramas pueden ser su rama de origen y qué ramas deben ser sus objetivos de fusión.

> De ninguna manera estas ramas son "especiales" desde una perspectiva técnica. Los tipos de ramas se clasifican según cómo los usamos . Por supuesto, son simples ramas viejas de Git.

### Ramas de caracteristicas

> Las ramas de características (o a veces denominadas ramas temáticas) se utilizan para desarrollar nuevas características para la próxima versión futura o futura. Al comenzar el desarrollo de una característica, la versión de destino en la que se incorporará esta característica puede ser desconocida en ese momento. La esencia de una rama de características es que existe mientras la característica esté en desarrollo, pero eventualmente se fusionará nuevamente develop(para agregar definitivamente la nueva característica a la próxima versión) o se descartará (en caso de un experimento decepcionante).

> Las ramas de características generalmente existen solo en repositorios de desarrolladores, no en origin.

!["Imagen"](https://nvie.com/img/fb@2x.png)

>Puede ramificarse de:

* **develop**

> Debe fusionarse nuevamente en:

* **develop**

### Liberar Ramas

> El momento clave para ramificar una nueva rama de lanzamiento developes cuando el desarrollo (casi) refleja el estado deseado de la nueva versión. Al menos todas las características que están destinadas a la versión para ser construida deben fusionarse en developeste momento. Es posible que no todas las funciones destinadas a futuras versiones: deben esperar hasta que se ramifique la rama de la versión.

> Es exactamente al comienzo de una rama de lanzamiento que al próximo lanzamiento se le asigna un número de versión, no antes. Hasta ese momento, la develop rama reflejaba los cambios para la "próxima versión", pero no está claro si esa "próxima versión" eventualmente se convertirá en 0.3 o 1.0, hasta que se inicie la rama de la versión. Esa decisión se toma al comienzo de la rama de lanzamiento y se lleva a cabo según las reglas del proyecto sobre el cambio de número de versión.

> Puede ramificarse de:

* **develop**

Debe fusionarse nuevamente en:

* **develop y master**

### Ramas de revision

> Las ramas de revisión son muy parecidas a las ramas de lanzamiento, ya que también están destinadas a prepararse para un nuevo lanzamiento de producción, aunque no planificado. Surgen de la necesidad de actuar inmediatamente sobre un estado no deseado de una versión de producción en vivo. Cuando un error crítico en una versión de producción debe resolverse de inmediato, una rama de revisión puede separarse de la etiqueta correspondiente en la rama maestra que marca la versión de producción.

!["Imagen"](https://nvie.com/img/hotfix-branches@2x.png)

> Puede ramificarse de:

* **master**

> Debe fusionarse nuevamente en:

* **develop y master**

