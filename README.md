
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


| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**EJEMPLO DE SALIDA**
| Descripción |
|:-------|
| Salida |


| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
|**validaciones imput**| adsadads|

