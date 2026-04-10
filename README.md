
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
| **Verbo**                | RF01 |
| **Idenpotente**                | Registro de Torneo |
| **Razón**           | El sistema debe permitir al organizador crear un nuevo torneo proporcionando la información básica requerida (fechas, cantidad de equipos, costo). El torneo se crea inicialmente en estado 

**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Nombre del Torneo | Nombre con el cual aparecera el torneo en la pagina| String | No debe extir un torneo con el mismo nombre que se encuentre activo o en progreso|Sí|
| Fecha inicial | Fecha de inicio del torneo | Fecha (date) | Debe ser igual o posterior a la fecha actual | Sí |
| Fecha final | Fecha de finalización del torneo | Fecha (date) | Debe ser estrictamente posterior a la fecha inicial | Sí |
| Cantidad de equipos | Número máximo de equipos participantes | Numérico (entero) | Debe ser un número par ≥ 4 | Sí |
| Costo por equipo | Valor de inscripción por equipo | Moneda (decimal) | Debe ser ≥ 0 | Sí |

**DATOS DE SALIDA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del torneo | Identificador único del torneo creado | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Estado | Estado inicial del torneo | Texto (enum) | Siempre se retorna como "Borrador" al crear | Sí |
| Mensaje de confirmación | Notificación de creación exitosa | Texto | Se muestra al organizador tras el guardado | Sí |

**FLUJO BÁSICO:**

| Paso | Actor | Descripción | Excepciones |
|:-----|:------|:------------|:------------|
| 1 | Organizador | Accede al módulo de torneos y selecciona "Crear torneo" | — |
| 2 | Organizador | Ingresa fecha inicial, fecha final, cantidad de equipos y costo por equipo. | — |
| 3 | Organizador| Recibe la confimacion de la creación del torneo en pantalla, con el Id de torneo. | — |

**FLUJO ALTERNO:**

| Paso | Actor | Descripción | Excepciones |
|:-----|:------|:------------|:------------|
| E1 | Organizador | El usuario al hacer el registro de la fecha puso la fecha final igual o anterior a la incial. Muestra el mensaje: "La fecha final debe ser posterior a la fecha inicial" y no permite el guardado | Regresa al paso 2 |
| E2 | Organizador| El usuario al ingresar los datos pone una cantidad de equipos menor a 4. Muestra el mensaje: "La cantidad de equipos debe ser un número par mayor o igual a 4" | Regresa al paso 2 |
| E3 | Organizador| El usuario ingresa un nombre de torneo que ya existe. Muestra el mensaje: "Ya existe un torneo activo o en progreso para el periodo indicado" | Regresa al paso 2 |
| A1 | Organizador |El usuario pone el torneo como borrar y si desea desde las configuraciones del torneo, selecciona "Activar Torneo" desde el panel de gestión o en el estado del torneo selescciona "Activo | No le puuede dar activo si ya fue completado o eliminado |
| A3 | Organizador | El organizador desea finalizar el torneo va a las configuraciones del torneo y selecciona "Finalizar torneo" | E6: Hay partidos sin resultado registrado |
| E4 | organizador | El organizador desea activar el torneo pero no ha finalizado todos los coampos obligatorios. Muestra el  mensaje: "Debe completar la configuración del torneo antes de activarlo (RF06)" | Regresa al panel de gestión |
| E5 | Organizador | El usuario seleecciona iniciar torneo sin equipos inscritos .Muestra mensaje: "No se puede iniciar un torneo sin equipos inscritos" | Regresa al panel de gestión |
| E6 | Organizador |El organizador selecciona finalizar o eliminar torneo. Muestra el mensaje: "Existen partidos pendientes de resultado" | Regresa al panel de gestión |




| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) El torneo se crea siempre en estado **Borrador** o en **Activo** si el administrador lo define. También puede pasar a *In Progress*, *Completed* o *Deleted*.</li><li>2) Transiciones permitidas: **Borrador → Activo → En Progreso → Finalizado**.</li><li>3) No se permiten transiciones inversas ni saltar estados.</li><li>4) La fecha final debe ser estrictamente posterior a la inicial.</li><li>5) Cantidad de equipos: número par $\ge 4$.</li><li>6) Un torneo **Finalizado** es de solo lectura.</li></ul> |
| **Anexos** | **Prototipos:** Mockup de Gestión Administrativa. <br> **Abreviaturas:** N/A <br><br> **Caso de Uso:** <br> ![Diagrama de Caso de Uso](https://github.com/user-attachments/assets/2c6a483f-16f0-4a38-bd5c-e780dd2dc764) |
| **Historial de Revisión** | <ul><li>**Elaborado por:** Vanessa Torres</li><li>**Aprobado por:** David Cajamarca</li><li>**Fecha:** 03/03/2026</li><li>**Cambios:** Se expandieron las reglas de negocio para incluir transiciones de estado y validaciones de fechas según feedback docente.</li></ul> |
