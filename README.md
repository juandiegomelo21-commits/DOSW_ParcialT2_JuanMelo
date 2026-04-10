
### Requerimientos Funcionales (RF)
* RF01: Registro de Usuario
* RF02: Registro vehiculo
* RF03: Restriccion de cantidad Vehiculo
* RF04: Tipo usuario fijo
* RF05: Autenticación
* RF06: Solicitud de viaje
* RF07: Cancelar Viaje
* RF08: Aceptar viaje Conductor
* RF09: Historial de Viajes


### Requerimientos No Funcionales (RNF)
* RNF10: Sistema responsive

---

## 2. Detalle de Requerimientos Funcionales

### RF01: Registro de Usuario

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                |   POST |
| **Idenpotente**                | NO |
| **Razón**           | Cuando se llama cada vez se crea un usuario nuevo
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| identificador | numero unico | Numerico (entero) |debe ser unico|Sí|
| Nombre | nombre del usuario | string | no puede tener numeros | Sí |
| Correo Electronico | correo electronico valido | string | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Contraseña | seguridad de la cuenta | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Foto de perfil | foto de la persona | Moneda (decimal) | Debe ser ≥ 0 | Sí |
|Rol| puede ser conductor o pasajero| string | no puede ser vacio  | Sí|
|Numero de identificación| Numérico (entero) | debe contener solo numeros | Sí| 

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| 100,juan,pepito@gmail.com, ******, img.pjg, conductor,001|

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| estado de registro | exitoso o no | Texto (UUID) | tiene que ser unico | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| registro exitoso |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | el usuario no se puede registrar 2 veces |
|**validaciones imput**| validacion numerica de id y campos string |

---

### RF02: Registro de Vehiculo

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                | POST |
| **Idenpotente**                | NO |
| **Razón**           | Cuando se llama cada vez se crea un nuevo carro
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| Entrada |

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|

---

### RF01: Registro de Torneo

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                | GET |
| **Idenpotente**                | NO |
| **Razón**           | El sistema debe permitir al organizador crear un nuevo torneo proporcionando la información básica requerida (fechas, cantidad de equipos, costo). El torneo se crea inicialmente en estado 
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| Entrada |

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|


### RF01: Registro de Torneo

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                | GET |
| **Idenpotente**                | NO |
| **Razón**           | El sistema debe permitir al organizador crear un nuevo torneo proporcionando la información básica requerida (fechas, cantidad de equipos, costo). El torneo se crea inicialmente en estado 
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| Entrada |

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|


### RF01: Registro de Torneo

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                | GET |
| **Idenpotente**                | NO |
| **Razón**           | El sistema debe permitir al organizador crear un nuevo torneo proporcionando la información básica requerida (fechas, cantidad de equipos, costo). El torneo se crea inicialmente en estado 
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| Entrada |

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|


### RF01: Registro de Torneo

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                | GET |
| **Idenpotente**                | NO |
| **Razón**           | El sistema debe permitir al organizador crear un nuevo torneo proporcionando la información básica requerida (fechas, cantidad de equipos, costo). El torneo se crea inicialmente en estado 
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| Entrada |

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|


### RF01: Registro de Torneo

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                | GET |
| **Idenpotente**                | NO |
| **Razón**           | El sistema debe permitir al organizador crear un nuevo torneo proporcionando la información básica requerida (fechas, cantidad de equipos, costo). El torneo se crea inicialmente en estado 
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| Entrada |

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|


### RF01: Registro de Torneo

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                | GET |
| **Idenpotente**                | NO |
| **Razón**           | El sistema debe permitir al organizador crear un nuevo torneo proporcionando la información básica requerida (fechas, cantidad de equipos, costo). El torneo se crea inicialmente en estado 
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| Entrada |

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|


### RF01: Registro de Torneo

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                | GET |
| **Idenpotente**                | NO |
| **Razón**           | El sistema debe permitir al organizador crear un nuevo torneo proporcionando la información básica requerida (fechas, cantidad de equipos, costo). El torneo se crea inicialmente en estado 
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| Entrada |

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|


### RF01: Registro de Torneo

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                | GET |
| **Idenpotente**                | NO |
| **Razón**           | El sistema debe permitir al organizador crear un nuevo torneo proporcionando la información básica requerida (fechas, cantidad de equipos, costo). El torneo se crea inicialmente en estado 
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| Entrada |

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|


### RF01: Registro de Torneo

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Verbo**                | GET |
| **Idenpotente**                | NO |
| **Razón**           | El sistema debe permitir al organizador crear un nuevo torneo proporcionando la información básica requerida (fechas, cantidad de equipos, costo). El torneo se crea inicialmente en estado 
| **Rol**             |usuario|


**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**EJEMPLO DE ENTRADA**
| Descripción |
|:-------|
| Entrada |

**DATOS DE SALIDA**
| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


**REGLAS DE NEGOCIO Y VALIDACIONES**
| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|

