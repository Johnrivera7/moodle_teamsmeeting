# Reunión de Microsoft Teams para Moodle

Este plugin permite integrar Microsoft Teams con Moodle, proporcionando funcionalidades como la programación de reuniones, la descarga de grabaciones, y el acceso a reportes detallados de asistencia y listas de participantes directamente desde Moodle.

## Características

- **Programación de reuniones**: Permite crear reuniones de Microsoft Teams directamente desde Moodle como actividades.
- **Unirse a reuniones**: Los usuarios pueden acceder a reuniones con un solo clic.
- **Descarga y visualización de grabaciones**:
  - Botón para ver grabaciones directamente desde Moodle.
  - Botón para descargar grabaciones en formato MP4.
- **Reportes de asistencia**:
  - Descarga de reportes detallados de los participantes en formato CSV.
  - Datos como nombres, tiempos de entrada y salida, duración de asistencia y roles.
- **Gestión integrada**: Conexión con Azure Active Directory (Azure AD) y Microsoft Graph API para sincronización de datos.
- **Soporte multilenguaje**: Traducciones para varios idiomas, permitiendo una experiencia más amigable para usuarios de diferentes regiones.

## Requisitos

1. **Moodle**: Versión 3.9 o superior.
2. **Microsoft Azure AD**: Una aplicación registrada con permisos específicos para interactuar con Microsoft Teams.
3. **Servidor Moodle**: Acceso al servidor para instalar el plugin y configurar las tareas programadas.

## Instalación

1. Copie la carpeta `teamsmeeting` en el directorio `mod` de su instalación de Moodle.
2. Acceda a la página de notificaciones de Moodle para completar la instalación del plugin.
3. Configure los ajustes del plugin en `Administración del sitio > Plugins > Actividades > Reunión de Teams`:
   - Ingrese el `Tenant ID`, `Client ID` y `Client Secret` de su aplicación registrada en Azure AD.
   - Especifique la ruta donde se almacenarán las grabaciones.

## Configuración en Azure AD

1. Registre una nueva aplicación en el portal de Azure ([Instrucciones oficiales de Microsoft](https://learn.microsoft.com)).
2. Asigne los siguientes permisos a la aplicación:
   - **Application Permissions**:
     - `OnlineMeeting.ReadWrite.All`
     - `CallRecords.Read.All`
     - `OnlineMeetingRecording.Read.All`
   - **Delegated Permissions**:
     - `User.Read`
     - `Calendars.ReadWrite`
3. Conceda consentimiento administrativo para los permisos asignados.
4. Copie el `Tenant ID`, `Client ID` y `Client Secret` de la aplicación y configúrelos en el plugin.

## Configuración Adicional

### Tareas Programadas

Este plugin utiliza tareas programadas para sincronizar grabaciones y reportes de asistencia. Asegúrese de que las siguientes tareas estén habilitadas:

1. **Descargar grabaciones de reuniones de Teams**:
   - Ruta: `\mod_teamsmeeting\task\download_recordings`
   - Descripción: Obtiene las grabaciones de reuniones finalizadas desde Microsoft Teams y las almacena en la ruta configurada.

2. **Descargar reportes de asistencia de Teams**:
   - Ruta: `\mod_teamsmeeting\task\download_attendance_reports`
   - Descripción: Descarga los reportes de asistencia de las reuniones finalizadas e incluye detalles de los participantes.

### Permisos Adicionales

- Asegúrese de que su servidor Moodle tiene acceso a la API de Microsoft Graph.
- Verifique que la ruta especificada para almacenar las grabaciones tiene los permisos necesarios para lectura/escritura.

## Uso del Plugin

1. **Agregar Actividades**:
   - En un curso de Moodle, agregue una nueva actividad del tipo "Reunión de Teams".
   - Configure los detalles de la reunión, como el nombre, la descripción, y las fechas.

2. **Unirse a Reuniones**:
   - Los estudiantes y profesores pueden unirse a las reuniones a través del enlace generado en Moodle.

3. **Acceso a Grabaciones y Reportes**:
   - Después de la reunión, los usuarios pueden:
     - Ver y descargar las grabaciones.
     - Ver y descargar reportes detallados de asistencia en formato CSV.

## Consideraciones

- **Uso de la API Beta**:
  - Algunas funcionalidades, como el acceso a grabaciones, utilizan endpoints de la API de Microsoft Graph en su versión beta. Esto implica posibles cambios en el futuro.
  - No se recomienda su uso en entornos de producción sin pruebas exhaustivas.

- **Actualizaciones y Eliminación**:
  - Las grabaciones y reportes se almacenan de forma independiente del plugin, por lo que no se eliminan al desinstalar o actualizar el plugin.

## Créditos y Licencia

- **Autor**: John Rivera Gonzalez <johnriveragonzalez7@gmail.com>
- **Licencia**: [GNU General Public License v3](http://www.gnu.org/copyleft/gpl.html)

Para soporte o contribuciones, visite el repositorio oficial del plugin o contacte al autor.
