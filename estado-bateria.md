---
title: Estado de la batería del portatil
---
# Estado de la batería del portatil

Y mientras escribo estas pocas líneas, no sabía el estado de la batería del portátil, y una rápida busqueda me llevó a utilizar el siguiente comando:

    acpi -V

El resultado fue:

```
$ acpi -V 
Battery 0: Discharging, 86%, 04:51:37 remaining 
Battery 0: design capacity 6450 mAh, last full capacity 5315 mAh = 82% 
Adapter 0: off-line 
Thermal 0: ok, 54.0 degrees C 
Thermal 0: trip point 0 switches to mode critical at temperature 100.0 degrees C 
Thermal 0: trip point 1 switches to mode passive at temperature 95.0 degrees C 
Thermal 1: ok, 54.0 degrees C 
Thermal 1: trip point 0 switches to mode critical at temperature 100.0 degrees C 
Cooling 0: x86_pkg_temp no state information available Cooling 1: LCD 15 of 15 
Cooling 2: intel_powerclamp no state information available 
Cooling 3: Processor 0 of 10 Cooling 4: 
Processor 0 of 10 Cooling 5: Processor 0 of 10 
Cooling 6: Processor 0 of 10
```

¡Uffff!

Mucha más información de la que necesitaba, pero al menos ya sé que la batería está a un 86% y tengo algunas horas por delante para seguir acá.

Pero de momento leeré `man acpi` para saber qué otras opciones tiene dicho comando.

:)
