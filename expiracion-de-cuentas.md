---
title: Evitar expiración de cuentas
---
# Evitar expiración de cuentas

En mi lugar de trabajo tengo un servidor llamado webpages.pega.com y cada
usuario puede tener su página web en webpages.pega.com/~$USER. Y en ocasiones
las cuentas expiran y los usuarios se contactan con la mesa de ayuda
solicitando la reactivación de sus cuentas.

## Verificando los datos

En el último caso que revisé, Juán Perez se comunicó y solicitó que su cuenta fuese reactivada.

Ejecutando el siguiente comando pude verificar los datos de esta persona


```
webpages ~ # chage -l jperez 
Last password change : Aug 23, 2013 
Password expires : Oct 22, 2013 
Password Inactive : Nov 26, 2013 
Account expires : never 
Minimum number of days between password change : 7 
Maximum number of days between password change : 60 
Number of days of warning before password expires : 14
```

`chage -l $USER` entrega la información de expiración de los cambios de
contraseña.

# Cambiando los datos del usuario.

`chage` también permite realizar cambios en los datos de la cuenta, utilizando `chage $USER` y configurando los valores como sigue:


```
webpages ~ # chage jperez 
Changing the aging information for jperez 
Enter the new value, or press ENTER for the default 
Minimum Password Age [7]: 0 
Maximum Password Age [60]: 99999 
Last Password Change (YYYY-MM-DD) [2013-08-23]: 
Password Expiration Warning [14]: -1 
Password Inactive [35]: -1 
Account Expiration Date (YYYY-MM-DD) [1969-12-31]:
```

o en una sola línea con:

```
webpages ~ # chage -I -1 -m 0 -M 999999 -E -1 jperez
```
donde los parámetros son:

  * `-I -1` Indica la Inactividad a -1, lo que equivale a eliminar la inactividad.
  * `-m 0` Indica que el usuario deberá cambiar la contraseña luego del número de días especificado.
  * `-M 99999` Indica el número de días que la contraseña será válida.
  * `-E -1` Número de días desde el 1 de Enero de 1970 desde que la cuenta sea inaccesible.

## Verificando los cambios realizados.

Luego de que se han modificado los datos, vuelvo a ejecutar
```
webpages ~ # chage -l jperez
```

para poder notar los cambios realizados.


```
Last password change                        : Aug 23, 2013 
Password expires                        : never 
Password inactive                        : never 
Account expires                              : never 
Minimum number of days between password change          : 0 
Maximum number of days between password change          : 99999 
Number of days of warning before password expires    : -1
```
Y ya podré indicar a Juán Perez que puede seguir utilizando su cuenta sin
problemas.
