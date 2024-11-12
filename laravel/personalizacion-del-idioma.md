# Personalización del idioma

Para configurar el idioma en un proyecto Laravel y utilizar el archivo `es.json` para las traducciones en español, seguiremos estos pasos:

1. **Creamos la carpeta donde se alojarán los archivos de traducción de de Laravel**\
   Primero, creamos manualmente la carpeta `resources/lang/`
2.  **Crear el archivo `es.json` para traducciones personalizadas**\
    En `resources/lang/`, creamos un archivo llamado `es.json`. Este archivo nos permitirá almacenar nuestras traducciones en formato JSON. Podemos añadir las claves y valores que necesitamos traducir. Por ejemplo:

    ```json
    {
      "Welcome": "Bienvenido",
      "Login": "Iniciar sesión",
      "Logout": "Cerrar sesión"
    }
    ```

    Cada clave representa un texto que se traducirá al español.
3.  **Configurar el idioma predeterminado en Laravel**\
    Vamos al fichero `.env` y cambiamos la opción `LOCALE` de `en` a `es`, de modo que el español sea el idioma predeterminado de nuestra aplicación:

    ```php
    APP_LOCALE=es
    ```
4.  **Usar las traducciones en nuestras vistas**\
    Para utilizar las traducciones en nuestras vistas, empleamos el helper `__('clave')` o el método `@lang('clave')` de Blade. Laravel buscará la clave en el archivo `es.json` si el idioma configurado es el español.

    Ejemplo en una vista Blade:

    ```blade
    <h1>{{ __('Welcome') }}</h1>
    <a href="{{ route('login') }}">{{ __('Login') }}</a>
    ```

    Con esto, los textos se mostrarán en español usando las traducciones definidas en el archivo `es.json`.

Siguiendo estos pasos, tendremos nuestro proyecto Laravel configurado para usar el idioma español.

Podemos utilizar el siguiente fichero es.json para disponer de un gran número de traducciones, varias de ellas utilizadas por Jetstream.

````json

