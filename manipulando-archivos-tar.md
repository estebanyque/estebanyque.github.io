---
title: Manipulando archivos .tar
---
# Manipulando archivos .tar

En mi lugar de trabajo, existen usuarios que usan un servidor para respaldar sus archivos. Uno de ellos me preguntó la posibilidad de manipular archivos `.tar.gz` de alguna manera y a continuación presento los apuntes que he tomado.

## Creando archivos .tar

La creación de archivos `.tar.gz` es bastante sencilla. Como ejemplo asumamos que:

    $ ls -l 
    -rw-r--r-- 1 user users 0 sep  3 22:40 file1 
    -rw-r--r-- 1 user users 0 sep  3 22:40 file2 
    -rw-r--r-- 1 user users 0 sep  3 22:40 file3 
    -rw-r--r-- 1 user users 0 sep  3 22:40 file4 
    -rw-r--r-- 1 user users 0 sep  3 22:40 file5

Entonces deseamos crear un archivo que contenga cada uno de los archivos
anteriores:

    tar cfv respaldo.tar file1 file2 file3 file4 file5

El comando ejecutado fue `tar` con los parámetros **f** de crear, seguido de **f** que indica un archivo, en este caso **respaldo.tar** , y el último parámetro **v** indica modo verbose. Todo eso seguido por la lista de los archivos a respaldar.

De momento solo tenemos un gran archivo **respaldo.tar** con una lista de
archivos en su interior.

## Listando el contenido de archivos .tar

También es normal querer saber qué contiene un archivo .tar.

Siguiendo con nuestro caso anterior, es posible ejecutar:

    $ tar tf respaldo.tar 
    file1 
    file2 
    file3 
    file4 
    file5

En este caso, el parámetro **t** indica la orden de listar el contenido, sobre el archivo indicado gracias al parámetro **f**.

## Borrando un archivo desde dentro de un .tar

En el caso de que necesitemos solo borrar un archivo de dentro de nuestro
archivo `.tar` es posible ejecutar:

    $ tar --delete --file respaldo.tar file3

En este caso, hemos indicado que se eliminará el archivo **file3** de nuestro **respaldo.tar**.

Listemos el contenido luego de nuestra última modificación.

    $ tar tf respaldo.tar 
    file1 
    file2 
    file4 
    file5

## Agregando contenido a un archivo .tar ya existente

En el caso de que debamos agregar un nuevo archivo, se utiliza:

    tar rf respaldo.tar newfile

Dicho comando agrega **newfile** al archivo **respaldo.tar**.

La explicación del parámetro **r** , es la de añadir, sobre el archivo
indicado con el parámetro **f**.

# Extrayendo el contenido de un .tar

Ya tenemos el respaldo, lo modificamos y necesitamos extraer el contenido, para eso utilizaremos los parámetros **x**, para la extracción y el parámetro **f** para indicar sobre qué archivo se debe trabajar. El parámetro **v** indica mode **verbose**:

    $ tar xfv respaldo.tar 
    file1 
    file2 
    file4 
    file5 
    newfile

## Comprimiendo archivos .tar

En el caso de querer hacer más portable un archivo tar, es posible comprimirlo de la siguiente forma:

    gzip respaldo.tar

## Creando y extrayendo archivos tar.gz

Pero existe una forma rápida de crear, desde un inicio un archivo de menor tamaño.

Tomemos el comando `tar cf` y agreguemos el parámetro **z** que indica que se utilizará un método de compresión.

    tar czf respaldo.tar.gz file1 file2 file3 file4 file5

Esto nos permitirá realizar en una sola acción la creación y compresión de nuestro **respaldo.tar.gz**.

En el caso en que deseemos recuperar el contenido, basta agregar el mismo
parámetro de compresión **z** a la orden de desempaquetar nuestro archivo:

    tar xfvz respaldo.tar.gz

## Finalizando

Existen muchas otras opciones para el uso del comando **tar**, como
diferentes métodos de compresión, actualizar el contenido de un archivo .tar, preservación de permisos y más.

Ojo, no todas las versiones del comando **tar** son iguales. Personalmente la opción de eliminación de contenido solo me ha funcionado en máquinas GNU/Linux, no así en OS X.

Recuerden ejecutar `man tar` para informarse de los distintos parámetros y opciones.
