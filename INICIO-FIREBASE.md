# Sukuna Reports · Activación de Firebase

La aplicación ya usa el proyecto `lmsupana`, autentica con correo/contraseña y guarda reportes y notas en su propia ruta de Firestore (`sr_7f3k9v_sukuna_reports`). Cada usuario ve únicamente su espacio.

## Antes de iniciar

1. En Firebase Console, habilita **Authentication → Sign-in method → Email/Password** y crea el usuario que usará Sukuna Reports. La página no incluye registro público.
2. Verifica que **Cloud Firestore** esté creado en el proyecto.
3. En **Firestore → Rules**, agrega el contenido de `firestore-regla-sukuna.txt` dentro del bloque existente `match /databases/{database}/documents { ... }`. Conserva las reglas actuales de tus otras aplicaciones; no reemplaces todo el archivo de reglas con este fragmento. Revisa también que no exista una regla global permisiva que haga públicos todos los documentos.
4. Desde esta carpeta, ejecuta `firebase deploy --only hosting`. El `.firebaserc` apunta a `lmsupana`.
5. Si Firebase Auth lo solicita, agrega el dominio de Hosting a **Authentication → Settings → Authorized domains**.

El Excel se guarda como una nueva carga y, al volver a iniciar sesión, la página abre la carga más reciente. Los comentarios y minutos exonerados se sincronizan por separado dentro de la misma área privada.

Los reportes quedan separados por UID de Firebase. Solo el usuario autenticado dueño de esa ruta puede leerla o modificarla. Las reglas de Firestore se combinan entre coincidencias; si tus reglas actuales ya permiten acceso global, deben ajustarse para que esta ruta quede privada.

La clave `apiKey` incluida en el HTML es la configuración pública de cliente de Firebase; nunca pongas contraseñas ni claves de servicio en el navegador.