{
    "API Token": "Token API",
    "API Tokens": "Tokens API",
    "API tokens allow third-party services to authenticate with our application on your behalf.": "Los tokens API permiten que servicios de terceros se autentiquen con nuestra aplicación en su nombre.",
    "Add Team Member": "Añadir miembro al equipo",
    "Add": "Añadir",
    "Added.": "Añadido.",
    "Administrator": "Administrador",
    "All of the people that are part of this team.": "Todas las personas que forman parte de este equipo.",
    "Already registered?": "¿Ya estás registrado?",
    "Browser Sessions": "Sesiones del navegador",
    "Cancel": "Cancelar",
    "Close": "Cerrar",
    "Code": "Código",
    "Confirm Password": "Confirmar contraseña",
    "Confirm": "Confirmar",
    "Create Account": "Crear cuenta",
    "Create API Token": "Crear token API",
    "Create New Team": "Crear nuevo equipo",
    "Create Team": "Crear equipo",
    "Create": "Crear",
    "Created.": "Creado.",
    "Current Password": "Contraseña actual",
    "Dashboard": "Panel",
    "Delete Account": "Eliminar cuenta",
    "Delete API Token": "Eliminar token API",
    "Delete Team": "Eliminar equipo",
    "Delete": "Eliminar",
    "Disable": "Deshabilitar",
    "Done.": "Hecho.",
    "Editor": "Editor",
    "Email Password Reset Link": "Enviar enlace de restablecimiento",
    "Email": "Email",
    "Enable": "Habilitar",
    "Ensure your account is using a long, random password to stay secure.": "Asegúrese de que su cuenta esté usando una contraseña larga y aleatoria para mantenerse seguro.",
    "For your security, please confirm your password to continue.": "Por su seguridad, confirme su contraseña para continuar.",
    "Forgot your password?": "¿Olvidaste tu contraseña?",
    "Forgot your password? No problem. Just let us know your email address and we will email you a password reset link that will allow you to choose a new one.": "¿Olvidaste tu contraseña? No hay problema. Simplemente déjanos saber tu dirección de correo electrónico y te enviaremos un enlace para restablecer la contraseña que te permitirá elegir una nueva.",
    "I agree to the :terms_of_service and :privacy_policy": "Acepto los :terms_of_service y la :privacy_policy",
    "If necessary, you may log out of all of your other browser sessions across all of your devices. Some of your recent sessions are listed below; however, this list may not be exhaustive. If you feel your account has been compromised, you should also update your password.": "Si es necesario, puede cerrar sesión en todas sus otras sesiones de navegador en todos sus dispositivos. Algunas de sus sesiones recientes se enumeran a continuación; sin embargo, esta lista puede no ser exhaustiva. Si cree que su cuenta se ha visto comprometida, también debe actualizar su contraseña.",
    "Last active": "Última actividad",
    "Last used": "Último uso",
    "Leave Team": "Abandonar equipo",
    "Leave": "Abandonar",
    "Log in": "Iniciar sesión",
    "Log Out Other Browser Sessions": "Cerrar sesiones en otros navegadores",
    "Log Out": "Cerrar sesión",
    "Manage Account": "Administrar cuenta",
    "Manage and log out your active sessions on other browsers and devices.": "Administre y cierre sus sesiones activas en otros navegadores y dispositivos.",
    "Manage API Tokens": "Administrar tokens API",
    "Manage Role": "Administrar rol",
    "Manage Team": "Administrar equipo",
    "Name": "Nombre",
    "Nevermind": "Cancelar",
    "New Password": "Nueva contraseña",
    "Not Found": "No encontrado",
    "Oh no": "Oh no",
    "Once a team is deleted, all of its resources and data will be permanently deleted. Before deleting this team, please download any data or information regarding this team that you wish to retain.": "Una vez que se elimina un equipo, todos sus recursos y datos se eliminarán de forma permanente. Antes de eliminar este equipo, descargue cualquier dato o información sobre este equipo que desee conservar.",
    "Once your account is deleted, all of its resources and data will be permanently deleted. Before deleting your account, please download any data or information that you wish to retain.": "Una vez que se elimine su cuenta, todos sus recursos y datos se eliminarán de forma permanente. Antes de eliminar su cuenta, descargue cualquier dato o información que desee conservar.",
    "Password": "Contraseña",
    "Permanently delete this team.": "Eliminar este equipo de forma permanente.",
    "Permanently delete your account.": "Eliminar su cuenta de forma permanente.",
    "Permissions": "Permisos",
    "Photo": "Foto",
    "Please confirm access to your account by entering the authentication code provided by your authenticator application.": "Confirme el acceso a su cuenta ingresando el código de autenticación proporcionado por su aplicación de autenticación.",
    "Please confirm your password before continuing.": "Confirme su contraseña antes de continuar.",
    "Privacy Policy": "Política de privacidad",
    "Profile Information": "Información de perfil",
    "Profile": "Perfil",
    "Recovery Code": "Código de recuperación",
    "Regenerate Recovery Codes": "Regenerar códigos de recuperación",
    "Register": "Registrarse",
    "Remember me": "Recuérdame",
    "Remove Photo": "Eliminar foto",
    "Remove Team Member": "Eliminar miembro del equipo",
    "Remove": "Eliminar",
    "Resend Verification Email": "Reenviar correo de verificación",
    "Reset Password Notification": "Notificación de restablecimiento de contraseña",
    "Reset Password": "Restablecer contraseña",
    "Save": "Guardar",
    "Saved.": "Guardado.",
    "Select A New Photo": "Seleccionar una nueva foto",
    "Server Error": "Error del servidor",
    "Service Agreement": "Acuerdo de servicio",
    "Show Recovery Codes": "Mostrar códigos de recuperación",
    "Switch Teams": "Cambiar de equipo",
    "Team Details": "Detalles del equipo",
    "Team Members": "Miembros del equipo",
    "Team Name": "Nombre del equipo",
    "Team Owner": "Propietario del equipo",
    "Team Settings": "Configuración del equipo",
    "Terms of Service": "Términos de servicio",
    "Thanks for signing up! Before getting started, could you verify your email address by clicking on the link we just emailed to you? If you didn't receive the email, we will gladly send you another.": "¡Gracias por registrarte! Antes de comenzar, ¿podría verificar su dirección de correo electrónico haciendo clic en el enlace que le acabamos de enviar? Si no recibió el correo electrónico, con gusto le enviaremos otro.",
    "The :attribute must be at least :length characters and contain at least one number.": "La :attribute debe tener al menos :length caracteres y contener al menos un número.",
    "The :attribute must be at least :length characters and contain at least one special character and one number.": "La :attribute debe tener al menos :length caracteres y contener al menos un carácter especial y un número.",
    "The :attribute must be at least :length characters and contain at least one special character.": "La :attribute debe tener al menos :length caracteres y contener al menos un carácter especial.",
    "The :attribute must be at least :length characters and contain at least one uppercase character and one number.": "La :attribute debe tener al menos :length caracteres y contener al menos una mayúscula y un número.",
    "The :attribute must be at least :length characters and contain at least one uppercase character and one special character.": "La :attribute debe tener al menos :length caracteres y contener al menos una mayúscula y un carácter especial.",
    "The :attribute must be at least :length characters and contain at least one uppercase character, one number, and one special character.": "La :attribute debe tener al menos :length caracteres y contener al menos una mayúscula, un número y un carácter especial.",
    "The :attribute must be at least :length characters and contain at least one uppercase character.": "La :attribute debe tener al menos :length caracteres y contener al menos una mayúscula.",
    "The :attribute must be at least :length characters.": "La :attribute debe tener al menos :length caracteres.",
    "The provided password does not match your current password.": "La contraseña proporcionada no coincide con su contraseña actual.",
    "The provided password was incorrect.": "La contraseña proporcionada no es correcta.",
    "The provided two factor authentication code was invalid.": "El código de autenticación de dos factores proporcionado no es válido.",
    "The team's name and owner information.": "Nombre del equipo e información del propietario.",
    "This device": "Este dispositivo",
    "This is a secure area of the application. Please confirm your password before continuing.": "Esta es un área segura de la aplicación. Confirme su contraseña antes de continuar.",
    "This password does not match our records.": "Esta contraseña no coincide con nuestros registros.",
    "This password reset link will expire in :count minutes.": "Este enlace de restablecimiento de contraseña caducará en :count minutos.",
    "This user already belongs to the team.": "Este usuario ya pertenece al equipo.",
    "This user has already been invited to the team.": "Este usuario ya ha sido invitado al equipo.",
    "Token Name": "Nombre del token",
    "Two Factor Authentication": "Autenticación de dos factores",
    "Two factor authentication is now enabled. Scan the following QR code using your phone's authenticator application.": "La autenticación de dos factores ahora está habilitada. Escanee el siguiente código QR usando la aplicación de autenticación de su teléfono.",
    "Update Password": "Actualizar contraseña",
    "Update your account's profile information and email address.": "Actualice la información de perfil y la dirección de correo electrónico de su cuenta.",
    "Use a recovery code": "Usar un código de recuperación",
    "Use an authentication code": "Usar un código de autenticación",
    "We were unable to find a registered user with this email address.": "No pudimos encontrar un usuario registrado con esta dirección de correo electrónico.",
    "When two factor authentication is enabled, you will be prompted for a secure, random token during authentication. You may retrieve this token from your phone's Google Authenticator application.": "Cuando la autenticación de dos factores está habilitada, se le solicitará un token seguro y aleatorio durante la autenticación. Puede recuperar este token desde la aplicación Google Authenticator de su teléfono.",
    "Whoops! Something went wrong.": "¡Ups! Algo salió mal.",
    "You are logged in!": "¡Has iniciado sesión!",
    "You have enabled two factor authentication.": "Has habilitado la autenticación de dos factores.",
    "You have not enabled two factor authentication.": "No has habilitado la autenticación de dos factores.",
    "You may delete any of your existing tokens if they are no longer needed.": "Puede eliminar cualquiera de sus tokens existentes si ya no los necesita.",
    "You may not delete your personal team.": "No puede eliminar su equipo personal.",
    "You may not leave a team that you created.": "No puede abandonar un equipo que usted creó."
 }
 
```
````
