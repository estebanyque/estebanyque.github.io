---
title: Installing Untrusted Packages With Munk and the Managed Center Software
---
# Installing Untrusted Packages With Munki and the Managed Center Software

Si se desea instalar software sin firmar o considerado _no confiable_ mediante Munki, es posible modificar el siguiente archivo:

    /usr/local/munki/munkilib/installer.py

La línea número 168 tiene la siguiente información:

    cmd = ['/usr/sbin/installer', '-verboseR', '-pkg', pkgpath, '-target', '/']

Y modificándola a:

    cmd = ['/usr/sbin/installer', '-verboseR', '-allowUntrusted', '-pkg', pkgpath, '-target', '/']

podremos instalar aplicaciones _no confiables_.

Una vez realizada esta modificación, ejecutar los siguientes comandos en una terminal como **super usuario**:

```bash
rm /usr/local/munki/munkilib/installer.pyc
managedsoftwarecenter
managedsoftwarecenter --installonly
```

Es necesario tener cuidado de lo que se desea instalar, ya que estaremos agregando una posible brecha de seguridad.

## Bonus

También para evitar que el _Managed Center Software_ muestre las notificaciones de paquetes a actualizar, como **super usuario** podemos ejecutar en una shell:

    defaults write /Library/Preferences/ManagedInstalls SuppressUserNotification -bool True

Salud!
