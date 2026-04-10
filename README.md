# DOSW_ParcialT2_JuanMelo
preparación de ambiente de trabajo


| Codigo | verbo | idenpotente | Razón | Roles |
|:-----|:------|:------------|:------------|:-------|
| RF1 | Usuario | El usuario ingres| Regresa al paso 1 | 
| RF2 | Usuario | El usuario inten | Regresa al paso 1 |
| RF3 | Usuario | El usuario ingres | Regresa al paso 2 |
| RF4 | Usuario | El usuario activa  | No puede activarse si no ha completado campos obligatorios |
| RF5 | Usuario | El usuario recibe| E4: Ya pertenece a un equipo |
| RF6 | Usuario | El usuario intenta  | Regresa al panel de gestión |
| RF7 | Usuario | El usuario intenta| Regresa al panel de gestión |

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


| Sección | Detalle |
| :--- | :--- |
| **Reglas de Negocio** | <ul><li>1) Usuarios institucionales deben usar @escuelaing.edu.co y familiares @gmail.com.</li><li>2) El número dorsal es único por equipo (se valida al unirse formalmente).</li><li>3) Solo jugadores con estado **Disponible** son visibles para reclutamiento.</li><li>4) Un jugador no puede estar vinculado a dos equipos simultáneamente.</li><li>5) El sistema aplica patrón **Factory Method** para la creación de tipos de usuario.</li></ul> |
| **Anexos** | **Prototipos:** Mockup de Registro y Perfil. <br> **Abreviaturas:** ECI (Escuela Colombiana de Ingeniería). <br><br> **Caso de Uso:** <img width="380" height="149" alt="image" src="https://github.com/user-attachments/assets/cf59150a-2bf8-4ceb-a429-ae468f0eea46" />
| **Historial de Revisión** | <ul><li>**Elaborado por:** Vanessa Torres</li><li>**Aprobado por:** David Cajamarca</li><li>**Fecha:** 19/03/2026</li><li>**Cambios:** Reconstrucción de requerimiento tras pérdida de datos; ajuste de flujo alterno y eliminación de sistema como actor.</li></ul> |
