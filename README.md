# DOSW_ParcialT2_JuanMelo
preparación de ambiente de trabajo


### RF02: Registro de Jugadores

| Campo                     | Detalle |
|:--------------------------|:--------|
| **Código**                | RF02 |
| **Nombre**                | Registro de Jugadores |
| **Descripción**           | El sistema debe permitir a los participantes registrarse proporcionando su información básica y cuenta de correo (@escuelaing.edu.co para institucionales o @gmail.com para familiares). Una vez registrado, el usuario podrá completar su perfil deportivo (posiciones, dorsal, foto) y gestionar su disponibilidad para ser contactado por capitanes o responder a invitaciones de equipos. |
| **Cómo se ejecutará**     | A través de un formulario de registro con validación de dominio de correo y un panel de perfil deportivo donde el jugador define sus preferencias de juego y estado de disponibilidad. |
| **Actor principal**       | Estudiante, Graduado, Profesor, Personal Administrativo, Familiar |
| **Precondiciones**        | 1) El participante debe contar con un correo válido según su tipo de usuario. <br> 2) El correo electrónico no debe estar previamente registrado en el sistema. |

**DATOS DE ENTRADA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| Correo electrónico | Correo para el registro | Email (texto) | Debe ser @escuelaing.edu.co o @gmail.com (familiares) | Sí |
| Contraseña | Clave de acceso | Texto (password) | Mínimo 8 caracteres, una mayúscula y un número | Sí |
| Nombre completo | Nombre y apellidos | Texto | Mínimo 3 caracteres | Sí |
| Tipo de usuario | Clasificación del usuario | Selección (enum) | Estudiante, Graduado, Profesor, Administrativo, Familiar | Sí |
| Posiciones de juego | Posiciones preferidas | Selección múltiple | Portero, Defensa, Volante, Delantero | Sí |
| Número dorsal | Número de camiseta | Numérico (entero) | Rango de 1 a 99 | Sí |
| Foto de perfil | Imagen del jugador | Imagen (archivo) | Formatos: JPG, PNG. Máximo: 2MB | No |
| Disponibilidad | Estado para búsquedas | Booleano | Por defecto: false | No |
| Semestre | Semestre del estudiante | Numérico (entero) | Solo para estudiantes (Rango 1-10) | Condicional |

**DATOS DE SALIDA:**

| Nombre | Descripción | Tipo de campo | Reglas / Aplicación | Obligatorio |
|:-------|:------------|:--------------|:--------------------|:------------|
| ID del jugador | Identificador único | Texto (UUID) | Generado automáticamente por el sistema | Sí |
| Perfil deportivo | Datos del perfil | Objeto JSON | Información técnica del jugador grabada | Sí |
| Mensaje de confirmación | Notificación de éxito | Texto | Se muestra al finalizar el registro o edición | Sí |

**FLUJO BÁSICO:**

| Paso | Actor | Descripción | Excepciones |
|:-----|:------|:------------|:------------|
| 1 | Usuario | Accede al módulo de registro y selecciona su tipo de usuario e ingresa sus datos básicos. | — |
| 2 | Usuario | Completa su perfil deportivo indicando posiciones, número dorsal y disponibilidad. | — |
| 3 | Usuario | Recibe la confirmación del registro exitoso en pantalla con su ID único de jugador. | — |

**FLUJO ALTERNO:**

| Paso | Actor | Descripción | Excepciones |
|:-----|:------|:------------|:------------|
| E1 | Usuario | El usuario ingresa un correo cuyo dominio no corresponde al tipo de usuario seleccionado. Muestra el mensaje: "El dominio del correo no corresponde al tipo de usuario seleccionado" | Regresa al paso 1 |
| E2 | Usuario | El usuario intenta registrar un correo que ya existe. Muestra el mensaje: "Este correo ya se encuentra registrado en el sistema" | Regresa al paso 1 |
| E3 | Usuario | El usuario ingresa un número dorsal fuera del rango permitido (1-99). Muestra el mensaje: "El número dorsal debe estar entre 1 y 99" | Regresa al paso 2 |
| A1 | Usuario | El usuario activa el estado de disponibilidad desde su panel de gestión para aparecer en las búsquedas de los capitanes. | No puede activarse si no ha completado campos obligatorios |
| A2 | Usuario | El usuario recibe una invitación de un equipo y selecciona "Aceptar invitación" desde su panel de notificaciones. | E4: Ya pertenece a un equipo |
| E4 | Usuario | El usuario intenta aceptar una invitación pero ya está vinculado a otro equipo. Muestra el mensaje: "No puedes aceptar la invitación porque ya perteneces a un equipo" | Regresa al panel de gestión |

| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) Usuarios institucionales deben usar @escuelaing.edu.co y familiares @gmail.com.</li><li>2) El número dorsal es único por equipo (se valida al unirse formalmente).</li><li>3) Solo jugadores con estado **Disponible** son visibles para reclutamiento.</li><li>4) Un jugador no puede estar vinculado a dos equipos simultáneamente.</li><li>5) El sistema aplica patrón **Factory Method** para la creación de tipos de usuario.</li></ul> |
| **Anexos** | **Prototipos:** Mockup de Registro y Perfil. <br> **Abreviaturas:** ECI (Escuela Colombiana de Ingeniería). <br><br> **Caso de Uso:** <img width="380" height="149" alt="image" src="https://github.com/user-attachments/assets/cf59150a-2bf8-4ceb-a429-ae468f0eea46" />
| **Historial de Revisión** | <ul><li>**Elaborado por:** Vanessa Torres</li><li>**Aprobado por:** David Cajamarca</li><li>**Fecha:** 19/03/2026</li><li>**Cambios:** Reconstrucción de requerimiento tras pérdida de datos; ajuste de flujo alterno y eliminación de sistema como actor.</li></ul> |
